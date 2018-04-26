---
title: Erste Schritte mit SQL Server 2017 unter Docker | Microsoft-Dokumentation
description: In diesem Schnellstart wird erläutert, wie Sie das Containerimage von SQL Server 2017 mit Docker ausführen können. Anschließend erstellen Sie mit dem Hilfsprogramm „sqlcmd“ eine Datenbank und fragen diese ab.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/07/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: d422a4a755061837c08a6f4f8de4e1889768ac5d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-run-the-sql-server-2017-container-image-with-docker"></a>Schnellstart: Führen Sie die 2017 von SQL Server-Container-Image mit Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Schnellstart wird Docker verwendet, um das SQL Server 2017-Containerimage [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) mithilfe von Pull zu übertragen und auszuführen. Stellen Sie anschließend eine Verbindung mit **sqlcmd** her, um Ihre erste Datenbank zu erstellen und Abfragen auszuführen.

Dieses Image enthält SQL Server für Linux (basierend auf Ubuntu 16.04). Es kann unter Linux mit der Docker-Engine 1.8 und höher und in Docker für Mac bzw. Windows verwendet werden.

> [!NOTE]
> In diesem Schnellstart liegt der Fokus auf dem Image „mssql-sever-**linux**“. Das Windows-Image wird hier zwar nicht behandelt, aber auf der [Docker-Hubseite zu „mssql-server-windows-developer“](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/) erhalten Sie weitere Informationen.

## <a id="requirements"></a> Erforderliche Komponenten

