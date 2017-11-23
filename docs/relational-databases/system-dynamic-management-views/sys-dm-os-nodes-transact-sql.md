---
title: dm_os_nodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cf36f7156f9297231fc232e8fecafee5e77427c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine interne Komponente mit der Bezeichnung SQLOS erstellt Knotenstrukturen, die die Lage des Hardwareprozessors imitieren. Diese Strukturen können geändert werden, indem soft-NUMA verwendet wird, um benutzerdefinierte Knotenlayouts zu erstellen.  
  
 Die folgende Tabelle enthält Informationen zu diesen Knoten.  
  
> **Hinweis:** dieser DMV aus aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_nodes**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ID des Knotens.|  
|node_state_desc|**nvarchar(256)**|Beschreibung des Knotenzustands. Die Werte werden zuerst mit den sich gegenseitig ausschließenden Werten angezeigt, gefolgt von den kombinierbaren Werten. Beispiel:<br /><br /> Online, Thread Resources Low, Lazy Preemptive<br /><br /> Es gibt vier sich gegenseitig ausschließende Node_state_desc-Werte. Sie können mit ihren Beschreibungen sind unten aufgeführt.<br /><br /> ONLINE: Knoten online ist<br /><br /> OFFLINEMODUS: Knoten ist offline<br /><br /> Im Leerlauf: Knoten verfügt über keine ausstehenden arbeitsanforderungen und hat einen Leerlaufzustand angenommen.<br /><br /> IDLE_READY: Knoten verfügt über keine ausstehenden arbeitsanforderungen und ist bereit für den Leerlauf wechselt.<br /><br /> Es gibt fünf kombinierbare Node_state_desc-Werte, die mit ihren Beschreibungen unten aufgeführt.<br /><br /> DAC: Dieser Knoten ist für die dedizierte Verwaltungsverbindung reserviert.<br /><br /> THREAD_RESOURCES_LOW: Keine neuen Threads können auf diesem Knoten aufgrund einer Bedingung Speichermangel erstellt werden.<br /><br /> HOT ADDED: Gibt an, die Knoten hinzugefügt wurden, als Antwort auf eine aktive CPU-Ereignis hinzufügen.|  
|memory_object_address|**varbinary(8)**|Adresse des Speicherobjekts ist diesem Knoten zugeordnet. 1:1-Beziehung zu sys.dm_os_memory_objects.memory_object_address.|  
|memory_clerk_address|**varbinary(8)**|Adresse des Speicherclerks ist diesem Knoten zugeordnet. 1:1-Beziehung zu sys.dm_os_memory_clerks.memory_clerk_address.|  
|io_completion_worker_address|**varbinary(8)**|Adresse des Arbeitsthreads ist dem E/A-Abschluss für diesen Knoten zugewiesen. 1:1-Beziehung zu sys.dm_os_workers.worker_address.|  
|memory_node_id|**smallint**|ID des Arbeitsspeicherknotens, zu dem dieser Knoten gehört. n:1-Beziehung zu sys.dm_os_memory_nodes.memory_node_id.|  
|cpu_affinity_mask|**bigint**|Bitmap, das die CPUs identifiziert, die diesem Knoten zugeordnet sind.|  
|online_scheduler_count|**smallint**|Die Anzahl der onlinescheduler, die von diesem Knoten verwaltet werden.|  
|idle_scheduler_count|**smallint**|Anzahl der Onlinescheduler, die über keinen aktiven Arbeitsthread verfügen.|  
|active_worker_count|**int**|Anzahl der Arbeitsthreads, die auf allen von diesem Knoten verwalteten Zeitplanungsmodulen aktiv sind.|  
|avg_load_balance|**int**|Durchschnittliche Anzahl von Tasks pro Zeitplanungsmodul auf diesem Knoten.|  
|timer_task_affinity_mask|**bigint**|Bitmap, das die Zeitplanungsmodule identifiziert, denen Zeitgebertasks zugewiesen sein können.|  
|permanent_task_affinity_mask|**bigint**|Bitmap, das die Zeitplanungsmodule identifiziert, denen permanente Zeitgebertasks zugewiesen sein können.|  
|resource_monitor_state|**bit**|Jeder Knoten verfügt über einen zugewiesenen Ressourcenmonitor. Der Ressourcenmonitor kann ausgeführt werden oder sich im Leerlauf befinden. Der Wert 1 gibt an, dass der Monitor ausgeführt wird, der Wert 0 gibt an, dass er sich im Leerlauf befindet.|  
|online_scheduler_mask|**bigint**|Identifiziert die Prozessaffinitätsmaske für diesen Knoten.|  
|processor_group|**smallint**|Identifiziert die Gruppe von Prozessoren für diesen Knoten.|  
|cpu_count |**int** |Anzahl der CPUs, die für diesen Knoten verfügbar. |
|pdw_node_id|**int**|Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.<br /><br /> **Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
  
## <a name="see-also"></a>Siehe auch  
  
 [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  


