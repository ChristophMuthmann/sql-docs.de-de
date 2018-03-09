---
title: SICHTEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fdfae119d9ed1c214c745de30f019588f47e1a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für Sichten zurück, auf die der aktuelle Benutzer in der aktuellen Datenbank zugreifen kann.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA.** *View_name*.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**"TABLE_CATALOG"**|**Nvarchar (**128**)**|Sichtqualifizierer|  
|**TABLE_SCHEMA**|**Nvarchar (**128**)**|Der Name des Schemas, das die Sicht enthält.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**TABELLENNAME**|**Nvarchar (**128**)**|Ansichtsname.|  
|**VIEW_DEFINITION**|**Nvarchar (**4000**)**|Wenn die Länge der Definition überschreitet **Nvarchar (**4000**)**, ist diese Spalte NULL. Andernfalls enthält diese Spalte den Text der Sichtdefinition.|  
|**CHECK_OPTION**|**Varchar (**7**)**|WITH CHECK OPTION-Typ. Wenn die Originalsicht mit WITH CHECK OPTION erstellt wurde, wird CASCADE zurückgegeben. Andernfalls wird NONE zurückgegeben.|  
|**IS_UPDATABLE**|**Varchar (**2**)**|Gibt an, ob die Sicht aktualisierbar ist. Es wird immer NO zurückgegeben.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
