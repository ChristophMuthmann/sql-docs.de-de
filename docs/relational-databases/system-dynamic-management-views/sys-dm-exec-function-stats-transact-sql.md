---
title: dm_exec_function_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c85e25130214a6b12e630c186f275e75efd4b3d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>dm_exec_function_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Gibt die aggregatleistungsstatistik für zwischengespeicherte Funktionen aus. Die Sicht gibt eine Zeile für jeden Plan der zwischengespeicherten Funktion und die Lebensdauer der Zeile wird solange die Funktion ist zwischengespeichert. Wenn eine Funktion aus dem Cache entfernt wird, wird die entsprechende Zeile aus dieser Sicht gelöscht. Zu diesem Zeitpunkt wird ein Leistungsstatistik-SQL-Ablaufverfolgungsereignis ausgelöst, das **sys.dm_exec_query_stats**entspricht. Gibt Informationen zu Skalarfunktionen, einschließlich der in-Memory-Funktionen und CLR-Skalarfunktionen zurück. Informationen zu Tabellenwertfunktionen wird nicht zurückgegeben werden.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.  
  
> [!NOTE]
> Erste Abfrage von **dm_exec_function_stats** kann zu ungenauen Ergebnissen führen, wenn eine hohe arbeitsauslastung auf dem Server vorhanden ist. Erneutes Ausführen der Abfrage liefert unter Umständen genauere Ergebnisse.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, in dem die Funktion gespeichert ist.|  
|**object_id**|**int**|Objekt-ID der Funktion.|  
|**type**|**char(2)**|Typ des Objekts: FN = Skalarwertfunktionen|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Objekttyps: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|Dies kann verwendet werden, um die Korrelation mit Abfragen in **Sys. dm_exec_query_stats** , die in dieser Funktion aus ausgeführt wurden.|  
|**plan_handle**|**varbinary(64)**|Bezeichner für den speicherinternen Plan. Dieser Bezeichner ist vorübergehend und bleibt nur für die Dauer der Speicherung des Plans im Cache konstant. Dieser Wert kann mit der dynamischen Verwaltungssicht **sys.dm_exec_cached_plans** verwendet werden.<br /><br /> Immer wird 0 x 000, wenn eine systemintern kompilierte Funktion Abfragen einer speicheroptimierten Tabelle sein.|  
|**cached_time**|**datetime**|Zeitpunkt, zu dem die Funktion zum Cache hinzugefügt wurde.|  
|**last_execution_time**|**datetime**|Die letzten, an dem die Funktion ausgeführt wurde.|  
|**execution_count**|**bigint**|Anzahl der Fälle, in denen die Funktion seit dem ausgeführt wurde letzten Kompilierung.|  
|**total_worker_time**|**bigint**|Gesamtumfang des CPU-Gesamtzeit Mikrosekunden, durch die Ausführung dieser Funktion seit der Kompilierung.<br /><br /> Für systemintern kompilierte Funktionen **Total_worker_time** möglicherweise nicht genau, wenn zahlreiche Ausführungen weniger als 1 Millisekunde dauern.|  
|**last_worker_time**|**bigint**|CPU-Zeit in Mikrosekunden, die zuletzt verarbeitet wurde, die die Funktion ausgeführt wurde. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Minimale CPU-Zeit in Mikrosekunden, diese Funktion immer eine einzelne Ausführung. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Maximale CPU-Zeit in Mikrosekunden, diese Funktion immer eine einzelne Ausführung. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Gesamtanzahl physischer Lesevorgänge für Ausführungen dieser Funktion seit der Kompilierung.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**last_physical_reads**|**bigint**|Anzahl der physischen Lesevorgänge ausgeführt, der letzten Ausführung der Funktion ausgeführt wurde.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**min_physical_reads**|**bigint**|Minimale Anzahl physischer Lesevorgänge, die diese Funktion eine einzelne Ausführung bisherige.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**max_physical_reads**|**bigint**|Maximale Anzahl der physischen Lesevorgänge, die diese Funktion eine einzelne Ausführung bisherige.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**total_logical_writes**|**bigint**|Gesamtanzahl logischer Schreibvorgänge für Ausführungen dieser Funktion seit der Kompilierung.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**last_logical_writes**|**bigint**|Die Anzahl der Pufferpoolseiten, die seit der letzten Planausführung modifiziert wurden. Wenn eine Seite bereits modifiziert (geändert) wurde, werden keine Schreibvorgänge gezählt.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**min_logical_writes**|**bigint**|Minimale Anzahl logischer Schreibvorgänge, die diese Funktion eine einzelne Ausführung bisherige.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**max_logical_writes**|**bigint**|Maximale Anzahl logischer Schreibvorgänge, die diese Funktion eine einzelne Ausführung bisherige.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**total_logical_reads**|**bigint**|Gesamtanzahl logischer Lesevorgänge für Ausführungen dieser Funktion seit der Kompilierung.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**last_logical_reads**|**bigint**|Anzahl logischer Lesevorgänge ausgeführt, der letzten Ausführung der Funktion ausgeführt wurde.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**min_logical_reads**|**bigint**|Minimale Anzahl logischer Lesevorgänge, die diese Funktion eine einzelne Ausführung bisherige.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**max_logical_reads**|**bigint**|Maximale Anzahl logischer Lesevorgänge, die diese Funktion eine einzelne Ausführung bisherige.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**total_elapsed_time**|**bigint**|Insgesamt verstrichene Zeit in Mikrosekunden, die für abgeschlossene Ausführungen dieser Funktion.|  
|**last_elapsed_time**|**bigint**|Verstrichene Zeit in Mikrosekunden, die für die letzte abgeschlossene Ausführung dieser Funktion.|  
|**min_elapsed_time**|**bigint**|Mindestens verstrichene Zeit, die in Mikrosekunden, die für eine beliebige abgeschlossene Ausführung dieser Funktion.|  
|**max_elapsed_time**|**bigint**|Maximal verstrichene Zeit, die in Mikrosekunden, die für eine beliebige abgeschlossene Ausführung dieser Funktion.|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Informationen zu den obersten zehn Funktionen mit dem durchschnittlichen verstrichenen Zeit zurück.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
