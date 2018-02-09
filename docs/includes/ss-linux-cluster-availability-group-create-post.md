
## <a name="add-a-database-to-the-availability-group"></a>Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe

Stellen Sie sicher, dass die Datenbank, die Sie mit der verfügbarkeitsgruppe hinzufügen verfügt über eine gültige Sicherung befindet sich im vollständigen Wiederherstellungsmodus. Wenn dies eine Testdatenbank oder eine neu erstellte Datenbank ist, nehmen Sie eine datenbanksicherung. Auf dem primären SQL-Server führen Sie das folgende Transact-SQL-Skript zum Erstellen und Sichern Sie eine Datenbank mit dem Namen `db1`:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1] 
   TO DISK = N'/var/opt/mssql/data/db1.bak';
```

Führen Sie die folgende Transact-SQL-Skript, um eine Datenbank mit dem Namen hinzufügen, auf dem primären Replikat für die SQL Server `db1` zu einer verfügbarkeitsgruppe namens `ag1`:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Sicherstellen, dass die Datenbank auf den sekundären Servern erstellt wird

Führen Sie auf jedem sekundären Replikat für die SQL Server die folgende Abfrage aus, um festzustellen, ob die `db1` -Datenbank erstellt und synchronisiert wird:

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
