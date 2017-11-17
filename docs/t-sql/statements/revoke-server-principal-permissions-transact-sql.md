---
title: "REVOKE-Berechtigungen für Serverprinzipal (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, impersonation
- permissions [SQL Server], impersonation
- permissions [SQL Server], logins
- impersonate [SQL Server], revoking
- logins [SQL Server], revoking
- REVOKE statement, logins
ms.assetid: 75409024-f150-4326-af16-9d60e900df18
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13dca8052ad8bc74491136c941677606ccecbe3c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-server-principal-permissions-transact-sql"></a>REVOKE (Berechtigungen für Serverprinzipal) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hebt die Berechtigungen auf, die für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen erteilt oder verweigert wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey     
    | server_role  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen aufgehoben werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 Anmeldung **::** *SQL_Server_login*  
 Gibt an, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung auf dem die Berechtigung aufgehoben wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 SERVERROLLE **::** *Server_role*  
 Gibt die Serverrolle an, für die die Berechtigung aufgehoben wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 {AUS | AN} \<Server_principal > Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldename oder eine Serverrolle, die von dem die Berechtigung aufgehoben wird.  
  
 *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_Windows_login*  
 Gibt einen aus einem Windows-Anmeldenamen erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_certificate*  
 Gibt einen einem Zertifikat zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_AsymKey*  
 Gibt einen einem asymmetrischen Schlüssel zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *server_role*  
 Gibt den Namen einer benutzerdefinierten Serverrolle an.  
  
 GRANT OPTION  
 Gibt an, dass das Recht zum Erteilen der angegebenen Berechtigung für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *SQL_Server_login*  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet.  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen und Serverrollen sind sicherungsfähige Elemente auf Serverebene. Die spezifischsten und restriktivsten Berechtigungen, die für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen oder für eine Serverrolle aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die in diesen implizit enthalten sind.  
  
|SQL Server-Anmeldename oder Serverrollenberechtigung|Impliziert durch SQL Server-Anmeldename oder Serverrollenberechtigung|Impliziert durch die Serverberechtigung|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert bei Anmeldenamen die CONTROL-Berechtigung bei der Anmeldung oder die ALTER ANY LOGIN-Berechtigung für den Server.  
  
 Erfordert bei Serverrollen die CONTROL-Berechtigung für die Serverrolle oder die ALTER ANY SERVER ROLE-Berechtigung für den Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-revoking-impersonate-permission-on-a-login"></a>A. Aufheben der IMPERSONATE-Berechtigung für einen Anmeldenamen  
 Das folgende Beispiel hebt `IMPERSONATE` -Berechtigung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung `WanidaBenshoof` aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung aus der Windows-Benutzer erstellt `AdvWorks\YoonM`.  
  
```  
USE master;  
REVOKE IMPERSONATE ON LOGIN::WanidaBenshoof FROM [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-with-cascade"></a>B. Aufheben der VIEW DEFINITION-Berechtigung mit CASCADE OPTION  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `EricKurjan` für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `RMeyyappan` aufgehoben. Mit der `CASCADE`-Option wird angegeben, dass die `VIEW DEFINITION`-Berechtigung für `EricKurjan` ebenfalls für die Prinzipale aufgehoben wird, denen diese Berechtigung von `RMeyyappan` erteilt wurde.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON LOGIN::EricKurjan FROM RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-revoking-view-definition-permission-on-a-server-role"></a>C. Aufheben der VIEW DEFINITION-Berechtigung für eine Serverrolle  
 Im folgenden Beispiel wird `VIEW DEFINITION` für die Serverrolle `Sales` der Serverrolle `Auditors` aufgehoben.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [DENY (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Gespeicherte Sicherheitsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  


