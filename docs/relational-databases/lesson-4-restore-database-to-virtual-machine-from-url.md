---
title: "Lektion 4: Wiederherstellen einer Datenbank auf einem virtuellen Computer über URLs | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f641f3df1010396d54a655beaaf982a7bff63972
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-4-restore-database-to-virtual-machine-from-url"></a>Lektion 4: Wiederherstellen einer Datenbank auf einem virtuellen Computer über URLs
In dieser Lektion werden Sie die AdventureWorks2014-Datenbank für Ihre Instanz von SQL Server 2016 auf dem virtuellen Computer in Microsoft Azure wiederherstellen.  
  
> [!NOTE]  
> Der Einfachheit halber verwenden wir in diesem Tutorial den gleichen Container für die Daten und Protokolldateien, die wir für die Datenbanksicherung verwenden. In einer Produktionsumgebung würden Sie wahrscheinlich mehrere Container und häufig auch mehrere Datendateien verwenden. Mit SQL Server 2016 könnten Sie auch ein Striping der Sicherung über mehrere Blobs erwägen, um die Backup-Leistung zu steigern, wenn Sie eine große Datenbank sichern.  
  
Zum Wiederherstellen einer SQL Server 2014-Datenbank von Azure Blob Storage auf Ihre SQL Server 2016-Instanz auf dem virtuellen Computer in Microsoft Azure gehen Sie folgendermaßen vor:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie ein neues Abfragefenster und stellen Sie eine Verbindung mit der SQL Server 2016-Instanz des Datenbankmoduls auf Ihrem virtuellen Azure-Computer her.  
  
3.  Kopieren Sie das folgende Transact-SQL-Skript in das Abfragefenster. Ändern Sie die URL gemäß Ihres Speicherkontonamens und des Containers, den Sie in Lektion 1 angegeben haben, und führen Sie dieses Skript anschließend aus.  
  
    ```  
  
    -- Restore AdventureWorks2014 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Data.mdf'  
         ,MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  Öffnen Sie den Objekt-Explorer und erstellen Sie eine Verbindung mit Ihrer Azure SQL Server 2016-Instanz.  
  
5.  Erweitern Sie im Objekt-Explorer den Knoten Datenbanken und überprüfen Sie, ob die AdventureWorks2014-Datenbank wiederhergestellt wurde (Aktualisieren Sie den Knoten nach Bedarf).  
  
    ![Adventure Works 2014-Datenbank in SQL Server 2016 im virtuellen Computer wiederhergestellt](../relational-databases/media/311f69a6-8443-4df5-8f30-3103c2472300.JPG "Adventure Works 2014 database restored to SQL Server 2016 in virtual machine")  
  
6.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf AdventureWorks2014 und klicken Sie auf Eigenschaften (klicken Sie auf „Abbrechen“, wenn fertig).  
  
7.  Klicken Sie auf Dateien und überprüfen Sie, dass die Pfade für die zwei Datenbankdateien URLs sind, die auf Blobs in Ihrem Azure-Blog-Container verweisen.  
  
    ![Datenbankeigenschaften, die den Dateipfad der logischen Datendateien als URL anzeigen](../relational-databases/media/cfeee576-6319-460e-9fa2-f0922e02ee23.JPG "database properties showing file path of logical data files as URL")  
  
8.  Stellen Sie im Objekt-Explorer eine Verbindung mit dem Azure-Speicher her.  
  
9. Container erweitern – erweitern Sie den Container, den Sie in Lektion 1 erstellt haben, und überprüfen Sie, ob „AdventureWorks2014_Data.mdf“ und „AdventureWorks2014_Log.ldf“ aus Schritt 3 oben in diesem Container erscheinen, zusammen mit der Backup-Datei aus Lektion 3 (aktualisieren Sie den Knoten nach Bedarf).  
  
    ![Adventure Works 2014 Daten- und Protokolldateien erscheinen als Blobs in Azure-Container](../relational-databases/media/156c7d73-44be-4754-9653-04cccb6c3066.JPG "Adventure Works 2014 data and log file appear as blobs in Azure container")  
  
**Nächste Lektion:**  
  
[Lektion 5: Backup einer Datenbank mit Dateimomentaufnahme-Sicherung](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
  
