---
title: "Lektion 6: Generieren von Aktivität und Erstellen einer Sicherung eines Protokolls mithilfe der Dateimomentaufnahme-Sicherung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ba32c2a03abab77de366687c5e4fe3e72834204
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup"></a>Lektion 6: Generate activity and backup log using file-snapshot backup (Generieren von Aktivität und Erstellen einer Sicherung eines Protokolls mithilfe der Dateimomentaufnahme-Sicherung)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In dieser Lektion generieren Sie Aktivität in der AdventureWorks2014-Datenbank und erstellen regelmäßig Transaktionsprotokollsicherungen mithilfe von Dateimomentaufnahme-Sicherungen. Weitere Informationen zur Verwendung von Momentaufnahme-Sicherungen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Um Aktivität in der AdventureWorks2014-Datenbank zu generieren und regelmäßig Transaktionsprotokollsicherungen mithilfe von Dateimomentaufnahme-Sicherungen zu erstellen, befolgen Sie folgende Schritte:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie zwei neue Abfragefenster und stellen Sie von jedem Abfragefenster aus eine Verbindung mit der SQL Server 2016-Instanz des Datenbankmoduls auf Ihrem virtuellen Azure-Computer her.  
  
3.  Kopieren Sie das folgende Transact-SQL-Skript, fügen Sie es in ein Abfragefenster ein und führen Sie es aus. Beachten Sie, dass die Production.Location-Tabelle über 14 Zeilen verfügt, bevor wir neue Zeilen in Schritt 4 hinzufügen.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
4.  Kopieren Sie die folgenden zwei Transact-SQL-Skripts, und geben Sie sie in die beiden separaten Abfragefenster ein. Ändern Sie die URL gemäß Ihres Speicherkontonamens und des Containers, den Sie in Lektion 1 angegeben haben, und führen Sie diese Skript anschließend gleichzeitig in separaten Abfragefenstern aus. Die Ausführung dieser Skripts nimmt etwa sieben Minuten in Anspruch.  
  
    ```  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2014.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
    ```  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2014.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2014 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  Überprüfen Sie die Ausgabe des ersten Skripts, und beachten Sie, dass die endgültige Zeilenanzahl jetzt 29.939 beträgt.  
  
    ![Zeilenanzahl 29,939 wird angezeigt](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "Zeilenanzahl 29,939 wird angezeigt")  
  
6.  Überprüfen Sie die Ausgabe des zweiten Skripts und beachten Sie, dass jedes Mal, wenn die BACKUP LOG-Anweisung ausgeführt wird, zwei neue Dateimomentaufnahmen erstellt werden: eine Dateimomentaufnahme der Protokolldatei und eine Dateimomentaufnahme der Datendatei – insgesamt also zwei Dateimomentaufnahmen für jede Datenbankdatei. Wenn das zweite Skript abgeschlossen ist, beachten Sie, dass es jetzt insgesamt 16 Dateimomentaufnahmen gibt, also 8 für jede Datenbankdatei: eine von der BACKUP DATABASE-Anweisung und eine für jede Ausführung der BACKUP LOG-Anweisung.  
  
    ![Bereich „Ergebnisse“ zeigt Dateimomentaufnahmen von Daten- und Protokolldateien, wenn eine Protokollsicherung ausgeführt wird](../relational-databases/media/acd213b8-895e-425c-bd72-2bf10e65a5ba.JPG "Bereich „Ergebnisse“ zeigt Dateimomentaufnahmen von Daten- und Protokolldateien, wenn eine Protokollsicherung ausgeführt wird")  
  
    ![Vier Dateimomentaufnahmen werden angezeigt](../relational-databases/media/e7eff77d-85b9-4e52-abd8-e49952c8118a.JPG "Vier Dateimomentaufnahmen werden angezeigt")  
  
    ![Bereich „Ergebnisse“ zeigt insgesamt 16 Dateimomentaufnahmen](../relational-databases/media/c3ddff17-a83c-4bf0-a670-a38834f9c922.JPG "Bereich „Ergebnisse“ zeigt insgesamt 16 Dateimomentaufnahmen")  
  
7.  Stellen Sie im Objekt-Explorer eine Verbindung mit dem Azure-Speicher her.  
  
8.  Erweitern Sie „Container“, erweitern Sie den Container, den Sie in Lektion 1 erstellt haben, und überprüfen Sie, ob 7 neue Sicherungsdateien zusammen mit den Blobs der vorangegangenen Lektionen erscheinen (Aktualisieren Sie, falls notwendig).  
  
    ![Azure-Container zeigt 7 Protokollsicherungblobs](../relational-databases/media/cfa5a326-87a2-4202-9a04-38bf577d2d0b.JPG "Azure container showing 7 log backup blobs")  
  
**Nächste Lektion:**  
  
[Lektion 7: Wiederherstellen des Standes einer Datenbank zu einem bestimmten Zeitpunkt](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
  
