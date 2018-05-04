---
title: Check_constraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- CHECK_CONSTRAINTS
- CHECK_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK_CONSTRAINTS view
- INFORMATION_SCHEMA.CHECK_CONSTRAINTS view
ms.assetid: e9577fd2-c349-4dff-874c-9e57d2e5a3ec
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 186e0dffb769eb36354601c35c04a89a67fb9a3b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="checkconstraints-transact-sql"></a>CHECK_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jede CHECK-Einschränkung in der aktuellen Datenbank zurück. Diese Informationsschemasicht gibt Informationen zu den Objekten zurück, für die der aktuelle Benutzer Berechtigungen besitzt.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA. *** View_name*.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**Nvarchar (** 128 **)**|Einschränkungsqualifizierer|  
|**CONSTRAINT_SCHEMA**|**Nvarchar (** 128 **)**|Name des Schemas, zu dem die Einschränkung gehört.<br /><br /> **\*\* Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**CONSTRAINT_NAME**|**sysname**|Einschränkungsname|  
|**CHECK_CLAUSE**|**Nvarchar (** 4000 **)**|Tatsächlicher Text der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Definitionsanweisung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
