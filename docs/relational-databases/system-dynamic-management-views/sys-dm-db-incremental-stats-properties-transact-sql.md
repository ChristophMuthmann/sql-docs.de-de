---
title: sys.dm_db_incremental_stats_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server 2014
f1_keywords:
- sys.dm_db_incremental_stats_properties
- sys.dm_db_incremental_stats_properties_TSQL
- dm_db_incremental_stats_properties
- dm_db_incremental_stats_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_incremental_stats_properties
ms.assetid: aa0db893-34d1-419c-b008-224852e71307
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6187179f6599404dac86f92403cba507eb5e5fcc
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbincrementalstatsproperties-transact-sql"></a>sys.dm_db_incremental_stats_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Gibt inkrementelle Statistikeigenschaften für das angegebene Datenbankobjekt (Tabelle) in der aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank zurück. Die Verwendung von `sys.dm_db_incremental_stats_properties` (enthält eine Partitionsnummer) ähnelt der von `sys.dm_db_stats_properties` , das für nicht inkrementelle Statistiken verwendet wird. 
  
  Diese Funktion wurde in eingeführt [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] Service Pack 2 und [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Service Pack 1.
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_db_incremental_stats_properties (object_id, stats_id)  
```  
  
## <a name="arguments"></a>Argumente  
 *object_id*  
 ID des Objekts in der aktuellen Datenbank, für die Eigenschaften einer der enthaltenen inkrementellen Statistiken angefordert werden. *object_id* ist **int**.  
  
 *stats_id*  
 ID der Statistik für die angegebene *object_id*. Die Statistik-ID kann aus der dynamischen Verwaltungssicht [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) abgerufen werden. *stats_id* ist **int**.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID des Objekts (Tabelle), für das die Eigenschaften des Statistikobjekts zurückgegeben werden sollen.|  
|stats_id|**int**|Die ID des Statistikobjekts. Ist eindeutig innerhalb der Tabelle. Weitere Informationen finden Sie unter [sysenthalten.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)enthalten.|
|partition_number|**int**|Nummer der Partition, die den Teil der Tabelle enthält.|  
|last_updated|**datetime2**|Datum und Uhrzeit der letzten Aktualisierung des Statistikobjekts. Weitere Informationen finden Sie unter der ["Hinweise"](#Remarks) Abschnitt auf dieser Seite.|  
|rows|**bigint**|Gesamtanzahl der Zeilen in der Tabelle zum Zeitpunkt der letzten Aktualisierung der Statistik. Wenn die Statistik gefiltert wird oder einem gefilterten Index entspricht, kann die Anzahl der Zeilen geringer als die Anzahl der Zeilen in der Tabelle sein.|  
|rows_sampled|**bigint**|Gesamtzahl der Zeilen, die für die statistischen Berechnungen in die Stichprobe aufgenommen wurden.|  
|steps|**int**|Anzahl der Schritte im Histogramm. Weitere Informationen finden Sie unter [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)enthalten.|  
|unfiltered_rows|**bigint**|Gesamtanzahl der Zeilen in der Tabelle vor dem Anwenden des Filterausdrucks (für gefilterte Statistiken). Wenn die Statistik nicht gefiltert ist, entspricht „unfiltered_rows“ dem in der rows-Spalte zurückgegebenen Wert.|  
|modification_counter|**bigint**|Gesamtanzahl der Änderungen für die führende Statistikspalte (auf der das Histogramm basiert) seit der letzten Aktualisierung der Statistik.<br /><br /> Diese Spalte enthält keine Informationen für speicheroptimierte Tabellen.|  
  
## <a name="Remarks"></a> Hinweise  
 `sys.dm_db_incremental_stats_properties` gibt unter den folgenden Bedingungen ein leeres Rowset zurück:  
  
-   `object_id` oder `stats_id` ist NULL.   
-   Das angegebene Objekt wurde nicht gefunden bzw. entspricht keiner Tabelle mit inkrementeller Statistik.  
-   Die angegebene Statistik-ID entspricht keiner vorhandenen Statistik für die angegebene Objekt-ID.  
-   Der aktuelle Benutzer verfügt nicht über die erforderlichen Berechtigungen zum Anzeigen des Statistikobjekts.
 
 Dieses Verhalten ermöglicht die sichere Verwendung von `sys.dm_db_incremental_stats_properties` , wenn die Funktion übergreifend auf Zeilen in Sichten wie `sys.objects` und `sys.stats`angewendet wird. Diese Methode kann Eigenschaften für die Statistik zurückgeben, die den einzelnen Partitionen entsprechen. Verwenden Sie stattdessen „dm_db_stats_properties“, um die Eigenschaften für die zusammengeführten Statistiken für alle Partitionen kombiniert anzuzeigen. 

Statistiken Aktualisierungsdatum befindet sich in der [Statistik-Blob-Objekt](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics) zusammen mit den [Histogramm](../../relational-databases/statistics/statistics.md#histogram) und [dichtevektor](../../relational-databases/statistics/statistics.md#density), nicht in den Metadaten. Wenn keine Daten gelesen werden, um statistische Daten zu generieren, die Statistik-Blob nicht erstellt, das Datum ist nicht verfügbar, und die *Last_updated* Spalte ist NULL. Dies ist der Fall für gefilterte Statistiken für die das Prädikat keine Zeilen zurückgibt, oder für neue, leere Tabellen.

## <a name="permissions"></a>Berechtigungen  
 Erfordert, dass der Benutzer über SELECT-Berechtigungen für Statistikspalten verfügt, Besitzer der Tabelle oder Mitglied der festen Serverrolle `sysadmin`, der festen Datenbankrolle `db_owner` oder der festen Datenbankrolle `db_ddladmin` ist.  
  
## <a name="examples"></a>Beispiele  

### <a name="a-simple-example"></a>A. Einfaches Beispiel
Das folgende Beispiel gibt die Statistiken für die `PartitionTable` -Tabelle zurück, die unter dem Thema [Erstellen partitionierter Tabellen und Indizes](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)beschrieben wird.

```sql
SELECT * FROM sys.dm_db_incremental_stats_properties (object_id('PartitionTable'), 1);
``` 

Vorschläge zur zusätzlichen Nutzung finden Sie unter  [dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md).
  
## <a name="see-also"></a>Siehe auch  
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Objektbezogene dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
 [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
