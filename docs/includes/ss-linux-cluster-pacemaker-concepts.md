## <a name="pacemakerNotify"></a>Grundlegendes zum SQL Server-Ressourcen-Agent für Pacemaker

Vor Version CTP 1.4 konnte der Pacemaker-Ressourcen-Agent für Verfügbarkeitsgruppen nicht ermitteln, ob ein als `SYNCHRONOUS_COMMIT` markiertes Replikat tatsächlich auf dem neuesten Stand war. Es konnte vorkommen, dass das Replikat nicht mehr mit dem primären synchronisierte, dies jedoch unbemerkt blieb. So konnte der Agent ein veraltetes Replikat zu einem primären heraufstufen, was bei Erfolg zu Datenverlust führte. 

SQL Server 2017 CTP 1.4 hat `sequence_number` zu `sys.availability_groups` hinzugefügt, um dieses Problem zu lösen. `sequence_number` ist ein monoton ansteigender BIGINT-Datentyp, der darstellt, wie aktuell das lokale Verfügbarkeitsgruppenreplikat in Bezug auf den Rest der Replikate in der Verfügbarkeitsgruppe ist. Durch das Durchführen von Failovern, Hinzufügen oder Entfernen von Replikaten und andere Verfügbarkeitsgruppenvorgänge wird diese Zahl aktualisiert. Die Zahl wird auf dem primären Replikat aktualisiert und anschließend an sekundäre Replikate übertragen. Daher verfügt ein aktualisiertes sekundäres Replikat über die gleiche Sequenznummer (sequence_number) wie das primäre Replikat. 

Wenn Pacemaker entscheidet, ein Replikat zum einem primären heraufzustufen, wird zuerst eine Benachrichtigung an alle Replikate gesendet (eine sogenannte Vorabbenachrichtigung über die Heraufstufung), um die Sequenznummer zu extrahieren und zu speichern. Wenn Pacemaker als Nächstes tatsächlich versucht, ein Replikat zu einem primären heraufzustufen, stuft das Replikat sich selbst nur herauf, wenn seine Sequenznummer die höchste aller Replikate ist, und lehnt andernfalls die Heraufstufung ab. Auf diese Weise kann nur das Replikat mit der höchsten Sequenznummer zu einem primären heraufgestuft werden, sodass es nicht zu Datenverlust kommt. 

Beachten Sie, dass dies nur sicher funktioniert, solange mindestens ein für die Heraufstufung verfügbares Replikat über die gleiche Sequenznummer wie das bisherige primäre Replikat verfügt. Um dies sicherzustellen, legt der Pacemaker-Ressourcen-Agent `REQUIRED_COPIES_TO_COMMIT` standardmäßig automatisch fest, sodass mindestens ein sekundären Replikat mit synchronem Commit auf dem neuesten Stand und als Ziel für ein automatisches Failover verfügbar ist. Mit jeder Überwachungsaktion wird der Wert `REQUIRED_COPIES_TO_COMMIT` mithilfe der Formel „Anzahl der Replikate mit synchronem Commit“ geteilt durch zwei“ berechnet und ggf. aktualisiert. Zum Zeitpunkt des Failovers erfordert der Ressourcen-Agent (`total number of replicas` - `required_copies_to_commit`-Replikate) eine Reaktion auf die Vorabbenachrichtigung, um ein Replikat zum primären heraufzustufen. Das Replikat mit der höchsten `sequence_number` wird zum primären heraufgestuft. 

Verwenden wir als Beispiel eine Verfügbarkeitsgruppe mit drei synchronen Replikaten: einem primären Replikat und zwei sekundären Replikate mit synchronem Commit.

- `REQUIRED_COPIES_TO_COMMIT`  ist 3 / 2 = 1

- Die für die Antwort auf die Vorabbenachrichtigung erforderliche Anzahl von Replikaten ist 3 - 1 = 2. Es muss also zwei Replikate geben, damit das Failover ausgelöst werden kann. Wenn also das primäre Replikat ausfällt und nur eines der sekundären Replikate auf die Vorabaktion zum Heraufstufen reagiert, kann der Ressourcen-Agent nicht garantieren, dass das sekundäre Replikat, das geantwortet hat, die höchste Sequenznummer hat. Ein Failover wird daher nicht ausgelöst.

Ein Benutzer kann das Standardverhalten bei Bedarf überschreiben und die Verfügbarkeitsgruppenressource so konfigurieren, dass `REQUIRED_COPIES_TO_COMMIT` nicht wie oben beschrieben automatisch festgelegt wird.

