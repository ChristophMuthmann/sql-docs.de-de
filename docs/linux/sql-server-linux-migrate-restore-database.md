---
title: Migration von einer SQL Server-Datenbank von Windows, Linux | Microsoft Docs
description: Dieses Thema veranschaulicht das Erstellen einer Sicherung einer SQL Server-Datenbank auf Windows und auf einem Linux-Computer mit SQL Server 2017 RC2 wiederherstellen.
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 2e23ba46381b1fb80b8ac335f6d7630f02a222bb
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Migration von einer SQL Server-Datenbank von Windows, Linux mit Sicherung und Wiederherstellung

SQL Server die Sicherung und die Wiederherstellungsfunktion ist die empfohlene Methode zum Migrieren einer Datenbank von SQL Server unter Windows auf SQL Server 2017 RC2 unter Linux. Dieses Thema enthält eine schrittweise Anleitung für dieses Verfahren. In diesem Tutorial lernen Sie Folgendes:

- Herunterladen der AdventureWorks-Sicherungsdatei auf einem Windows-Computer
- Übertragen Sie die Sicherung auf den Linux-Computer
- Wiederherstellen der Datenbank mithilfe von Transact-SQL-Befehle

> [!NOTE] 
> In diesem Lernprogramm wird davon ausgegangen, dass Sie installiert haben [SQL Server 2017 RC2](sql-server-linux-setup.md) und [SQL Server-Tools](sql-server-linux-setup-tools.md) auf dem Ziel-Linux-Server.

## <a name="download-the-adventureworks-database-backup"></a>Herunterladen der AdventureWorks-Datenbank-Sicherung

Obwohl Sie die gleichen Schritte verwenden können, um eine Datenbank wiederherstellen, stellt die AdventureWorks-Beispieldatenbank ein gutes Beispiel bereit. Es wird als einer vorhandenen Datenbank-Sicherungsdatei.

>[!NOTE] 
> Zum Wiederherstellen einer Datenbank auf SQL Server on Linux muss die Quelle Sicherung von SQL Server 2014 oder SQL Server 2016 übernommen werden. Die SQL Server-Buildnummer Sicherung darf nicht größer als die Wiederherstellung Buildnummer für SQL Server sein.  

1. Wechseln Sie auf dem Windows-Computer zu [https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661) und zum Herunterladen der **Adventure Works 2014 Full Database Backup.zip**.

   > [!TIP] 
   > Obwohl dieses Lernprogramm Sicherung und Wiederherstellung zwischen Windows- und Linux veranschaulicht, können Sie einen Browser auch unter Linux verwenden, die AdventureWorks-Beispiel direkt auf den Linux-Computer herunterladen.

2. Öffnen Sie die Zip-Datei, und extrahieren Sie die Datei AdventureWorks2014.bak in einen Ordner auf Ihrem Computer.

## <a name="transfer-the-backup-file-to-linux"></a>Übertragen Sie die Sicherungsdatei auf Linux

Um die Datenbank wiederherzustellen, müssen Sie zuerst die Sicherungsdatei aus dem Windows-Computer auf den Linux-Zielcomputer übertragen.

