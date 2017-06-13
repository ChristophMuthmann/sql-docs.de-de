## <a name="managing-synchronous-commit-mode"></a>Verwalten des synchronen Commit-Modus

>[!WARNING]
>In einigen Fällen kann eine SQL Server-Verfügbarkeitsgruppe im synchronen Commit-Modus unter Linux anfällig für Datenverlust sein. Sehen Sie sich die folgenden Details zur eigentlichen Ursache und deren Umgehung an, um Datenverlust zu vermeiden. Dieses Problem wird in den zukünftigen Versionen behoben.

###<a name="pacemaker-notification-for-availability-group-resource-promotion"></a>Pacemaker-Benachrichtigung für Ressourcenheraufstufung von Verfügbarkeitsgruppen

Vor Version CTP 1.4 konnte der Pacemaker-Ressourcenagent für Verfügbarkeitsgruppen nicht ermitteln, ob ein als `SYNCHRONOUS_COMMIT` markiertes Replikat tatsächlich auf dem neuesten Stand war. Es konnte vorkommen, dass das Replikat nicht mehr mit dem primären synchronisierte, dies jedoch unbemerkt blieb. So konnte der Agent ein veraltetes Replikat zu einem primären heraufstufen, was bei Erfolg zu Datenverlust führte. 

SQL Server 2017 CTP 1.4 fügt `sequence_number` auf `sys.availability_groups` zur Behebung dieses Problems. `sequence_number` ist ein monoton ansteigender BIGINT-Datentyp, der darstellt, wie aktuell das lokale AG-Replikat in Bezug auf den Rest des Systems ist. Durch das Durchführen von Failovern, Hinzufügen bzw. Entfernen von Replikaten und andere AG-Vorgänge wird diese Zahl aktualisiert. Die Zahl wird auf dem primären Replikat aktualisiert und anschließend an sekundäre Replikate übertragen. Daher verfügt ein aktualisiertes sekundäres Replikat über die gleiche Zahl wie das primäre Replikat.

Wenn Pacemaker entscheidet, ein Replikat zum einem primären heraufzustufen, wird zuerst eine Benachrichtigung an alle Replikate gesendet, um die Sequenznummer zu extrahieren und zu speichern. Wenn Pacemaker als Nächstes tatsächlich versucht, ein Replikat zu einem primären heraufzustufen, stuft das Replikat sich selbst nur herauf, wenn seine Sequenznummer die höchste ist, und lehnt andernfalls die Heraufstufung ab. Auf diese Weise kann nur das Replikat mit der höchsten Sequenznummer zu einem primären heraufgestuft werden, sodass es nicht zu Datenverlust kommt.

Beachten Sie, dass dies nur sicher funktioniert, solange mindestens ein für die Heraufstufung verfügbares Replikat über die gleiche Sequenznummer wie das bisherige primäre Replikat verfügt. Da es für den Ressourcenagent erforderlich ist, dass Pacemaker Benachrichtigungen an alle Replikate übermittelt, muss die Verfügbarkeitsressource mit `notify=true` konfiguriert werden. Für jede vorhandene `ocf:mssql:ag`-Ressource muss der Benutzer die Ressourcenkonfiguration mit `notify=true` aktualisieren, bevor er das `mssql-server-ha`-Paket auf die Version CTP 1.4 aktualisiert, da die Ressource andernfalls in den Fehlerstatus wechselt. 

### <a name="how-to-avoid-potential-for-data-loss"></a>Vermeiden der Anfälligkeit für Datenverlust 

Im folgenden Fall kann eine Verfügbarkeitsgruppe noch immer anfällig für Datenverlust sein. Wenn bei einem Cluster mit fünf Knoten eine Verfügbarkeitsgruppe mit Replikaten auf drei Instanzen von SQL Server vorhanden ist, können das primäre Replikat und ein sekundäres Replikat dem anderen sekundären Replikat voraus sein. Wenn sie bereits einen Vorsprung haben, ist die `sequence_number` in `sys.availability_groups` größer als bei den anderen Replikaten. Wenn in diesem Zustand die beiden Replikate die Verbindung zum Rest des Clusters verlieren, betrachtet Pacemaker möglicherweise die verbleibenden drei Knoten als Quorum und ermöglicht dem latenten Replikat, sich zu einem primären heraufzustufen. In dieser Situation kann es zu Datenverlust kommen.

sql2017 führt eine neue Funktion zum Erzwingen einer bestimmten Anzahl an sekundäre Replikate verfügbar sein, bevor alle Transaktionen ein Commit auf dem primären Replikat ausgeführt werden können. Mit `REQUIRED_COPIES_TO_COMMIT` können Sie eine Reihe von Replikaten festlegen, für die ein Commit an die Transaktionsprotokolle sekundärer Replikatdatenbanken ausgeführt werden muss, bevor eine Transaktion fortgesetzt werden kann. Sie können diese Option mit `CREATE AVAILABILITY GROUP` oder `ALTER AVAILABILITY GROUP` verwenden. Siehe [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx).

Sie können die oben beschriebene Anfälligkeit für Datenverlust vermeiden, indem Sie `REQUIRED_COPIES_TO_COMMIT` auf die maximale Anzahl von synchronisierten Replikaten festlegen. Zukünftige Versionen werden über integrierte Logik zur automatischen Einstellung von `REQUIRED_COPIES_TO_COMMIT` verfügen.
Wenn `REQUIRED_COPIES_TO_COMMIT` festgelegt wurde, warten Transaktionen an den primären Replikatdatenbanken, bis für die Transaktion ein Commit auf der erforderlichen Anzahl von Transaktionsprotokollen synchroner sekundärer Replikatdatenbanken ausgeführt wurde. Wenn nicht genügend synchrone sekundäre Replikate online sind, werden die Transaktionen angehalten, bis die Kommunikation mit genügend sekundären Replikaten wieder aufgenommen wird.

Im folgenden Beispiel wird der Name einer Verfügbarkeitsgruppe [ag1] auf `REQUIRED_COPIES_TO_COMMIT = 2` festgelegt. 

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1]
SET (REQUIRED_COPIES_TO_COMMIT = 2)
```

Wenn im obigen Beispiel die Verfügbarkeitsgruppe zwei sekundäre Replikate besitzt, wartet sie, bis beide sekundären Replikate die Commits bestätigen. Wenn ein Replikat nicht mehr reagiert, werden Transaktionen blockiert.
