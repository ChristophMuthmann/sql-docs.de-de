---
title: Sys. column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a23388dd2333694f779b9f78de81dd9659916b49
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnstoresegments-transact-sql"></a>sys.column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

Gibt eine Zeile für jedes Spaltensegment in einen columnstore-Index zurück. Es ist ein Spaltensegment pro Spalte pro Zeilengruppe. Beispielsweise gibt eine Tabelle mit 10 Zeilengruppen und Spalten 34 340 Zeilen zurück. 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|Gibt die Partitions-ID an. Ist innerhalb einer Datenbank eindeutig.|  
|**hobt_id**|**bigint**|ID des Heaps oder B-Struktur-Indexes (hobt) für die Tabelle, die diesen columnstore-Index aufweist.|  
|**column_id**|**int**|ID der columnstore-Spalte.|  
|**segment_id**|**int**|Die ID der Zeilengruppe. Aus Kompatibilitätsgründen weiterhin der Spaltenname Segment_id aufgerufen werden, obwohl dies die Rowgroup-ID ist Sie können eindeutig identifizieren, ein Segment mit \<Hobt_id, Partition_id, Column_id >, < Segment_id >.|  
|**version**|**int**|Die Version des Spaltensegmentformats.|  
|**encoding_type**|**int**|Der Typ für dieses Segment verwendete Codierungstyp:<br /><br /> 1 = VALUE_BASED - Zeichenfolge/Binärdaten mit kein Wörterbuch (sehr ähnlich wie 4 mit einige interne Varianten)<br /><br /> 2 = VALUE_HASH_BASED - Zeichenfolge/Binary-Spalte mit dem häufig verwendete Werte im Wörterbuch<br /><br /> 3 = STRING_HASH_BASED - Zeichenfolge/Binary-Spalte mit gemeinsamen Werten im Wörterbuch<br /><br /> 4 = STORE_BY_VALUE_BASED - Zeichenfolge/Binärdaten mit kein Wörterbuch<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED - Zeichenfolge/binäre kein Wörterbuch<br /><br /> Alle Codierungen nutzen Bit-Verpackung und Ausführung Länge Codierung nach Möglichkeit.|  
|**row_count**|**int**|Die Anzahl der Zeilen in der Zeilengruppe.|  
|**has_nulls**|**int**|1, wenn das Spaltensegment NULL-Werte enthält.|  
|**base_id**|**bigint**|Basiswert-Id, wenn der Codierungstyp 1 verwendet wird.  Wenn der Codierungstyp 1 nicht verwendet wird, wird Base_id auf 1 festgelegt.|  
|**Größe**|**float**|Größe, wenn der Codierungstyp 1 verwendet wird.  Wenn der Codierungstyp 1 nicht verwendet wird, wird Magnitude auf 1 festgelegt.|  
|**primary_dictionary_id**|**int**|Der Wert 0 stellt die globale Wörterbuch dar. Der Wert-1 gibt an, dass es keine globalen Wörterbuch für diese Spalte erstellt gibt.|  
|**secondary_dictionary_id**|**int**|Ein Wert ungleich 0 (null) verweist auf die lokalen Wörterbuch für diese Spalte in das aktuelle Segment (d. h. die Zeilengruppe). Der Wert-1 gibt an, dass keine lokales Wörterbuch für dieses Segment vorhanden ist.|  
|**min_data_id**|**bigint**|Die minimale Daten-ID im Spaltensegment.|  
|**max_data_id**|**bigint**|Die maximale Daten-ID im Spaltensegment.|  
|**null_value**|**bigint**|Ein Wert, der zum Darstellen von NULL-Werten verwendet wird.|  
|**on_disk_size**|**bigint**|Die Größe des Segments in Byte.|  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Abfrage gibt Informationen zu Segmenten eines columnstore-Indexes zurück.  
  
```tsql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Spalten erfordern mindestens **SICHTDEFINITION** Berechtigung für die Tabelle. Die folgenden Spalten geben null zurück, es sei denn, der Benutzer verfügt auch über **wählen** Berechtigung: Has_nulls, Base_id, Magnitude, Min_data_id, Max_data_id und Null_value.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys. ALL_COLUMNS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [computed_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
  

