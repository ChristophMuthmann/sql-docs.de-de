---
title: 'Tutorial: SQL Server-Sicherung und -Wiederherstellung mit dem Azure-BLOB-Speicherdienst | Microsoft-Dokumentation'
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5de443574ba279fb695f8e6aee9e9238eaae7afc
ms.lasthandoff: 04/11/2017

---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Tutorial: SQL Server-Sicherung und -Wiederherstellung mit dem Azure-BLOB-Speicherdienst
In diesem Tutorial erfahren Sie, wie Sie Sicherungen in den Azure-BLOB-Speicherdienst schreiben und daraus wiederherstellen.  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Tutorial erfahren Sie, wie Sie ein Speicherkonto, einen BLOB-Container und Anmeldeinformationen für den Zugriff auf das Speicherkonto erstellen, eine Sicherung in den BLOB-Dienst schreiben und eine einfache Wiederherstellung ausführen. Dieses Lernprogramm ist in vier Lektionen aufgeteilt:  
  
[Lektion 1: Erstellen von Azure-Speicherobjekten](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5)  
In dieser Lektion erstellen Sie ein Azure-Speicherkonto und einen BLOB-Container.  
  
[Lektion 2: Erstellen von SQL Server-Anmeldeinformationen](http://msdn.microsoft.com/library/64f8805c-1ddc-4c96-a47c-22917d12e1ab)  
In dieser Lektion erstellen Sie Anmeldeinformationen, um die Sicherheitsinformationen für den Zugriff auf das Azure-Speicherkonto zu speichern.  
  
[Lektion 3: Schreiben einer vollständigen Datenbanksicherung in den Azure-BLOB-Speicherdienst](http://msdn.microsoft.com/library/454c8296-64e9-46ed-b141-5ebfbc8a4fe2)  
In dieser Lektion geben Sie eine T-SQL-Anweisung aus, um eine Sicherung der AdventureWorks2012-Datenbank in den Azure-BLOB-Speicherdienst zu schreiben.  
  
[Lektion 4: Ausführen einer Wiederherstellung von einer vollständigen Datenbanksicherung](http://msdn.microsoft.com/library/580f76e6-9802-4abc-9043-db6de592c733)  
In dieser Lektion geben Sie eine T-SQL-Anweisung aus, um die in der vorherigen Lektion erstellte Datenbanksicherung wiederherzustellen.  
  
### <a name="requirements"></a>Anforderungen  
Um dieses Tutorial abzuschließen, müssen Sie mit den Sicherungs- und Wiederherstellungskonzepten in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und der T-SQL-Syntax vertraut sein. Damit Sie dieses Lernprogramm ausführen können, muss Ihr System die folgenden Anforderungen erfüllen:  
  
-   Eine Instanz von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] und die AdventureWorks2012-Datenbank sind installiert.  
  
    Die SQL Server-Instanz kann lokal oder auf einem virtuellen Azure-Computer gespeichert sein.  
  
    Anstelle von AdventureWorks2012 können Sie eine Benutzerdatenbank verwenden und die T-SQL-Syntax entsprechend ändern.  
  
-   Das zum Ausgeben von BACKUP- oder RESTORE-Befehlen verwendete Benutzerkonto sollte Mitglied der Datenbankrolle **db_backup operator** sein und über Berechtigungen zum **Ändern beliebiger Anmeldeinformationen** verfügen.  
  
### <a name="additional-reading"></a>Zusätzliches Lesematerial  
Die folgenden Themen werden empfohlen, um das Verständnis der Konzepte und bewährten Verfahren zu verbessern, die Sie bei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Sicherungen im Azure-BLOB-Speicherdienst verwenden.  
  
1.  [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server-URL-Sicherung – bewährte Methoden und Problembehandlung](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)


