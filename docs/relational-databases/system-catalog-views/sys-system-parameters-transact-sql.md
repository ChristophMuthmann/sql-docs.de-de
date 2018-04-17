---
title: Sys. system_parameters (Transact-SQL) | Microsoft Docs
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
- sys.system_parameters
- sys.system_parameters_TSQL
- system_parameters_TSQL
- system_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_parameters catalog view
ms.assetid: 0d135c5f-68b5-4009-a0da-35e6abfee0ff
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 66ef0a52aa2e02520897629903111f0d241b2531
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssystemparameters-transact-sql"></a>sys.system_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jedes Systemobjekt, das über Parameter verfügt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID des Objekts, zu dem dieser Parameter gehört.|  
|**name**|**sysname**|Der Name des Parameters. Ist eindeutig innerhalb des Objekts.<br /><br /> Wenn es sich bei dem Objekt um eine skalare Funktion handelt, ist der Parametername eine leere Zeichenfolge in der Zeile, die den zurückgegebenen Wert darstellt.|  
|**parameter_id**|**int**|ID des Parameters. Ist eindeutig innerhalb des Objekts. Handelt es sich bei dem Objekt um eine Skalarfunktion, stellt **parameter_id** = 0 den Rückgabewert dar.|  
|**system_type_id**|**tinyint**|ID des Systemtyps des Parameters.|  
|**user_type_id**|**int**|Die ID des vom Benutzer definierten Typs des Parameters.<br /><br /> Um den Namen des Typs zurückzugeben, verknüpfen Sie mit der [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) -Katalogsicht für diese Spalte.|  
|**max_length**|**smallint**|Die maximale Länge des Parameters (in Byte). Der Wert beträgt -1, wenn der Datentyp **varchar(max)**, **nvarchar(max)**, **varbinary(max)**oder **xml**ist.|  
|**precision**|**tinyint**|Genauigkeit des Parameters, wenn dieser numerisch ist. Andernfalls ist der Wert 0.|  
|**scale**|**tinyint**|Dezimalstellen des Parameters, wenn dieser numerisch ist. Andernfalls ist der Wert 0.|  
|**is_output**|**bit**|1 = Parameter ist ein Ausgabeparameter (oder Rückgabeparameter), andernfalls 0|  
|**is_cursor_ref**|**bit**|1 = Der Parameter ist ein Cursorverweis.|  
|**has_default_value**|**bit**|1 = Der Parameter hat einen Standardwert.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwaltet nur Standardwerte für CLR-Objekte in dieser Katalogsicht; aus diesem Grund müssen diese Spalte immer der Wert 0 für [!INCLUDE[tsql](../../includes/tsql-md.md)] Objekte. Zum Anzeigen des Standardwert eines Parameters in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Objekt, das Abfragen der **Definition** Spalte die [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht angezeigt werden soll, oder verwenden Sie die [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)-Systemfunktion.|  
|**is_xml_document**|**bit**|1 = Der Inhalt ist ein vollständiges XML-Dokument.<br /><br /> 0 = Inhalt ist ein Dokumentfragment, oder der Datentyp der Spalte ist nicht **xml**.|  
|**default_value**|**sql_variant**|Wenn **has_default_value** gleich 1 ist, entspricht der Wert dieser Spalte dem Standardwert für den Parameter, andernfalls ist er NULL.|  
|**xml_collection_id**|**int**|Ungleich 0, wenn der Datentyp des Parameters **xml** ist, und XML typisiert ist. Der Wert ist die ID der Auflistung, die den prüfenden XML-Schemanamespace für den Parameter enthält.<br /><br /> 0 = Es ist keine XML-Schemaauflistung vorhanden.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [Sys. all_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)  
  
  
