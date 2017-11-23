---
title: dm_db_column_store_row_group_physical_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/04/2017
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
- sys.dm_db_column_store_row_group_physical_stats_TSQL
- sys.dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats
- dm_db_column_store_row_group_physical_stats_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dm_db_column_store_row_group_physical_stats
- sys.dm_db_column_store_row_group_physical_stats dynamic management view
caps.latest.revision: "15"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e1c1e25181ff25d354ad29dcd2db4f5210ce1b2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbcolumnstorerowgroupphysicalstats-transact-sql"></a>dm_db_column_store_row_group_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Stellt die aktuellen Sperren auf Informationen zu allen columnstore-Indizes in der aktuellen Datenbank.  
  
 Dies erweitert die Katalogsicht [column_store_row_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID der zugrunde liegenden Tabelle.|  
|**index_id**|**int**|ID der diesen columnstore-Index auf *Object_id* Tabelle.|  
|**Partitionsnummer**|**int**|ID der Tabellenpartition, die enthält *Row_group_id*. Sie können partition_number verwenden, um diese DMV mit sys.partitions zu verknüpfen.|  
|**row_group_id**|**int**|ID der dieser Zeilengruppe. Bei partitionierten Tabellen ist dies in der Partition eindeutig.<br /><br /> -1 für eine in-Memory-Erweiterung.|  
|**delta_store_hobt_id**|**bigint**|Die Hobt_id für eine Zeilengruppe in der deltaspeicher.<br /><br /> NULL, wenn die Zeilengruppe nicht im deltastore vorhanden ist.<br /><br /> NULL für Ende einer in-Memory-Tabelle.|  
|**Status**|**tinyint**|Verbundene ID-Nummer *State_description*.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED<br /><br /> 4 = TOMBSTONE<br /><br /> KOMPRIMIERTE ist der einzige Zustand, der für Tabellen im Arbeitsspeicher gilt.|  
|**state_desc**|**nvarchar(60)**|Beschreibung des Status der Zeile:<br /><br /> INVISIBLE – ein Zeilengruppe, die erstellt wird. Beispiel: <br />Eine Zeilengruppe im Columnstore ist UNSICHTBAR, während die Daten komprimiert werden. Nachdem Sie die Komprimierung einer Switch-Metadatenänderungen wurde der Zustand der Zeile columnstore-Gruppe aus UNSICHTBAR COMPRESSED und der Status der Deltastore-Zeilengruppe von geschlossen, TOMBSTONE.<br /><br /> OPEN Sie: eine Deltastore-Zeilengruppe, die neue Zeilen akzeptiert wird. Eine offene Zeilengruppe befindet sich weiterhin im rowstore-Format und wurde nicht in das columnstore-Format komprimiert.<br /><br /> CLOSED: eine Zeilengruppe in der deltaspeicher, der die maximale Anzahl von Zeilen enthält, und wartet darauf, dass tupelverschiebungsprozess es in den Columnstore komprimiert.<br /><br /> COMPRESSED: eine Zeilengruppe, die mit der columnstore-Komprimierung komprimiert und im Columnstore gespeichert.<br /><br /> TOMBSTONE – verwendet eine Zeilengruppe, die früher wurde in den Deltastore und nicht länger.|  
|**total_rows**|**bigint**|Anzahl der Zeilen, die physische gespeichert, in der Zeilengruppe. Für komprimierte Zeilengruppen schließt dies die Zeilen, die markiert sind, gelöscht.|  
|**deleted_rows**|**bigint**|Anzahl der Zeilen in eine komprimierte Zeilengruppe physisch gespeichert, die zum Löschen markiert sind.<br /><br /> 0 für Zeilengruppen, in denen in der deltaspeicher befinden.|  
|**size_in_bytes**|**bigint**|Gesamtgröße in Bytes aller Seiten in dieser Zeilengruppe. Diese Größe schließt nicht die Größe, die zum Speichern von Metadaten oder freigegebenen Wörterbüchern erforderlich.|  
|**trim_reason**|**tinyint**|Grund für die komprimierte Zeilengruppe haben ausgelöst ist kleiner als die maximale Anzahl von Zeilen.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION<br /><br /> 1 - NO_TRIM<br /><br /> 2 – BULKLOAD<br /><br /> 3 – REORG<br /><br /> 4 – DICTIONARY_SIZE<br /><br /> 5 – MEMORY_LIMITATION<br /><br /> 6 – RESIDUAL_ROW_GROUP<br /><br /> 7 - STATS_MISMATCH<br /><br /> 8 - LANGER|  
|**trim_reason_desc**|**nvarchar(60)**|Beschreibung des *Trim_reason*.<br /><br /> 0 – UNKNOWN_UPGRADED_FROM_PREVIOUS_VERSION: aufgetreten ist, beim Upgrade von der vorherigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 - NO_TRIM: Die Zeilengruppe wurde nicht abgeschnitten. Die Zeilengruppe wurde mit dem Maximum von 1,048,476 Zeilen komprimiert.  Die Anzahl der Zeilen kann kleiner sein, wenn eine Subsset von Zeilen gelöscht wurde, nachdem der Delta-Zeilengruppe geschlossen wurde<br /><br /> 2 – BULKLOAD: Die Batchgröße der Bulk Load beschränkt die Anzahl der Zeilen an.<br /><br /> 3 – REORG: Gezwungen Komprimierung im Rahmen des neuorganisierungsbefehls.<br /><br /> 4 – DICTIONARY_SIZE: Wörterbuch Größe vergrößert zu groß, um alle Zeilen zusammen komprimiert wurde.<br /><br /> 5 – MEMORY_LIMITATION: Nicht genügend Arbeitsspeicher verfügbar, um alle Zeilen zusammen zu komprimieren.<br /><br /> 6 – RESIDUAL_ROW_GROUP: Geschlossen im Rahmen des letzten Zeilengruppe mit Zeilen < 1 Million während der indexerstellung an<br /><br /> STATS_MISMATCH: nur für Columnstore in in-Memory-Tabelle. Wenn Statistiken nicht ordnungsgemäß angegeben > = 1 Million gekennzeichneten Zeilen in das Protokollfragment jedoch weniger wurde, weist der komprimierten Zeilengruppe < 1 million Zeilen<br /><br /> LANGER: nur für Columnstore in in-Memory-Tabelle. Tail > 1 million gekennzeichneten Zeilen verfügt, werden die letzten Stapel verbleibenden Zeilen komprimiert ist die Anzahl die 100 KB bis 1 million|  
|**transition_to_compressed_state**|tinyint|Zeigt an, wie dieser Zeilengruppe aus dem Deltastore in einem komprimierten Zustand in den Columnstore verschoben wurde.<br /><br /> 1 - NOT_APPLICABLE<br /><br /> 2 – INDEX_BUILD<br /><br /> 3 – TUPLE_MOVER<br /><br /> 4 – REORG_NORMAL<br /><br /> 5 – REORG_FORCED<br /><br /> 6 - BULKLOAD<br /><br /> 7 - ZUSAMMENFÜHREN|  
|**transition_to_compressed_state_desc**|nvarchar(60)|NOT_APPLICABLE – gilt der Vorgang nicht in den deltastore verschoben. Oder die Zeilengruppe wurde vor dem Upgrade auf komprimiert [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] in diesem Fall nicht der Verlauf beibehalten wird.<br /><br /> INDEX_BUILD – Erstellen eines Indexes oder indexneuerstellung komprimierte Zeilengruppe.<br /><br /> TUPLE_MOVER – komprimiert die tupelverschiebungsfunktion im Hintergrund ausgeführte die Zeilengruppe. Dies erfolgt, nachdem die Zeilengruppe vom GEÖFFNETEN Zustand auf "geschlossen" ändert.<br /><br /> REORG_NORMAL – die Neuorganisation ALTER INDEX... NEUORGANISATION, die GESCHLOSSENE Zeilengruppe aus dem Deltastore in den Columnstore verschoben. Dies aufgetreten ist, bevor die tupelverschiebungsfunktion die Zeilengruppe zu verschieben konnte.<br /><br /> REORG_FORCED – dieser Zeilengruppe wurde in den Deltastore geöffnet und in den Columnstore erzwungen wurde, bevor sie eine vollständige Anzahl von Zeilen enthielt.<br /><br /> BULKLOAD – komprimiert ein Massenimport die Zeilengruppe direkt ohne Verwendung des deltastores.<br /><br /> MERGE – ein Merge-Vorgang eine oder mehrere Zeilengruppen in dieser Zeilengruppe konsolidiert und anschließend ausgeführt, die columnstore-Komprimierung.|  
|**has_vertipaq_optimization**|bit|Vertipaq-Optimierung verbessert columnstore-Komprimierung durch das Neuanordnen der Reihenfolge der Zeilen in der Zeilengruppe höhere Komprimierung erzielen. Diese Optimierung erfolgt automatisch in den meisten Fällen. Es gibt zwei Fälle, die Vertipaq-Optimierung nicht verwendet wird:<br/>  a. Wenn eine Delta-Zeilengruppe in den Columnstore verschoben werden und es einen oder mehrere nicht gruppierte Indizes für den columnstore-Index gibt - wird in diesem Fall Vertipaq Optimierung übersprungen, um Änderungen an den Zuordnungsindex minimiert;<br/> b. für columnstore-Indizes für Speicheroptimierte Tabellen. <br /><br /> 0 = Nein<br /><br /> 1 = Ja|  
|**Generation**|bigint|Zeile Gruppe Generierung dieser Zeilengruppe zugeordnet sind.|  
|**created_time**|datetime2|Uhrzeit für die Erstellung dieser Zeilengruppe.<br /><br /> NULL – für einen columnstore-Index für eine Tabelle im Arbeitsspeicher.|  
|**closed_time**|datetime2|Uhrzeit für die bei dieser Zeilengruppe geschlossen wurde.<br /><br /> NULL – für einen columnstore-Index für eine Tabelle im Arbeitsspeicher.|  
  
## <a name="results"></a>Ergebnisse  
 Gibt eine Zeile für jede Zeilengruppe in der aktuellen Datenbank zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Berechtigungen sind erforderlich:  
  
-   CONTROL-Berechtigung für die Tabelle.  
  
-   VIEW DATABASE STATE-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calculate-fragmentaton-to-decide-when-to-reorganize-or-rebuild-a-columnstore-index"></a>A. Fragmentaton, um zu entscheiden, wann Neuorganisieren oder Neuerstellen eines columnstore-Indexes zu berechnen.  
 Für columnstore-Indizes ist der Prozentsatz der gelöschten Zeilen ein gutes Maß für die Fragmentierung in einer Zeilengruppe. Wenn die Fragmentierung liegt bei 20 % oder mehr wird empfohlen, die gelöschten Zeilen zu entfernen.  Beispiele finden Sie unter [columnstore-Index-Defragmentierung](~/relational-databases/indexes/columnstore-indexes-defragmentation.md).  
  
 In diesem Beispiel verknüpft **dm_db_column_store_row_group_physical_stats** mit anderen System-Tabellen und berechnet dann die `Fragmentation` Spalte als eine Schätzung der Effizienz der jede Zeilengruppe in der aktuellen Datenbank.     Nach Informationen zu einer einzelnen Tabelle entfernen, die kommentarbindestriche vor, der **, in denen** Klausel, und geben Sie einen Tabellennamen an.  
  
```tsql  
SELECT i.object_id,   
    object_name(i.object_id) AS TableName,   
    i.name AS IndexName,   
    i.index_id,   
    i.type_desc,   
    CSRowGroups.*,  
    100*(ISNULL(deleted_rows,0))/total_rows AS 'Fragmentation'  
FROM sys.indexes AS i  
JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id AND i.index_id = CSRowGroups.index_id   
-- WHERE object_name(i.object_id) = 'table_name'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys. ALL_COLUMNS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [computed_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [column_store_dictionaries &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
