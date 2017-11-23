---
title: Sys.pdw_nodes_column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31eb71e09e041f6d23c0c88e1ca1423f3693faa7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodescolumnstorerowgroups-transact-sql"></a>Sys.pdw_nodes_column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu gruppierten columnstore-Indizes auf Segmentbasis der Administrator System Management in Entscheidungen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. **Sys.pdw_nodes_column_store_row_groups** verfügt über eine Spalte für die Gesamtzahl der physisch gespeicherten Zeilen (einschließlich jenen, als gelöscht markiert) und eine Spalte für die Anzahl der Zeilen, die als gelöscht markiert. Verwendung **sys.pdw_nodes_column_store_row_groups** um zu bestimmen, welche Gruppen, haben Sie einen hohen Prozentsatz der gelöschten Zeilen, und sollte neu erstellt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID der zugrunde liegenden Tabelle. Dies ist der physische Tabelle auf den Computeknoten nicht die Objekt-ID für die logische Tabelle auf den Knoten "Zugriffssteuerung". Object_id stimmt beispielsweise nicht mit Object_id in sys.tables überein.<br /><br /> Verwenden Sie zum Verknüpfen mit sys.tables sys.pdw_index_mappings.|  
|**index_id**|**int**|ID des gruppierten columnstore-Indexes auf *Object_id* Tabelle.|  
|**Partitionsnummer**|**int**|ID der Tabellenpartition, die Zeilengruppe enthält *Row_group_id*. Sie können *Partition_number* auf diese DMV mit sys.partitions zu verknüpfen.|  
|**row_group_id**|**int**|ID der dieser Zeilengruppe. Diese ist innerhalb der Partition eindeutig.|  
|**dellta_store_hobt_id**|**bigint**|Die hobt_id für Deltazeilengruppen oder NULL, wenn der Zeilengruppentyp nicht Delta ist. Eine Deltazeilengruppe ist eine Zeilengruppe mit Lese-/Schreibzugriff, die neue Datensätze akzeptiert. Eine deltazeilengruppe hat die **öffnen** Status. Eine Deltazeilengruppe befindet sich weiterhin im rowstore-Format und wurde nicht in das columnstore-Format komprimiert.|  
|**Status**|**tinyint**|Die der state_description zugeordnete ID.<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|Beschreibung des persistenten Status der Zeilengruppe:<br /><br /> OPEN: Eine Zeilengruppe mit Lese-/Schreibzugriff, die neue Datensätze akzeptiert. Eine offene Zeilengruppe befindet sich weiterhin im rowstore-Format und wurde nicht in das columnstore-Format komprimiert.<br /><br /> CLOSED: Eine Zeilengruppe, die aufgefüllt, aber vom Tupelverschiebungsprozess noch nicht komprimiert wurde.<br /><br /> COMPRESSED: Eine Zeilengruppe, die aufgefüllt und komprimiert wurde.|  
|**total_rows**|**bigint**|Gesamtzahl der Zeilen, die in der Zeilengruppe physisch gespeichert sind. Einige wurden u. U. gelöscht, sind aber weiterhin gespeichert. Die maximale Anzahl der Zeilen in einer Zeilengruppe beträgt 1.048.576 (hexadezimal FFFFF).|  
|**deleted_rows**|**bigint**|Anzahl der Zeilen in der Zeilengruppe physisch gespeichert, die zum Löschen markiert sind.<br /><br /> Die Zeile immer 0 für DELTA-Gruppen.|  
|**size_in_bytes**|**int**|Gesamtgröße in Bytes aller Seiten in dieser Zeilengruppe. Diese Größe schließt nicht die Größe, die zum Speichern von Metadaten oder freigegebenen Wörterbüchern erforderlich.|  
|**pdw_node_id**|**int**|Eindeutige Id des ein [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Knoten.|  
|**distribution_id**|**int**|Eindeutige Id der Verteilung.|
  
## <a name="remarks"></a>Hinweise  
 Gibt eine Zeile für jede columnstore-Zeilengruppe für jede Tabelle zurück, die über einen gruppierten oder nicht gruppierten columnstore-Index verfügt.  
  
 Verwendung **sys.pdw_nodes_column_store_row_groups** bestimmt die Anzahl der Zeilen in der Zeilengruppe und die Größe der Zeilengruppe enthalten.  
  
 Wenn die Anzahl der gelöschten Zeilen in einer Zeilengruppe auf einen hohen Prozentsatz der Gesamtzeilen ansteigt, wird die Tabelle weniger effizient. Erstellen Sie den columnstore-Index neu, um die Tabellengröße zu verringern und die Datenträger-E/A zu reduzieren, die zum Lesen der Tabelle erforderlich ist. Die Verwendung des columnstore-Index neu erstellt die **REBUILD** -Option von der **ALTER INDEX** Anweisung.  
  
 Aktualisierbare Columnstore fügt zunächst neue Daten in eine **öffnen** Zeilengruppe, die im Rowstore-Format und wird manchmal auch als Deltatabelle bezeichnet.  Sobald eine offene Zeilengruppe voll ist, ändert sich der Status **geschlossen**. Eine geschlossene Zeilengruppe wird durch die tupelverschiebungsfunktion in columnstore-Format komprimiert und ändert den Zustand zu **COMPRESSED**.  Die Tupelverschiebungsfunktion ist ein Hintergrundprozess, der regelmäßig aktiv wird und überprüft, ob geschlossene Zeilengruppen vorhanden sind, die in eine columnstore-Zeilengruppe komprimiert werden können.  Die Tupelverschiebungsfunktion gibt außerdem alle Zeilengruppen frei, in denen alle Zeilen gelöscht wurden. Freigegebene Zeilengruppen werden als **ZURÜCKGEZOGEN**. Um die tupelverschiebungsfunktion direkt auszuführen, verwenden die **REORGANIZE** -Option von der **ALTER INDEX** Anweisung.  
  
 Wenn eine columnstore-Zeilengruppe aufgefüllt wurde, wird sie komprimiert und akzeptiert keine neuen Zeilen mehr. Wenn aus einer komprimierten Gruppe Zeilen gelöscht werden, verbleiben sie zwar, werden aber als gelöscht gekennzeichnet. Updates einer komprimierten Gruppe werden als Löschvorgang für die komprimierte Gruppe und als Einfügevorgang für eine offene Gruppe implementiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **VIEW SERVER STATE** Berechtigung.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel verknüpft die **sys.pdw_nodes_column_store_row_groups** Tabelle mit anderen Systemtabellen, um Informationen über bestimmte Tabellen zurückzugeben. Die berechnete `PercentFull`-Spalte ist eine Schätzung der Effizienz der Zeilengruppe. Zum Suchen von Informationen zu einer einzelnen Tabelle entfernen Kommentar Bindestriche vor der WHERE-Klausel aus, und geben Sie einen Tabellennamen.  
  
```  
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
AND CSRowGroups.index_id = NI.index_id      
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

Die folgenden [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] Beispiel zählt die Zeilen pro Partition, für die gruppierte Spalte ebenfalls speichert, wie viele Zeilen in Gruppen geöffnet, geschlossen oder komprimierte Zeile sind:  

```
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
JOIN sys.pdw_nodes_tables pt
ON rg.object_id = pt.object_id AND rg.pdw_node_id = pt.pdw_node_id AND pt.distribution_id = rg.distribution_id
JOIN sys.pdw_table_mappings tm
ON pt.name = tm.physical_name
INNER JOIN sys.tables t
ON tm.object_id = t.object_id
INNER JOIN sys.schemas s
ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Erstellen Sie columnstore-INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [Sys.pdw_nodes_column_store_segments &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [Sys.pdw_nodes_column_store_dictionaries &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
