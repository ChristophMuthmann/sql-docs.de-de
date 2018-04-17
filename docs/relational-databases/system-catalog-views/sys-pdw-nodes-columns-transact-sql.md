---
title: Sys.pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 709598377fddb833bb11415cc42348b2958f3717
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodescolumns-transact-sql"></a>Sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Zeigt die Spalten für benutzerdefinierte Tabellen und benutzerdefinierte Ansichten.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|Die ID des Objekts, zu dem diese Spalte gehört.||  
|name|**sysname**|Der Name der Spalte. Eindeutig im-Objekt.||  
|column_id|**int**|ID der Spalte. Eindeutig im-Objekt.||  
|system_type_id|**tinyint**|Die ID des Systemtyps der Spalte.||  
|user_type_id|**int**|Die ID des vom Benutzer definierten Typs der Spalte.||  
|max_length|**smallint**|Maximale Länge (in Byte) für die Spalte.|Enthält 1, die nicht unterstützten Spaltentypen (ungültig).|  
|precision|**tinyint**|Die Genauigkeit der Spalte, wenn sie auf numerischen Werten basiert; andernfalls 0.||  
|scale|**tinyint**|Die Skalierung der Spalte, wenn sie auf numerischen Werten basiert; andernfalls 0.||  
|collation_name|**sysname**|Der Name der Sortierung der Spalte, wenn Sie zeichenbasierte; Andernfalls wird NULL verwendet.||  
|is_nullable|**bit**|1 = Spalte lässt NULL-Werte zu.||  
|is_ansi_padded|**bit**|1 = Spalte verwendet ANSI_PADDING ON-Verhalten, wenn es sich um Zeichen- oder Binärdaten bzw. Daten vom Typ Variant handelt.|Immer 0.|  
|is_rowguidcol|**bit**|1 = Spalte ist eine deklarierte ROWGUIDCOL.|Immer 0.|  
|is_identity|**bit**|1 = Spalte verfügt über Identitätswerte.|Immer 0.|  
|is_computed|**bit**|1 = Spalte ist eine berechnete Spalte.|Immer 0.|  
|is_filestream|**bit**|1 = Spalte ist eine FILESTREAM-Spalte.|Immer 0.|  
|is_replicated|**bit**|1 = Spalte wird repliziert.|Immer 0.|  
|is_non_sql_subscribed|**bit**|1 = Spalte weist einen nicht-SQL-Abonnenten.|Immer 0.|  
|is_merge_published|**bit**|1 = Spalte verwendet die Mergeveröffentlichung.|Immer 0.|  
|is_dts_replicated|**bit**|1 = Spalte werden mithilfe von SSIS repliziert.|Immer 0.|  
|is_xml_document|**bit**|1 = Der Inhalt ist ein vollständiges XML-Dokument.|Immer 0.|  
|xml_collection_id|**int**|0 = Keine XML-Schemaauflistung|Immer 0.|  
|default_object_id|**int**|Die ID des Standardobjekts; 0 = kein Standard.|Immer 0.|  
|rule_object_id|**int**|ID der eigenständigen Regel, die an die Spalte gebunden werden. <br />0 = Keine eigenständige Regel.|Immer 0.|  
|is_sparse|**bit**|1 = Spalte ist eine Sparsespalte.|Immer 0.|  
|is_column_set|**bit**|1 = Spalte ist ein Spaltensatz.|Immer 0.|  
|pdw_node_id|**int**|Der eindeutige Bezeichner einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Knoten.|NOT NULL|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