>[!IMPORTANT]
>Wenn `REQUIRED_COPIES_TO_COMMIT` 0 (null) entspricht, besteht das Risiko von Datenverlust. Wenn das primäre Replikat ausfällt, löst der Ressourcen-Agent nicht automatisch ein Failover aus. Der Benutzer muss entscheiden, ob gewartet wird, bis das primäre Replikat wiederhergestellt wird, oder ob ein manuelles Failover durchgeführt werden soll.

Um `REQUIRED_COPIES_TO_COMMIT` auf 0 (null) festzulegen, führen Sie Folgendes aus:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

Der entsprechende Befehl, der crm (unter SLES) nutzt, ist:

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

Um es auf den standardmäßig berechneten Wert zurückzusetzen, führen Sie Folgendes aus:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>Das Aktualisieren der Ressourceneigenschaften bewirkt, dass alle Replikate beendet und neu gestartet werden. Das bedeutet, dass das primäre vorübergehend zum sekundären Replikat herabgestuft und dann erneut heraufgestuft wird. Deswegen sind Schreibvorgänge vorübergehend nicht verfügbar. Der neue Wert für REQUIRED_COPIES_TO_COMMIT wird erst nach dem Neustart der Replikate festgelegt, also nicht gleichzeitig mit dem pcs-Befehl.

## <a name="balancing-high-availability-and-data-protection"></a>Ausgleich zwischen Hochverfügbarkeit und Datenschutz 

Das oben beschriebene Standardverhalten gilt auch für den Fall von zwei synchronen Replikaten (ein primäres und ein sekundäres). Pacemaker legt `REQUIRED_COPIES_TO_COMMIT = 1` auf das Standardverhalten fest, um sicherzustellen, dass das sekundäre Replikat für maximalen Datenschutz immer auf dem neuesten Stand ist.  

>[!WARNING]
>Dies geht mit einem höheren Risiko von Nichtverfügbarkeit des primären Replikats aufgrund von geplanten und ungeplanten Ausfällen auf dem sekundären Replikat einher. Der Benutzer kann das Standardverhalten des Ressourcen-Agents ändern und `REQUIRED_COPIES_TO_COMMIT` wahlweise auf 0 überschreiben:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Wenn die Überschreibung beendet ist, nutzt der Ressourcen-Agent die neue Einstellung für `REQUIRED_COPIES_TO_COMMIT` und berechnet sie nicht mehr. Dies bedeutet, dass Benutzer diese entsprechend manuell aktualisieren müssen (z.B. wenn sie die Anzahl der Replikate erhöhen).

In der folgenden Tabelle wird das Ergebnis eines Ausfalls des primären oder sekundären Replikats in verschiedenen Ressourcenkonfigurationen von Verfügbarkeitsgruppen beschrieben:

### <a name="availability-group---2-sync-replicas"></a>Verfügbarkeitsgruppe – 2 Synchronisierungsreplikate

| |Ausfall des primären Replikats |Ausfall eines sekundären Replikats
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Der Benutzer muss ein manuelles Failover durchführen. <br>Möglicherweise kommt es zu Datenverlusten.<br> Neues primäres Replikat ist R/W |Primäres Replikat ist R/W, mit Gefahr von Datenverlusten
|`REQUIRED_COPIES_TO_COMMIT=1` * |Cluster gibt automatisch FAILOVER aus <br>Kein Datenverlust. <br> Das neue primäre Replikat lehnt alle Verbindungen ab, bis das vorherige primäre Replikat wiederhergestellt ist und als sekundäres Replikat mit der Verfügbarkeitsgruppe verknüpft wird. |Das primäre Replikat lehnt alle Verbindungen ab, bis das sekundäre wiederhergestellt ist.

\* Standardverhalten des SQL Server-Ressourcen-Agents für Pacemaker.

### <a name="availability-group---3-sync-replicas"></a>Verfügbarkeitsgruppe – 3 Synchronisierungsreplikate

| |Ausfall des primären Replikats |Ausfall eines sekundären Replikats
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Der Benutzer muss ein manuelles Failover durchführen. <br>Möglicherweise kommt es zu Datenverlusten. <br>Neues primäres Replikat ist R/W |Primäres Replikat ist R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |Der Cluster gibt automatisch FAILOVER aus. <br>Kein Datenverlust. <br>Neues primäres Replikat ist R/W |Primäres Replikat ist R/W 

\* Standardverhalten des SQL Server-Ressourcen-Agents für Pacemaker.