---
title: Sys.Types (Transact-SQL) | Microsoft Docs
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
- types
- types_TSQL
- sys.types_TSQL
- sys.types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.types catalog view
- table-valued parameters,sys.types
ms.assetid: a5dbc842-71a0-4f62-b5e0-f560a99b7f8c
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 17230214cbcbe4061de77ec01fbf848d3826914c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="systypes-transact-sql"></a>sys.types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jeden Systemtyp und jeden benutzerdefinierten Typ.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name des Typs. Ist innerhalb des Schemas eindeutig.|  
|**system_type_id**|**tinyint**|Die ID des internen Systemtyps des Typs|  
|**user_type_id**|**int**|Die ID des Typs. Ist in der Datenbank eindeutig. Für Systemdatentypen gilt **user_type_id** = **system_type_id**.|  
|**schema_id**|**int**|Die ID des Schemas, zu dem der Typ gehört.|  
|**principal_id**|**int**|Die ID des einzelnen Besitzers, falls sie sich vom Schemabesitzer unterscheidet. Standardmäßig gehören Objekte mit Schemabereich dem Schemabesitzer. Mit der ALTER AUTHORIZATION-Anweisung kann jedoch ein anderer Besitzer angegeben werden.<br /><br /> Hat den Wert NULL, falls kein alternativer individueller Besitzer angegeben ist.|  
|**max_length**|**smallint**|Maximale Länge (in Bytes) für den Typ.<br /><br /> -1 = Spaltendatentyp ist **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, oder **Xml**.<br /><br /> Für **Text** Spalten, die **Max_length** Wert ist 16.|  
|**precision**|**tinyint**|Die maximale Genauigkeit des Typs, wenn es sich um einen zahlenbasierten Typ handelt; andernfalls 0.|  
|**scale**|**tinyint**|Die maximalen Dezimalstellen des Typs, wenn es sich um einen zahlenbasierten Typ handelt; andernfalls 0.|  
|**collation_name**|**sysname**|Der Name der Sortierung des Typs wird jedoch zeichenbasierte; andere Wise NULL.|  
|**is_nullable**|**bit**|Der Typ lässt NULL-Werte zu.|  
|**is_user_defined**|**bit**|1 = Benutzerdefinierter Typ.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp.|  
|**is_assembly_type**|**bit**|1 = Die Implementierung des Typs wird in einer CLR-Assembly definiert.<br /><br /> 0 = Der Typ basiert auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp.|  
|**default_object_id**|**int**|ID des eigenständigen Standards, die in den Typ gebunden ist, mithilfe von [Sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md).<br /><br /> 0 = Kein Standard vorhanden.|  
|**rule_object_id**|**int**|ID der eigenständigen Regel, die in den Typ gebunden ist, mithilfe von [Sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md).<br /><br /> 0 = Keine Regel vorhanden.|  
|**is_table_type**|**bit**|Gibt an, dass der Typ eine Tabelle ist.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Skalartypen &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
