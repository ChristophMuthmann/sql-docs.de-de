---
title: Sys.Indexes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f36ab998b84379900746ae39957b3b4acee15f04
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile pro Index oder Heap eines tabellarischen Objekts, wie z. B. einer Tabelle, Sicht oder Tabellenwertfunktion.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Objekts, zu dem dieser Index gehört.|  
|**name**|**sysname**|Der Name des Indexes. **Namen** ist nur innerhalb des Objekts eindeutig.<br /><br /> NULL = Heap|  
|**index_id**|**int**|Die ID des Index. **Index_id** ist nur innerhalb des Objekts eindeutig.<br /><br /> 0 = Heap<br /><br /> 1 = Gruppierter Index<br /><br /> > 1 = Nicht gruppierter Index|  
|**Typ**|**tinyint**|Typ des Index:<br /><br /> 0 = Heap<br /><br /> 1 = In einem Cluster gruppiert<br /><br /> 2 = Nicht gruppiert<br /><br /> 3 = XML<br /><br /> 4 = Räumlich<br /><br /> 5 = gruppierter columnstore-Index. **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 6 = nicht gruppierter columnstore-Index. **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 7 = nicht gruppierter Hashindex. **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Typs des Index:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> GRUPPIERTE COLUMNSTORE - **betrifft**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nicht gruppierte COLUMNSTORE - **betrifft**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> NONCLUSTERED HASH: Nicht gruppierte Hashindizes werden nur auf Speicheroptimierte Tabellen unterstützt. Die sys.hash_indexes-Sicht zeigt die aktuellen Hashindizes und Hasheigenschaften an. Weitere Informationen finden Sie unter [hash_indexes &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md). **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_unique**|**bit**|1 = Der Index ist eindeutig.<br /><br /> 0 = Der Index ist nicht eindeutig.<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**data_space_id**|**int**|ID des Datenspeicherplatzes für diesen Index. Der Datenspeicherplatz ist entweder eine Dateigruppe oder ein Partitionsschema.<br /><br /> 0 = **Object_id** ist eine Funktion mit Tabellenrückgabe oder der Index im Arbeitsspeicher.|  
|**IGNORE_DUP_KEY**|**bit**|1 = IGNORE_DUP_KEY ist ON.<br /><br /> 0 = IGNORE_DUP_KEY ist OFF.|  
|**is_primary_key**|**bit**|1 = Der Index ist Teil einer PRIMARY KEY-Einschränkung.<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**is_unique_constraint**|**bit**|1 = Der Index ist Teil einer UNIQUE-Einschränkung.<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**Fill_Factor auf den Wert**|**tinyint**|> 0 = FILLFACTOR-Prozentsatz, der beim Erstellen oder Neuerstellen des Index verwendet wurde.<br /><br /> 0 = Standardwert<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**is_padded**|**bit**|1 = PADINDEX ist ON.<br /><br /> 0 = PADINDEX ist OFF.<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**is_disabled**|**bit**|1 = Der Index ist deaktiviert.<br /><br /> 0 = Der Index ist nicht deaktiviert.|  
|**is_hypothetical**|**bit**|1 = Der Index ist hypothetisch und kann nicht direkt als Datenzugriffspfad verwendet werden. Hypothetische Indizes enthalten Statistiken auf Spaltenebene.<br /><br /> 0 = Der Index ist nicht hypothetisch.|  
|**allow_row_locks**|**bit**|1 = Der Index lässt Zeilensperren zu.<br /><br /> 0 = Der Index lässt Zeilensperren nicht zu.<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**allow_page_locks**|**bit**|1 = Der Index lässt Seitensperren zu.<br /><br /> 0 = Der Index lässt Seitensperren nicht zu.<br /><br /> Immer 0 für gruppierte columnstore-Indizes.|  
|**has_filter**|**bit**|1 = Index hat einen Filter und enthält nur Zeilen, die der Filterdefinition entsprechen.<br /><br /> 0 = Index hat keinen Filter.|  
|**filter_definition**|**nvarchar(max)**|Ausdruck für die Teilmenge von Zeilen, die im gefilterten Index enthalten sind.<br /><br /> NULL für Heap oder nicht gefilterten Index.|  
|**auto_created**|**bit**|1 = der Index wurde erstellt, durch die automatische Optimierung.<br /><br />0 = Index wurde vom Benutzer erstellt.
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Indizes für die Tabelle `Production.Product` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Sys. xml_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. key_constraints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys. partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
