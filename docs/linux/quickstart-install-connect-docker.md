---
title: Erste Schritte mit SQL Server-2017 auf Docker | Microsoft Docs
description: "Dieser Schnellstart-Lernprogramm zeigt, wie Docker Container-Image von SQL Server-2017 ausgeführt. Anschließend erstellen und Abfragen einer Datenbank mit Sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 77d8c7d01cd5d7a1787b9deddbe7003e09e32e6f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Führen Sie die 2017 von SQL Server-Container-Image mit Docker

In diesem Schnellstart-Tutorial, verwenden Sie Docker zum Abrufen und führen Sie das SQL Server 2017 RC2-containerimage [Mssql-Server – Linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). Verbinden Sie dann mit **Sqlcmd** Ihre erste Datenbank zu erstellen und Ausführen von Abfragen.

Dieses Image besteht aus SQL Server auf Grundlage 16.04 Ubuntu Linux ausgeführt wird. Sie können mit dem Docker-Modul 1.8 unter Linux oder auf Docker für Mac/Windows verwendet werden.

> [!NOTE]
> Mit diesem Schnellstart wird speziell zur Verwendung der Mssql-Server-Linux-Image. Das Windows-Abbild wird nicht behandelt, aber Sie können weitere Informationen finden sie auf der [Mssql-Server-Windows Docker Hub-Seite](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a id="requirements"></a> Erforderliche Komponenten

- Docker-Modul 1.8 für ein beliebiges unterstützt für Mac/Windows, Linux-Distribution oder Docker.
- Mindestens 4 GB Speicherplatz
- Mindestens 4 GB RAM
- [Systemanforderungen für SQL Server on Linux](sql-server-linux-setup.md#system).

> [!IMPORTANT]
> Die Standardeinstellung zu Docker für Mac und Docker für Windows beträgt 2 GB für die VM Moby, damit auf 4 GB geändert werden muss. Wenn Sie auf Mac oder Windows ausgeführt werden, verwenden Sie die folgenden Verfahren, um den Arbeitsspeicher zu erhöhen.

### <a name="increase-docker-memory-to-4-gb-mac"></a>Erhöhen Sie den Docker-Arbeitsspeicher auf 4 GB (Mac)

Die folgenden Schritte geben Sie Speicher für Docker für Mac auf 4 GB.

1. Klicken Sie auf das Docker-Logo in der oberen Statusleiste.
1. Wählen Sie **Voreinstellungen**.
1. Verschieben Sie den Indikator Arbeitsspeicher auf 4 GB oder mehr.
1. Klicken Sie auf die **Neustart** Schaltfläche auf die Schaltfläche des Bildschirms.

### <a name="increase-docker-memory-to-4-gb-windows"></a>Erhöhen Sie den Docker-Arbeitsspeicher auf 4 GB (Windows)

Die folgenden Schritte geben Sie Speicher für Docker für Windows auf 4 GB.

1. Mit der rechten Maustaste auf das Symbol "Docker" aus der Taskleiste.
1. Klicken Sie auf **Einstellungen** unter diesem Menü.
1. Klicken Sie auf die **erweiterte** Registerkarte.
1. Verschieben Sie den Indikator Arbeitsspeicher auf 4 GB oder mehr.
1. Klicken Sie auf die **übernehmen** Schaltfläche.

## <a name="pull-and-run-the-container-image"></a>Ziehen Sie aus, und führen Sie das Container-Bild

1. Ziehen Sie die Container-Image von Docker Hub.

    ```bash
    docker pull microsoft/mssql-server-linux
    ```

    > [!TIP]
    > Für Linux, abhängig von Ihrer Konfiguration System- und Benutzer müssen möglicherweise jede voranzustellen `docker` mit `sudo`.

1. Um die Container-Image mit Docker auszuführen, können Sie den folgenden Befehl in einem Bash-Shell (Linux/MacOS):

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    Wenn Sie Docker für Windows verwenden, verwenden Sie den folgenden Befehl an einer PowerShell-Eingabeaufforderung:

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
    ```

    > [!NOTE]
    > Der einzige Unterschied zwischen der Bash (Linux/MacOS) und dem PowerShell (Windows)-Beispiel ist die einfache Anführungszeichen und doppelte Anführungszeichen um die Umgebungsvariablen. "Docker run" Befehl schlägt fehl, wenn Sie die falsche Datei verwenden. Im Rest dieses Themas werden Bash und PowerShell-Codeblöcken der Einfachheit halber bereitgestellt. Ist nur ein Beispiel, funktioniert es auf allen Plattformen, einschließlich Windows.

    Die folgende Tabelle enthält eine Beschreibung der Parameter in der vorherigen `docker run` Beispiel:

    | Parameter | Description |
    |-----|-----|
    | **-e "ACCEPT_EULA = Y"** |  Legen Sie die **ACCEPT_EULA** -Variable auf einen beliebigen Wert und bestätigen Sie Ihre Zustimmung zu den [Endbenutzer-Lizenzvertrag](http://go.microsoft.com/fwlink/?LinkId=746388). Erforderlich für das Image von SQL Server festlegen. |
    | **-e "MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>"** | Geben Sie Ihren eigenen sicheres Kennwort, das mindestens 8 Zeichen lang und erfüllt [kennwortanforderungen wie SQL Server](../relational-databases/security/password-policy.md). Erforderlich für das Image von SQL Server festlegen. |
    | **-e "MSSQL_PID = Entwickler"** | Gibt die Edition oder Product Key an. In diesem Beispiel wird kostenlos lizenzierte Developer Edition nicht für die Produktion zu Testzwecken verwendet. Weitere Werte finden Sie unter [konfigurieren Sie SQL Server-Einstellungen mit Umgebungsvariablen unter Linux](sql-server-linux-configure-environment-variables.md). |
    | **--SYS_PTRACE Cap-hinzufügen** | Fügt die Linux-Funktion für die Ablaufverfolgung von eines Prozess hinzu. Dadurch werden SQL Server zum Generieren von Dumps einer Ausnahme abgebrochen. |
    | **p - 1401:1433** | Zuordnen von TCP-Port für die hostumgebung (erster Wert) mit einem TCP-Port im Container (zweite Wert). In diesem Beispiel wird SQL Server lauscht an TCP 1433 im Container, und dies ist an den Port nach 1401, auf dem Host verfügbar gemacht. |
    | **Microsoft/Mssql-Server – linux** | Das SQL Server-Linux-containerimage. Sofern nicht anders angegeben, wird standardmäßig die **neueste** Bild. |

1. Verwenden Sie zum Anzeigen der Docker-Containers die `docker ps` Befehl.

    ```bash
    docker ps -a
    ```

    Ähnlich wie im folgenden Bildschirmfoto Ausgabe sollte angezeigt werden:

    ![Ps-Befehlsausgabe docker](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Wenn die **STATUS** Spalte zeigt den Status **einrichten**, klicken Sie dann SQL Server ausgeführt wird, in dem Container und am Port gelauscht angegeben, der **PORTS** Spalte. Wenn die **STATUS** Spalte für die SQL Server-Container zeigt **Exited**, finden Sie unter der [Problembehandlung Abschnitt des Handbuchs Konfiguration](sql-server-linux-configure-docker.md#troubleshooting).

Es gibt zwei nützliche `docker run` Optionen, die im vorherigen Beispiel nicht verwendet werden, aus Gründen der Einfachheit. Die `-h` (Hostname) Parameter ändert den internen Namen des Containers in einen benutzerdefinierten Wert. Dies ist der Name, die Sie sehen, in der folgenden Transact-SQL-Abfrage zurückgegeben:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Stellen Sie außerdem möglicherweise die `--name` Parameter nützlich, benennen Sie den Container, anstatt einen generierten Containernamen an. Festlegen von `-h` und `--name` auf den gleichen Wert ist eine gute Möglichkeit, den Zielcontainer leicht zu erkennen.

## <a name="change-the-sa-password"></a>Ändern Sie das SA-Kennwort

Das SA-Konto ist ein Systemadministrator für die SQL Server-Instanz, die während des Setups erstellt wird. Nach dem Erstellen des SQL Server-Containers, der `MSSQL_SA_PASSWORD` Umgebungsvariable, die Sie angegeben ist erkennbar, durch Ausführen `echo $MSSQL_SA_PASSWORD` im Container. Aus Gründen der Sicherheit ändern Sie Ihrer SA-Kennwort.

1. Wählen Sie ein sicheres Kennwort für das SA-Benutzer verwenden.

1. Verwendung `docker exec` auszuführende **Sqlcmd** , die mithilfe von Transact-SQL-Kennwort zu ändern. Ersetzen Sie `<Old Password>` und `<New Password>` mit Ihrem Kennwortwerten.

> ```bash
> docker exec -it <Container ID> /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<Old Password>' -Q 'ALTER LOGIN SA WITH PASSWORD="<New Password>";'
> ```

## <a name="connect-to-sql-server"></a>Verbindung mit SQL Server herstellen

Die folgenden Schritte verwenden den SQL Server-Befehlszeilentool **Sqlcmd**, innerhalb des Containers für die Verbindung mit SQL Server.

1. Verwenden der `docker exec -it` Befehl zum Starten einer interaktiven Bash-Shell innerhalb Ihres Containers ausgeführt. Im folgenden Beispiel `e69e056c702d` die Container-ID.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Sie müssen immer die gesamte Container-Id angeben. Sie müssen nur genügend Zeichen zur eindeutigen Identifizierung angeben. In diesem Beispiel wird es ausreichend, um die verwenden u. u. `e6` oder `e69` und nicht die vollständige Id.

1. Einmal innerhalb des Containers, verbinden Sie lokal mit Sqlcmd. Sqlcmd ist nicht im Pfad standardmäßig, daher Sie den vollständigen Pfad angeben müssen.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

   > [!TIP]
   > Sie können das Kennwort in der Befehlszeile auslassen, damit Sie aufgefordert werden, es einzugeben.

1. Wenn dies erfolgreich war, sollten zu einer **sqlcmd** Eingabeaufforderung: `1>` gelangen.

## <a name="create-and-query-data"></a>Erstellen und Abfragen von Daten

Die folgenden Abschnitte führen Sie durch die Verwendung von **sqlcmd** und Transact-SQL, um eine neue Datenbank zu erstellen, Daten hinzuzufügen und eine einfache Abfrage auszuführen.

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

1. Zum Beenden der **sqlcmd**-Sitzung, geben Sie `QUIT` ein:

   ```sql
   QUIT
   ```

1. Geben Sie zum Beenden der interaktive eingabeaufforderungs im Container `exit`. Der Container wird weiterhin ausgeführt wird, nach dem Beenden der interaktiven Bash-Shell.

## <a name="connect-from-outside-the-container"></a>Herstellen einer Verbindung von außerhalb des Containers

Sie können aber auch mit der SQL Server-Instanz auf dem Docker-Computer alle externen Tools von Linux, Windows oder MacOS verbinden, die SQL-Verbindungen unterstützt.

Die folgenden Schritte verwenden **Sqlcmd** außerhalb Ihres Containers zur Verbindung mit SQL Server ausgeführt wird, im Container. Diese Schritte setzen voraus, dass Sie bereits SQL Server-Befehlszeilentools, die außerhalb Ihres Containers installiert haben. Die gleichen Prinzipale anwenden, wenn Sie andere Tools verwenden, aber die das Herstellen einer Verbindung für jedes Tool eindeutig ist.

1. Suchen Sie die IP-Adresse für den Computer, der den Container hostet. Verwenden Sie unter Linux, **Ifconfig** oder **IP-Adresse**. Unter Windows verwenden, **"ipconfig"**.

1. Ausführen von Sqlcmd Angabe der IP-Adresse und des Ports, die an Port 1433 im Container zugeordnet. In diesem Beispiel ist, der Port 1401 auf dem Hostcomputer.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
   ```

1. Führen Sie Transact-SQL-Befehle. Wenn Sie fertig sind, geben Sie `QUIT`.

Andere häufig verwendete Tools für die Verbindung mit SQL Server gehören:

- [Visual Studio-Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) unter Windows](sql-server-linux-develop-use-ssms.md)

## <a name="next-steps"></a>Nächste Schritte

So untersuchen Sie die anderen Szenarien, z. B. das Ausführen mehrerer Container, Datenpersistenz und Troublehshooting, finden Sie unter [Konfigurieren von SQL Server-2017 Container Bilder auf Docker](sql-server-linux-configure-docker.md).

Darüber hinaus sehen Sie sich die [Mssql-Docker-GitHub-Repository](https://github.com/Microsoft/mssql-docker) für Ressourcen, Feedback und bekannte Probleme.

