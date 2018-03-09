---
title: Sys. security_policies (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e30a903e31ce8ba7951f9756a8fd258375fb8e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syssecuritypolicies-transact-sql"></a>Sys. security_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Sicherheitsrichtlinie in der Datenbank zurück.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Der Name der Sicherheitsrichtlinie, der innerhalb der Datenbank eindeutig ist.|  
|object_id|**int**|Die ID der Sicherheitsrichtlinie.|  
|principal_id|**int**|Die ID des Besitzers der Sicherheitsrichtlinie gemäß der Registrierung in der Datenbank. NULL, wenn der Besitzer über das Schema bestimmt wird.|  
|schema_id|**int**|Die ID des Schemas, in dem sich das Objekt befindet.|  
|parent_object_id|**int**|Die ID des Objekts, zu dem die Richtlinie gehört. Muss den Wert 0 (null) haben.|  
|Typ|**vachar(2)**|Muss **SP**.|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**.|  
|create_date|**datetime**|Das UTC-Datum, an dem die Sicherheitsrichtlinie erstellt wurde.|  
|modify_date|**datetime**|Das UTC-Datum, an dem die Sicherheitsrichtlinie zuletzt geändert wurde.|  
|is_ms_shipped|**bit**|Immer false.|  
|is_enabled|**bit**|Spezifikationsstatus der Sicherheitsrichtlinie:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|is_not_for_replication|**bit**|Die Richtlinie wurde mit der Option NOT FOR REPLICATION erstellt.|  
|uses_database_collation|**bit**|Verwendet dieselbe Sortierung wie die Datenbank.|  
|is_schemabinding_enabled|**bit**|SCHEMABINDING-Status für die Sicherheitsrichtlinie für:<br /><br /> 0 oder NULL = aktiviert<br /><br /> 1 = deaktiviert|  
  
## <a name="permissions"></a>Berechtigungen  
 Prinzipale mit den **ALTER ANY SECURITY POLICY** -Berechtigung haben Zugriff auf alle Objekte in dieser Katalogsicht sowie jede Person mit **SICHTDEFINITION** für das Objekt.  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
