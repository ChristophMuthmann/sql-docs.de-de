---
title: Sys.dm_exec_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 11620da7ab49a4f45aeda3b2c24dad1559cbeee1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>Sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Workern DMS-Schritte.  
  
 In dieser Ansicht werden die Daten für die letzten 1000 Anforderungen und den aktiven Anforderungen; aktive Anforderungen haben immer die Daten in dieser Ansicht vorhanden.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Fragen Sie, dass dieser Worker DMS Teil of.request_id, Step_index, und Dms_step_index bilden den Schlüssel für diese Ansicht ein.||  
|step_index|**int**|Fragen Sie Schritt, mit dem dieser Arbeitsthread DMS gehört.|Finden Sie unter schrittindex in [sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Der Schritt in der DMS-Plan, den dieser Arbeitsthread ausgeführt wird.|Finden Sie unter [sys.dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|Knoten, der der Arbeitsthread ausgeführt wird.|Finden Sie unter [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|||  
|Typ|**nvarcha(32)**|||  
|status|**nvarchar(32)**|Status dieses Schritts|"Ausstehend" "abgebrochen"Ausführen","Vollständig","Fehlgeschlagen","UndoFailed","PendingCancel",", "Rückgängig", "Abgebrochen"|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|Zeitpunkt, zu dem der Schritt Ausführung begonnen hat|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich End_compile_time der Abfrage zu der dieser Schritt gehört.|  
|end_time|**datetime**|Zeitpunkt, zu dem dieser Schritt hat die Ausführung abgeschlossen, wurde abgebrochen oder fehlerhaft.|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich Start_time, für die Schritte in der Ausführung auf NULL festgelegt oder in die Warteschlange eingereiht.|  
|total_elapsed_time|**int**|Gesamtzeit hinzuaddiert, die die abfrageschritt, in Millisekunden ausgeführt wurde|Zwischen 0 und der Unterschied zwischen End_time und Start_time. 0 für Schritte in Warteschlange.|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|Befehl|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
