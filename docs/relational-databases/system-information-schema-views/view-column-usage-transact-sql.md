---
title: VIEW_COLUMN_USAGE-Sicht (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VIEW_COLUMN_USAGE
- VIEW_COLUMN_USAGE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.VIEW_COLUMN_USAGE view
- VIEW_COLUMN_USAGE view
ms.assetid: fc0b3608-a7e8-4532-8215-32235d6670f1
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5be4a28a371f71be51f1661d57ddbe54af6cac2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="viewcolumnusage-transact-sql"></a>VIEW_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jede Spalte in der aktuellen Datenbank zurück, die in einer Sichtdefinition verwendet wird. Diese Informationsschemasicht gibt Informationen zu den Objekten zurück, für die der aktuelle Benutzer Berechtigungen besitzt.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA.** *View_name*.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**Nvarchar (**128**)**|Sichtqualifizierer|  
|**VIEW_SCHEMA**|**Nvarchar (**128**)**|Der Name des Schemas, das die Sicht enthält.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**VIEW_NAME**|**sysname**|Ansichtsname.|  
|**"TABLE_CATALOG"**|**Nvarchar (**128**)**|Tabellenqualifizierer|  
|**TABLE_SCHEMA**|**Nvarchar (**128**)**|Der Name des Schemas, das die Tabelle enthält.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**TABELLENNAME**|**sysname**|Basistabelle.|  
|**SPALTENNAME**|**sysname**|Spaltenname.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys. sql_dependencies &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
