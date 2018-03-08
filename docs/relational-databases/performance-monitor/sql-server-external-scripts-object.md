---
title: SQL Server, Externes Skript-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa53d84e29b23d73f73c93641306b11a328fc2e1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, Externes Skript-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das **SQLServer:Externes Skript** -Objekt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Leistungsindikatoren zum Überwachen der Aktionen in Verbindung mit der Ausführung externer Skripts bereit. Informationen zum Ausführen von externen Skripts finden Sie unter [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 Diese Tabelle beschreibt die Leistungsindikatoren für **externe Skripts** für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Leistungsindikatoren für externe SQL Server-Skripts|Description|  
|------------------------------------------|-----------------|  
|**Execution Errors**|Die Anzahl von Fehlern beim Ausführen externer Skripts.|  
|**Implied Auth. Anmeldungen**|Die Anzahl von Anmeldungen über Satellitenprozesse, die über die implizite Authentifizierung authentifiziert wurden.|  
|**Parallel Executions**|Die Anzahl externer Skripts, die mit @parallel = 1 ausgeführt wurden.|  
|**SQL CC Executions**|Die Anzahl externer Skripts, die mit SQL Compute Context ausgeführt wurden.|  
|**Streaming Executions**|Die Anzahl externer Skripts, die mit dem @r_rowsPerRead-Parameter ausgeführt wurden.|  
|**Total Execution Time (ms)**|Die Gesamtzeit für das Ausführen externer Skripts.|  
|**Total Executions**|Die Anzahl ausgeführter externer Skripts.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
