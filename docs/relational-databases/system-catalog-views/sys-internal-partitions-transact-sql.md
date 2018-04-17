---
title: Sys.internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 160441134e0f848d9b4c46d6501638e8d46e3244
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysinternalpartitions-transact-sql"></a>Sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes Rowset, das die interne Daten für columnstore-Indizes für datenträgerbasierte Tabellen nachverfolgt. Diese Rowsets sind für columnstore-Indizes intern, und speichern nachverfolgen, die gelöschte Zeilen, Zeilengruppe Zuordnungen und Delta-Zeilengruppen. Sie verfolgen Daten für jede für jede Tabellenpartition; Jede Tabelle weist mindestens eine Partition. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Rowsets wird neu erstellt jedes Mal, die sie den columnstore-Index neu erstellt.   
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|Partitions-ID für diese Partition. Sie ist innerhalb einer Datenbank eindeutig.|  
|object_id|**int**|Objekt-ID für die Tabelle mit der Partition an.|  
|index_id|**int**|Index-ID für den columnstore-Index für die Tabelle definiert.<br /><br /> 1 = gruppierter columnstore-Index<br /><br /> 2 = nicht gruppierter columnstore-Index|  
|partition_number|**int**|Die Nummer der Partition.<br /><br /> 1 = der ersten Partition einer partitionierten Tabelle oder die eine Partition einer partitionierten Tabelle.<br /><br /> 2 = zweite Partition, und so weiter.|  
|internal_object_type|**tinyint**|Rowset-Objekte, die interne Daten für den columnstore-Index verfolgen.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP – verfolgt diese Bitmapindex Zeilen, die markiert sind, wie aus dem Columnstore gelöscht. Die Bitmap ist für jede Zeilengruppe, da Partitionen Zeilen in mehrere Zeilengruppen aufweisen können. Die Zeilen sind bereit, die physisch weiterhin vorhanden und belegt Speicherplatz im Columnstore sind.<br /><br /> COLUMN_STORE_DELTA_STORE – speichert Gruppen von Zeilen, wird aufgerufen, Zeilengruppen, die in spaltenweise Speicherung nicht komprimiert wurden. Jeder Tabellenpartition können NULL oder mehr Deltastore-Zeilengruppen.<br /><br /> COLUMN_STORE_DELETE_BUFFER – für die Verwaltung von Löschvorgängen an aktualisierbare nicht gruppierte columnstore-Indizes. Wenn eine Abfrage eine Zeile aus der zugrunde liegenden Rowstore-Tabelle gelöscht wird, verfolgt löschpuffers das Löschen aus dem Columnstore. Wenn die Anzahl der gelöschten Zeilen 1048576 überschritten wird, werden sie wieder in der Delete-Bitmap mit Tupelverschiebungsvorgang Thread oder durch einen expliziten Reorganize-Befehl zusammengeführt.  Zu jedem gegebenen Zeitpunkt zeitlich stellt die Kombination der Delete-Bitmap und löschpuffers alle gelöschte Zeilen.<br /><br /> COLUMN_STORE_MAPPING_INDEX – wird verwendet, nur, wenn der gruppierte columnstore-Index einen sekundären nicht gruppierten Index aufweist. Dies ordnet nicht gruppierten Indexschlüssel auf die richtige Zeilengruppe und die Zeilen-ID in den Columnstore. Es speichert nur die Schlüssel für Zeilen, die in einer anderen Zeilengruppe zu verschieben; Dies tritt auf, wenn eine deltazeilengruppe komprimiert wird, in den Columnstore und einem Zusammenführungsvorgang Zeilen aus zwei verschiedenen Zeilengruppen.|  
|Row_group_id|**int**|ID für die Delta-Zeilengruppe. Jeder Tabellenpartition können NULL oder mehr Deltastore-Zeilengruppen.|  
|hobt_id|**bigint**|Die ID des Rowsetobjekts, interne. Dies ist eine gute Schlüssel zum Verknüpfen mit anderen DMVs, um weitere Informationen über die physischen Merkmale der internen Rowset abzurufen.|  
|rows|**bigint**|Die ungefähre Anzahl der Zeilen in dieser Partition.|  
|data_compression|**tinyint**|Der Status der Komprimierung für das Rowset.<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|Der Status der Komprimierung für jede Partition. Mögliche Werte für rowstore-Tabellen sind NONE, ROW und PAGE. Mögliche Werte für columnstore-Tabellen sind COLUMNSTORE und COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neue interne Columnstore-Indizes wird neu erstellt jedes Mal, die es erstellt oder neu erstellt einen columnstore-Index.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. Alle von der internen Rowsets für eine Tabelle anzeigen  
 In diesem Beispiel gibt alle von der internen columnstore-Rowsets für eine Tabelle zurück. Sie können auch die Hobt_id verwenden, finden Sie weitere Informationen zu bestimmten Rowset.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
