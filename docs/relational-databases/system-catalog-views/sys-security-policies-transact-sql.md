---
title: Sys. security_policies (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0221d0a61a8f7207fe1b0a1ab49a0bd59f88396d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syssecuritypolicies-transact-sql"></a>Sys. security_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Sicherheitsrichtlinie in der Datenbank zurück.  
  
|Spaltenname|Datentyp|Description|  
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
  
  
