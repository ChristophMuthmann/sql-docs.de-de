---
title: DROP SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c493ed6556bde690f6b4a9ec6b46aeb3ceb59ae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-server-role-transact-sql"></a>DROP SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  Entfernt eine benutzerdefinierte Serverrolle.  
  
 Benutzerdefinierte Serverrollen sind neu in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP SERVER ROLE role_name  
```  
  
## <a name="arguments"></a>Argumente  
 *Rollenname*  
 Gibt die benutzerdefinierte Serverrolle an, die vom Server gelöscht werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Benutzerdefinierte Serverrollen, die sicherungsfähige Elemente besitze, können nicht vom Server gelöscht werden. Wenn eine benutzerdefinierte Serverrolle mit sicherungsfähigen Elementen gelöscht werden soll, müssen Sie zunächst den Besitz der sicherungsfähigen Elemente übertragen oder sie aus der Datenbank löschen.  
  
 Benutzerdefinierte Serverrollen, die über Elemente verfügen, können nicht gelöscht werden. Um eine benutzerdefinierte Serverrolle zu löschen, die als Member enthält, müssen Sie zuerst Mitglieder der Rolle entfernen, mit [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Feste Serverrollen können nicht entfernt werden.  
  
 Sie können Informationen zur Rollenmitgliedschaft anzeigen, indem Sie Abfragen der [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) -Katalogsicht angezeigt.  
  
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
 Verwenden Sie zum Anzeigen der Rollenmitgliedschaft der **-Serverrolle (Mitglieder**) auf der Seite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder führen Sie folgende Abfrage:  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [Erstellen Sie die Rolle "" &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  

