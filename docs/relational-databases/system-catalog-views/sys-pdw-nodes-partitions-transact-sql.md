---
title: Sys.pdw_nodes_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 94f7ab8cb379c2147446b67d9865e8ad415dcf84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodespartitions-transact-sql"></a>sys.pdw_nodes_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jede Partition aller Tabellen und die meisten Typen von Indizes in einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Datenbank. Alle Tabellen und Indizes enthalten mindestens eine Partition, und zwar unabhängig davon, ob sie explizit partitioniert sind.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|partition_id|`bigint`|die ID der Partition. Ist innerhalb einer Datenbank eindeutig.|  
|object_id|`int`|die ID des Objekts, zu dem diese Partition gehört. Jede Tabelle oder Sicht besteht aus mindestens einer Partition.|  
|index_id|`int`|die ID des Indexes innerhalb des Objekts, zu dem diese Partition gehört.|  
|partition_number|`int`|Auf 1 basierende Partitionsnummer im besitzenden Index oder Heap. Für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], der Wert dieser Spalte ist 1.|  
|hobt_id|`bigint`|Die ID des Datenheaps oder der B-Struktur, der bzw. die die Zeilen für diese Partition enthält.|  
|rows|`bigint`|Die ungefähre Anzahl der Zeilen in dieser Partition. |  
|data_compression|`int`|Gibt den Status der Komprimierung für jede Partition an:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|`nvarchar(60)`|Gibt den Status der Komprimierung für jede Partition an. Mögliche Werte sind NONE, ROW und PAGE.|  
|pdw_node_id|`int`|Der eindeutige Bezeichner einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Knoten.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>Beispiel A: Anzeige Zeilen in jeder Partition innerhalb jedes Verteilungspunkts 

Gilt für: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
Verwenden Sie zum Anzeigen der Anzahl der Zeilen in jeder Partition innerhalb jedes Verteilungspunkts [DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) .

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>Beispiel B: verwendet-Systemsichten auf Zeilen in jeder Partition der einzelnen Verteilungspunkte in einer Tabelle anzuzeigen.

Gilt für: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
Diese Abfrage gibt die Anzahl der Zeilen in jeder Partition der einzelnen Verteilungspunkte in der Tabelle `myTable`.  
 
```  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

