---
title: Wiederherstellen einer Datenbank und Binden der Datenbank an einen Ressourcenpool | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd9e0ff8de0d4c7099200dfbb329709db437bb53
ms.lasthandoff: 04/11/2017

---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>Wiederherstellen einer Datenbank und Binden der Datenbank an einen Ressourcenpool
  Obwohl Sie über genügend Arbeitsspeicher zum Wiederherstellen einer Datenbank mit speicheroptimierten Tabellen verfügen, sollten Sie bewährte Methoden befolgen und die Datenbank an einen benannten Ressourcenpool binden. Da die Datenbank vorhanden sein muss, bevor Sie diese an den Pool binden können, besteht die Wiederherstellung der Datenbank aus mehreren Schritten. In diesem Thema werden die einzelnen Schritte erläutert.  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>Wiederherstellen einer Datenbank mit speicheroptimierten Tabellen  
 Mit den folgenden Schritten wird die IMOLTP_DB-Datenbank vollständig wiederhergestellt und an Pool_IMOLTP gebunden.  
  
1.  [Wiederherstellen mit NORECOVERY](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_NORECOVERY)  
  
2.  [Erstellen des Ressourcenpools](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_createPool)  
  
3.  [Binden der Datenbank und des Ressourcenpools](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_bind)  
  
4.  [Wiederherstellen mit RECOVERY](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_RECOVERY)  
  
5.  [Überwachen der Ressourcenpoolleistung](../../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md#bkmk_Monitor)  
  
###  <a name="bkmk_NORECOVERY"></a> Wiederherstellen mit NORECOVERY  
 Wenn Sie eine Datenbank mit NORECOVERY wiederherstellen, wird die Datenbank erstellt und das Datenträgerimage wiederhergestellt, ohne dass Speicher beansprucht wird.  
  
```tsql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
###  <a name="bkmk_createPool"></a> Erstellen des Ressourcenpools  
 Durch folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code wird ein Ressourcenpool mit dem Namen "Pool_IMOLTP" erstellt. 50 % des verfügbaren Arbeitsspeichers werden dem Pool zur Verfügung gestellt.  Nachdem der Pool erstellt wurde, wird die Ressourcenkontrolle neu konfiguriert, um "Pool_IMOLTP" einzuschließen.  
  
```tsql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
###  <a name="bkmk_bind"></a> Binden der Datenbank und des Ressourcenpools  
 Binden Sie die Datenbank mithilfe der `sp_xtp_bind_db_resource_pool` -Systemfunktion an den Ressourcenpool. Die Funktion akzeptiert zwei Parameter: den Datenbanknamen gefolgt vom Ressourcenpoolnamen.  
  
 Mit folgender [!INCLUDE[tsql](../../includes/tsql-md.md)] wird eine Bindung zwischen der IMOLTP_DB-Datenbank und dem Pool_IMOLTP-Ressourcenpool definiert. Die Bindung wird erst wirksam, nachdem der nächste Schritt ausgeführt wurde.  
  
```tsql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
###  <a name="bkmk_RECOVERY"></a> Wiederherstellen mit RECOVERY  
 Wenn Sie die Datenbank mit RECOVERY wiederherstellen, werden die Datenbank online geschaltet und alle Daten wiederhergestellt.  
  
```tsql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
###  <a name="bkmk_Monitor"></a> Überwachen der Ressourcenpoolleistung  
 Überwachen Sie das "Statistiken für Ressourcenpools"-Objekt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sobald die Datenbank an den benannten Ressourcenpool gebunden und mit RECOVERY wiederhergestellt wurde. Weitere Informationen finden Sie unter [SQL Server, "Statistiken für Ressourcenpools"-Objekt](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Binden einer Datenbank mit speicheroptimierten Tabellen an einen Ressourcenpool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [SQL Server, "Statistiken für Ressourcenpools"-Objekt](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
