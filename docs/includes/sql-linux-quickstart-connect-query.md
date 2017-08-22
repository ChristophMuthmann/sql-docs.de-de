## <a name="connect-locally"></a>Lokal verbinden

Die folgenden Schritte verwenden **sqlcmd**, um sich lokal mit Ihrer neuen SQL Server-Instanz zu verbinden.

1. Führen Sie **sqlcmd** mit Parametern für Ihren SQL Servernamen (-S), den Benutzernamen (-U) und das Kennwort (-P) aus. In diesem Tutorial verbinden Sie sich lokal, damit der Name des Servers `localhost` ist. Der Benutzername ist `SA`, und das Kennwort ist jenes, welches Sie während des Setups für das SA-Konto angegeben haben.

   ```bash
   sqlcmd -S localhost -U SA -P '<YourPassword>'
   ```

   > [!TIP]
   > Sie können das Kennwort in der Befehlszeile auslassen, damit Sie aufgefordert werden, dieses einzugeben.

   > [!TIP]
   > Wenn Sie später eine Remoteverbindung herstellen möchten, geben Sie den Computernamen oder die IP-Adresse für den Parameter **-S** ein, und stellen Sie sicher, dass der Port 1433 in Ihrer Firewall geöffnet ist.

1. Wenn dies erfolgreich war, sollten zu einer **sqlcmd** Eingabeaufforderung: `1>` gelangen.

1. Wenn Sie einen Verbindungsfehler erhalten, versuchen Sie zunächst das Problem aus der Fehlermeldung zu ermitteln. Überprüfen Sie anschließend die [Empfehlungen zur Verbindungsproblembehandlung](../linux/sql-server-linux-troubleshooting-guide.md#connection).

## <a name="create-and-query-data"></a>Erstellen und Abfragen von Daten
Die folgenden Abschnitte führen Sie durch die Verwendung von **sqlcmd**, um eine neue Datenbank zu erstellen, Daten hinzuzufügen und eine einfache Abfrage auszuführen.

### <a name="create-a-new-database"></a>Erstellen einer neuen Datenbank

Mit den folgenden Schritten wird eine neue Datenbank mit dem Namen `TestDB` erstellt.

1. Fügen Sie aus der **sqlcmd**-Eingabeaufforderung den folgenden Transact-SQL-Befehl zur Erstellung einer Testdatenbank ein:

   ```sql
   CREATE DATABASE TestDB
   ```

1. Schreiben Sie in der nächsten Zeile eine Abfrage, um den Namen all Ihrer Datenbanken auf Ihrem Server zurückzugeben:

   ```sql
   SELECT Name from sys.Databases
   ```

1. Die vorherigen beiden Befehle wurden nicht sofort ausgeführt. Sie müssen `GO` in einer neuen Zeile eingeben, um die zuvor eingegebenen Befehle auszuführen:

   ```sql
   GO
   ```

### <a name="insert-data"></a>Einfügen von Daten

Erstellen Sie als Nächstes eine neue Tabelle, `Inventory`, und fügen Sie zwei neue Zeilen ein.

1. Wechseln Sie den Kontext aus der **sqlcmd**-Eingabeaufforderung zur neuen `TestDB`-Datenbank:

   ```sql
   USE TestDB
   ```

1. Erstellen Sie eine neue Tabelle mit dem Namen `Inventory`:

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. Fügen Sie Daten in die neue Tabelle ein:

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. Geben Sie `GO` ein, um die zuvor eingegebenen Befehle auszuführen:

   ```sql
   GO
   ```

### <a name="select-data"></a>Auswählen von Daten

Führen Sie nun eine Abfrage zum Zurückgeben von Daten aus der `Inventory`-Tabelle aus.

1. Geben Sie aus der **sqlcmd**-Eingabeaufforderung eine Abfrage ein, die Reihen aus der `Inventory`-Tabelle zurückgibt, bei denen die Menge größer als 152 ist:

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. Führen Sie den Befehl aus:

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>Beenden der sqlcmd-Eingabeaufforderung

Zum Beenden der **sqlcmd**-Sitzung, geben Sie `QUIT` ein:

```sql
QUIT
```

## <a name="connect-from-windows"></a>Herstellen einer Verbindung aus Windows

SQL Server-Tools unter Windows stellen eine Verbindung mit SQL Server-Instanzen unter Linux auf die gleiche Weise her, wie sie sich mit einer beliebigen Remoteinstanz von SQL Server verbinden würden.

Wenn Sie einen Windows-Computer haben, der mit Ihrem Linux-Computer eine Verbindung herstellen kann, versuchen Sie die gleichen Schritte in diesem Thema aus einer Windows-Befehlszeile, die **sqlcmd** ausführt. Stellen Sie sicher, dass Sie den Linux-Zielcomputernamen oder die IP-Adresse und nicht localhost verwenden, und stellen Sie sicher, dass der TCP-Port 1433 geöffnet ist. Unter [Empfehlungen zur Verbindungsproblembehandlung](../linux/sql-server-linux-troubleshooting-guide.md#connection) finden Sie weitere Informationen, wenn beim Herstellen einer Verbindung von Windows Probleme auftreten.

Andere Tools, die unter Windows ausgeführt werden, die sich aber mit SQL Server unter Linux verbinden, finden Sie unter:

- [SQL Server Management Studio (SSMS)](../linux/sql-server-linux-develop-use-ssms.md)
- [Windows PowerShell](../linux/sql-server-linux-manage-powershell.md)
- [SQL Server Data Tools (SSDT)](../linux/sql-server-linux-develop-use-ssdt.md)

## <a name="next-steps"></a>Nächste Schritte

Weitere Installationsszenarios finden Sie in den folgenden Ressourcen:

|||
|---|---|
| [Upgrade](../linux/sql-server-linux-setup.md#upgrade) | Erfahren Sie, wie Sie eine vorhandene Installation von SQL unter Linux aktualisieren können. |
| [Deinstallieren](../linux/sql-server-linux-setup.md#uninstall) | Deinstallieren von SQL Server unter Linux |
| [Unbeaufsichtigtes Installieren](../linux/sql-server-linux-setup.md#unattended) | Erfahren Sie, wie Sie die Installation ohne Aufforderungen skripten können. |
| [Offlineinstallation](../linux/sql-server-linux-setup.md#offline) | Erfahren Sie, wie Sie die Pakete für die Offlineinstallation manuell herunterladen können. |

Unter [Visual Studio Code](../linux/sql-server-linux-develop-use-vscode.md) und [SQL Server Management Studio](../linux/sql-server-linux-develop-use-ssms.md) finden Sie andere Möglichkeiten zum Verbinden und Verwalten von SQL Server.

Um mehr über das Schreiben von Transact-SQL-Anweisungen und -Abfragen zu erfahren, schauen Sie sich dieses [Tutorial: Writing Transact-SQL Statements (Tutorial: Schreiben von Transact-SQL-Anweisungen)](../t-sql/tutorial-writing-transact-sql-statements.md) an.
