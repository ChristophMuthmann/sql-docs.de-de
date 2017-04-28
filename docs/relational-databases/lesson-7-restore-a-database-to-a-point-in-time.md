---
title: 'Lektion 7: Wiederherstellen des Standes einer Datenbank zu einem bestimmten Zeitpunkt | Microsoft-Dokumentation'
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a25788a3b7eda518aeff01329eb5e207d9092bd6
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>Lektion 7: Wiederherstellen des Standes einer Datenbank zu einem bestimmten Zeitpunkt
In dieser Lektion stellen Sie eine AdventureWorks2014-Datenbank zu einem Zeitpunkt zwischen zwei Transaktionsprotokollsicherungen wieder her.  
  
Um bei herkömmlichen Sicherungen einen bestimmten Zeitpunkt wiederherzustellen zu können, müssen Sie über eine vollständige Sicherung der Datenbank, z.B. eine differenzielle Sicherung, sowie über alle Transaktionsprotokolldateien bis zu diesem und direkt nach diesem Zeitpunkt verfügen, den Sie wiederherstellen möchten. Mit Dateimomentaufnahme-Sicherungen benötigen Sie nur die zwei angrenzenden Protokollsicherungsdateien als Zeitrahmen, den Sie wiederherstellen möchten. Sie benötigen nur zwei Momentaufnahmesicherungssätze, weil jede Momentaufnahmesicherung einer Protokolldatei eine Dateimomentaufnahme jeder Datenbankdatei (jede Datendatei und die Protokolldatei) erstellt.  
  
Zum Wiederherstellen einer Datenbank bis zu einem bestimmten Zeitpunkt per Dateimomentaufnahmesicherungssätzen gehen Sie folgendermaßen vor:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie ein neues Abfragefenster und stellen Sie eine Verbindung mit der SQL Server 2016-Instanz des Datenbankmoduls auf Ihrem virtuellen Azure-Computer her.  
  
3.  Kopieren Sie das folgende Transact-SQL-Skript, fügen Sie es in das Abfragefenster ein und führen Sie es aus. Überprüfen Sie, ob die Production.Location-Tabelle 29.939 Zeilen hat, bevor wir sie zu einem bestimmten Zeitpunkt wiederherstellen, wenn in Schritt 5 weniger Zeilen vorhanden sind.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![Zeilenanzahl 29,939 wird angezeigt](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "Zeilenanzahl 29,939 wird angezeigt")  
  
4.  Kopieren Sie das folgende Transact-SQL-Skript in das Abfragefenster. Wählen Sie zwei aufeinander folgende Backup-Log-Dateien und konvertieren Sie den Dateinamen in das Datum und die Zeit, die Sie für dieses Skript benötigen. Ändern Sie die URL gemäß Ihres Speicherkontonamens und des Containers, den Sie in Lektion 1 angegeben haben, geben Sie die Namen der ersten und zweiten Protokollsicherungsdatei an, geben Sie die STOPAT-Zeit im Format „June 26, 2015 01:48 PM“ an und führen Sie dieses Skript anschließend aus. Dieses Skript wird einige Minuten in Anspruch nehmen.  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  Überprüfen Sie die Ausgabe. Beachten Sie, dass nach der Wiederherstellung die Anzahl der Zeilen 18.389 ist, also eine Zeilenzahl zwischen Sicherung 5 und 6 ist (die Zeilenanzahl variiert).  
  
    ![Bereich „Ergebnisse“ zeigt die Anzahl der Zeilen nach der Zeitpunktwiederherstellung](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "Bereich „Ergebnisse“ zeigt die Anzahl der Zeilen nach der Zeitpunktwiederherstellung")  
  
**Nächste Lektion:**  
  
[Lektion 8. Wiederherstellen als neue Datenbank aus der Protokollsicherung](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
  

