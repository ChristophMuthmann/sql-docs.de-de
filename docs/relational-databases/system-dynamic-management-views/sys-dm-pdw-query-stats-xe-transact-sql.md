---
title: Sys.dm_pdw_query_stats_xe (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a3f1258ca3c15d7910bb52206c4b7e8e7b2d1845
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwquerystatsxe-transact-sql"></a>Sys.dm_pdw_query_stats_xe (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Diese DMV ist veraltet und wird in einer zukünftigen Version entfernt. In dieser Version gibt es 0 Zeilen zurück.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|Ereignis|**nvarchar(60)**|Der Schlüssel für diese Ansicht.||  
|event_id|**nvarchar(36)**|||  
|create_time|**datetime**|||  
|session_id|**int**|Die Id für die Sitzung.|Finden Sie unter Session_id in [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|cpu|**int**|||  
|reads|**int**|Anzahl logischer Lesevorgänge seit dem Start des Ereignisses.||  
|writes|**int**|Anzahl logischer Schreibvorgänge seit dem Start des Ereignisses.||  
|"sql_text"|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|Knoten, auf denen diese Xevent-Instanz ausgeführt wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
