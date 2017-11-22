---
title: Sys.dm_exec_distributed_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 922f2ce79dbabe3670b3488299a530b2a28e0cc2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>Sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Enthält Informationen über alle Verteilungen der SQL-Abfrage als Teil eines SQL-Schritts in der Abfrage.  In dieser Ansicht werden die Daten für die letzten 1000 Anforderungen; aktive Anforderungen haben immer die Daten in dieser Ansicht vorhanden.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Execution_id und Step_index bilden zusammen den Schlüssel für diese Ansicht. Eindeutige numerische Id der Anforderung zugeordnet ist.|Finden Sie unter-ID in [Sys. dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Der Index des Schritts Abfrage, die diesem Verteilungspunkt gehört.|Finden Sie unter Step_index in [sys.dm_exec_distributed_request_steps &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|compute_node_id|**int**|Der Typ des Vorgangs durch diesen Schritt dargestellt.|Finden Sie unter Compute_node_id in [dm_exec_compute_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|Gibt an, auf dem der Schritt ausgeführt wird.|-1 für die im Gültigkeitsbereich Knoten nicht Verteilungsbereich ausgeführten Anforderungen festgelegt ist.|  
|status|**nvarchar(32)**|Status dieses Schritts|Aktive, abgebrochene, abgeschlossenen, fehlerhafte, in der Warteschlange|  
|error_id|**nvarchar(36)**|Eindeutige Id des Fehlers bei diesem Schritt verknüpft sind, sofern vorhanden|Finden Sie die Id des [sys.dm_exec_compute_node_errors &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL, wenn kein Fehler aufgetreten ist.|  
|start_time|**datetime**|Zeitpunkt, zu dem der Schritt Ausführung begonnen hat|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich End_compile_time der Abfrage zu der dieser Schritt gehört.|  
|end_time|**datetime**|Zeitpunkt, zu dem dieser Schritt hat die Ausführung abgeschlossen, wurde abgebrochen oder fehlerhaft.|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich Start_time, für die Schritte in der Ausführung auf NULL festgelegt oder in die Warteschlange eingereiht.|  
|total_elapsed_time|**int**|Gesamtzeit hinzuaddiert, die die abfrageschritt, in Millisekunden ausgeführt wurde|Zwischen 0 und der Unterschied zwischen End_time und Start_time. 0 für Schritte in Warteschlange.|  
|row_count|**bigint**|Gesamtanzahl der Zeilen, die geändert oder von dieser Anforderung zurückgegeben|0 für Schritte, die nicht ändern oder Daten, Anzahl der betroffenen andernfalls Zeilen zurückgeben. -1 für DMS-Schritte festgelegt ist.|  
|spid|**int**|Sitzungs-Id für die SQL Server-Instanz, die die Verteilung von Abfragen ausführen||  
|Befehl|nvarchar(4000)|Enthält den vollständigen Text des Befehls dieses Schritts an.|Eine beliebige gültige Anforderungszeichenfolge für einen Schritt. Bei mehr als 4000 Zeichen abgeschnitten.|  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
