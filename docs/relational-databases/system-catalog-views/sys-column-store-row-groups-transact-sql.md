---
title: column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.column_store_row_groups_TSQL
- column_store_row_groups
- sys.column_store_row_groups
- column_store_row_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_row_groups catalog view
ms.assetid: 76e7fef2-d1a4-4272-a2bb-5f5dcd84aedc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ea17802f24a60df24fdc4107f52a5170ca4f0ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnstorerowgroups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu gruppierten Columnstore-Indizes auf Segmentbasis bereit, um den Administrator bei Fragen zur Systemverwaltung zu unterstützen. **column_store_row_groups** verfügt über eine Spalte für die Gesamtzahl der physisch gespeicherten Zeilen (einschließlich jenen, als gelöscht markiert) und eine Spalte für die Anzahl der Zeilen, die als gelöscht markiert. Verwendung **column_store_row_groups** um zu bestimmen, welche Gruppen, haben Sie einen hohen Prozentsatz der gelöschten Zeilen, und sollte neu erstellt.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID der Tabelle, in der dieser Index definiert ist.|  
|**index_id**|**int**|ID des Indexes, der diesen columnstore-Index enthält.|  
|**Partitionsnummer**|**int**|ID der Tabellenpartition, die die row_group_id der Zeilengruppe enthält. Sie können partition_number verwenden, um diese DMV mit sys.partitions zu verknüpfen.|  
|**row_group_id**|**int**|Die dieser Zeilengruppe zugeordnete Zeilengruppenzahl. Diese ist innerhalb der Partition eindeutig.<br /><br /> -1 = Ende einer in-Memory-Tabelle.|  
|**delta_store_hobt_id**|**bigint**|Die Hobt_id für offene Zeilengruppe im deltastore.<br /><br /> NULL, wenn die Zeilengruppe nicht im deltastore vorhanden ist.<br /><br /> NULL für das Ende einer in-Memory-Tabelle.|  
|**Status**|**tinyint**|Die der state_description zugeordnete ID.<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED <br /><br /> 4 = TOMBSTONE|  
|**state_description**|**nvarchar(60)**|Beschreibung des persistenten Status der Zeilengruppe:<br /><br /> INVISIBLE – Ein ausgeblendetes komprimiertes Segment wird gerade aus Daten in einem Deltastore erstellt. Lesevorgänge nutzen den Deltastore, bis das unsichtbare komprimierte Segment abgeschlossen ist. Anschließend werden das neue Segment sichtbar gemacht und der Quelldeltastore entfernt.<br /><br /> OPEN: Eine Zeilengruppe mit Lese-/Schreibzugriff, die neue Datensätze akzeptiert. Eine offene Zeilengruppe befindet sich weiterhin im rowstore-Format und wurde nicht in das columnstore-Format komprimiert.<br /><br /> CLOSED: Eine Zeilengruppe, die aufgefüllt, aber vom Tupelverschiebungsprozess noch nicht komprimiert wurde.<br /><br /> COMPRESSED: Eine Zeilengruppe, die aufgefüllt und komprimiert wurde.|  
|**total_rows**|**bigint**|Gesamtzahl der Zeilen, die in der Zeilengruppe physisch gespeichert sind. Einige wurden u. U. gelöscht, sind aber weiterhin gespeichert. Die maximale Anzahl der Zeilen in einer Zeilengruppe beträgt 1.048.576 (hexadezimal FFFFF).|  
|**deleted_rows**|**bigint**|Gesamtzahl der Zeilen in der Zeilengruppe, die als gelöscht markiert sind. Dies ist für DELTA-Zeilengruppen immer 0.|  
|**size_in_bytes**|**bigint**|Größe aller Daten (in Bytes) in dieser Zeilengruppe (ausgenommen von Metadaten oder freigegebenen Wörterbüchern) sowohl für DELTA- als auch für COLUMNSTORE-Zeilengruppen.|  
  
## <a name="remarks"></a>Hinweise  
 Gibt eine Zeile für jede columnstore-Zeilengruppe für jede Tabelle zurück, die über einen gruppierten oder nicht gruppierten columnstore-Index verfügt.  
  
 Verwendung **column_store_row_groups** bestimmt die Anzahl der Zeilen in der Zeilengruppe und die Größe der Zeilengruppe enthalten.  
  
 Wenn die Anzahl der gelöschten Zeilen in einer Zeilengruppe auf einen hohen Prozentsatz der Gesamtzeilen ansteigt, wird die Tabelle weniger effizient. Erstellen Sie den columnstore-Index neu, um die Tabellengröße zu verringern und die Datenträger-E/A zu reduzieren, die zum Lesen der Tabelle erforderlich ist. Die Verwendung des columnstore-Index neu erstellt die **REBUILD** -Option von der **ALTER INDEX** Anweisung.  
  
 Aktualisierbare Columnstore fügt zunächst neue Daten in eine **öffnen** Zeilengruppe, die im Rowstore-Format und wird manchmal auch als Deltatabelle bezeichnet.  Sobald eine offene Zeilengruppe voll ist, ändert sich der Status **geschlossen**. Eine geschlossene Zeilengruppe wird durch die tupelverschiebungsfunktion in columnstore-Format komprimiert und ändert den Zustand zu **COMPRESSED**.  Die Tupelverschiebungsfunktion ist ein Hintergrundprozess, der regelmäßig aktiv wird und überprüft, ob geschlossene Zeilengruppen vorhanden sind, die in eine columnstore-Zeilengruppe komprimiert werden können.  Die Tupelverschiebungsfunktion gibt außerdem alle Zeilengruppen frei, in denen alle Zeilen gelöscht wurden. Freigegebene Zeilengruppen werden als **TOMBSTONE**. Um die tupelverschiebungsfunktion direkt auszuführen, verwenden die **REORGANIZE** -Option von der **ALTER INDEX** Anweisung.  
  
 Wenn eine columnstore-Zeilengruppe aufgefüllt wurde, wird sie komprimiert und akzeptiert keine neuen Zeilen mehr. Wenn aus einer komprimierten Gruppe Zeilen gelöscht werden, verbleiben sie zwar, werden aber als gelöscht gekennzeichnet. Updates einer komprimierten Gruppe werden als Löschvorgang für die komprimierte Gruppe und als Einfügevorgang für eine offene Gruppe implementiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Gibt Informationen für eine Tabelle zurück, wenn der Benutzer hat **SICHTDEFINITION** Berechtigung für die Tabelle.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel verknüpft die **column_store_row_groups** Tabelle mit anderen Systemtabellen, um Informationen über bestimmte Tabellen zurückzugeben. Die berechnete `PercentFull`-Spalte ist eine Schätzung der Effizienz der Zeilengruppe. Nach Informationen zu einer einzelnen Tabelle entfernen, die kommentarbindestriche vor, der **, in denen** Klausel, und geben Sie einen Tabellennamen an.  
  
```  
SELECT i.object_id, object_name(i.object_id) AS TableName,   
i.name AS IndexName, i.index_id, i.type_desc,   
CSRowGroups.*,   
100*(total_rows - ISNULL(deleted_rows,0))/total_rows AS PercentFull    
FROM sys.indexes AS i  
JOIN sys.column_store_row_groups AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id  
AND i.index_id = CSRowGroups.index_id   
--WHERE object_name(i.object_id) = '<table_name>'   
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
  
  

