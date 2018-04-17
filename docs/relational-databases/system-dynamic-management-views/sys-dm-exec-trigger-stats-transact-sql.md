---
title: Sys. dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2018
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
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b80fdb97162bcf980f9c9c95d8a54433c3a5f489
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Aggregatleistungsstatistik für zwischengespeicherte Trigger zurück. Diese Sicht enthält eine Zeile pro Trigger, und die Lebensdauer der Zeile entspricht der Verweildauer des Triggers im Cache. Bei Entfernung eines Triggers aus dem Cache wird die entsprechende Zeile aus dieser Sicht gelöscht. Zu diesem Zeitpunkt wird ein Leistungsstatistik-SQL-Ablaufverfolgungsereignis ausgelöst, das **sys.dm_exec_query_stats**entspricht.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, in der sich der Trigger befindet.|  
|**object_id**|**int**|Objekt-ID des Triggers.|  
|**type**|**char(2)**|Der Objekttyp:<br /><br /> TA = Assembly (CLR) Trigger<br /><br /> TR = SQL-Trigger|  
|**Type_desc**|**nvarchar(60)**|Beschreibung des Objekttyps:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Kann zur Korrelation mit Abfragen in **sys.dm_exec_query_stats** verwendet werden, die aus diesem Trigger ausgeführt wurden.|  
|**plan_handle**|**varbinary(64)**|Bezeichner für den speicherinternen Plan. Dieser Bezeichner ist vorübergehend und bleibt nur für die Dauer der Speicherung des Plans im Cache konstant. Dieser Wert kann mit der dynamischen Verwaltungssicht **sys.dm_exec_cached_plans** verwendet werden.|  
|**cached_time**|**datetime**|Der Zeitpunkt, zu dem der Trigger dem Cache hinzugefügt wurde.|  
|**last_execution_time**|**datetime**|Der Zeitpunkt, zu dem der Trigger zuletzt ausgeführt wurde.|  
|**execution_count**|**bigint**|Die Anzahl der Fälle, in denen der Trigger seit ausgeführt wurde der letzten Kompilierung.|  
|**total_worker_time**|**bigint**|Die Gesamtmenge der CPU-Zeit in Mikrosekunden, die von Ausführungen dieses Triggers genutzt wurde, seit der Kompilierung.|  
|**last_worker_time**|**bigint**|CPU-Zeit (in Mikrosekunden) für die letzte Ausführung des Triggers.|  
|**min_worker_time**|**bigint**|Die maximale CPU-Zeit in Mikrosekunden, dieses Triggers jemals eine einzelne Ausführung.|  
|**max_worker_time**|**bigint**|Die maximale CPU-Zeit in Mikrosekunden, dieses Triggers jemals eine einzelne Ausführung.|  
|**total_physical_reads**|**bigint**|Die Gesamtanzahl physischer Lesevorgänge für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_physical_reads**|**bigint**|Die Anzahl der physischen Lesevorgänge ausgeführt, der letzten Ausführung des Triggers.|  
|**min_physical_reads**|**bigint**|Die minimale Anzahl physischer Lesevorgänge, die diese Trigger eine einzelne Ausführung bisherige.|  
|**max_physical_reads**|**bigint**|Die maximale Anzahl der physischen Lesevorgänge, die diese Trigger eine einzelne Ausführung bisherige.|  
|**total_logical_writes**|**bigint**|Die Gesamtanzahl logischer Schreibvorgänge für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_logical_writes**|**bigint**|Die Anzahl der logischen Schreibvorgänge ausgeführt, der letzten Ausführung des Triggers.|  
|**min_logical_writes**|**bigint**|Die minimale Anzahl logischer Schreibvorgänge, die diese Trigger eine einzelne Ausführung bisherige.|  
|**max_logical_writes**|**bigint**|Die maximale Anzahl logischer Schreibvorgänge, die diese Trigger eine einzelne Ausführung bisherige.|  
|**total_logical_reads**|**bigint**|Die Gesamtanzahl logischer Lesevorgänge für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_logical_reads**|**bigint**|Die Anzahl der logischen Lesevorgänge ausgeführt, der letzten Ausführung des Triggers.|  
|**min_logical_reads**|**bigint**|Die minimale Anzahl logischer Lesevorgänge, die diese Trigger eine einzelne Ausführung bisherige.|  
|**max_logical_reads**|**bigint**|Die maximale Anzahl logischer Lesevorgänge, die diese Trigger eine einzelne Ausführung bisherige.|  
|**total_elapsed_time**|**bigint**|Die insgesamt verstrichene Zeit in Mikrosekunden für abgeschlossene Ausführungen dieses Triggers.|  
|**last_elapsed_time**|**bigint**|Verstrichene Zeit (in Mikrosekunden) für die letzte abgeschlossene Ausführung dieses Triggers.|  
|**min_elapsed_time**|**bigint**|Die mindestens verstrichene Zeit in Mikrosekunden, die für eine beliebige abgeschlossene Ausführung dieses Triggers.|  
|**max_elapsed_time**|**bigint**|Die maximal verstrichene Zeit in Mikrosekunden, die für eine beliebige abgeschlossene Ausführung dieses Triggers.| 
|**total_spills**|**bigint**|Die Gesamtanzahl der Seiten, die der Aggregierung überlaufen durch die Ausführung dieses Triggers seit der Kompilierung.<br /><br /> **Gilt für**: beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|Die Anzahl der Seiten gefüllt, Zeitpunkt der letzten des Triggers Ausführung.<br /><br /> **Gilt für**: beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|Die minimale Anzahl der Seiten, die diese Trigger jemals eine einzelne Ausführung übergelaufen.<br /><br /> **Gilt für**: beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|Die maximale Anzahl der Seiten, die diese Trigger jemals eine einzelne Ausführung übergelaufen.<br /><br /> **Gilt für**: beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.  

Statistiken in der Sicht werden nach Abschluss einer Abfrage aktualisiert.  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Informationen zu den fünf Triggern mit der höchsten durchschnittlichen verstrichenen Zeit zurück.  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
[Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
