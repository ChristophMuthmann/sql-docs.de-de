---
title: Sys. query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cf026cb9beff10c6570a94bdd805aa2b78c0a4d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>Sys. query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Enthält Informationen über die Common Language Runtime Statistiken Ausführungsinformationen für die Abfrage.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Bezeichner der Zeile für die laufzeitausführung für die **"Plan_id"**, **Execution_type** und **Runtime_stats_interval_id**. Es ist nur für die vergangenen Runtime Statistiken Intervalle eindeutig. Für aktuell aktiven Intervalls möglicherweise mehrere Zeilen, die Laufzeitstatistiken für den Plan verweist darstellt **"Plan_id"**, mit den Ausführungstyp dargestellte **Execution_type**. In der Regel stellt eine Zeile Laufzeitstatistiken, der geleert werden auf den Datenträger, während andere (s) im Speicher enthaltenen Status darstellen. Daher wird beim Abrufen der tatsächlichen Status für jedes Intervall, müssen Sie aggregierte Metrik Gruppieren nach **"Plan_id"**, **Execution_type** und **Runtime_stats_interval_id**. |  
|**"Plan_id"**|**bigint**|Fremdschlüssel. Verknüpft mit [Sys. query_store_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Fremdschlüssel. Verknüpft mit [sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Bestimmt die Art der Ausführung einer Abfrage:<br /><br /> 0 – regelmäßigen Ausführung (erfolgreich abgeschlossen wurde)<br /><br /> 3 – Client initiiert hat die Ausführung aufgrund<br /><br /> 4 - Ausnahme abgebrochen Ausführung|  
|**execution_type_desc**|**vom Datentyp nvarchar(128)**|Die textbeschreibung des Ausführung Type-Feld:<br /><br /> 0 – Normal<br /><br /> 3 – abgebrochen<br /><br /> 4 - Ausnahme|  
|**first_execution_time**|**datetimeoffset**|Erste Ausführungszeit für den Abfrageplan in aggregationsintervalls.|  
|**last_execution_time**|**datetimeoffset**|Letzte Ausführungszeit für die Abfrage innerhalb des aggregationsintervalls zu planen.|  
|**count_executions**|**bigint**|Die Gesamtzahl der Ausführungen für den Abfrageplan in aggregationsintervalls.|  
|**avg_duration-Spalte**|**float**|Die durchschnittliche Dauer für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**last_duration**|**bigint**|Planen Sie die letzten Dauer für die Abfrage innerhalb der aggregationsintervall (in Mikrosekunden gemeldet).|  
|**min_duration**|**bigint**|Die Mindestdauer für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**max_duration**|**bigint**|Maximale Dauer für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**stdev_duration**|**float**|Dauer der Standardabweichung für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**avg_cpu_time**|**float**|Die durchschnittliche CPU-Zeit für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**last_cpu_time**|**bigint**|Planen Sie die letzte CPU-Zeit für die Abfrage innerhalb der aggregationsintervall (in Mikrosekunden gemeldet).|  
|**min_cpu_time**|**bigint**|Minimale CPU-Zeit für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**max_cpu_time**|**bigint**|Maximale CPU-Zeit für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**stdev_cpu_time**|**float**|CPU-Zeit die Standardabweichung für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**avg_logical_io_reads**|**float**|Durchschnittliche Anzahl der logischen e/a liest, für den Abfrageplan in aggregationsintervalls. (angegeben als Anzahl von 8KB-Seiten lesen).|  
|**last_logical_io_reads**|**bigint**|Letzten Anzahl logische e/a-Lesevorgänge für den Abfrageplan in aggregationsintervalls. (angegeben als Anzahl von 8KB-Seiten lesen).|  
|**min_logical_io_reads**|**bigint**|Minimale Anzahl logischer e/a-liest, für den Abfrageplan in aggregationsintervalls. (angegeben als Anzahl von 8KB-Seiten lesen).|  
|**max_logical_io_reads**|**bigint**|Maximale Anzahl von logische EA liest für den Abfrageplan in aggregationsintervalls. (angegeben als Anzahl von 8KB-Seiten lesen). |  
|**stdev_logical_io_reads**|**float**|Anzahl der logischen e/a liest die Standardabweichung für den Abfrageplan in aggregationsintervalls. (angegeben als Anzahl von 8KB-Seiten lesen).|  
|**avg_logical_io_writes**|**float**|Durchschnittliche Anzahl der logischen e/a schreibt für den Abfrageplan in aggregationsintervalls.|  
|**last_logical_io_writes**|**bigint**|Letzten Anzahl logische e/a-Schreibvorgänge für den Abfrageplan in aggregationsintervalls.|  
|**min_logical_io_writes**|**bigint**|Minimale Anzahl logischer e/a-schreibt für den Abfrageplan in aggregationsintervalls.|  
|**max_logical_io_writes**|**bigint**|Maximale Anzahl von logischen e/a schreibt für den Abfrageplan in aggregationsintervalls.|  
|**stdev_logical_io_writes**|**float**|Anzahl der logischen e/a schreibt Standardabweichung für den Abfrageplan in aggregationsintervalls.|  
|**avg_physical_io_reads**|**float**|Durchschnittliche Anzahl der physischen e/a liest, für den Abfrageplan innerhalb der aggregationsintervall (ausgedrückt als Anzahl von 8KB-Seiten lesen).|  
|**last_physical_io_reads**|**bigint**|Anzahl der physischen e/a letzten liest für den Abfrageplan innerhalb der aggregationsintervall (ausgedrückt als Anzahl von 8KB-Seiten lesen).|  
|**min_physical_io_reads**|**bigint**|Minimale Anzahl physischer e/a-Lesevorgängen für Abfrageplan innerhalb der aggregationsintervall (ausgedrückt als Anzahl von 8KB-Seiten lesen).|  
|**max_physical_io_reads**|**bigint**|Maximale Anzahl der physischen e/a liest, für den Abfrageplan innerhalb der aggregationsintervall (ausgedrückt als Anzahl von 8KB-Seiten lesen).|  
|**stdev_physical_io_reads**|**float**|Anzahl der physischen e/a liest die Standardabweichung für den Abfrageplan innerhalb der aggregationsintervall (ausgedrückt als Anzahl von 8KB-Seiten lesen).|  
|**avg_clr_time**|**float**|Durchschnittliche CLR-Zeit für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**last_clr_time**|**bigint**|Planen Sie CLR-zuletzt für die Abfrage innerhalb der aggregationsintervall (in Mikrosekunden gemeldet).|  
|**min_clr_time**|**bigint**|Minimale CLR-Zeit für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**max_clr_time**|**bigint**|Maximale CLR-Zeit für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**stdev_clr_time**|**float**|CLR Zeit die Standardabweichung für den Abfrageplan in die aggregationsintervall (in Mikrosekunden gemeldet).|  
|**avg_dop**|**float**|Durchschnittliche DOP (Grad an Parallelität) für den Abfrageplan in aggregationsintervalls.|  
|**last_dop**|**bigint**|Die letzten Sie DOP (Grad an Parallelität) für den Abfrageplan in aggregationsintervalls.|  
|**min_dop**|**bigint**|Minimale DOP (Grad an Parallelität) für den Abfrageplan in aggregationsintervalls.|  
|**MAX_DOP**|**bigint**|Maximale DOP (Grad an Parallelität) für den Abfrageplan in aggregationsintervalls.|  
|**stdev_dop**|**float**|DOP (Grad an Parallelität) die Standardabweichung für den Abfrageplan in aggregationsintervalls.|  
|**avg_query_max_used_memory**|**float**|Durchschnittliche arbeitsspeicherzuweisung (angegeben als Anzahl von 8 KB-Seiten) für den Abfrageplan in aggregationsintervalls. 0 für Abfragen, die systemintern kompilierte immer Speicheroptimierte Prozeduren.|  
|**last_query_max_used_memory**|**bigint**|Letzte arbeitsspeicherzuweisung (angegeben als Anzahl von 8 KB-Seiten) für den Abfrageplan in aggregationsintervalls. 0 für Abfragen, die systemintern kompilierte immer Speicheroptimierte Prozeduren.|  
|**min_query_max_used_memory**|**bigint**|Minimale arbeitsspeicherzuweisung nutzen (angegeben als Anzahl von 8 KB-Seiten) für den Abfrageplan in aggregationsintervalls. 0 für Abfragen, die systemintern kompilierte immer Speicheroptimierte Prozeduren.|  
|**max_query_max_used_memory**|**bigint**|Maximale arbeitsspeicherzuweisung (angegeben als Anzahl von 8 KB-Seiten) für den Abfrageplan in aggregationsintervalls. 0 für Abfragen, die systemintern kompilierte immer Speicheroptimierte Prozeduren.|  
|**stdev_query_max_used_memory**|**float**|Arbeitsspeicherzuweisung (angegeben als Anzahl von 8 KB-Seiten) Standardabweichung für den Abfrageplan in aggregationsintervalls. 0 für Abfragen, die systemintern kompilierte immer Speicheroptimierte Prozeduren.|  
|**avg_rowcount**|**float**|Durchschnittliche Anzahl der zurückgegebenen Zeilen für den Abfrageplan in aggregationsintervalls.|  
|**last_rowcount**|**bigint**|Die Anzahl der zurückgegebenen Zeilen bei der letzten Ausführung des Abfrageplans in aggregationsintervalls.|  
|**min_rowcount**|**bigint**|Minimale Anzahl von zurückgegebenen Zeilen für die Abfrage innerhalb des aggregationsintervalls planen.|  
|**max_rowcount**|**bigint**|Maximale Anzahl von zurückgegebenen Zeilen für die Abfrage innerhalb des aggregationsintervalls planen.|  
|**stdev_rowcount**|**float**|Die Anzahl der zurückgegebenen Zeilen Standardabweichung für den Abfrageplan in aggregationsintervalls.|
|**avg_log_bytes_used**|**float**|Durchschnittliche Anzahl von Bytes im Protokoll von den Abfrageplan in aggregationsintervalls verwendet. Wendet **nur für Azure SQL-Datenbank**.|    
|**last_log_bytes_used**|**bigint**|Anzahl der Bytes im Datenbankprotokoll der letzten Ausführung des Abfrageplans, innerhalb des aggregationsintervalls verwendet. Wendet **nur für Azure SQL-Datenbank**.|  
|**min_log_bytes_used**|**bigint**|Die Mindestanzahl von Bytes im Protokoll von den Abfrageplan in aggregationsintervalls verwendet.  Wendet **nur für Azure SQL-Datenbank**.|  
|**max_log_bytes_used**|**bigint**|Maximale Anzahl von Bytes im Protokoll von den Abfrageplan in aggregationsintervalls verwendet.  Wendet **nur für Azure SQL-Datenbank**.| 
|**stdev_log_bytes_used**|**float**|Standardabweichung der die Anzahl der Bytes im Datenbankprotokoll von innerhalb des aggregationsintervalls eines Abfrageplans verwendet.  Wendet **nur für Azure SQL-Datenbank**.|
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **VIEW DATABASE STATE** Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Sys.query_context_settings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [Sys. query_store_plan &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [Sys.query_store_query_text &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [Sys.query_store_runtime_stats_interval &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Der Abfragespeicher gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
