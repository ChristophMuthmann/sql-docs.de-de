---
title: Wiederherstellen einer SQL Server-Datenbank in Docker | Microsoft Docs
description: In diesem Lernprogramm werden wiederherstellen wie einer SQL Server-datenbanksicherung in einem neuen Linux-Docker-Container.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: ad11495a927d5ca37e15cb872a200a55beb93b35
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Wiederherstellen einer SQL Server-Datenbank in einem Linux-Docker-container

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Lernprogramm veranschaulicht, wie verschoben und Wiederherstellen einer SQL Server-Sicherungsdatei in einem SQL Server 2017 Linux-containerimage in Docker ausgeführt wird.

> [!div class="checklist"]
> * Pull übertragen Sie, und führen Sie das neueste SQL Server 2017 Linux-Container-Bild.
> * Kopieren Sie die World Wide Importers-Datenbankdatei in den Container.
> * Wiederherstellen der Datenbank im Container.
> * Führen Sie Transact-SQL-Anweisungen zum Anzeigen und ändern die Datenbank an.
> * Sichern Sie die geänderte Datenbank.

## <a name="prerequisites"></a>Erforderliche Komponenten

* Docker-Engine 1.8 und höher auf unterstütztem Linux-Betriebssystem oder Docker für Mac bzw. Windows. Weitere Informationen finden Sie unter [Install Docker (Installieren von Docker)](https://docs.docker.com/engine/installation/).
* Mindestens 2 GB freier Speicherplatz auf dem Datenträger
* Mindestens 2 GB RAM
* [Systemanforderungen von SQL Server unter Linux](sql-server-linux-setup.md#system)

## <a name="pull-and-run-the-container-image"></a>Übertragen mithilfe von Pull und Ausführen von Containerimages

1. Öffnen Sie ein Terminal Bash auf Linux/Mac oder einer mit erhöhten Rechten auf Windows PowerShell-Sitzung.

1. Übertragen Sie das Linux-Containerimage von SQL Server 2017 mithilfe von Pull aus dem Docker-Hub.

    ```bash
    sudo docker pull microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker pull microsoft/mssql-server-linux:2017-latest
    ```

    > [!TIP]
    > In diesem Lernprogramm werden Beispiele für Docker-Befehle für die Bash-Shell (Linux/Mac) und der PowerShell (Windows) angegeben.

1. Um die Container-Image mit Docker auszuführen, können Sie den folgenden Befehl aus:

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql1' -p 1401:1433 \
       -v sql1data:/var/opt/mssql \
       -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql1" -p 1401:1433 `
       -v sql1data:/var/opt/mssql `
       -d microsoft/mssql-server-linux:2017-latest
    ```

    Dieser Befehl erstellt einen 2017 von SQL Server-Container mit der Developer Edition (Standard). SQL Server-Port **1433** wird verfügbar gemacht werden, auf dem Host als Port **1401**. Das optionale `-v sql1data:/var/opt/mssql` Parameter erstellt einen Daten-Volume-Container mit dem Namen **sql1ddata**. Dient zur persistenten Speicherung der Daten, die von SQL Server erstellt.

   > [!NOTE]
   > Der Prozess zum Ausführen von SQL Server-Editionen Produktion in Containern ist etwas anders. Weitere Informationen finden Sie unter [Run production container images (Ausführen von Containerimages für Produktionsumgebungen)](sql-server-linux-configure-docker.md#production). Wenn Sie die gleichen Containernamen und Ports verwenden, funktioniert die restliche in dieser exemplarischen Vorgehensweise weiterhin mit Produktions-Containern.

1. Verwenden Sie den Befehl `docker ps`, um Ihre Docker-Container anzeigen zu lassen.

    ```bash
    sudo docker ps -a
    ```

    ```PowerShell
    docker ps -a
    ```
 
1. Wenn in der Spalte **STATUS** **Up** (Aktiv) eingetragen ist, wird SQL Server im Container ausgeführt und überwacht den Port, der in der Spalte **PORTS** angegeben ist. Wenn in der Spalte **STATUS** Ihres SQL Server-Containers **Exited** (Beendet) steht, lesen Sie bitte im [Abschnitt „Problembehebung“ im Konfigurationshandbuch](sql-server-linux-configure-docker.md#troubleshooting) nach.

   ```
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        microsoft/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

## <a name="change-the-sa-password"></a>Ändern des Systemadministratorkennworts

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>Kopieren einer Sicherungsdatei in den container

Dieses Lernprogramm verwendet den [Beispieldatenbank von Wide World Importers](../sample/world-wide-importers/wide-world-importers-documentation.md). Verwenden Sie die folgenden Schritte aus, um herunterladen und kopieren Sie die Datenbanksicherungsdatei Wide World Importers in Ihrer SQL Server-Container.

1. Verwenden Sie zuerst **Docker Exec** zum Erstellen eines Sicherungsordners. Der folgende Befehl erstellt eine **/Var/opt/Mssql/** innerhalb der SQL Server-Container.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. Als Nächstes Herunterladen der [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) Datei auf dem Hostcomputer. Die folgenden Befehle, navigieren Sie zu Hause/Benutzerverzeichnis und lädt die Sicherungsdatei als **wwi.bak**.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. Verwendung **Docker cp** , kopieren die Sicherungsdatei in den Container in der **/var/opt/mssql/backup** Verzeichnis.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>Stellen Sie die Datenbank wieder her.

Die Sicherungsdatei befindet sich jetzt innerhalb des Containers. Bevor Sie die Sicherung wiederherstellt, ist es wichtig zu wissen, logische Dateinamen und Dateitypen in der Sicherung. Die folgenden Transact-SQL-Befehle überprüfen Sie die Sicherung und die Ausführung der Wiederherstellung mit **Sqlcmd** im Container.

> [!TIP]
> Dieses Lernprogramm verwendet **Sqlcmd** innerhalb des Containers, da der Container mit diesem Tool vorinstallierte Version stammt. Sie können jedoch auch ausführen Transact-SQL-Anweisungen mit anderen Client Tools außerhalb der Container, z. B. [Visual Studio Code](sql-server-linux-develop-use-vscode.md) oder [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md). Um eine Verbindung herzustellen, verwenden Sie den hostPort, der Port 1433 im Container zugeordnet wurde. In diesem Beispiel ist das **"localhost", "1401** auf dem Hostcomputer und **Host_IP_Address 1401** Remote.

1. Führen Sie **Sqlcmd** im Container aufzulisten logischen Dateinamen und Pfade innerhalb der Sicherung. Dies erfolgt mit der **RESTORE FILELISTONLY** Transact-SQL-Anweisung.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   Ausgabe ähnlich der folgenden sollte angezeigt werden:

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. Rufen Sie die **RESTORE DATABASE** Befehl zum Wiederherstellen der Datenbank innerhalb des Containers. Geben Sie neue Pfade für die einzelnen Dateien im vorherigen Schritt.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   Ausgabe ähnlich der folgenden sollte angezeigt werden:

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>Überprüfen Sie die wiederhergestellte Datenbank

Führen Sie die folgende Abfrage aus, um eine Liste von Datenbanknamen im Container anzuzeigen:

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

Daraufhin sollte **"wideworldimporters"** in der Liste der Datenbanken.

## <a name="make-a-change"></a>Nehmen Sie eine Änderung

Die folgenden Schritte stellen eine Änderung in der Datenbank.

1. Führen Sie eine Abfrage zum Anzeigen der obersten 10 Elemente in der **Warehouse.StockItems** Tabelle.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   Eine Liste der Element-IDs und Namen sollte angezeigt werden:

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. Aktualisieren Sie die Beschreibung des ersten Elements mit den folgenden **UPDATE** Anweisung:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   Ähnliche Informationen wie in den folgenden Text sollte angezeigt werden:

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>Erstellen Sie eine neue Sicherung

Nachdem Sie Ihre Datenbank in einen Container wiederhergestellt haben, möchten Sie möglicherweise auch regelmäßig datenbanksicherungen im ausgeführten Container zu erstellen. Die Schritte eines ähnlichen Musters mit den vorherigen Schritten jedoch in umgekehrter Reihenfolge.

1. Verwenden der **SICHERUNGSDATENBANK** Transact-SQL-Befehl aus, um eine Sicherung im Container zu erstellen. In diesem Lernprogramm erstellt eine neue Sicherungsdatei **wwi_2.bak**, in dem zuvor erstellten **/var/opt/mssql/backup** Verzeichnis.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   Ausgabe ähnlich der folgenden sollte angezeigt werden:

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. Kopieren Sie anschließend die Sicherungsdatei aus dem Container, und klicken Sie auf dem Hostcomputer.

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>Verwenden Sie die beibehaltenen Daten

Zusätzlich zum Einbinden von datenbanksicherungen für Ihre Daten zu schützen, können Sie auch datenvolumecontainer verwenden. Anfang des Lernprogramms erstellt die **sql1** Container mit der `-v sql1data:/var/opt/mssql` Parameter. Die **sql1data** volumecontainer Daten weiterhin die **/var/opt/mssql** Daten, nachdem der Container entfernt wurde. Entfernen Sie die folgenden Schritte aus der **sql1** Container, und erstellen Sie einen neuen Container **sql2**, mit der persistenten Daten.

1. Beenden der **sql1** Container.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Entfernen des Containers an. Dadurch wird nicht das zuvor erstellte gelöscht **sql1data** Data-Volume-Container und die persistenten Daten.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Erstellen Sie einen neuen Container **sql2**, und Wiederverwenden der **sql1data** Data-Volume-Container.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

1. Die Wide World Importers-Datenbank ist jetzt in den neuen Container. Führen Sie eine Abfrage, um die vorangegangene Änderung zu überprüfen, die Sie vorgenommen.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > Das SA-Kennwort ist nicht das Kennwort für die Angabe der **sql2** Container `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Alle SQL Server-Daten aus wiederhergestellt wurde **sql1**, z. B. das geänderte Kennwort aus zuvor im Lernprogramm. Aktiviert ist, sind einige Optionen wie folgt wegen Wiederherstellen der Daten in /var/opt/mssql ignoriert. Aus diesem Grund ist das Kennwort `<YourNewStrong!Passw0rd>` wie hier gezeigt.

## <a name="next-steps"></a>Nächste Schritte

In diesem Lernprogramm haben Sie gelernt, wie Sichern einer Datenbank auf Windows und verschieben Sie sie für einen Linux-Server, die mit SQL Server 2017 RC2. Sie haben gelernt, wie auf:
> [!div class="checklist"]
> * SQL Server 2017 Linux-Container-Images zu erstellen.
> * Kopieren Sie Sicherungen für SQL Server-Datenbank in einen Container.
> * Ausführen von Transact-SQL-Anweisungen innerhalb des Containers mit **Sqlcmd**.
> * Erstellen und Sichern von Dateien aus einem Container zu extrahieren.
> * Verwenden Sie datenvolumecontainer in Docker, um SQL Server-Daten beizubehalten.

Überprüfen Sie dann die anderen Docker-Konfiguration und Problembehandlung von Szenarien:

> [!div class="nextstepaction"]
>[Für die Basiskonfiguration für SQL Server-2017 für Docker](sql-server-linux-configure-docker.md)
