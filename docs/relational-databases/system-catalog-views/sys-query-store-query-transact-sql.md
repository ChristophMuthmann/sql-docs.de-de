---
title: query_store_query (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 698478831feeb5ad8719147e03a006ab56ba0eb3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysquerystorequery-transact-sql"></a>query_store_query (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Enthält Informationen über die Abfrage und die zugehörigen allgemeinen aggregierten laufzeitausführung.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**"query_id"**|**bigint**|Der Primärschlüssel.|  
|**query_text_id**|**bigint**|Fremdschlüssel. Verknüpft mit [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|Fremdschlüssel. Verknüpft mit [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md).|  
|**object_id**|**bigint**|ID des Datenbankobjekts, das die Abfrage angehört (gespeicherte Prozedur, Trigger, CLR-UDF/UDAgg, usw..). 0, wenn die Abfrage nicht als Teil eines Datenbankobjekts (Ad-hoc-Abfrage) ausgeführt wird.|  
|**batch_sql_handle**|**varbinary(64)**|ID des-Anweisungsbatch, die Abfrage stammt. Nur aufgefüllt, wenn die Abfrage temporäre Tabellen oder Tabellenvariablen verweist auf.|  
|**query_hash**|**binary(8)**|MD5-Hash der einzelnen Abfrage basierend auf der logischen Abfragestruktur. Enthält Hinweise für den Abfrageoptimierer an.|  
|**is_internal_query**|**bit**|Die Abfrage wurde intern generiert.|  
|**query_parameterization_type**|**tinyint**|Die Art der Parametrisierung:<br /><br /> 0 – keine<br /><br /> 1 – Benutzer<br /><br /> 2 – einfach<br /><br /> 3 – erzwungen|  
|**query_parameterization_type_desc**|**nvarchar(60)**|Die textbeschreibung für den Typ der Parametrisierung.|  
|**initial_compile_start_time**|**datetimeoffset**|Kompilieren Sie die Startzeit.|  
|**last_compile_start_time**|**datetimeoffset**|Kompilieren Sie die Startzeit.|  
|**last_execution_time**|**datetimeoffset**|Zeitpunkt der letzten Ausführung bezieht sich auf die letzte Endzeit des Abfrageplans /.|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|Handle der letzten SQL-Batches, die in der Abfrage zuletzt verwendet wurde. Es kann angegeben werden, als Eingabe für [Sys. dm_exec_sql_text &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) beim Abrufen des vollständigen Texts des Batches.|  
|**last_compile_batch_offset_start**|**bigint**|Informationen, die für Sys. dm_exec_sql_text zusammen mit Last_compile_batch_sql_handle bereitgestellt werden kann.|  
|**last_compile_batch_offset_end**|**bigint**|Informationen, die für Sys. dm_exec_sql_text zusammen mit Last_compile_batch_sql_handle bereitgestellt werden kann.|  
|**count_compiles**|**bigint**|Statistiken, die Kompilierung.|  
|**avg_compile_duration**|**float**|Statistiken, die Kompilierung in Mikrosekunden.|  
|**last_compile_duration**|**bigint**|Statistiken, die Kompilierung in Mikrosekunden.|  
|**avg_bind_duration**|**float**|Binden von Statistiken in Mikrosekunden.|  
|**last_bind_duration**|**bigint**|Statistiken, die Bindung.|  
|**avg_bind_cpu_time**|**float**|Statistiken, die Bindung.|  
|**last_bind_cpu_time**|**bigint**|Statistiken, die Bindung.|  
|**avg_optimize_duration**|**float**|Statistiken zur abfrageoptimierung in Mikrosekunden.|  
|**last_optimize_duration**|**bigint**|Statistiken zur abfrageoptimierung.|  
|**avg_optimize_cpu_time**|**float**|Statistiken zur abfrageoptimierung in Mikrosekunden.|  
|**last_optimize_cpu_time**|**bigint**|Statistiken zur abfrageoptimierung.|  
|**avg_compile_memory_kb**|**float**|Kompilieren einer Speicherstatistik an.|  
|**last_compile_memory_kb**|**bigint**|Kompilieren einer Speicherstatistik an.|  
|**max_compile_memory_kb**|**bigint**|Kompilieren einer Speicherstatistik an.|  
|**is_clouddb_internal_query**|**bit**|Immer 0 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lokal.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW DATABASE STATE** Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys. query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [Sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
