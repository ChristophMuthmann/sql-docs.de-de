---
title: Sys. internal_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cbdff6493fca5bbb9aae67a8a7c7be58b7554556
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysinternaltables-transact-sql"></a>sys.internal_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes Objekt zurück, bei dem es sich um eine interne Tabelle handelt. Interne Tabellen werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch generiert und dienen der Unterstützung verschiedener Funktionen. Wenn Sie beispielsweise einen primären XML-Index erstellen, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch eine interne Tabelle zur persistenten Aufbewahrung der aufgeteilten XML-Dokumentdaten. Interne Tabellen sind der **Sys** -Schema jeder Datenbank, und weisen eindeutige, vom System generierte Namen, die ihrer Funktion, z. B. angeben **xml_index_nodes_2021582240_32001** oder  **queue_messages_1977058079**  
  
 Interne Tabellen enthalten keine Daten, auf die von Benutzern zugegriffen werden kann. Ihre Schemas stehen fest und können nicht geändert werden. Sie können in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht auf interne Tabellennamen verweisen. Beispielsweise kann nicht ausführen eine Anweisung wie SELECT \* FROM  *\<internal_table_name >*. Sie können Katalogsichten jedoch abfragen, um die Metadaten interner Tabellen anzuzeigen.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<Von sys.objects geerbte Spalten >**||Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**internal_type**|**tinyint**|Der Typ der internen Tabelle:<br /><br /> 201 = **Queue_messages**<br /><br /> 202 = **Xml_index_nodes**<br /><br /> 203 = **Fulltext_catalog_freelist**<br /><br /> 205 = **Query_notification**<br /><br /> 206 = **Service_broker_map**<br /><br /> 207 = **Extended_indexes** (z. B. ein räumlicher Index)<br /><br /> 208 = **Filestream_tombstone**<br /><br /> 209 = **Change_tracking**<br /><br /> 210 = **Tracked_committed_transactions**|  
|**internal_type_desc**|**nvarchar(60)**|Die Beschreibung des Typs der internen Tabelle:<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS|  
|**Parent_ID**|**int**|ID des übergeordneten Elements, unabhängig davon, ob es über einen Schemabereich verfügt oder nicht. Andernfalls 0, wenn es kein übergeordnetes Element gibt.<br /><br /> **Queue_messages** = **Object_id** der Warteschlange<br /><br /> **Xml_index_nodes** = **Object_id** des XML-Indexes<br /><br /> **Fulltext_catalog_freelist** = **Fulltext_catalog_id** des Volltext-Katalogs<br /><br /> **Fulltext_index_map** = **Object_id** des Volltext-Indexes<br /><br /> **Query_notification**, oder **Service_broker_map** = 0<br /><br /> **Extended_indexes** = **Object_id** eines erweiterten Indexes, z. B. ein räumlicher Index<br /><br /> **Object_id** der Tabelle, für welche Tabelle die änderungsnachverfolgung aktiviert ist = **Change_tracking**|  
|**parent_minor_id**|**int**|Die Neben-ID des übergeordneten Elements.<br /><br /> **Xml_index_nodes** = **Index_id** des XML-Indexes<br /><br /> **Extended_indexes** = **Index_id** eines erweiterten Indexes, z. B. ein räumlicher Index<br /><br /> 0 = **Queue_messages**, **Fulltext_catalog_freelist**, **Fulltext_index_map**, **Query_notification**,  **Service_broker_map**, oder **Change_tracking**|  
|**lob_data_space_id**|**int**|Ein Wert ungleich Null ist die ID des Datenbereichs (Dateigruppe oder Partitionsschema), der die LOB-Daten (Large Object) für diese Tabelle enthält.|  
|**filestream_data_space_id**|**int**|Zur künftigen Verwendung reserviert.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Hinweise  
 Interne Tabellen werden in dieselbe Dateigruppe wie die übergeordnete Entität platziert. Sie können die in Beispiel F unten dargestellte Katalogabfrage zur Rückgabe der Anzahl von Seiten verwenden, die interne Tabellen für Daten innerhalb und außerhalb von Zeilen sowie LOB-Daten (Large Object) benötigen.  
  
 Sie können die [Sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) Systemprozedur speicherverwendungsdaten für interne Tabellen zurückgeben. **Sp_spaceused** meldet interne Tabellenbereich auf folgende Weise:  
  
-   Wird ein Warteschlangenname angegeben, wird auf die zugrunde liegende interne Tabelle, die der Warteschlange zugeordnet ist, verwiesen und ihre Speicherverwendung gemeldet.  
  
-   Die von den internen Tabellen von XML-Indizes, räumliche Indizes und Volltextindizes verwendeten Seiten befinden sich die **Index_size** Spalte. Wenn eine Tabelle oder indizierte Sichtname angegeben wird, sind die Seiten für die XML-Indizes, räumlichen Indizes und Volltextindizes für dieses Objekt in den Spalten enthalten **reservierte** und **Index_size**.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen wird die Abfrage von Metadaten interner Tabellen mithilfe von Katalogsichten veranschaulicht.  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>A. Anzeigen interner Tabellen, die Spalten aus der sys.objects-Katalogsicht erben  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>B. Zurückgeben aller Metadaten interner Tabellen (einschließlich der von sys.objects geerbten)  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>C. Zurückgeben von Spalten und Spaltendatentypen interner Tabellen  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>D. Zurückgeben der Indizes interner Tabellen  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>E. Zurückgeben der Statistiken interner Tabellen  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>F. Zurückgeben von Informationen zu Partitionen und Zuordnungseinheiten interner Tabellen  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>G. Zurückgeben der Metadaten interner Tabellen für XML-Indizes  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>H. Zurückgeben der Metadaten interner Tabellen für Service Broker-Warteschlangen  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>I. Zurückgeben der Metadaten interner Tabellen für alle Service Broker-Dienste  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [-Objekt Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
