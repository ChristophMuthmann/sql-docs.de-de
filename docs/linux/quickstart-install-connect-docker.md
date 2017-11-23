---
title: Erste Schritte mit SQL Server-2017 auf Docker | Microsoft Docs
description: "Dieser Schnellstart-Lernprogramm zeigt, wie Docker Container-Image von SQL Server-2017 ausgeführt. Anschließend erstellen und Abfragen einer Datenbank mit Sqlcmd."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: acd47bd1e2104027610f7ee38c9b135a785429e5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>Führen Sie die 2017 von SQL Server-Container-Image mit Docker

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Schnellstart-Tutorial, verwenden Sie Docker zum Abrufen und führen Sie das SQL Server-2017 Container-Bild [Mssql-Server – Linux](https://hub.docker.com/r/microsoft/mssql-server-linux/). Verbinden Sie dann mit **Sqlcmd** Ihre erste Datenbank zu erstellen und Ausführen von Abfragen.

Dieses Image besteht aus SQL Server auf Grundlage 16.04 Ubuntu Linux ausgeführt wird. Sie können mit dem Docker-Modul 1.8 unter Linux oder auf Docker für Mac/Windows verwendet werden.

> [!NOTE]
> Dieser Schnellstart konzentriert speziell zur Verwendung der Mssql-Server -**Linux** Bild. Das Windows-Abbild wird nicht behandelt, aber Sie können weitere Informationen finden sie auf der [Mssql-Server-Windows-Entwickler Docker Hub-Seite](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a id="requirements"></a> Erforderliche Komponenten

- Docker-Modul 1.8 für ein beliebiges unterstützt für Mac/Windows, Linux-Distribution oder Docker. Weitere Informationen finden Sie unter [installieren Sie Docker](https://docs.docker.com/engine/installation/).
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

1. Ziehen Sie die SQL Server 2017 Linux-Container-Image von Docker Hub.

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   Mit dem vorherige Befehl ruft das neueste 2017 von SQL Server-Container-Bild. Wenn Sie ein bestimmtes Abbild abrufen möchten, fügen einen Doppelpunkt und der Name des Tags (z. B. `microsoft/mssql-server-linux:2017-GA`). Um alle verfügbaren Images anzeigen zu können, finden Sie unter [der Mssql-Server-Linux-Docker Hub-Seite](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Um die Container-Image mit Docker auszuführen, können Sie den folgenden Befehl aus einer Bash-Shell (Linux/MacOS) oder das PowerShell-Eingabeaufforderung mit erhöhten Rechten.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1401:1433 --name sql1 \
      -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1401:1433 --name sql1 `
      -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > Dies erstellt standardmäßig einen Container mit der Developer-Edition von SQL Server-2017. Der Prozess zum Ausführen von Produktions-Editionen in Containern ist etwas anders. Weitere Informationen finden Sie unter [ausführen Produktion containerimages](sql-server-linux-configure-docker.md#production).

   Die folgende Tabelle enthält eine Beschreibung der Parameter in der vorherigen `docker run` Beispiel:

   | Parameter | Description |
   |-----|-----|
   | **-e "ACCEPT_EULA = Y"** |  Legen Sie die **ACCEPT_EULA** -Variable auf einen beliebigen Wert und bestätigen Sie Ihre Zustimmung zu den [Endbenutzer-Lizenzvertrag](http://go.microsoft.com/fwlink/?LinkId=746388). Erforderlich für das Image von SQL Server festlegen. |
   | **-e "MSSQL_SA_PASSWORD =\<YourStrong! Passw0rd\>"** | Geben Sie Ihren eigenen sicheres Kennwort, das mindestens 8 Zeichen lang und erfüllt die [SQL Server-kennwortanforderungen](../relational-databases/security/password-policy.md). Erforderlich für das Image von SQL Server festlegen. |
   | **p - 1401:1433** | Zuordnen von TCP-Port für die hostumgebung (erster Wert) mit einem TCP-Port im Container (zweite Wert). In diesem Beispiel wird SQL Server lauscht an TCP 1433 im Container, und dies ist an den Port nach 1401, auf dem Host verfügbar gemacht. |
   | **– Name sql1** | Geben Sie einen benutzerdefinierten Namen für den Container, anstatt eine zufällig generierte. Wenn Sie mehrere Container ausführen, können nicht Sie diesen Namen wiederverwenden. |
   | **Microsoft/Mssql-Server-Linux:2017-neueste** | Das SQL Server 2017 Linux-Container-Bild. |

1. Verwenden Sie zum Anzeigen der Docker-Containers die `docker ps` Befehl.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   Ähnlich wie im folgenden Bildschirmfoto Ausgabe sollte angezeigt werden:

   ![Ps-Befehlsausgabe docker](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Wenn die **STATUS** Spalte zeigt den Status **einrichten**, klicken Sie dann SQL Server ausgeführt wird, in dem Container und am Port gelauscht angegeben, der **PORTS** Spalte. Wenn die **STATUS** Spalte für die SQL Server-Container zeigt **Exited**, finden Sie unter der [Problembehandlung Abschnitt des Handbuchs Konfiguration](sql-server-linux-configure-docker.md#troubleshooting).

Die `-h` (Hostname)-Parameter ist auch nützlich, aber er wird nicht in diesem Lernprogramm aus Gründen der Einfachheit verwendet. Dies ändert den internen Namen des Containers, um einen benutzerdefinierten Wert. Dies ist der Name, die Sie sehen, in der folgenden Transact-SQL-Abfrage zurückgegeben:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Festlegen von `-h` und `--name` auf den gleichen Wert ist eine gute Möglichkeit, den Zielcontainer leicht zu erkennen.

## <a name="change-the-sa-password"></a>Ändern Sie das SA-Kennwort

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>Verbindung mit SQL Server herstellen

Die folgenden Schritte verwenden den SQL Server-Befehlszeilentool **Sqlcmd**, innerhalb des Containers für die Verbindung mit SQL Server.

1. Verwenden der `docker exec -it` Befehl zum Starten einer interaktiven Bash-Shell innerhalb Ihres Containers ausgeführt. Im folgenden Beispiel `sql1` wird angegeben, indem die `--name` -Parameter, wenn Sie bei der Erstellung des Containers.

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. Einmal innerhalb des Containers, verbinden Sie lokal mit Sqlcmd. Sqlcmd ist nicht im Pfad standardmäßig, daher Sie den vollständigen Pfad angeben müssen.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
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

## <a id="connectexternal"></a>Herstellen einer Verbindung von außerhalb des Containers

Sie können aber auch mit der SQL Server-Instanz auf dem Docker-Computer alle externen Tools von Linux, Windows oder MacOS verbinden, die SQL-Verbindungen unterstützt.

Die folgenden Schritte verwenden **Sqlcmd** außerhalb Ihres Containers zur Verbindung mit SQL Server ausgeführt wird, im Container. Diese Schritte setzen voraus, dass Sie bereits SQL Server-Befehlszeilentools, die außerhalb Ihres Containers installiert haben. Die gleichen Prinzipale anwenden, wenn Sie andere Tools verwenden, aber die das Herstellen einer Verbindung für jedes Tool eindeutig ist.

1. Suchen Sie die IP-Adresse für den Computer, der den Container hostet. Verwenden Sie unter Linux, **Ifconfig** oder **IP-Adresse**. Unter Windows verwenden, **"ipconfig"**.

1. Ausführen von Sqlcmd Angabe der IP-Adresse und des Ports, die an Port 1433 im Container zugeordnet. In diesem Beispiel ist, der Port 1401 auf dem Hostcomputer.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. Führen Sie Transact-SQL-Befehle. Wenn Sie fertig sind, geben Sie `QUIT`.

Andere häufig verwendete Tools für die Verbindung mit SQL Server gehören:

- [Visual Studio-Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) unter Windows](sql-server-linux-develop-use-ssms.md)

## <a name="remove-your-container"></a>Entfernen Sie Ihres Containers

Wenn Sie den SQL Server-Container, die in diesem Lernprogramm verwendete entfernen möchten, führen Sie die folgenden Befehle aus:

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Beenden und Entfernen eines Containers dauerhaft löscht alle SQL Server-Daten im Container. Wenn Sie Ihre Daten erhalten bleiben müssen [erstellen, und kopieren Sie eine Sicherungsdatei aus dem Container](tutorial-restore-backup-in-sql-server-container.md) , oder verwenden Sie eine [Container Data Persistenz-Technik](sql-server-linux-configure-docker.md#persist).

## <a name="next-steps"></a>Nächste Schritte

Ein Lernprogramm zum Wiederherstellen der Datenbank-Sicherungsdateien in einen Container, finden Sie unter [Wiederherstellen einer SQL Server-Datenbank in einem Linux-Docker-Container](tutorial-restore-backup-in-sql-server-container.md). So untersuchen Sie die anderen Szenarien, z. B. das Ausführen von mehreren Containern Datenpersistenz und Fehlerbehebungen, finden Sie unter [Konfigurieren von SQL Server-2017 Container Bilder auf Docker](sql-server-linux-configure-docker.md).

Darüber hinaus sehen Sie sich die [Mssql-Docker-GitHub-Repository](https://github.com/Microsoft/mssql-docker) für Ressourcen, Feedback und bekannte Probleme.
