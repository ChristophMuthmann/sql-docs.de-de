---
title: ALTER SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7ce5b5223f5c755c89cb3e105ceb6517087d699f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

Ändert die Mitgliedschaft einer Serverrolle oder ändert Namen einer benutzerdefinierten Serverrolle. Feste Serverrollen können nicht umbenannt werden.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>Argumente  
*server_role_name*  
Der Name der zu ändernden Serverrolle.  
  
ADD MEMBER *Server_principal*  
Fügt der Serverrolle den angegebenen Serverprinzipal hinzu. *Server_principal* kann ein Anmeldename oder eine benutzerdefinierte Serverrolle sein. *Server_principal* nicht mit einer festen Serverrolle, Datenbankrolle oder sa.  
  
DROP MEMBER *Server_principal*  
Entfernt den angegebenen Serverprinzipal aus der Serverrolle. *Server_principal* kann ein Anmeldename oder eine benutzerdefinierte Serverrolle sein. *Server_principal* nicht mit einer festen Serverrolle, Datenbankrolle oder sa.  
  
MIT dem Namen  **=**  *New_server_role_name*  
Gibt den neuen Namen der benutzerdefinierten Serverrolle an. Dieser Name darf nicht bereits auf dem Server vorhanden sein.  
  
## <a name="remarks"></a>Hinweise  
Durch das Ändern des Namens einer benutzerdefinierten Serverrolle werden die ID-Nummer, der Besitzer oder Berechtigungen der Rolle nicht geändert.  
  
Zum Ändern der Mitgliedschaft in Datenbankrolle `ALTER SERVER ROLE` Sp_addsrvrolemember und Sp_dropsrvrolemember ersetzt. Diese gespeicherten Prozeduren sind veraltet.  
  
Sie können Serverrollen anzeigen, indem Sie die `sys.server_role_members`- Katalogsicht und die `sys.server_principals`-Katalogsicht abfragen.  
  
Um den Besitzer einer benutzerdefinierten Serverrolle zu ändern, verwenden [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert `ALTER ANY SERVER ROLE` Berechtigung auf dem Server zum Ändern des Namens einer benutzerdefinierten Serverrolle.  
  
**Feste Serverrollen**  
  
Wenn Sie einer festen Serverrolle ein Mitglied hinzufügen möchten, müssen Sie Mitglied dieser festen Serverrolle oder Mitglied der festen Serverrolle `sysadmin` sein.  
  
> [!NOTE]  
>  Die `CONTROL SERVER` und `ALTER ANY SERVER ROLE` Berechtigungen sind nicht ausreichend auszuführende `ALTER SERVER ROLE` für eine feste Serverrolle und `ALTER` Berechtigung kann auf einer festen Serverrolle nicht gewährt werden.  
  
**Benutzerdefinierte Serverrollen**  
  
Um eine benutzerdefinierte Serverrolle ein Mitglied hinzuzufügen, muss ein Mitglied der `sysadmin` festen Serverrolle oder haben `CONTROL SERVER` oder `ALTER ANY SERVER ROLE` Berechtigung. Oder Sie müssen über die `ALTER` -Berechtigung für diese Rolle.  
  
> [!NOTE]  
>  Anders als bei festen Serverrollen verfügen Mitglieder einer benutzerdefinierten Serverrolle nicht unbedingt über die Berechtigung, dieser Rolle Mitglieder hinzuzufügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-name-of-a-server-role"></a>A. Ändern des Namens einer Serverrolle  
Im folgenden Beispiel wird die Serverrolle `Product` erstellt, und anschließend wird der Name der Serverrolle in `Production` geändert.  
  
```  
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>B. Hinzufügen eines Domänenkontos zu einer Serverrolle  
Im folgenden Beispiel wird ein Domänenkonto mit dem Namen `adventure-works\roberto0` der benutzerdefinierten Serverrolle mit dem Namen `Production`.  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>C. Hinzufügen einer SQL Server-Anmeldung zu einer Serverrolle  
Im folgenden Beispiel wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename `Ted` auf die `diskadmin` festen Serverrolle "".  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>D. Entfernen eines Domänenkontos aus einer Serverrolle  
Im folgenden Beispiel wird ein Domänenkonto mit dem Namen `adventure-works\roberto0` aus der benutzerdefinierten Serverrolle mit dem Namen `Production`.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>E. Entfernen einer SQL Server-Anmeldung aus einer Serverrolle  
Im folgenden Beispiel wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung `Ted` aus der `diskadmin` festen Serverrolle "".  
  
```  
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>F. Gewähren der Berechtigung zum Hinzufügen von Anmeldungen zu einer benutzerdefinierten Serverrolle für eine Anmeldung  
Im folgenden Beispiel wird `Ted` die Berechtigung erteilt, der benutzerdefinierten Serverrolle `Production` weitere Anmeldungen hinzuzufügen.  
  
```  
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>G. Anzeigen der Rollenmitgliedschaft  
Verwenden Sie zum Anzeigen der Rollenmitgliedschaft der **-Serverrolle (Mitglieder)** auf der Seite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder führen Sie folgende Abfrage:  
  
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
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>H. Grundlegende Syntax  
Im folgenden Beispiel wird die Anmeldung `Anna` auf die `LargeRC` -Serverrolle.  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>I. Entfernen Sie einen Anmeldenamen aus einer Ressourcenklasse.  
Das folgende Beispiel löscht Annas Mitgliedschaft der `LargeRC` -Serverrolle.  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen Sie SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[DROP SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[Erstellen Sie die Rolle "" &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[DROP ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[Sys. server_role_members &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
