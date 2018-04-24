---
title: 'Lektion 8: Wiederherstellen als neue Datenbank aus der Protokollsicherung | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 632c6dbc496da650418ef4bc7239605b0e9e8149
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-8-restore-as-new-database-from-log-backup"></a>Lektion 8: Wiederherstellen als neue Datenbank aus der Protokollsicherung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In dieser Lektion stellen Sie eine AdventureWorks2014-Datenbank als eine neue Datenbank aus einer Sicherung einer Protokolldatei für Datei-Momentaufnahmen wieder her.  
  
In diesem Szenario führen Sie eine Wiederherstellung auf eine SQL Server-Instanz auf einem anderen virtuellen Computer für Geschäftsanalysen und Berichterstellung aus. Die Wiederherstellung auf eine andere Instanz auf einem anderen virtuellen Computer verlagert die Arbeitsauslastung auf einen virtuellen Computer, der für diesen Zweck dediziert und der Größe angepasst ist und entfernt dessen Ressourcenanforderungen vom Transaktionssystem.  
  
Die Wiederherstellung von einer Transaktionsprotokollsicherung mit Dateimomentaufnahme-Sicherung ist sehr schnell und ist erheblich schneller als die traditionelle Streamingsicherung. Mit dem herkömmlichen Streaming von Sicherungen müssten Sie die vollständige Datenbanksicherung, vielleicht eine differenzielle Sicherung und einige oder alle Transaktionsprotokollsicherungen (oder eine neue vollständige Datenbanksicherung) verwenden. Jedoch benötigen Sie bei Dateimomentaufnahme-Sicherungen nur die letzte Protokollsicherung (oder jede andere Protokollsicherung oder zwei angrenzende Protokollsicherungen für die Point-in-Time-Wiederherstellung auf einen Zeitpunkt zwischen zwei Zeitpunkten von Protokollsicherungen). Um es einfacher auszudrücken: Sie benötigen nur einen Momentaufnahmen-Sicherungssatz einer Protokolldatei, weil jede Momentaufnahmesicherung einer Protokolldatei eine Dateimomentaufnahme jeder Datenbankdatei (jede Datendatei und die Protokolldatei) erstellt.  
  
Befolgen Sie folgende Schritte, um eine Datenbank auf eine neue Datenbank einer Transaktionsprotokollsicherung mithilfe einer Dateimomentaufnahme-Sicherung wiederherzustellen:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie ein neues Abfragefenster, und stellen Sie eine Verbinden mit der SQL Server 2016-Instanz des Datenbankmoduls auf einem virtuellen Azure-Computer her.  
  
    > [!NOTE]  
    > Wenn es sich hierbei um einen anderen virtuellen Azure-Computer handelt, als denjenigen, den Sie für die vorherigen Lektionen verwendet haben, stellen Sie sicher, dass Sie die Schritte in [Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)befolgt haben. Wenn Sie eine Wiederherstellung in einen anderen Container durchführen möchten, befolgen Sie die Schritte in [Lektion 1: Erstellen einer Richtlinie und eine Shared Access Signature (SAS) in einem Azure-Container](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md) und [Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md) für den neuen Container.  
  
3.  Kopieren Sie das folgende Transact-SQL-Skript in das Abfragefenster. Wählen Sie die Protokollsicherungsdatei aus, die Sie verwenden möchten. Ändern Sie die URL gemäß Ihres Speicherkontonamens und des Containers, den Sie in Lektion 1 angegeben haben, geben Sie den Namen der Protokollsicherungsdatei an, und führen Sie dieses Skript anschließend aus.  
  
    ```  
  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2014_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE  
  
    ```  
  
4.  Überprüfen Sie die Ausgabe, um sicherzustellen, dass die Wiederherstellung erfolgreich war.  
  
5.  Stellen Sie im Objekt-Explorer eine Verbindung mit dem Azure-Speicher her.  
  
6.  Erweitern Sie „Container“, erweitern Sie den Container, den Sie in Lektion 1 erstellt haben (aktualisieren Sie, falls notwendig), und überprüfen Sie, ob die neuen Daten- und Protokolldateien zusammen mit den Blobs der vorangegangenen Lektionen im Container erscheinen.  
  
    ![Azure-Container zeigt die Daten- und Protokolldateien für die neue Datenbank](../relational-databases/media/e9705083-86bc-4309-a0bf-92c15f174c0a.JPG "Azure-Container zeigt die Daten- und Protokolldateien für die neue Datenbank")  
  
[Lektion 9: Verwalten von Sicherungssätzen und Dateimomentaufnahme-Sicherungen](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)  
  
  
  
