---
title: dm_exec_cached_plan_dependent_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plan_dependent_objects
- dm_exec_cached_plan_dependent_objects_TSQL
- sys.dm_exec_cached_plan_dependent_objects_TSQL
- dm_exec_cached_plan_dependent_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plan_dependent_objects dynamic management function
ms.assetid: 9b6cf5f7-b267-44fb-aac8-f49c9aa10cc1
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e9303dd028cdc979e978e05ea87afe7718a566ba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexeccachedplandependentobjects-transact-sql"></a>sys.dm_exec_cached_plan_dependent_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jeden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ausführungsplan, CLR-Ausführungsplan (Common Language Runtime) und einem Plan zugeordneten Cursor zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
dm_exec_cached_plan_dependent_objects(plan_handle)  
```  
  
## <a name="arguments"></a>Argumente  
 *plan_handle*  
 Führt eine eindeutige Identifizierung eines Abfrageausführungsplans für einen ausgeführten Batch aus, dessen Plan sich im Plancache befindet. *plan_handle* ist vom Datentyp **varbinary(64)**. *plan_handle* kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**usecounts**|**int**|Die Anzahl von Verwendungen des Ausführungskontexts oder Cursors.<br /><br /> NULL-Werte sind in der Spalte nicht zulässig.|  
|**memory_object_address**|**varbinary(8)**|Speicheradresse des Ausführungskontexts oder Cursors.<br /><br /> NULL-Werte sind in der Spalte nicht zulässig.|  
|**cacheobjtype**|**nvarchar(50)**|Der Plan-Cache-Objekttyp. NULL-Werte sind in der Spalte nicht zulässig. Folgende Werte sind möglich:<br /><br /> Ausführbarer Plan<br /><br /> CLR-kompilierte Funktion<br /><br /> CLR-kompilierte Prozedur<br /><br /> Cursor|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="physical-joins"></a>Physische Joins  
 ![Attributbeziehungsdiagramm](../../relational-databases/system-dynamic-management-views/media/dm-dependent-objects.gif "Beziehungsdiagramm")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|On|Beziehung|  
|----------|--------|--------|------------------|  
|**dm_exec_cached_plan_dependent_objects**|**dm_os_memory_objects**|**memory_object_address**|1:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.syscacheobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)  
  
  
