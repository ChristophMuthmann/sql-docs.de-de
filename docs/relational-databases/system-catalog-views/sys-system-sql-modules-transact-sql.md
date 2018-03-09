---
title: Sys. system_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- system_sql_modules_TSQL
- sys.system_sql_modules
- sys.system_sql_modules_TSQL
- system_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_sql_modules catalog view
ms.assetid: ad3548bc-4780-4821-b962-b421d52daed9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66917b2a30649119ee7921f4343d79765efbb8b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syssystemsqlmodules-transact-sql"></a>sys.system_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile pro Systemobjekt zurück, das ein in der SQL-Sprache definiertes Modul enthält. Systemobjekten vom Typ FN, IF, P, PC, TF, V ist ein SQL-Modul zugeordnet. Um das enthaltende Objekt zu identifizieren, können Sie diese Ansicht verknüpfen [system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die Objekt-ID des enthaltenden Objekts, die innerhalb einer Datenbank eindeutig ist.|  
|**Definition**|**nvarchar(max)**|Der SQL-Text, der dieses Modul definiert.|  
|**uses_ansi_nulls**|**bit**|1 = Beim Erstellen des Moduls war die Datenbankoption SET ANSI_NULLS auf ON festgelegt.<br /><br /> Gibt immer 1 zurück.|  
|**uses_quoted_identifier**|**bit**|1 = Das Modul wurde mit SET QUOTED_IDENTIFIER ON erstellt.<br /><br /> Gibt immer 1 zurück.|  
|**is_schema_bound**|**bit**|0 = Das Modul wurde nicht mit der Option SCHEMABINDING erstellt.<br /><br /> Es wird immer 0 zurückgegeben.|  
|**uses_database_collation**|**bit**|0 = Das Modul hängt nicht von der Standardsortierung der Datenbank ab.<br /><br /> Es wird immer 0 zurückgegeben.|  
|**is_recompiled**|**bit**|0 = Die Prozedur wurde nicht mit der Option WITH RECOMPILE erstellt.<br /><br /> Es wird immer 0 zurückgegeben.|  
|**null_on_null_input**|**bit**|0 = Das Modul wurde nicht so erstellt, dass auf eine NULL-Eingabe eine NULL-Ausgabe folgt.<br /><br /> Es wird immer 0 zurückgegeben.|  
|**execute_as_principal_id**|**int**|Gibt immer NULL zurück|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys. all_sql_modules &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
