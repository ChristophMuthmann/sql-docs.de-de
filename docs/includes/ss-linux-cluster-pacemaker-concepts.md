## <a name="pacemakerNotify"></a>SQL Server-Agent-Ressource für Schrittmacher verstehen

Vor der Version CTP 1.4 der Schrittmacher Ressource-Agent für Verfügbarkeitsgruppen konnte nicht wissen, ob ein Replikat als markiert `SYNCHRONOUS_COMMIT` oder nicht tatsächlich auf dem neuesten Stand war. Es konnte vorkommen, dass das Replikat nicht mehr mit dem primären synchronisierte, dies jedoch unbemerkt blieb. Der Agent konnte daher eine veraltete Replikat zum primären - höher stufen, die bei erfolgreicher Ausführung zu Datenverlust führen würde. 

SQL Server 2017 CTP 1.4 hinzugefügt `sequence_number` auf `sys.availability_groups` zur Behebung dieses Problems. `sequence_number`ist eine monoton ansteigende "bigint", das darstellt, das lokale verfügbarkeitsreplikat für die Gruppe in Bezug auf den Rest der Replikate in der verfügbarkeitsgruppe wird wie auf dem neuesten Stand. Failover durchführen, hinzufügen oder Entfernen von Replikaten und andere Verfügbarkeit Gruppieren von Operationen aktualisieren diese Zahl auf. Die Anzahl der primären Datenbank aktualisiert, dann auf sekundäre Replikate abgelegt. Daher wird ein sekundäres Replikat, das auf dem neuesten Stand ist der gleiche Sequence_number wie die primäre Datenbank verfügen. 

Wenn Schrittmacher entscheidet, die ein Replikat zur primären höher stufen, ihn zuerst sendet eine Benachrichtigung an alle Replikate, um die Sequenznummer extrahieren und speichern es (nennen wir dies die bereits höher stufen Benachrichtigung). Als Nächstes Schrittmacher tatsächlich versucht, ein Replikat zur primären höher stufen, stuft das Replikat nur selbst wenn die Sequenznummer die höchste die Sequenznummern von allen Replikaten wird und lehnt andernfalls den Promote-Vorgang. Auf diese Weise kann nur das Replikat mit der höchsten Sequenznummer zu einem primären heraufgestuft werden, sodass es nicht zu Datenverlust kommt. 

Beachten Sie, dass dies nur sicher funktioniert, solange mindestens ein für die Heraufstufung verfügbares Replikat über die gleiche Sequenznummer wie das bisherige primäre Replikat verfügt. Um dies sicherzustellen, ist das Standardverhalten für den Ressource Schrittmacher-Agent, um automatisch `REQUIRED_COPIES_TO_COMMIT` so, dass mindestens ein synchrones commit sekundären Replikat ist, auf dem neuesten Stand sind und für das Ziel ein automatisches Failover verfügbar. Mit jeder Überwachung Aktion, den Wert des `REQUIRED_COPIES_TO_COMMIT` berechnet (und bei Bedarf aktualisiert) als ("Anzahl der Replikate mit synchronem Commit" / 2). Klicken Sie dann zum Zeitpunkt der Failover der Ressourcen-Agent benötigen (`total number of replicas`  -  `required_copies_to_commit` Replikate) So reagieren Sie auf die Benachrichtigung eines davon zum primären höher stufen können vorab heraufstufen. Das Replikat mit der höchsten `sequence_number` wird zum primären heraufgestuft werden. 

Wir betrachten Sie beispielsweise die Groß-/Kleinschreibung einer verfügbarkeitsgruppe mit drei synchronen Replikaten - ein primäres Replikat und zwei sekundärer Replikate mit synchronem Commit.

- `REQUIRED_COPIES_TO_COMMIT`3 / 2 = 1

- Die erforderliche Anzahl von Replikaten zu reagieren, um eine Aktion vorab zu erzielen, ist 3 minus 1 = 2. Daher 2 Replikate müssen für das Failover ausgelöst werden soll. Dies bedeutet, dass bei Ausfall der primären, wenn einer der sekundären Replikate nicht mehr reagiert und nur eine von den sekundären Replikaten reagiert auf die vorab heraufstufen Aktion, der Agent für die Ressource kann nicht garantieren, dass die sekundäre Datenbank, die geantwortet hat die höchste Sequence_number hat und ein Failover wird nicht ausgelöst.

