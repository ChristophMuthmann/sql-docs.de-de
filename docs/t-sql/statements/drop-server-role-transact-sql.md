---
title: DROP SERVER ROLE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP SERVER ROLE
- DROP_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, DROP
- DROP SERVER ROLE statement
ms.assetid: a2a1e6e6-e40c-4d6a-81be-d197b80bf226
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 289407f382e5872179e33984a34eb9dbd523e9ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-server-role-transact-sql"></a>DROP SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  Entfernt eine benutzerdefinierte Serverrolle.  
  
 Benutzerdefinierte Serverrollen sind neu in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP SERVER ROLE role_name  
```  
  
## <a name="arguments"></a>Argumente  
 *role_name*  
 Gibt die benutzerdefinierte Serverrolle an, die vom Server gelöscht werden soll.  
  
## <a name="remarks"></a>Remarks  
 Benutzerdefinierte Serverrollen, die sicherungsfähige Elemente besitze, können nicht vom Server gelöscht werden. Wenn eine benutzerdefinierte Serverrolle mit sicherungsfähigen Elementen gelöscht werden soll, müssen Sie zunächst den Besitz der sicherungsfähigen Elemente übertragen oder sie aus der Datenbank löschen.  
  
 Benutzerdefinierte Serverrollen, die über Elemente verfügen, können nicht gelöscht werden. Um eine benutzerdefinierte Serverrolle mit Mitgliedern zu löschen, müssen Sie zuerst Mitglieder der Rolle mit [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) entfernen.  
  
 Feste Serverrollen können nicht entfernt werden.  
  
 Sie können die [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)-Katalogsicht abfragen, um Informationen zu Rollenmitgliedschaften anzuzeigen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Serverrolle oder die ALTER ANY SERVER ROLE-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-to-drop-a-server-role"></a>A. Löschen einer Serverrolle  
 Im folgenden Beispiel wird die Serverrolle `purchasing` gelöscht.  
  
```  
DROP SERVER ROLE purchasing;  
GO  
```  
  
### <a name="b-to-view-role-membership"></a>B. Anzeigen der Rollenmitgliedschaft  
 Um die Rollenmitgliedschaft anzuzeigen, verwenden Sie die Seite **Serverrolle (Mitglieder)** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], oder führen Sie die folgende Abfrage aus:  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
### <a name="c-to-view-role-membership"></a>C. Anzeigen der Rollenmitgliedschaft  
 Um zu ermitteln, ob eine Serverrolle eine andere Serverrolle besitzt, führen Sie die folgende Abfrage aus:  
  
```  
SELECT SP1.name AS RoleOwner, SP2.name AS Server_Role  
FROM sys.server_principals AS SP1  
JOIN sys.server_principals AS SP2  
    ON SP1.principal_id = SP2.owning_principal_id   
ORDER BY SP1.name ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
