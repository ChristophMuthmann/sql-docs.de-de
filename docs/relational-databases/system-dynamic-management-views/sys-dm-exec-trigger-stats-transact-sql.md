---
title: Sys. dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Aggregatleistungsstatistik für zwischengespeicherte Trigger zurück. Diese Sicht enthält eine Zeile pro Trigger, und die Lebensdauer der Zeile entspricht der Verweildauer des Triggers im Cache. Bei Entfernung eines Triggers aus dem Cache wird die entsprechende Zeile aus dieser Sicht gelöscht. Zu diesem Zeitpunkt wird ein Leistungsstatistik-SQL-Ablaufverfolgungsereignis ausgelöst, das **sys.dm_exec_query_stats**entspricht.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, in der sich der Trigger befindet.|  
|**object_id**|**int**|Objekt-ID des Triggers.|  
|**Typ**|**char(2)**|Der Objekttyp:<br /><br /> TA = Assembly (CLR) Trigger<br /><br /> TR = SQL-Trigger|  
|**Type_desc**|**nvarchar(60)**|Beschreibung des Objekttyps:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Kann zur Korrelation mit Abfragen in **sys.dm_exec_query_stats** verwendet werden, die aus diesem Trigger ausgeführt wurden.|  
|**plan_handle**|**varbinary(64)**|Bezeichner für den speicherinternen Plan. Dieser Bezeichner ist vorübergehend und bleibt nur für die Dauer der Speicherung des Plans im Cache konstant. Dieser Wert kann mit der dynamischen Verwaltungssicht **sys.dm_exec_cached_plans** verwendet werden.|  
|**cached_time**|**datetime**|Der Zeitpunkt, zu dem der Trigger dem Cache hinzugefügt wurde.|  
|**last_execution_time**|**datetime**|Der Zeitpunkt, zu dem der Trigger zuletzt ausgeführt wurde.|  
|**execution_count**|**bigint**|Die Anzahl von Ausführungen des Triggers seit der letzten Kompilierung.|  
|**total_worker_time**|**bigint**|Die CPU-Gesamtzeit (in Mikrosekunden) für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_worker_time**|**bigint**|CPU-Zeit (in Mikrosekunden) für die letzte Ausführung des Triggers.|  
|**min_worker_time**|**bigint**|Bisherige maximale CPU-Zeit (in Mikrosekunden) für eine einzelne Ausführung dieses Triggers.|  
|**max_worker_time**|**bigint**|Bisherige maximale CPU-Zeit (in Mikrosekunden) für eine einzelne Ausführung dieses Triggers.|  
|**total_physical_reads**|**bigint**|Gesamtanzahl physischer Lesevorgänge für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_physical_reads**|**bigint**|Anzahl physischer Lesevorgänge bei der letzten Ausführung des Triggers.|  
|**min_physical_reads**|**bigint**|Bisherige minimale Anzahl physischer Lesevorgänge für eine einzelne Ausführung dieses Triggers.|  
|**max_physical_reads**|**bigint**|Bisherige maximale Anzahl physischer Lesevorgänge für eine einzelne Ausführung dieses Triggers.|  
|**total_logical_writes**|**bigint**|Gesamtanzahl logischer Schreibvorgänge für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_logical_writes**|**bigint**|**total_physical_reads**Anzahl logischer Schreibvorgänge bei der letzten Ausführung des Triggers.|  
|**min_logical_writes**|**bigint**|Bisherige minimale Anzahl logischer Schreibvorgänge für eine einzelne Ausführung dieses Triggers.|  
|**max_logical_writes**|**bigint**|Bisherige maximale Anzahl logischer Schreibvorgänge für eine einzelne Ausführung dieses Triggers.|  
|**total_logical_reads**|**bigint**|Gesamtanzahl logischer Lesevorgänge für Ausführungen dieses Triggers seit der Kompilierung.|  
|**last_logical_reads**|**bigint**|Anzahl logischer Lesevorgänge bei der letzten Ausführung des Triggers.|  
|**min_logical_reads**|**bigint**|Bisherige minimale Anzahl logischer Lesevorgänge für eine einzelne Ausführung dieses Triggers.|  
|**max_logical_reads**|**bigint**|Bisherige maximale Anzahl logischer Lesevorgänge für eine einzelne Ausführung dieses Triggers.|  
|**total_elapsed_time**|**bigint**|Insgesamt verstrichene Zeit (in Mikrosekunden) für abgeschlossene Ausführungen dieses Triggers.|  
|**last_elapsed_time**|**bigint**|Verstrichene Zeit (in Mikrosekunden) für die letzte abgeschlossene Ausführung dieses Triggers.|  
|**min_elapsed_time**|**bigint**|Mindestens verstrichene Zeit (in Mikrosekunden) für eine beliebige abgeschlossene Ausführung dieses Triggers.|  
|**max_elapsed_time**|**bigint**|Maximal verstrichene Zeit (in Mikrosekunden) für eine beliebige abgeschlossene Ausführung dieses Triggers.|  
  
## <a name="remarks"></a>Hinweise  
 In Windows Azure SQL-Datenbank können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf den Datenbankeinschluss auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.  

Statistiken in der Sicht werden nach Abschluss einer Abfrage aktualisiert.  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.
  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Informationen zu den fünf Triggern mit der höchsten durchschnittlichen verstrichenen Zeit zurück.  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys. dm_exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [Sys. dm_exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [Sys. dm_exec_procedure_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [dm_exec_cached_plans &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
