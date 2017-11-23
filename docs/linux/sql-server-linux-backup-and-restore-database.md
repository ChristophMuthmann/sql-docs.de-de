---
title: Sichern und Wiederherstellen von SQL Server-Datenbanken unter Linux | Microsoft Docs
description: Informationen Sie zum Sichern und Wiederherstellen von SQL Server-Datenbanken unter Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 11/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.workload: On Demand
ms.openlocfilehash: 4693d53a8318a4d8ac5ecfa696203688737dad25
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Sichern und Wiederherstellen der SQL Server-Datenbanken unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Sie können Sicherungen der Datenbanken von SQL Server-2017 unter Linux mit den gleichen Tools wie andere Plattformen schalten. Auf einem Linux-Server, können Sie **Sqlcmd** zum Herstellen einer Verbindung mit SQL Server und Sicherungen. Sie können von Windows Herstellen einer Verbindung mit SQL Server on Linux und Sicherungen mit der Benutzeroberfläche. Die Sicherungsfunktion für entspricht dem über Plattformen hinweg. Beispielsweise können Sie Datenbanken sichern, lokal, remote-Laufwerke oder zu [Microsoft Azure Blob-Speicherdienst](../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="backup-a-database"></a>Sichern einer Datenbank

Im folgenden Beispiel **Sqlcmd** eine Verbindung mit der lokalen SQL Server-Instanz her und nimmt eine vollständige Sicherung einer Benutzerdatenbank aufgerufen `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Wenn Sie den Befehl ausführen, wird SQL Server zur Kennworteingabe aufgefordert. Nachdem Sie das Kennwort eingegeben haben, wird die Shell die Ergebnisse der Sicherungsstatus zurück. Beispiel:

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>Sichern des Transaktionsprotokolls

Wenn Ihre Datenbank in das vollständige Wiederherstellungsmodell ist, können Sie auch Sicherungen des Transaktionsprotokolls für eine detailliertere Wiederherstellungsoptionen vornehmen. Im folgenden Beispiel **Sqlcmd** eine Verbindung mit der lokalen SQL Server-Instanz her und nimmt ein Transaktionsprotokoll sichern.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>Wiederherstellen einer Datenbank

Im folgenden Beispiel **Sqlcmd** eine Verbindung mit der lokalen Instanz von SQL Server her und stellt die Demodb-Datenbank wieder her. Beachten Sie, dass die `NORECOVERY` Option wird verwendet, um zusätzliche Wiederherstellung von protokollsicherungen für die Datei zu ermöglichen. Wenn Sie nicht beabsichtigen, zusätzliche Protokolldateien wiederhergestellt werden, entfernen die `NORECOVERY` Option.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'/var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> Wenn Sie versehentlich WITH NORECOVERY, aber keine zusätzlichen Protokollsicherungsdateien, führen Sie den Befehl `RESTORE DATABASE demodb` ohne zusätzliche Parameter. Die Wiederherstellung abzuschließen wird und die Datenbank bleibt einsatzbereit.

### <a name="restore-the-transaction-log"></a>Wiederherstellen des Transaktionsprotokolls

Der folgende Befehl stellt vorherige Sicherung des Transaktionsprotokolls wieder her.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Sicherung und-Wiederherstellung mit dem SQL Server Management Studio (SSMS)

Sie können SSMS auf einem Windows-Computer verwenden, eine Verbindung mit einer Linux-Datenbank und erstellen Sie eine Sicherung über die Benutzeroberfläche.

>[!NOTE] 
> Verwenden Sie die neueste Version von SSMS, um die Verbindung mit SQL Server. Zum Herunterladen und installieren Sie die neueste Version, finden Sie unter [SSMS herunterladen](../ssms/download-sql-server-management-studio-ssms.md). Weitere Informationen zum Verwenden von SSMS finden Sie unter [Verwenden von SSMS zum Verwalten von SQL Server on Linux](sql-server-linux-manage-ssms.md).

Die folgenden Schritte führen über eine Sicherung mit SSMS. 

1. Starten Sie SSMS aus, und verbinden Sie Ihre Server in SQL Server-2017 unter Linux.

1. Objekt-Explorer mit der Maustaste auf die Datenbank aus, klicken Sie auf **Aufgaben**, und klicken Sie dann auf **sichern...** .

1. In der **Sicherung Datenbank** im Dialogfeld die Optionen und Parameter überprüfen, und klicken Sie auf **OK**.
 
SQL Server ist die datenbanksicherung abgeschlossen.

### <a name="restore-with-sql-server-management-studio-ssms"></a>Wiederherstellen Sie mit SQL Server Management Studio (SSMS) 

Die folgenden Schritte führen Sie durch das Wiederherstellen einer Datenbank mit SSMS.

1. In SSMS mit der Maustaste **Datenbanken** , und klicken Sie auf **Wiederherstellen von Datenbanken...** . 

1. Klicken Sie unter **Quelle** klicken Sie auf **Gerät:** , und klicken Sie dann auf die Auslassungspunkte (...).

1. Ihre Datenbank-Sicherungsdatei suchen, und klicken Sie auf **OK**. 

1. Klicken Sie unter **Wiederherstellungsplan**, überprüfen Sie die Sicherungsdatei und die Einstellungen. Klicken Sie auf **OK**. 

1. SQL Server stellt die Datenbank wieder her. 

## <a name="see-also"></a>Siehe auch

* [Erstellen einer vollständigen Datenbanksicherung (SQLServer)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [Sichern eines Transaktionsprotokolls (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [SQL Server-Sicherung über URLs](../relational-databases/backup-restore/sql-server-backup-to-url.md)
