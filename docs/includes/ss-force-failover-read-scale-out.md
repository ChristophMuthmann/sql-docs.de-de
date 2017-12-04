Jede Verfügbarkeitsgruppe hat nur ein primäres Replikat. Das primäre Replikat lässt Lese- und Schreibvorgänge zu. Zum Ändern, welches Replikat ein Primärschlüssel ist, können Sie ein Failover ausführen. In einer Verfügbarkeitsgruppe für Hochverfügbarkeit automatisiert der Cluster-Manager den Failovervorgang. In einer Verfügbarkeitsgruppe zur Leseskalierung wird der Failovervorgang manuell ausgeführt. 

Es gibt zwei Möglichkeiten, die das primäre Replikat in einer Skalieren von Lesevorgängen verfügbarkeitsgruppe ein Failover aus:

- Erzwungenes Manuelles Failover ohne Datenverlust
- Manuelles Failover ohne Datenverlust

### <a name="forced-manual-failover-with-data-loss"></a>Erzwungenes Manuelles Failover ohne Datenverlust

Verwenden Sie diese Methode, wenn das primäre Replikat ist nicht verfügbar und kann nicht wiederhergestellt werden. 

Verbinden Sie zum Erzwingen eines Failovers mit Verlust von Daten, SQL Server-Instanz, die das sekundäre Zielreplikat und das Ausführen hostet:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>Manuelles Failover ohne Datenverlust

Verwenden Sie diese Methode, wenn das primäre Replikat verfügbar ist. Dabei müssen Sie allerdings vorübergehend oder dauerhaft die Konfiguration ändern und die SQL Server-Instanz ändern, die das primäre Replikat hostet. Bevor Sie das manuelle Failover ausgeben, stellen Sie sicher, dass das sekundäre Zielreplikat um potenzielle Datenverluste zu vermeiden auf dem neuesten Stand ist. 

Um manuell ein Failover ohne Datenverlust ausführen:

1. Stellen Sie das sekundäre Zielreplikat `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'**<node2>*' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Führen Sie die folgende Abfrage aus, um zu ermitteln, dass aktive Transaktionen auf dem primären Replikat und mindestens ein sekundäres Replikat ausgeführt werden: 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   Das sekundäre Replikat wird synchronisiert, wenn `synchronization_state_desc` `SYNCHRONIZED` ist.

3. Update `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` auf 1.

   Das folgende Skript legt `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` auf 1 für eine verfügbarkeitsgruppe mit dem Namen `ag1`. Bevor Sie das folgende Skript ausführen, ersetzen Sie `ag1` durch den Namen der verfügbarkeitsgruppe:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   Diese Einstellung wird sichergestellt, dass jeder aktiven Transaktion ein Commit ausgeführt wurde, auf dem primären Replikat und mindestens ein sekundäres Replikat ist. 

4. Herabstufen von das primäre Replikat an ein sekundäres Replikat. Nachdem das primäre Replikat herabgestuft wird, ist es schreibgeschützt. Führen Sie diesen Befehl für die SQL Server-Instanz, die zum Aktualisieren der Rolle, die das primäre Replikat hostet `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. Stufen Sie das sekundäre Zielreplikat höher ein als das Primäre. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Verwenden Sie zum Löschen einer verfügbarkeitsgruppe [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Für eine verfügbarkeitsgruppe mit CLUSTER_TYPE NONE oder extern erstellt wurden muss der Befehl auf allen Replikaten ausgeführt werden, die Teil der verfügbarkeitsgruppe sind.