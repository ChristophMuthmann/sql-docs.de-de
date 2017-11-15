---
title: "Lektion 9: Verwalten von Sicherungssätzen und Dateimomentaufnahme-Sicherungen | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 766a0846-db15-4346-b814-4049039bcbfc
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc4ce7fe2c3648da7923dbb35fbfe252c971b006
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-9-manage-backup-sets-and-file-snapshot-backups"></a>Lektion 9: Verwalten von Sicherungssätzen und Dateimomentaufnahme-Sicherungen
In dieser Lektion löschen Sie einen Sicherungssatz mithilfe der gespeicherten Systemprozedur [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) . Diese gespeicherte Systemprozedur löscht die Sicherungsdatei und die Dateimomentaufnahme in jeder Datenbankdatei, die diesem Sicherungssatz zugeordnet ist.  
  
> [!NOTE]  
> Wenn Sie versuchen, einen Sicherungssatz zu löschen, indem Sie einfach die Sicherungsdatei aus dem Azure-Blobcontainer löschen, löschen Sie nur die Sicherungsdatei selbst und die zugehörigen Dateimomentaufnahmen bleiben bestehen. Wenn Sie vor diesem Problem stehen, verwenden Sie die Systemfunktion [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) , um die URL der verwaisten Dateimomentaufnahmen zu identifizieren und anschließend die gespeicherte Systemprozedur [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) , um jede verwaiste Dateimomentaufnahme zu löschen. Weitere Informationen finden Sie unter  [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Befolgen Sie folgende Schritte, um einen Dateimomentaufnahme-Sicherungssatz zu löschen:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie ein neues Abfragefenster, und stellen Sie eine Verbinden mit der SQL Server 2016-Instanz des Datenbankmoduls auf Ihrem virtuellen Azure-Computer her (oder mit einer beliebigen SQL Server 2016-Instanz mit Lese-/Schreibberechtigungen für diesen Container).  
  
3.  Kopieren Sie das folgende Transact-SQL-Skript in das Abfragefenster. Wählen Sie die Protokollsicherung aus, die Sie zusammen mit den zugehörigen Dateimomentaufnahmen löschen möchten. Ändern Sie die URL gemäß Ihres Speicherkontonamens und des Containers, den Sie in Lektion 1 angegeben haben, geben Sie den Namen der Protokollsicherungsdatei an, und führen Sie dieses Skript anschließend aus.  
  
    ```  
  
    sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-9164-20150726012420.bak';  
  
    ```  
  
4.  Stellen Sie im Objekt-Explorer eine Verbindung mit dem Azure-Speicher her.  
  
5.  Erweitern Sie die Container, erweitern Sie den Container, den Sie in Lektion 1 erstellt haben und stellen Sie sicher, dass die Sicherung aus Schritt 3 nicht länger im Container angezeigt wird (aktualisieren Sie den Knoten bei Bedarf).  
  
    ![Azure-Container zeigt das Löschen des Speicherprotokollblobs](../relational-databases/media/c0070b08-4667-4db5-aaff-987a404ec934.JPG "Azure container showing the deletion of the log backup blob")  
  
6.  Kopieren Sie das folgende Transact-SQL-Skript, fügen Sie es in das Abfragefenster ein, und führen Sie es anschließend aus, um sicherzustellen, dass zwei Dateimomentaufnahmen gelöscht wurden.  
  
    ```  
  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![Bereich „Ergebnisse“ mit 2 gelöschten Dateimomentaufnahmen](../relational-databases/media/f3891361-dfb6-4f4d-a090-ebfeb977981e.JPG "Bereich „Ergebnisse“ mit 2 gelöschten Dateimomentaufnahmen")  
  
**Ende des Tutorials**  
  
## <a name="see-also"></a>Siehe auch  
[Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
  

