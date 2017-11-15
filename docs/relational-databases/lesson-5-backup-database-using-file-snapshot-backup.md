---
title: 'Lektion 5: Backup einer Datenbank mit Dateimomentaufnahme-Sicherung | Microsoft-Dokumentation'
ms.custom: SQL2016_New_Updated
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b5e0888f00f34fc3d85f6727cc98903c66c2239
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-backup-database-using-file-snapshot-backup"></a>Lektion 5: Backup einer Datenbank mit Dateimomentaufnahme-Sicherung
In dieser Lektion werden Sie in Ihrem virtuellen Azure-Computer Ihre AdventureWorks2014-Datenbank per Dateimomentaufnahme-Sicherung zum Ausführen einer nahezu sofortigen Sicherung mithilfe von Azure-Momentaufnahmen sichern. Weitere Informationen zu Momentaufnahme-Sicherungen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
  
So sichern Sie die AdventureWorks2014-Datenbank mithilfe der Dateimomentaufnahme-Sicherung:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie ein neues Abfragefenster und stellen Sie eine Verbindung mit der SQL Server 2016-Instanz des Datenbankmoduls auf Ihrem virtuellen Azure-Computer her.  
  
3.  Kopieren Sie das folgende Transact-SQL-Skript in das Abfragefenster und führen Sie es aus (schließen Sie dieses Abfragefenster nicht – Sie werden dieses Skript in Schritt 5 erneut ausführen). Diese vom System gespeicherte Prozedur ermöglicht Ihnen, die vorhandenen Dateimomentaufnahme-Sicherungen für jede Datei anzuzeigen, die eine angegebene Datenbank enthält. Sie werden feststellen, dass es keine Dateimomentaufnahme-Sicherungen für diese Datenbank gibt.  
  
    ```  
  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
4.  Kopieren Sie das folgende Transact-SQL-Skript in das Abfragefenster. Ändern Sie die URL gemäß Ihres Speicherkontonamens und des Containers, den Sie in Lektion 1 angegeben haben, und führen Sie dieses Skript anschließend aus. Beachten Sie, wie schnell diese Sicherung ausgeführt wird.  
  
    ```  
  
    -- Backup the AdventureWorks2014 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Azure.bak'   
       WITH FILE_SNAPSHOT;  
  
    ```  
  
    ![Bereich „Ergebnisse“ mit Dateimomentaufnahmen der einzelnen Datenbankdateien](../relational-databases/media/2a9320e0-067a-485a-8e0e-636660005e5c.JPG "results pane showing file snapshots of each database file")  
  
5.  Nachdem Sie überprüft haben, dass das Skript in Schritt 4 erfolgreich ausgeführt wurde, führen Sie das folgende Skript erneut aus. Beachten Sie, dass die Dateimomentaufnahme-Sicherung in Schritt 4 Dateimomentaufnahmen der Daten und der Protokolldatei generiert hat.  
  
    ```  
  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![Ergebnisse der sys.fn_db_backup_file_snapshots-Funktion mit 2 Momentaufnahmen](../relational-databases/media/fca1436e-9607-4432-97ee-f66ac2f2108d.JPG "results of the sys.fn_db_backup_file_snapshots function showing 2 snapshots")  
  
6.  Im Objekt-Explorer in Ihrer SQL Server 2016-Instanz in Ihrem virtuellen Azure-Computer erweitern Sie den Knoten Datenbanken, und überprüfen Sie, ob die AdventureWorks2014-Datenbank in dieser Instanz wiederhergestellt wurde (aktualisieren Sie den Knoten nach Bedarf).  
  
7.  Stellen Sie im Objekt-Explorer eine Verbindung mit dem Azure-Speicher her.  
  
8.  Container erweitern – erweitern Sie den Container, den Sie in Lektion 1 erstellt haben, und überprüfen Sie, ob die AdventureWorks2014_Azure.bak aus Schritt 4 oben in diesem Container erscheint, zusammen mit der Backup-Datei aus Lektion 3 und den Datenbank-Dateien aus Lektion 4 (aktualisieren Sie den Knoten nach Bedarf).  
  
    ![Dateimomentaufnahmesicherung wird im Azure-Container angezeigt](../relational-databases/media/181bc970-4af7-4272-a9ae-4bef674f2e02.JPG "File snapshot backup appears in the Azure container")  
  
**Nächste Lektion:**  
  
[Lektion 6: Generate activity and backup log using file-snapshot backup (Generieren von Aktivität und Erstellen einer Sicherung eines Protokolls mithilfe der Dateimomentaufnahme-Sicherung)](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
## <a name="see-also"></a>Siehe auch  
[Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
  
  
  
