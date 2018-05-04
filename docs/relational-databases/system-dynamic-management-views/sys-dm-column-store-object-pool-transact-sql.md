---
title: Sys.dm_column_store_object_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fecf0703bad0ae0d039848d15ed0bd9a5fae1a70
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>Sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Gibt die Anzahl verschiedener Typen Objekt Pool der Auslastung des Speichers für columnstore-Index-Objekte.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|Die ID der Datenbank. Dies ist eindeutig innerhalb einer Instanz von SQL Server-Datenbank oder einer Azure SQL-Datenbankserver. |  
|`object_id`|`int`|ID des Objekts. Das Objekt ist eines der object_types auf. | 
|`index_id`|`int`|ID des columnstore-Indexes.|  
|`partition_number`|`bigint`|Auf 1 basierende Partitionsnummer im Index oder Heap. Jede Tabelle oder Sicht verfügt über mindestens eine Partition.| 
|`column_id`|`int`|ID der columnstore-Spalte. Dies ist NULL für DELETE_BITMAP.| 
|`row_group_id`|`int`|Die ID der Zeilengruppe.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT – ein Spaltensegment. `object_id` die Segment-ID. Ein Segment werden alle Werte für eine Spalte innerhalb einer Zeilengruppe gespeichert. Beispielsweise, wenn eine Tabelle 10 Spalten verfügt, sind 10 spaltensegmente pro Zeilengruppe. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY – ein globaler Wörterbuch, das Informationen zur Suche aller spaltensegmente in der Tabelle enthält.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY – ein lokales Wörterbuch, das eine Spalte zugeordnet.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY – eine andere Darstellung der globalen Wörterbuch. Dies bietet eine umgekehrte Nachschlagen von Werten an Dictionary_id. Zum Erstellen von komprimierten Segmente als Teil der Tupelverschiebungsvorgang oder Massenladen verwendet.<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP – Löscht eine Bitmap, die Segment nachverfolgt. Es gibt eine Delete-Bitmap pro Partition.|  
|`access_count`|`int`|Anzahl der lesen oder Schreiben greift auf dieses Objekt.|  
|`memory_used_in_bytes`|`bigint`|Von diesem Objekt im Objektpool verwendete Arbeitsspeicher.|  
|`object_load_time`|`datetime`|Uhrzeit für Wenn Object_id im Objektpool geschaltet wurde.|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
 
## <a name="see-also"></a>Siehe auch  
  
 [Index Related Dynamic Management Views and Functions (Transact-SQL) (Indexbezogene dynamische Verwaltungssichten und -funktionen (Transact-SQL))](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
