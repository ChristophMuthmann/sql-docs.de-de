---
title: Sys.dm_exec_query_parallel_workers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/24/2017
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
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: "1"
author: pelopes
ms.author: pelopes
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: dd0653ae9177673026eb07bbc14f2b6769315e00
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>Sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Gibt Worker Verfügbarkeitsinformationen pro Knoten.  
  
|Name|Datentyp|Description|  
|----------|---------------|-----------------|  
|**"node_id"**|**int**|NUMA-Knoten-ID.|  
|**scheduler_count**|**int**|Die Anzahl der Zeitplanungsmodule auf diesem Knoten.|  
|**max_worker_count**|**int**|Maximale Anzahl von Arbeitsthreads für parallele Abfragen.|  
|**reserved_worker_count**|**int**|Anzahl der Arbeitsthreads, die von parallelen Abfragen reserviert sowie die Anzahl der wichtigsten Arbeitsthreads, die von allen Anforderungen verwendet.| 
|**free_worker_count**|**int**|Anzahl der Worker für Aufgaben zur Verfügung.<br /><br />**Hinweis:** jede eingehende Anforderung verarbeitet mindestens 1 Worker, die von der Anzahl der freien Arbeitsthreads subtrahiert wird.  Es ist möglich, dass die Anzahl der freien Worker auf einem stark ausgelasteten Server eine negative Zahl sein kann.| 
|**used_worker_count**|**int**|Anzahl von Arbeitsthreads, die von parallelen Abfragen verwendet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. Anzeigen von aktuellen parallelen Worker-Verfügbarkeit  

``` tsql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [dm_os_workers &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