1. Installieren Sie für Windows Bash-Shell. Es gibt mehrere Optionen, darunter folgende:

   - Laden Sie eine open-Source-Bash-Shell, wie z. B. [PuTTY](http://www.putty.org/).
   - Oder unter Windows 10, verwenden Sie die neue [integrierte Bash-Shell (Beta)](https://msdn.microsoft.com/en-us/commandline/wsl/about).
   - Oder, wenn Sie Git verwenden, verwenden Sie die [Git Bash-Shell](https://git-scm.com/downloads).

2. Öffnen Sie eine Bash-Shell (Terminaldienste), und navigieren Sie zu dem Verzeichnis, **AdventureWorks2014.bak**.

3. Verwenden der **scp** (sichere Copy)-Befehl, um die Datei auf dem Ziel-Linux-Computer übertragen. Das folgende Beispiel Übertragungen **AdventureWorks2014.bak** auf das Stammverzeichnis des *"user1"* auf dem Server mit dem Namen *linuxserver1*.

   ```bash
   sudo scp AdventureWorks2014.bak user1@linuxserver1:./
   ```
   
   Im vorherigen Beispiel können Sie stattdessen die IP-Adresse anstelle des Namens des Servers bereitstellen.

Es gibt verschiedene Alternativen zur über scp. Eine ist die Verwendung [Samba](https://help.ubuntu.com/community/Samba) beim Einrichten einer SMB-Netzwerkfreigabe zwischen Windows- und Linux. Eine exemplarische Vorgehensweise für Ubuntu finden Sie unter [zum Erstellen einer Netzwerk-Dateifreigabe über Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Sobald eingerichtet, können Sie darauf zugreifen, als eine Netzwerkdatei Freigeben von Windows, z. B.  **\\ \\Machinenameorip\\freigeben**.

## <a name="move-the-backup-file"></a>Verschieben Sie die Sicherungsdatei

An diesem Punkt wird die Sicherungsdatei auf dem Linux-Server. Vor dem Wiederherstellen der Datenbank mit SQL Server müssen Sie die Sicherung in einem Unterverzeichnis des anordnen **/var/opt/mssql**.

1. Öffnen Sie einen Terminal auf dem Ziel-Linux-Computer mit der Sicherung.

2. Geben Sie die Administrator-Modus.

   ```bash
   sudo su
   ```

3. Erstellen Sie ein neues Verzeichnis für die Sicherung. Der Parameter-p wird keine Aktion ausgeführt, wenn das Verzeichnis bereits vorhanden ist.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

4. Verschieben Sie die Sicherungsdatei auf dieses Verzeichnis. Im folgenden Beispiel wird die Sicherungsdatei im home-Verzeichnis befindet *"user1"*. Ändern Sie den Befehl entsprechend den Speicherort der **AdventureWorks2014.bak** auf Ihrem Computer.

   ```bash
   mv /home/user1/AdventureWorks2014.bak /var/opt/mssql/backup/
   ```

5. Exit-super User-Modus.

   ```bash
   exit
   ```

## <a name="restore-the-database-backup"></a>Stellen Sie die datenbanksicherung wieder her.

Um die Sicherung wiederherzustellen, können Sie die RESTORE DATABASE-Transact-SQL (TQL)-Befehl verwenden.

> [!NOTE] 
> Die folgenden Schritte verwenden die Sqlcmd-Tool. Wenn Sie die Installation noch nicht SQL Server-Tools finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).

1. Starten Sie in der gleichen Terminaldienste **Sqlcmd**. Im folgenden Beispiel wird eine Verbindung mit der lokalen SQL Server-Instanz mit der *SA* Benutzer. Geben Sie das Kennwort, wenn Sie dazu aufgefordert werden, oder geben Sie das Kennwort mit dem -P-Parameter.

   ```bash
   sqlcmd -S localhost -U SA
   ```

2. Nachdem die Verbindung hergestellt ist, geben Sie den folgenden **Datenbank wiederherstellen** Befehl nach jeder Zeile die EINGABETASTE drücken. Im Beispiel unten Wiederherstellungen der **AdventureWorks2014.bak** -Datei von der */var/opt/mssql/backup* Verzeichnis.

   ```sql
   RESTORE DATABASE AdventureWorks
   FROM DISK = '/var/opt/mssql/backup/AdventureWorks2014.bak'
   WITH MOVE 'AdventureWorks2014_Data' TO '/var/opt/mssql/data/AdventureWorks2014_Data.mdf',
   MOVE 'AdventureWorks2014_Log' TO '/var/opt/mssql/data/AdventureWorks2014_Log.ldf'
   GO
   ```

   Sie sollten eine Meldung erhalten, die die Datenbank erfolgreich wiederhergestellt wurde.

3. Überprüfen Sie die Wiederherstellung durch die erste, die den Kontext ändern, in der AdventureWorks-Datenbank ein. 

   ```sql
   USE AdventureWorks
   GO
   ```

4. Führen Sie die folgende Abfrage, die der obersten 10 Produkte in aufgeführt sind die **Production.Products** Tabelle.

   ```sql
   SELECT TOP 10 Name, ProductNumber FROM Production.Product ORDER BY Name
   GO
   ```

![Ausgabe aus der Production.Products-Abfrage](./media/sql-server-linux-migrate-restore-database/sql-server-linux-adventureworks-query.png)

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu anderen migrationstechniken Datenbank und die Daten, finden Sie unter [Migrieren von Datenbanken zu SQL Server on Linux](sql-server-linux-migrate-overview.md). 

