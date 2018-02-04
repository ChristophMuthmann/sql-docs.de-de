---
title: Sys. dm_db_stats_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_stats_properties_TSQL
- sys.dm_db_stats_properties
- dm_db_stats_properties_TSQL
- dm_db_stats_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_properties
ms.assetid: 8a54889d-e263-4881-9fcb-b1db410a9453
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3406cfffce07260fc425c2850e548d006f9d796a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbstatsproperties-transact-sql"></a>sys.dm_db_stats_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Statistikeigenschaften für das angegebene Datenbankobjekt (Tabelle oder indizierte Sicht) in der aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank zurück. Bei partitionierten Tabellen finden Sie unter ähnlichen [sys.dm_db_incremental_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md). 
 
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_db_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumente  
 *object_id*  
 ID des Objekts in der aktuellen Datenbank, für die Eigenschaften einer der enthaltenen Statistiken angefordert werden. *object_id* ist **int**.  
  
 *stats_id*  
 ID der Statistik für die angegebene *object_id*. Die Statistik-ID kann aus der dynamischen Verwaltungssicht [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) abgerufen werden. *stats_id* ist **int**.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID des Objekts (Tabelle oder indizierte Sicht), für das die Eigenschaften des Statistikobjekts zurückgegeben werden sollen.|  
|stats_id|**int**|Die ID des Statistikobjekts. Diese ist innerhalb der Tabelle oder indizierten Sicht eindeutig. Weitere Informationen finden Sie unter [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md).|  
|last_updated|**datetime2**|Datum und Uhrzeit der letzten Aktualisierung des Statistikobjekts. Weitere Informationen finden Sie unter der ["Hinweise"](#Remarks) Abschnitt auf dieser Seite.|  
|rows|**bigint**|Gesamtanzahl der Zeilen in der Tabelle oder indizierten Sicht zum Zeitpunkt der letzten Aktualisierung der Statistik. Wenn die Statistik gefiltert wird oder einem gefilterten Index entspricht, kann die Anzahl der Zeilen geringer als die Anzahl der Zeilen in der Tabelle sein.|  
|rows_sampled|**bigint**|Gesamtzahl der Zeilen, die für die statistischen Berechnungen in die Stichprobe aufgenommen wurden.|  
|steps|**int**|Anzahl der Schritte im Histogramm. Weitere Informationen finden Sie unter [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)enthalten.|  
|unfiltered_rows|**bigint**|Gesamtanzahl der Zeilen in der Tabelle vor dem Anwenden des Filterausdrucks (für gefilterte Statistiken). Wenn die Statistik nicht gefiltert ist, entspricht „unfiltered_rows“ dem in der rows-Spalte zurückgegebenen Wert.|  
|modification_counter|**bigint**|Gesamtanzahl der Änderungen für die führende Statistikspalte (auf der das Histogramm basiert) seit der letzten Aktualisierung der Statistik.<br /><br /> Speicheroptimierte Tabellen: ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] enthält diese Spalte: Gesamtzahl der Änderungen für die Tabelle, die seit der letzten Statistiken aktualisiert wurden oder die Datenbank wurde neu gestartet.|  
|persisted_sample_percent|**float**|Beibehalten von Prozentsatz für die Stichprobe verwendet wird, für die Statistik-Updates, die einen Sampling Prozentsatz nicht explizit angeben. Wenn der Wert 0 (null) ist, ist kein Prozentsatz der beibehaltenen Beispiel für diese Statistik festgelegt.<br /><br /> **Gilt für:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4|  
  
## <a name="Remarks"></a> Hinweise  
 **Sys. dm_db_stats_properties** unter einer der folgenden Bedingungen ein leeres Rowset zurück:  
  
-   **Object_id** oder **Stats_id** ist NULL.    
-   Das angegebene Objekt wurde nicht gefunden bzw. entspricht keiner Tabelle bzw. keiner indizierten Sicht.    
-   Die angegebene Statistik-ID entspricht keiner vorhandenen Statistik für die angegebene Objekt-ID.    
-   Der aktuelle Benutzer verfügt nicht über die erforderlichen Berechtigungen zum Anzeigen des Statistikobjekts.  
  
 Dieses Verhalten ermöglicht die sichere Verwendung von **dm_db_stats_properties** Wenn Cross angewendet auf Zeilen in Sichten wie z. B. **sys.objects** und **sys.stats**.  
 
Statistiken Aktualisierungsdatum befindet sich in der [Statistik-Blob-Objekt](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics) zusammen mit den [Histogramm](../../relational-databases/statistics/statistics.md#histogram) und [dichtevektor](../../relational-databases/statistics/statistics.md#density), nicht in den Metadaten. Wenn keine Daten gelesen werden, um statistische Daten zu generieren, die Statistik-Blob nicht erstellt, das Datum ist nicht verfügbar, und die *Last_updated* Spalte ist NULL. Dies ist der Fall für gefilterte Statistiken für die das Prädikat keine Zeilen zurückgibt, oder für neue, leere Tabellen.
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert, dass der Benutzer über SELECT-Berechtigungen für Statistikspalten verfügt, Besitzer der Tabelle oder Mitglied der festen Serverrolle `sysadmin`, der festen Datenbankrolle `db_owner` oder der festen Datenbankrolle `db_ddladmin` ist.  
  
## <a name="examples"></a>Beispiele  

### <a name="a-simple-example"></a>A. Einfaches Beispiel
Im folgende Beispiel gibt die Statistiken für die `Person.Person` -Tabelle in der AdventureWorks-Datenbank.

```sql
SELECT * FROM sys.dm_db_stats_properties (object_id('Person.Person'), 1);
``` 
  
### <a name="b-returning-all-statistics-properties-for-a-table"></a>B. Zurückgeben aller Statistikeigenschaften für eine Tabelle  
 Im folgenden Beispiel werden die Eigenschaften aller Statistiken zurückgegeben, die für die TEST-Tabelle vorhanden sind.  
  
```sql  
SELECT sp.stats_id, name, filter_definition, last_updated, rows, rows_sampled, steps, unfiltered_rows, modification_counter   
FROM sys.stats AS stat   
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE stat.object_id = object_id('TEST');  
```  
  
### <a name="c-returning-statistics-properties-for-frequently-modified-objects"></a>C. Zurückgeben von Statistikeigenschaften für häufig geänderte Objekte  
 Im folgenden Beispiel werden alle Tabellen, indizierten Sichten und Statistiken, für die die führende Spalte seit dem letzten Statistikupdate mehr als tausend Mal geändert wurde, aus der aktuellen Datenbank zurückgegeben.  
  
```sql  
SELECT obj.name, obj.object_id, stat.name, stat.stats_id, last_updated, modification_counter  
FROM sys.objects AS obj   
INNER JOIN sys.stats AS stat ON stat.object_id = obj.object_id  
CROSS APPLY sys.dm_db_stats_properties(stat.object_id, stat.stats_id) AS sp  
WHERE modification_counter > 1000;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Objektbezogene dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys.dm_db_incremental_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md)  
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  

