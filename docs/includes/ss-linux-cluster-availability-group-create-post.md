
## <a name="add-a-database-to-the-availability-group"></a>Hinzufügen einer Datenbank mit der verfügbarkeitsgruppe

Sicherstellen, dass die Datenbank, die Sie mit der verfügbarkeitsgruppe hinzufügen im vollständigen Wiederherstellungsmodus betrieben und verfügt über eine gültige Sicherung. Wenn dies eine Testdatenbank oder eine neue Datenbank erstellt ist, nehmen Sie eine datenbanksicherung. Führen Sie auf dem primären SQL-Server die folgende Transact-SQL zum Erstellen und Sichern Sie eine Datenbank mit dem Namen `db1`.

```Transact-SQL
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

Führen Sie auf dem primären Replikat für die SQL Server die folgende Transact-SQL zum Hinzufügen einer Datenbank mit dem Namen `db1` zu einer verfügbarkeitsgruppe namens `ag1`.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Stellen Sie sicher, dass die Datenbank auf den sekundären Servern erstellt wird

Führen Sie auf jedem sekundären Replikat für die SQL Server die folgende Abfrage aus, um festzustellen, ob die `db1` Datenbank wurde erstellt und synchronisiert ist.

```Transact-SQL
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
