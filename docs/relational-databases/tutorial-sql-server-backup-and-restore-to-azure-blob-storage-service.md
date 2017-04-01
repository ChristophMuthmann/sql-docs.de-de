---
title: "Lernprogramm: SQL Server-Sicherung und -Wiederherstellung im Windows Azure-BLOB-Speicherdienst | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016 Preview"
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Lernprogramm: SQL Server-Sicherung und -Wiederherstellung im Windows Azure-BLOB-Speicherdienst
Willkommen bei den ersten Schritten mit der SQL Server-Sicherung und -Wiederherstellung im Lernprogramm für den Windows Azure-BLOB-Speicherdienst. In diesem Lernprogramm erfahren Sie, wie Sie Sicherungen in den Windows Azure-BLOB-Speicherdienst schreiben und daraus wiederherstellen.  
  
## Lernziele  
In diesem Lernprogramm erfahren Sie, wie Sie ein Windows-Speicherkonto, einen BLOB-Container und Anmeldeinformationen für den Zugriff auf das Speicherkonto erstellen, eine Sicherung in den BLOB-Dienst schreiben und eine einfache Wiederherstellung ausführen. Dieses Lernprogramm ist in vier Lektionen aufgeteilt:  
  
[Lektion 1: Erstellen von Windows Azure-Speicherobjekten](../Topic/Lesson%201:%20Create%20Windows%20Azure%20Storage%20Objects.md)  
In dieser Lektion erstellen Sie ein Windows Azure-Speicherkonto und einen BLOB-Container.  
  
[Lektion 2: Erstellen einer SQL Server-Anmeldeinformationen](../Topic/Lesson%202:%20Create%20a%20SQL%20Server%20Credential.md)  
In dieser Lektion erstellen Sie Anmeldeinformationen, um die Sicherheitsinformationen für den Zugriff auf das Windows Azure-Speicherkonto zu speichern.  
  
[Lektion 3: Schreiben einer vollständigen Datenbanksicherung in den Windows Azure-BLOB-Speicherdienst](../Topic/Lesson%203:%20Write%20a%20Full%20Database%20Backup%20to%20the%20Windows%20Azure%20Blob%20Storage%20Service.md)  
In dieser Lektion geben Sie eine T-SQL-Anweisung aus, um eine Sicherung der AdventureWorks2012-Datenbank in den Windows Azure-BLOB-Speicherdienst zu schreiben.  
  
[Lektion 4: Ausführen einer Wiederherstellung von einer vollständigen Datenbanksicherung](../Topic/Lesson%204:%20Perform%20a%20Restore%20From%20a%20Full%20Database%20Backup.md)  
In dieser Lektion geben Sie eine T-SQL-Anweisung aus, um die in der vorherigen Lektion erstellte Datenbanksicherung wiederherzustellen.  
  
### Anforderungen  
Um dieses Lernprogramm abzuschließen, müssen Sie mit vertraut sein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Sichern und Wiederherstellen der Konzepte und T-SQL-Syntax. Damit Sie dieses Lernprogramm ausführen können, muss Ihr System die folgenden Anforderungen erfüllen:  
  
-   Eine Instanz von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]und die AdventureWorks2012-Datenbank sind installiert.  
  
    Die SQL Server-Instanz kann lokal oder auf einem virtuellen Windows Azure-Computer gespeichert sein.  
  
    Anstelle von AdventureWorks2012 können Sie eine Benutzerdatenbank verwenden und die T-SQL-Syntax entsprechend ändern.  
  
-   Das zum Ausgeben von BACKUP- oder RESTORE-Befehlen verwendete Benutzerkonto sollte Mitglied der Datenbankrolle **db_backup operator** sein und über Berechtigungen zum **Ändern beliebiger Anmeldeinformationen**verfügen.  
  
### Zusätzliches Lesematerial  
Die folgenden Themen werden empfohlen, um das Verständnis der Konzepte und bewährten Verfahren zu verbessern, die Sie bei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Sicherungen im Windows Azure-BLOB-Speicherdienst verwenden.  
  
1.  [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server-URL-Sicherung – bewährte Methoden und Problembehandlung](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## Siehe auch  
[Sichern der Datenbank und des Protokolls](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#databaselog)  
[Erstellen einer vollständigen Dateisicherung der primären Dateigruppe](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#filegroups)  
[Wiederherstellen einer Datenbank und Verschieben von Dateien](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#restoredbwithmove)  
  
