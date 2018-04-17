---
title: Sys. security_predicates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_PREDICATES
- SECURITY_PREDICATES
- SECURITY_PREDICATES_TSQL
- SYS.SECURITY_PREDICATES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_predicates catalog view
- security_predicates catalog view
ms.assetid: c7a2f28c-98da-463d-8b8a-8e5619e2c6a6
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 51799910d0e240d14b231c0d2c8d97f36cca66d8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssecuritypredicates-transact-sql"></a>Sys. security_predicates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes sicherheitsprädikat in der Datenbank zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Die ID der Sicherheitsrichtlinie, die das Prädikat enthält.|  
|security_predicate_id|**int**|Prädikat-ID innerhalb dieser Richtlinie.|  
|target_object_id|**int**|Die ID des Objekts, an das das Sicherheitsprädikat gebunden ist.|  
|predicate_definition|**nvarchar(max)**|Der vollqualifizierte Name der Funktion, die als Sicherheitsprädikat verwendet wird, einschließlich der Argumente. Beachten Sie, dass die `schema.function` Name möglicherweise normalisiert werden kann (d. h. durch Escapezeichen ersetzt) sowie alle anderen Elemente in den Text aus Gründen der Konsistenz. Beispiel:<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|Der Typ des Prädikats, die durch die Sicherheitsrichtlinie verwendet:<br /><br /> 0 = FILTERPRÄDIKAT<br /><br /> 1 = BLOCK-PRÄDIKAT|  
|predicate_type_desc|**nvarchar(60)**|Der Typ des Prädikats, die durch die Sicherheitsrichtlinie verwendet:<br /><br /> FILTER<br /><br /> BLOCKIEREN|  
|Vorgang|**int**|Der Typ des Vorgangs für das Prädikat angegeben:<br /><br /> NULL = alle anwendbaren Vorgänge<br /><br /> 1 = AFTER INSERT<br /><br /> 2 = AFTER UPDATE<br /><br /> 3 = VOR DEM UPDATE<br /><br /> 4 = VOR DEM LÖSCHEN|  
|operation_desc|**nvarchar(60)**|Der Typ des Vorgangs für das Prädikat angegeben:<br /><br /> NULL<br /><br /> NACH DEM EINFÜGEN<br /><br /> AFTER UPDATE<br /><br /> VOR DEM UPDATE<br /><br /> VOR DEM LÖSCHEN|  
  
## <a name="permissions"></a>Berechtigungen  
 Prinzipale mit den **ALTER ANY SECURITY POLICY** -Berechtigung haben Zugriff auf alle Objekte in dieser Katalogsicht sowie jede Person mit **SICHTDEFINITION** für das Objekt.  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
