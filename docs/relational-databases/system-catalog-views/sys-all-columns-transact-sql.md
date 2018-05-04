---
title: Sys. ALL_COLUMNS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- all_columns_TSQL
- all_columns
- sys.all_columns_TSQL
- sys.all_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_columns catalog view
ms.assetid: 40e04fe9-0b64-4799-84c0-57f128b2bdc2
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a1e0139e23349dc1a21ca8f9b76b2f0f38e707e9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysallcolumns-transact-sql"></a>sys.all_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Zeigt die Union aller Spalten an, die zu benutzerdefinierten Objekten und Systemobjekten gehören.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Die ID des Objekts, zu dem diese Spalte gehört.|  
|name|**sysname**|Der Name der Spalte. Ist eindeutig innerhalb des Objekts.|  
|column_id|**int**|ID der Spalte. Ist eindeutig innerhalb des Objekts.<br /><br /> Spalten-IDs sind möglicherweise nicht sequenziell.|  
|system_type_id|**tinyint**|ID des Systemtyps der Spalte.|  
|user_type_id|**int**|Die ID des vom Benutzer definierten Typs der Spalte.<br /><br /> Um den Namen des Typs zurückzugeben, verknüpfen Sie mit der [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) -Katalogsicht für diese Spalte.|  
|max_length|**smallint**|Maximale Länge (in Byte) für die Spalte.<br /><br /> -1 = Spaltendatentyp ist **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, oder **Xml**.<br /><br /> Für **Text** Spalten, die Max_length-Wert ist 16 oder dem durch Sp_tableoption 'Text in Row' festgelegten Wert.|  
|precision|**tinyint**|Die Genauigkeit der Spalte, wenn sie auf numerischen Werten basiert; andernfalls 0.|  
|scale|**tinyint**|Dezimalstellen der Spalte, wenn diese numerischen Ursprungs ist, andernfalls 0.|  
|collation_name|**sysname**|Der Name der Sortierung der Spalte, wenn Sie zeichenbasierte; Andernfalls wird NULL verwendet.|  
|is_nullable|**bit**|1 = Spalte lässt NULL-Werte zu.|  
|is_ansi_padded|**bit**|1 = Spalte verwendet ANSI_PADDING ON-Verhalten, wenn es sich um Zeichen- oder Binärdaten bzw. Daten vom Typ Variant handelt.<br /><br /> 0 = Bei der Spalte handelt es sich um Zeichen- oder Binärdaten bzw. Daten vom Typ Variant.|  
|is_rowguidcol|**bit**|1 = Spalte ist eine deklarierte ROWGUIDCOL.|  
|is_identity|**bit**|1 = Die Spalte verfügt über Identitätswerte.|  
|is_computed|**bit**|1 = Spalte ist eine berechnete Spalte.|  
|is_filestream|**bit**|1 = Spalte wurde für die Verwendung der Dateidatenstrom-Speicherung deklariert.|  
|is_replicated|**bit**|1 = Spalte wird repliziert.|  
|is_non_sql_subscribed|**bit**|1 = Die Spalte hat einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten.|  
|is_merge_published|**bit**|1 = Spalte verwendet die Mergeveröffentlichung.|  
|is_dts_replicated|**bit**|1 = Die Spalte wird mithilfe von [!INCLUDE[ssIS](../../includes/ssis-md.md)] repliziert.|  
|is_xml_document|**bit**|1 = Der Inhalt ist ein vollständiges XML-Dokument.<br /><br /> 0 = Der Inhalt ist ein Dokumentfragment, oder der Spaltendatentyp ist nicht XML.|  
|xml_collection_id|**int**|Ungleich 0, wenn der Spaltendatentyp ist **Xml** und XML typisiert ist. Der Wert ist die ID der Auflistung mit dem prüfenden XML-Schemanamespace der Spalte.<br /><br /> 0 = Keine XML-Schemaauflistung.|  
|default_object_id|**int**|ID des Standardobjekts, unabhängig davon, ob es eine eigenständige [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), oder eine DEFAULT-Einschränkung in der Zeile, auf Spaltenebene. Die parent_object_id-Spalte eines DEFAULT-Inlineobjekts ist ein Verweis auf die Tabelle selbst.<br /><br /> 0 = Kein Standard.|  
|rule_object_id|**int**|ID der eigenständigen Regel, die mithilfe von sys.sp_bindrule gebunden wird.<br /><br /> 0 = Keine eigenständige Regel.<br /><br /> CHECK-Einschränkungen auf Spaltenebene finden Sie unter [check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|bit|1 = Spalte ist eine Sparsespalte. Weitere Informationen finden Sie unter [Verwenden von Spalten mit geringer Dichte](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|bit|1 = Spalte ist ein Spaltensatz. Weitere Informationen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).|  
|"generated_always_type"|**tinyint**|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Der numerische Wert, der den Typ der Spalte darstellt:<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die textbeschreibung des Typs der Spalte:<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
