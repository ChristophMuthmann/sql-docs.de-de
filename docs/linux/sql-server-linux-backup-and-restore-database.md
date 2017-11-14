---
title: Sichern und Wiederherstellen von SQL Server-Datenbanken unter Linux | Microsoft Docs
description: Informationen Sie zum Sichern und Wiederherstellen von SQL Server-Datenbanken unter Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: a34954f14ad4c40fdc7376f3f35c6a3def6e2ec7
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Sichern und Wiederherstellen der SQL Server-Datenbanken unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Sie können Sicherungen der Datenbanken von SQL Server-2017 unter Linux mit den gleichen Tools wie andere Plattformen schalten. Auf einem Linux-Server, können Sie `sqlcmd` zum Herstellen einer Verbindung mit SQL Server und Sicherungen. Sie können von Windows Herstellen einer Verbindung mit SQL Server on Linux und Sicherungen mit der Benutzeroberfläche. Die Sicherungsfunktion für entspricht dem über Plattformen hinweg. Beispielsweise können Sie Datenbanken sichern, lokal, remote-Laufwerke oder zu [Microsoft Azure Blob-Speicherdienst](http://msdn.microsoft.com/library/dn435916.aspx). 

## <a name="backup-with-sqlcmd"></a>Sicherung mit sqlcmd

Im folgenden Beispiel `sqlcmd` eine Verbindung mit der lokalen SQL Server-Instanz her und nimmt eine vollständige Sicherung einer Benutzerdatenbank aufgerufen `demodb`.

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

### <a name="backup-log-with-sqlcmd"></a>Sicherung des Protokolls mit sqlcmd

Im folgenden Beispiel `sqlcmd` eine Verbindung mit der lokalen SQL Server-Instanz her und nimmt der Sicherung ein Protokollfragments. Nach Abschluss der Sicherung des Protokollfragments wird die Datenbank im Wiederherstellungsstatus befinden. 

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'/var/opt/mssql/data/demodb_LogBackup_2016-11-14_18-09-53.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup_2016-11-14_18-09-53', NOSKIP, NOREWIND, NOUNLOAD,  NORECOVERY ,  STATS = 5"
```

## <a name="restore-with-sqlcmd"></a>Wiederherstellen mit sqlcmd

Im folgenden Beispiel `sqlcmd` eine Verbindung mit der lokalen Instanz von SQL Server her und stellt eine Datenbank wieder her.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'/var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Sicherung und-Wiederherstellung mit dem SQL Server Management Studio (SSMS)

Sie können SSMS auf einem Windows-Computer verwenden, eine Verbindung mit einer Linux-Datenbank und erstellen Sie eine Sicherung über die Benutzeroberfläche. 

>[!NOTE] 
> Verwenden Sie die neueste Version von SSMS, um die Verbindung mit SQL Server. Zum Herunterladen und installieren Sie die neueste Version, finden Sie unter [SSMS herunterladen](http://msdn.microsoft.com/library/mt238290.aspx). 

Die folgenden Schritte führen über eine Sicherung mit SSMS. 

1. Starten Sie SSMS aus, und verbinden Sie Ihre Server in SQL Server-2017 unter Linux.

1. Objekt-Explorer mit der Maustaste auf die Datenbank aus, klicken Sie auf **Aufgaben**, und klicken Sie dann auf **sichern...** .

1. In der **Sicherung Datenbank** im Dialogfeld die Optionen und Parameter überprüfen, und klicken Sie auf **OK**.
 
SQL Server ist die datenbanksicherung abgeschlossen.

Weitere Informationen finden Sie unter [Verwenden von SSMS zum Verwalten von SQL Server on Linux](sql-server-linux-manage-ssms.md).

### <a name="restore-with-sql-server-management-studio-ssms"></a>Wiederherstellen Sie mit SQL Server Management Studio (SSMS) 

Die folgenden Schritte führen Sie durch das Wiederherstellen einer Datenbank mit SSMS.

1. In SSMS mit der Maustaste **Datenbanken** , und klicken Sie auf **Wiederherstellen von Datenbanken...** . 

1. Klicken Sie unter **Quelle** klicken Sie auf **Gerät:** , und klicken Sie dann auf die Auslassungspunkte (...).

1. Ihre Datenbank-Sicherungsdatei suchen, und klicken Sie auf **OK**. 

1. Klicken Sie unter **Wiederherstellungsplan**, überprüfen Sie die Sicherungsdatei und die Einstellungen. Klicken Sie auf **OK**. 

1. SQL Server stellt die Datenbank wieder her. 

## <a name="see-also"></a>Siehe auch

* [Erstellen einer vollständigen Datenbanksicherung (SQLServer)](http://msdn.microsoft.com/library/ms187510.aspx)
* [Sichern eines Transaktionsprotokolls (SQL Server)](http://msdn.microsoft.com/library/ms179478.aspx)
* [BACKUP (Transact-SQL)](http://msdn.microsoft.com/library/ms186865.aspx)
* [SQL Server-Sicherung über URLs](http://msdn.microsoft.com/library/dn435916.aspx)

