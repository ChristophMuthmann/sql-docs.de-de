---
title: Sys. all_parameters (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- all_parameters_TSQL
- sys.all_parameters
- all_parameters
- sys.all_parameters_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.all_parameters catalog view
ms.assetid: eecbb68e-9b4c-4243-94e2-8096a9cc7892
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a0513ae73ab3feb03bf2da24fcd2e0b458f4e9af
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysallparameters-transact-sql"></a>sys.all_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Zeigt die Vereinigungsmenge aller Parameter an, die zu einem benutzerdefinierten Objekt oder einem Systemobjekt gehören.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID des Objekts, zu dem dieser Parameter gehört.|  
|**name**|**sysname**|Name des Parameters. Ist eindeutig innerhalb des Objekts. Wenn es sich bei dem Objekt um eine skalare Funktion handelt, ist der Parametername eine leere Zeichenfolge in der Zeile, die den zurückgegebenen Wert darstellt.|  
|**parameter_id**|**int**|ID des Parameters. Ist eindeutig innerhalb des Objekts. Handelt es sich bei dem Objekt um eine Skalarfunktion, stellt **parameter_id** = 0 den Rückgabewert dar.|  
|**system_type_id**|**tinyint**|ID des Systemtyps des Parameters.|  
|**user_type_id**|**int**|Die ID des vom Benutzer definierten Typs des Parameters.<br /><br /> Um den Namen des Typs zurückzugeben, verknüpfen Sie mit der [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) -Katalogsicht für diese Spalte.|  
|**max_length**|**smallint**|Die maximale Länge des Parameters (in Byte).<br /><br /> -1 = Spaltendatentyp ist **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, oder **Xml**.|  
|**Genauigkeit**|**tinyint**|Genauigkeit des Parameters, wenn dieser auf Nummern basiert; andernfalls 0.|  
|**Skalierung**|**tinyint**|Skalierung des Parameters, wenn dieser auf Nummern basiert; andernfalls 0.|  
|**is_output**|**bit**|1 = Parameter ist ein Ausgabeparameter (oder Rückgabeparameter), andernfalls 0|  
|**is_cursor_ref**|**bit**|1 = Parameter ist ein Cursorverweisparameter.|  
|**has_default_value**|**bit**|1 = Parameter hat einen Standardwert.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwaltet nur Standardwerte für CLR-Objekte in dieser Katalogsicht; aus diesem Grund müssen diese Spalte immer der Wert 0 für [!INCLUDE[tsql](../../includes/tsql-md.md)] Objekte. Zum Anzeigen des Standardwert eines Parameters in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Objekt, das Abfragen der **Definition** Spalte die [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht angezeigt werden soll, oder verwenden Sie die [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)-Systemfunktion.|  
|**is_xml_document**|**bit**|1 = Der Inhalt ist ein vollständiges XML-Dokument.<br /><br /> 0 = Inhalt ist ein Dokumentfragment, oder der Datentyp der Spalte ist nicht **xml**.|  
|**Standardwert**|**sql_variant**|Wenn **Has_default_value** 1, ist der Wert dieser Spalte ist der Wert des Standards für den Parameter ist, andernfalls NULL.|  
|**xml_collection_id**|**int**|Die ID der XML-Schemaauflistung, die zur Überprüfung des Parameters verwendet wird.<br /><br /> Ungleich NULL, wenn der Datentyp des Parameters ist **Xml** und XML typisiert ist.<br /><br /> 0 = Es ist keine XML-Schemaauflistung vorhanden, oder der Parameter ist nicht XML.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [Sys. system_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
