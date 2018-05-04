---
title: Ausführung bezogene dynamische Verwaltungssichten und-Funktionen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dynamic management objects [SQL Server], execution
- execution-related dynamic management objects [SQL Server]
ms.assetid: aea07b33-f715-4b61-9d1e-8c77b03e9578
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11959a6b715cdf6ceef85433fbf4253a303066ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="execution-related-dynamic-management-views-and-functions-transact-sql"></a>Dynamische Verwaltungssichten und -funktionen im Zusammenhang mit der Ausführung (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Dieser Abschnitt enthält die folgenden dynamischen Verwaltungsobjekte.  
  

|||  
|-|-| 
|[sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)|[sys.dm_exec_background_job_queue_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-stats-transact-sql.md)|
|[sys.dm_exec_cached_plan_dependent_objects](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plan-dependent-objects-transact-sql.md)|[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)|
|[sys.dm_exec_compute_node_errors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|
|[sys.dm_exec_compute_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|
|[sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)|[sys.dm_exec_describe_first_result_set](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)|
|[sys.dm_exec_describe_first_result_set_for_object](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)|[sys.dm_exec_distributed_request_steps](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|
|[sys.dm_exec_distributed_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|
|[sys.dm_exec_dms_services](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|
|[sys.dm_exec_external_operations](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|
|[sys.dm_exec_function_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md)| [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)|
|[sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|[sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)|
|[sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)|[sys.dm_exec_query_optimizer_info](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql.md)|
|[sys.dm_exec_query_optimizer_memory_gateways](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-memory-gateways.md) |[sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) |
|[sys.dm_exec_query_parallel_workers](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-parallel-workers-transact-sql.md)|[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)|
|[sys.dm_exec_query_resource_semaphores](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)|[sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)|
|[sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|
|[sys.dm_exec_session_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)|[sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)|
|[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)|[sys.dm_exec_text_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)|
|[sys.dm_exec_trigger_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)|[sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)|
|[sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)|[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)|
|[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | |

  
> [!NOTE]  
>  Die **dm_exec_query_transformation_stats** -verwaltungssicht wird nur zu Informationszwecken identifiziert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

