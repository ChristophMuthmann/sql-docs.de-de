---
title: Sichern auf einem gespiegelten Mediensatz (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d273a8bb928abfd46e23d28dfdd362f2e8a1441
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Sichern auf einem gespiegelten Mediensatz (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie die [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md)-Anweisung zum Angeben eines gespiegelten Mediensatzes beim Sichern einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank verwendet wird. Geben Sie in der BACKUP-Anweisung den ersten Spiegel in der TO-Klausel an. Geben Sie anschließend jeden Spiegel in der MIRROR TO-Klausel des Spiegels an. In den TO- und MIRROR TO-Klauseln müssen die gleiche Anzahl und der gleiche Typ von Sicherungsmedien angegeben werden.  
  
## <a name="example"></a>Beispiel  
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
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 **So stellen Sie Daten von einer gespiegelten Sicherung wieder her**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