Ein Benutzer kann auswählen, um das Standardverhalten überschreiben, und konfigurieren die verfügbarkeitsgruppenressource nicht festgelegt `REQUIRED_COPIES_TO_COMMIT` automatisch wie oben beschrieben.

>[!IMPORTANT]
>Wenn `REQUIRED_COPIES_TO_COMMIT` ist Risiko eines Datenverlusts 0 vorhanden ist. Bei einem Ausfall des primären wird der Agent für die Ressource nicht automatisch einen Failover ausgelöst. Der Benutzer hat sich entscheiden, ob sie vom primären zum Wiederherstellen oder Manueller Failover warten möchten.

Festzulegende `REQUIRED_COPIES_TO_COMMIT` auf 0 (null) ausführen:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

Der entsprechende Befehl, der crm (unter SLES) nutzt, ist:

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

Auf Standardwert zurücksetzen möchten berechnet, Wert, der ausgeführt werden:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>Aktualisieren die Ressourceneigenschaften bewirkt, dass alle Replikate beenden und neu starten. Das bedeutet, dass der primäre wird vorübergehend werden zu sekundären herabgestuft, dann erneut heraufgestuft wird, die temporäre erreichen nichtverfügbarkeit geschrieben werden. Der neue Wert für REQUIRED_COPIES_TO_COMMIT wird nur festgelegt werden nach der Replikate erneut gestartet werden, damit er nicht unmittelbar mit den Pcs-Befehl ausführen.

## <a name="balancing-high-availability-and-data-protection"></a>Netzwerklastenausgleich hohe Verfügbarkeit und Datenschutz 

Das oben beschriebene Verhalten der Standardeinstellung gilt auch für den Fall 2 synchroner Replikate (Primäres + sekundären). Schrittmacher wird standardmäßig `REQUIRED_COPIES_TO_COMMIT = 1` um sicherzustellen, dass das sekundäre Replikat ist immer auf dem neuesten Stand für maximale Datenschutz.  

>[!WARNING]
>Dies ist mit höheren Risikos der Ausfall des primären Replikats aufgrund von geplanten und ungeplanten Ausfällen auf dem sekundären Replikat. Der Benutzer kann das Standardverhalten des Ressource-Agents ändern, und überschreiben Sie wahlweise die `REQUIRED_COPIES_TO_COMMIT` auf 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Sobald überschreiben die Resource-Agent verwendet die neue Einstellung für `REQUIRED_COPIES_TO_COMMIT` und beenden zu berechnen. Dies bedeutet, dass Benutzer manuell entsprechend aktualisieren (z. B. Wenn sie die Anzahl der Replikate erhöhen).

Die folgenden Tabellen wird das Ergebnis einer Ausfallzeit für die primären oder sekundären Replikate in einer anderen Ressource für verfügbarkeitsgruppenkonfigurationen beschrieben:

### <a name="availability-group---2-sync-replicas"></a>Verfügbarkeitsgruppe – 2 synchronisierungsreplikate

| |Primäre Ausfall |Ein sekundäres Replikat Ausfall
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Benutzer hat ein manuelles FAILOVER ausgeben. <br>Sie müssen möglicherweise Daten verloren gehen.<br> Neue primäre ist R/W |R/W, läuft Sie ungeschützt zu Datenverlusten ein Primärschlüssel ist
|`REQUIRED_COPIES_TO_COMMIT=1` * |Cluster wird FAILOVER automatisch ausstellen. <br>Kein Datenverlust. <br> Neue primäre lehnen alle Verbindungen, bis vorherigen primären wiederhergestellt und verknüpft die verfügbarkeitsgruppe als sekundär. |Primäre lehnen alle Verbindungen bis sekundären wiederhergestellt.

\*SQL Server-Agent-Ressource für Schrittmacher Standardverhalten.

### <a name="availability-group---3-sync-replicas"></a>Verfügbarkeitsgruppe – 3 synchronisierungsreplikate

| |Primäre Ausfall |Ein sekundäres Replikat Ausfall
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Benutzer hat ein manuelles FAILOVER ausgeben. <br>Sie müssen möglicherweise Daten verloren gehen. <br>Neue primäre ist R/W |Primäre ist R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |FAILOVER wird von der Cluster automatisch ausgestellt werden. <br>Kein Datenverlust. <br>Neue primäre ist RW |Primäre ist R/W 

\*SQL Server-Agent-Ressource für Schrittmacher Standardverhalten.