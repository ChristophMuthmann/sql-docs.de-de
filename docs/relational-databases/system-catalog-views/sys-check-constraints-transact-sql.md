---
title: Sys. check_constraints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs: TSQL
helpviewer_keywords: sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 99edd7d87c774d1f400c4fe060c1e28543d6311a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syscheckconstraints-transact-sql"></a>sys.check_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes Objekt, das eine CHECK-Einschränkung mit **sys.objects.type** = "C".  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<Von sys.objects geerbte Spalten >**||Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|Die CHECK-Einschränkung ist deaktiviert.|  
|**is_not_for_replication**|**bit**|Die CHECK-Einschränkung wurde mit der Option NOT FOR REPLICATION erstellt.|  
|**Sys. check_constraints**|**bit**|Die CHECK-Einschränkung wurde nicht vom System für alle Zeilen überprüft.|  
|**parent_column_id**|**int**|0 gibt eine CHECK-Einschränkung auf Tabellenebene an.<br /><br /> Ein Wert ungleich 0 gibt an, dass es sich um eine CHECK-Einschränkung auf Spaltenebene handelt, die für die Spalte mit dem angegebenen ID-Wert definiert ist.|  
|**Definition**|**nvarchar(max)**|Ein SQL-Ausdruck, der die CHECK-Einschränkung definiert.|  
|**uses_database_collation**|**bit**|1 = Die Einschränkungsdefinition hängt hinsichtlich einer richtigen Auswertung von der Standardsortierung der Datenbank ab, andernfalls 0. Durch diese Abhängigkeit wird verhindert, dass die Standardsortierung der Datenbank geändert wird.|  
|**is_system_named**|**bit**|1 = Der Name wurde vom System generiert.<br /><br /> 0 = Der Name wurde vom Benutzer angegeben.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
