---
title: "Sichern auf einem gespiegelten Mediensatz (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Sichern auf einem gespiegelten Mediensatz (Transact-SQL)
  In diesem Thema wird beschrieben, wie die [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) -Anweisung zum Angeben eines gespiegelten Mediensatzes beim Sichern einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank verwendet wird. Geben Sie in der BACKUP-Anweisung den ersten Spiegel in der TO-Klausel an. Geben Sie anschließend jeden Spiegel in der MIRROR TO-Klausel des Spiegels an. In den TO- und MIRROR TO-Klauseln müssen die gleiche Anzahl und der gleiche Typ von Sicherungsmedien angegeben werden.  
  
## Beispiel  
 Im folgenden Beispiel wird der in der vorherigen Abbildung dargestellte gespiegelte Mediensatz erstellt und die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank auf beiden Spiegeln gesichert.  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## Verwandte Aufgaben  
 **So stellen Sie Daten von einer gespiegelten Sicherung wieder her**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
## Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  