- Docker-Engine 1.8 und höher auf unterstütztem Linux-Betriebssystem oder Docker für Mac bzw. Windows. Weitere Informationen finden Sie unter [Install Docker (Installieren von Docker)](https://docs.docker.com/engine/installation/).
- Mindestens 2 GB freier Speicherplatz auf dem Datenträger
- Mindestens 2 GB RAM
- [Systemanforderungen von SQL Server unter Linux](sql-server-linux-setup.md#system)

## <a name="pull-and-run-the-container-image"></a>Übertragen mithilfe von Pull und Ausführen von Containerimages

1. Übertragen Sie das Linux-Containerimage von SQL Server 2017 mithilfe von Pull aus dem Docker-Hub.

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   Mit dem obenstehenden Befehl wird das neueste Containerimage von SQL Server 2017 mithilfe von Pull übertragen. Wenn Sie ein bestimmtes Image übertragen möchten, fügen Sie einen Doppelpunkt und den Tagnamen hinzu (z.B. `microsoft/mssql-server-linux:2017-GA`). Informationen zu allen verfügbaren Images finden Sie auf der [Docker-Hubseite zu „mssql-server-linux“](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).
   
   Für die Bash-Befehle in diesem Artikel `sudo` verwendet wird. Auf MacOS `sudo` möglicherweise nicht erforderlich. Unter Linux, wenn Sie nicht möchten, verwenden Sie `sudo` um Docker auszuführen, können Sie konfigurieren eine **Docker** Gruppe und Hinzufügen von Benutzern zu dieser Gruppe. Weitere Informationen finden Sie unter [nach der Installation die Schritte für Linux](https://docs.docker.com/install/linux/linux-postinstall/).

1. Zum Ausführen des Containerimages in Docker können Sie eine Bash-Shell (Linux bzw. macOS) oder eine PowerShell-Eingabeaufforderung mit erhöhten Rechten verwenden. Nachfolgend finden Sie den dafür benötigten Befehl:

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
   > Das Kennwort sollte der Standardrichtlinie für SQL Server-Kennwörter entsprechen. Ist dies nicht der Fall, kann der Container SQL Server nicht einrichten und funktioniert nicht mehr. Ein Standardkennwort enthält mindestens acht Zeichen, die aus drei der folgenden vier Kategorien stammen müssen: Großbuchstaben, Kleinbuchstaben, Grundzahlen (0-9) und Symbole. Mit dem Befehl [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) können Sie das Fehlerprotokoll untersuchen.

   > [!NOTE]
   > Standardmäßig wird dabei ein Container erstellt, der die Developer Edition von SQL Server 2017 enthält. Die Vorgehensweise zum Ausführen von Produktionseditionen in Containern weicht hiervon minimal ab. Weitere Informationen finden Sie unter [Run production container images (Ausführen von Containerimages für Produktionsumgebungen)](sql-server-linux-configure-docker.md#production).

   In der folgenden Tabelle finden Sie Beschreibungen der Parameter des vorangegangenen Beispiels für `docker run`:

   | Parameter | Description |
   |-----|-----|
   | **-e "ACCEPT_EULA = Y"** |  Legen Sie für die Variable **ACCEPT_EULA** einen beliebigen Wert fest, um Ihre Zustimmung zum [End-User Licensing Agreement (Benutzerlizenzvertrag)](http://go.microsoft.com/fwlink/?LinkId=746388) zu geben. Diese Einstellung ist für das SQL Server-Image zwingend erforderlich. |
   | **-e 'MSSQL_SA_PASSWORD=\<YourStrong!Passw0rd\>'** | Geben Sie ein starkes Kennwort ein, das aus mindestens acht Zeichen besteht und den [Kennwortanforderungen von SQL Server](../relational-databases/security/password-policy.md) entspricht. Diese Einstellung ist für das SQL Server-Image zwingend erforderlich. |
   | **-p 1401:1433** | Ordnen Sie einen TCP-Port in der Hostumgebung (erster Wert) einem TCP-Port im Container zu (zweiter Wert). In diesem Beispiel überwacht SQL Server Port TCP 1433 im Container. Diese Informationen sind Port 1401 des Hosts zugeordnet. |
   | **--name sql1** | Geben Sie dem Container selbst einen Namen, anstatt einen willkürlich generierten zu verwenden. Wenn Sie mehrere Container ausführen, können Sie nicht denselben Namen mehrfach verwenden. |
   | **microsoft/mssql-server-linux:2017-latest** | Das Linux-Containerimage von SQL Server 2017 |

1. Verwenden Sie den Befehl `docker ps`, um Ihre Docker-Container anzeigen zu lassen.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   Die Ausgabe sollte dann ähnlich wie in diesem Screenshot sein:

   ![Ausgabe des Befehls „docker ps“](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. Wenn in der Spalte **STATUS** **Up** (Aktiv) eingetragen ist, wird SQL Server im Container ausgeführt und überwacht den Port, der in der Spalte **PORTS** angegeben ist. Wenn in der Spalte **STATUS** Ihres SQL Server-Containers **Exited** (Beendet) steht, lesen Sie bitte im [Abschnitt „Problembehebung“ im Konfigurationshandbuch](sql-server-linux-configure-docker.md#troubleshooting) nach.

Der Parameter `-h` (Hostname) ist ebenfalls nützlich, wird der Einfachheit halber jedoch in diesem Tutorial nicht verwendet. Mit ihm lässt sich der interne Name eines Containers in einen benutzerdefinierten Wert ändern. Dieser Name wird in der folgenden Transact-SQL-Abfrage zurückgegeben:

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Wenn Sie für `-h` und `--name` denselben Wert festlegen, kann der Zielcontainer ganz einfach ermittelt werden.

## <a name="change-the-sa-password"></a>Ändern des Systemadministratorkennworts

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>Verbindung mit SQL Server herstellen

In den folgenden Schritten wird im Container das SQL Server-Befehlszeilentool **sqlcmd** genutzt, um eine Verbindung mit SQL Server herzustellen.

1. Verwenden Sie den Befehl `docker exec -it`, um in Ihrem laufenden Container eine interaktive Bash-Shell zu starten. Im folgenden Beispiel steht `sql1` für den Namen, den Sie bei der Erstellung des Containers mit dem Parameter `--name` angegeben haben.

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. Stellen Sie eine lokale Verbindung mit „sqlcmd“ her. „Sqlcmd“ verwendet nicht automatisch den richtigen Pfad. Sie müssen daher selbst den vollständigen Pfand angeben.

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

1. Geben Sie `exit` ein, um die interaktive Befehlszeile in Ihrem Container zu beenden. Der Container wird auch nach dem Beenden der interaktiven Bash-Shell weiter ausgeführt.

## <a id="connectexternal"></a> Herstellen einer Verbindung von außerhalb des Containers

Sie können auch über jedes externe Linux-, Windows- oder macOS-Tool, das SQL-Verbindungen unterstützt, eine Verbindung mit der SQL Server-Instanz auf Ihrem Docker-Computer herstellen.

Mithilfe der folgenden Schritte stellen Sie über **sqlcmd** von außerhalb Ihres Containers eine Verbindung mit SQL Server im Container her. Voraussetzung ist, dass Sie außerhalb Ihres Containers bereits SQL Server-Befehlszeilentools installiert haben. Für alle Tools gelten dieselben Prinzipien. Die Verbindung wird jedoch bei jedem Tool auf eine andere Weise hergestellt.

1. Ermitteln Sie die IP-Adresse des Computers, der Ihren Container hostet. Verwenden Sie dazu unter Linux **Ifconfig** oder **ip addr**. Verwenden Sie unter Windows **ipconfig**.

1. Führen Sie „sqlcmd“ aus. Geben Sie dabei die IP-Adresse und den Port an, der dem Port 1433 Ihres Containers zugeordnet ist. In diesem Beispiel ist das Port 1401 auf dem Hostcomputer.

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. Führen Sie Transact-SQL-Befehle aus. Wenn Sie fertig sind, geben Sie `QUIT` ein.

Für eine Verbindung mit SQL Server werden häufig auch folgende Tools verwendet:

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) unter Windows](sql-server-linux-develop-use-ssms.md)
- [SQL Server Operations Studio (Vorschauversion)](../sql-operations-studio/what-is.md)
- [mssql-cli (Vorschauversion)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>Entfernen Ihres Containers

Wenn Sie den in diesem Tutorial verwendeten SQL Server-Container entfernen möchten, führen Sie die folgenden Befehle aus:

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Wenn Sie einen Container beenden oder entfernen, werden die SQL Server-Daten dauerhaft aus diesem Container gelöscht. Wenn Sie Ihre Daten weiterhin benötigen, [erstellen Sie eine Sicherungskopie des Containers](tutorial-restore-backup-in-sql-server-container.md), oder nutzen Sie für die Containerdaten eine [Methode zur Datenpersistenz](sql-server-linux-configure-docker.md#persist).

## <a name="docker-demo"></a>Docker-Demo

Nachdem Sie nun das SQL Server-Containerimage für Docker getestet haben, sollten Sie auch wissen, welche Vorteile Ihnen Docker beim Entwickeln und Testen bringt. Im folgenden Video sehen Sie, wie sich Docker in einem Continuous Integration-Szenario bzw. einem Continuous Deployment-Szenario verwenden lässt.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>Nächste Schritte

Ein Tutorial zum Wiederherstellen von Sicherungskopien von Datenbanken in einem Container finden Sie unter [Restore a SQL Server database in a Linux Docker container (Wiederherstellen einer SQL Server-Datenbank in einem Docker-Container unter Linux)](tutorial-restore-backup-in-sql-server-container.md). Informationen zu anderen Szenarios, z.B. zum Ausführen mehrerer Container, zur Datenpersistenz und zum Beheben von Problemen, finden Sie unter [Configure SQL Server 2017 container images on Docker (Konfigurieren von SQL Server 2017-Containerimages in Docker)](sql-server-linux-configure-docker.md).

Ressourcen, Feedback und Informationen über bekannte Probleme finden Sie im [GitHub-Repository „mssql-docker“](https://github.com/Microsoft/mssql-docker).
