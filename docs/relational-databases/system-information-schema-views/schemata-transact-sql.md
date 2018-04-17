---
title: SCHEMAS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-information-schema-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e814026040e37b8467407ddca9f73c57438fa4bd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jedes Schema in der aktuellen Datenbank zurück. Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA. *** View_name*. Zum Abrufen von Informationen zu allen Datenbanken in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Abfrage der [sys.databases &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|Name der aktuellen Datenbank|  
|**SCHEMA_NAME**|**Nvarchar (**128**)**|Gibt den Namen des Schemas zurück.|  
|**SCHEMA_OWNER**|**Nvarchar (**128**)**|Name des Schemabesitzers.<br /><br /> **\*\* Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit, das Schema eines Objekts zu finden, besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**Varchar (**6**)**|Gibt immer NULL zurück.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**Varchar (**3**)**|Gibt immer NULL zurück.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|Gibt den Namen des Standardzeichensatzes zurück.|  

**Beispiel**  
Im folgenden Beispiel werden Informationen zu den Schemas in der master-Datenbank zurückgegeben:  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [Sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
