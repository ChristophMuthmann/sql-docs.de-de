---
title: Sys.Credentials (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs: TSQL
helpviewer_keywords: sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf03ffcc4dffb40aa53aff24d67e12487f3d069b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt eine Zeile für jeden Teil der Anmeldeinformationen auf Serverebene zurück.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|ID der Anmeldeinformationen. Ist im Server eindeutig.|  
|name|**sysname**|Name der Anmeldeinformationen. Ist im Server eindeutig.|  
|credential_identity|**nvarchar(4000)**|Name der zu verwendenden Identität. In der Regel ist dies ein Windows-Benutzer. Er muss nicht eindeutig sein.|  
|create_date|**datetime**|Der Zeitpunkt, zu dem die Anmeldeinformationen erstellt wurden.|  
|modify_date|**datetime**|Der Zeitpunkt, zu dem die Anmeldeinformationen zuletzt geändert wurden.|  
|target_type|**nvarchar(100)**|Anmeldeinformationstyp. Gibt NULL für herkömmliche Anmeldeinformationen und CRYPTOGRAPHIC PROVIDER für einem Kryptografieanbieter zugeordnete Anmeldeinformationen zurück. Weitere Informationen zu Anbietern Verwaltung externer Schlüssel finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  
|target_id|**int**|ID des Objekts, dem die Anmeldeinformationen zugeordnet werden. Gibt 0 für herkömmliche Anmeldeinformationen und einen Wert ungleich 0 für einem Kryptografieanbieter zugeordnete Anmeldeinformationen zurück. Weitere Informationen zu Anbietern Verwaltung externer Schlüssel finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  

## <a name="remarks"></a>Hinweise  
Auf Datenbankebene-Anmeldeinformationen finden Sie unter [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert entweder `VIEW ANY DEFINITION` Berechtigung oder `ALTER ANY CREDENTIAL` Berechtigung. Darüber hinaus dem Prinzipal nicht verweigert werden muss `VIEW ANY DEFINITION` Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
