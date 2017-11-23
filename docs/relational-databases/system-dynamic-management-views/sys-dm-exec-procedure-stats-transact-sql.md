---
title: Sys. dm_exec_procedure_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f935b0e9a4c150830a03ecb2ea1f67a4cd270d3f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die zusammengefasste Leistungsstatistik für zwischengespeicherte gespeicherte Prozeduren zurück. Diese Sicht gibt eine Zeile für jeden Plan der zwischengespeicherten gespeicherten Prozedur zurück, und die Lebensdauer der Zeile entspricht der Verweildauer der gespeicherten Prozedur im Cache. Bei Entfernung einer gespeicherten Prozedur aus dem Cache wird die entsprechende Zeile aus dieser Sicht gelöscht. Zu diesem Zeitpunkt wird ein Leistungsstatistik-SQL-Ablaufverfolgungsereignis ausgelöst, das **sys.dm_exec_query_stats**entspricht.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.  
  
> **Hinweis:** erste Abfrage von **dm_exec_procedure_stats** kann zu ungenauen Ergebnissen führen, wenn eine hohe arbeitsauslastung auf dem Server vorhanden ist. Erneutes Ausführen der Abfrage liefert unter Umständen genauere Ergebnisse.  
  
> **Hinweis für Azure SQL Datawarehouse!** Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_exec_procedure_stats**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, in der sich die gespeicherte Prozedur befindet.|  
|**object_id**|**int**|Objekt-ID der gespeicherten Prozedur.|  
|**Typ**|**char(2)**|Der Objekttyp:<br /><br /> P = Gespeicherte SQL-Prozedur<br /><br /> PC = Gespeicherte Assemblyprozedur (CLR)<br /><br /> X = Erweiterte gespeicherte Prozedur|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Objekttyps:<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|Dies kann verwendet werden, um die Korrelation mit Abfragen in **Sys. dm_exec_query_stats** , die von dieser gespeicherten Prozedur heraus ausgeführt wurden.|  
|**plan_handle**|**varbinary(64)**|Bezeichner für den speicherinternen Plan. Dieser Bezeichner ist vorübergehend und bleibt nur für die Dauer der Speicherung des Plans im Cache konstant. Dieser Wert kann mit der dynamischen Verwaltungssicht **sys.dm_exec_cached_plans** verwendet werden.<br /><br /> Ist immer 0x000, wenn eine systemintern kompilierte gespeicherte Prozedur eine speicheroptimierte Tabelle abfragt.|  
|**cached_time**|**datetime**|Der Zeitpunkt, zu dem die gespeicherte Prozedur dem Cache hinzugefügt wurde.|  
|**last_execution_time**|**datetime**|Der Zeitpunkt, zu dem die gespeicherte Prozedur zuletzt ausgeführt wurde.|  
|**execution_count**|**bigint**|Die Anzahl von Ausführungen der gespeicherten Prozedur seit der letzten Kompilierung.|  
|**total_worker_time**|**bigint**|Die CPU-Gesamtzeit (in Mikrosekunden) für Ausführungen dieser gespeicherten Prozedur seit der Kompilierung.<br /><br /> Wenn zahlreiche Ausführungen weniger als 1 Millisekunde dauern, wird **total_worker_time** bei nativ kompilierten gespeicherten Prozeduren u.U. nicht exakt angegeben.|  
|**last_worker_time**|**bigint**|Die CPU-Zeit (in Mikrosekunden) für die letzte Ausführung der gespeicherten Prozedur. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Die bisherige minimale CPU-Zeit (in Mikrosekunden) für eine einzelne Ausführung dieser gespeicherten Prozedur. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Die bisherige maximale CPU-Zeit (in Mikrosekunden) für eine einzelne Ausführung dieser gespeicherten Prozedur. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Die Gesamtanzahl physischer Lesevorgänge für Ausführungen dieser gespeicherten Prozedur seit der Kompilierung.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**last_physical_reads**|**bigint**|Die Anzahl physischer Lesevorgänge bei der letzten Ausführung der gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**min_physical_reads**|**bigint**|Die bisherige minimale Anzahl physischer Lesevorgänge für eine einzelne Ausführung dieser gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**max_physical_reads**|**bigint**|Die bisherige maximale Anzahl physischer Lesevorgänge für eine einzelne Ausführung dieser gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**total_logical_writes**|**bigint**|Die Gesamtanzahl logischer Schreibvorgänge für Ausführungen dieser gespeicherten Prozedur seit der Kompilierung.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**last_logical_writes**|**bigint**|Die Anzahl der Pufferpoolseiten, die seit der letzten Planausführung modifiziert wurden. Wenn eine Seite bereits modifiziert (geändert) wurde, werden keine Schreibvorgänge gezählt.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**min_logical_writes**|**bigint**|Die bisherige minimale Anzahl logischer Schreibvorgänge für eine einzelne Ausführung dieser gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**max_logical_writes**|**bigint**|Die bisherige maximale Anzahl logischer Schreibvorgänge für eine einzelne Ausführung dieser gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**total_logical_reads**|**bigint**|Die Gesamtanzahl logischer Lesevorgänge für Ausführungen dieser gespeicherten Prozedur seit der Kompilierung.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**last_logical_reads**|**bigint**|Die Anzahl logischer Lesevorgänge bei der letzten Ausführung der gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**min_logical_reads**|**bigint**|Die bisherige minimale Anzahl logischer Lesevorgänge für eine einzelne Ausführung dieser gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**max_logical_reads**|**bigint**|Die bisherige maximale Anzahl logischer Lesevorgänge für eine einzelne Ausführung dieser gespeicherten Prozedur.<br /><br /> Ist immer 0, wenn eine speicheroptimierte Tabelle abgefragt wird.|  
|**total_elapsed_time**|**bigint**|Die insgesamt verstrichene Zeit (in Mikrosekunden) für abgeschlossene Ausführungen dieser gespeicherten Prozedur.|  
|**last_elapsed_time**|**bigint**|Die verstrichene Zeit (in Mikrosekunden) für die letzte abgeschlossene Ausführung dieser gespeicherten Prozedur.|  
|**min_elapsed_time**|**bigint**|Die mindestens verstrichene Zeit (in Mikrosekunden) für eine beliebige abgeschlossene Ausführung dieser gespeicherten Prozedur.|  
|**max_elapsed_time**|**bigint**|Die maximal verstrichene Zeit (in Mikrosekunden) für eine beliebige abgeschlossene Ausführung dieser gespeicherten Prozedur.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
 <sup>1</sup> für systemintern kompilierte gespeicherte Prozeduren bei der Erfassung von Statistiken aktiviert ist, wird worker_time in Millisekunden. Wird die Abfrage in weniger als einer Millisekunde ausgeführt, lautet der Wert 0.  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto. 
  
## <a name="remarks"></a>Hinweise  
 Die Statistik in der Sicht wird aktualisiert, wenn die Ausführung einer gespeicherten Prozedur abgeschlossen ist.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Informationen zu den 10 gespeicherten Prozeduren mit der höchsten durchschnittlich verstrichenen Zeit zurück.  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys. dm_exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [Sys. dm_exec_trigger_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
  


