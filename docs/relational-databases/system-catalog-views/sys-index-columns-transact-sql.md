---
title: index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_columns
- sys.index_columns_TSQL
- index_columns
- index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.index_columns catalog view
ms.assetid: 211471aa-558a-475c-9b94-5913c143ed12
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 28917dfed2c032fc3a6646c77cbd869fc2982798
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysindexcolumns-transact-sql"></a>sys.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile pro Spalte, die Teil einer **sys.indexes** Index oder einer unsortierten Tabelle (Heap).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Objekts, für das der Index definiert wird|  
|**index_id**|**int**|ID des Indexes, in dem die Spalte definiert wird|  
|**index_column_id**|**int**|Die ID der Indexspalte. **Index_column_id** einzigartig ist nur **Index_id**.|  
|**column_id**|**int**|ID der Spalte in **object_id**.<br /><br /> 0 = Zeilenbezeichner (RID, Row Identifier) in einem nicht gruppierten Index.<br /><br /> **column_id** ist nur innerhalb von **object_id**eindeutig.|  
|**key_ordinal**|**tinyint**|Ordinalzahl (auf 1 basierend) innerhalb einer Gruppe von Schlüsselspalten.<br /><br /> 0 = Keine Schlüsselspalte oder ein XML-Index, columnstore-Index oder räumlicher Index.<br /><br /> Hinweis: Ein XML-Index oder räumlichen Index kann einen Schlüssel, da die zugrunde liegenden Spalten nicht vergleichbar sind, was bedeutet, dass ihre Werte nicht sortiert werden können.|  
|**partition_ordinal**|**tinyint**|Ordinalzahl (1-basiert) innerhalb einer Gruppe von Partitionierungsspalten. Ein gruppierter columnstore-Index kann maximal 1 Partitionierungsspalte aufweisen.<br /><br /> 0 = Keine Partitionierungsspalte.|  
|**is_descending_key**|**bit**|1 = Indexschlüsselspalte hat eine absteigende Sortierreihenfolge.<br /><br /> 0 = Indexschlüsselspalte hat eine aufsteigende Sortierreihenfolge, oder die Spalte ist Teil eines columnstore-Indexes oder Hashindexes.|  
|**is_included_column**|**bit**|1 = Spalte ist eine Nichtschlüsselspalte, die dem Index mit der CREATE INDEX INCLUDE-Klausel hinzugefügt wurde, oder die Spalte ist Teil eines columnstore-Indexes.<br /><br /> 0 = Spalte ist keine eingeschlossene Spalte.<br /><br /> Spalten, die implizit hinzugefügt werden, da sie Teil der Gruppierungsschlüssel sind in nicht aufgelisteten **index_columns**.<br /><br /> Spalten, die implizit hinzugefügt wurden, da sie eine Partitionierungsspalte sind, werden als 0 zurückgegeben.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Indizes und Indexspalten für die Tabelle `Production.BillOfMaterials` zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.object_id = OBJECT_ID('Production.BillOfMaterials');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
index_name                                                 column_name        index_column_id key_ordinal is_included_column  
---------------------------------------------------------- -----------------  --------------- ----------- -------------  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ProductAssemblyID  1               1           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ComponentID        2               2           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate StartDate          3               3           0  
PK_BillOfMaterials_BillOfMaterialsID                       BillOfMaterialsID  1               1           0  
IX_BillOfMaterials_UnitMeasureCode                         UnitMeasureCode    1               1           0  
  
(5 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
