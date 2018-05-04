---
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
caps.latest.revision: 6
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d051f1bfa08f49d5ad0549051afa823ac72e977c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt aktuelle e/a, Sperren auf Zeilenebene und Zugriff auf die Aktivität für komprimierte Zeilengruppen in einem columnstore-Index. Verwendung **sys.dm_db_column_store_row_group_operational_stats** zum Verfolgen der Zeitdauer eine Benutzerabfrage warten, bis die Lese- und Schreibvorgänge für eine komprimierte Zeilengruppe oder eine Partition eines columnstore-Indexes muss, und welche Zeilengruppen, die auftreten hohen e/a-Aktivitäten oder Hotspots.  
  
 In-Memory-columnstore-Indizes werden in dieser DMV nicht angezeigt.  
 
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID der Tabelle mit der columnstore-Index.|  
|**index_id**|**int**|ID des columnstore-Indexes.|  
|**partition_number**|**int**|Auf 1 basierende Partitionsnummer im Index oder Heap.|  
|**row_group_id**|**int**|Die ID der Zeilengruppe im columnstore-Index. Dies ist eindeutig innerhalb einer Partition.|  
|**scan_count**|**int**|Anzahl von Scanvorgängen durch die Zeilengruppe seit dem letzten Neustart der SQL.|  
|**delete_buffer_scan_count**|**int**|Anzahl der Häufigkeit, mit die löschpuffers verwendet wurde, um gelöschte Zeilen in dieser Zeilengruppe zu bestimmen. Dies schließt den Zugriff auf die Hashtabelle im Arbeitsspeicher und der zugrunde liegenden Btree.|  
|**index_scan_count**|**int**|Anzahl der Häufigkeit, mit der die Partition der columnstore-Index gescannt wurde. Dies gilt für alle Zeilengruppen in der Partition.|  
|**rowgroup_lock_count**|**bigint**|Kumulierte Anzahl der sperranforderungen, für die dieser Zeilengruppe seit dem letzten Neustart der SQL.|  
|**rowgroup_lock_wait_count**|**bigint**|Gesamthäufigkeit, mit auf Zeilensperre gewartet hat das Datenbankmodul dieser Zeilengruppe seit dem letzten Neustart der SQL.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Die kumulative Anzahl der Millisekunden auf Zeilensperre gewartet hat das Datenbankmodul dieser Zeilengruppe seit dem letzten Neustart der SQL.|  
  
## <a name="permissions"></a>Berechtigungen  
 Folgende Berechtigungen sind erforderlich:  
  
-   CONTROL-Berechtigung für die Tabelle von Object_id angegeben.  
  
-   VIEW DATABASE STATE-Berechtigung zum Zurückgeben von Informationen zu allen Objekten innerhalb der Datenbank mithilfe des Objekt-Platzhalters @*Object_id* = NULL  
  
 Wenn die VIEW DATABASE STATE-Berechtigung erteilt wurde, ist die Rückgabe für alle Objekte in der Datenbank zulässig, unabhängig davon, ob CONTROL-Berechtigungen für bestimmte Objekte verweigert wurden.  
  
 Nach dem Verweigern der VIEW DATABASE STATE-Berechtigung können keine Objekte in der Datenbank zurückgegeben werden, unabhängig von möglicherweise erteilten CONTROL-Berechtigungen für bestimmte Objekte. Auch wenn dem Datenbank-Platzhalter @*Database_id*= NULL angegeben wird, wird die Datenbank ausgelassen.  
  
 Weitere Informationen finden Sie unter [dynamische Verwaltungssichten und-Funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Index Related Dynamic Management Views and Functions (Transact-SQL) (Indexbezogene dynamische Verwaltungssichten und -funktionen (Transact-SQL))](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

