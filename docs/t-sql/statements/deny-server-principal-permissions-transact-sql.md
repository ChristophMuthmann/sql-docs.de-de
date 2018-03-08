---
title: "Verweigern von Berechtigungen für Serverprinzipal (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/09/2017
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
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 795c7dcc946966859e5d81382df75a4bb646e38d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="deny-server-principal-permissions-transact-sql"></a>DENY (Berechtigungen für Serverprinzipal) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verweigert Berechtigungen, die für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen erteilt wurden.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
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
 Gibt eine Berechtigung an, die für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen verweigert werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 Anmeldung **::** *SQL_Server_login*  
 Gibt an, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung auf dem die Berechtigung verweigert wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 SERVERROLLE **::** *Server_role*  
 Gibt den die Serverrolle an, für die die Berechtigung verweigert wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 UM \<Server_principal >  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen oder die Serverrolle an, denen die Berechtigung erteilt wird.  
  
 UM *SQL_Server_login*  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, für den die Berechtigung verweigert wird.  
  
 *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_Windows_login*  
 Gibt einen aus einem Windows-Anmeldenamen erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_certificate*  
 Gibt einen einem Zertifikat zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_AsymKey*  
 Gibt einen einem asymmetrischen Schlüssel zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *server_role*  
 Gibt den Namen der einer Serverrolle an.  
  
 CASCADE  
 Gibt an, dass die verweigerte Berechtigung auch anderen Prinzipalen verweigert wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde.  
  
 AS *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Verweigern der Berechtigung ableitet.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können nur verweigert werden, wenn master als aktuelle Datenbank verwendet wird.  
  
 Informationen zu Serverberechtigungen steht in den [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht angezeigt. Informationen zu serverprinzipalen finden Sie in der [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt.  
  
 Die DENY-Anweisung schlägt fehl, wenn CASCADE nicht angegeben ist, wenn Sie eine Berechtigung für einem Prinzipal verweigern, die diese Berechtigung mit GRANT OPTION erteilt wurde.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen und Serverrollen sind sicherungsfähige Elemente auf Serverebene. Die spezifischsten und restriktivsten Berechtigungen, die für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen oder eine Serverrolle verweigert werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
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
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. Verweigern der IMPERSONATE-Berechtigung für einen Anmeldenamen  
 Im folgenden Beispiel wird verweigert `IMPERSONATE` -Berechtigung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung `WanidaBenshoof` zu einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung aus der Windows-Benutzer erstellt `AdvWorks\YoonM`.  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. Verweigern der VIEW DEFINITION-Berechtigung mit CASCADE  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `EricKurjan` dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `RMeyyappan` verweigert. Mit der `CASCADE`-Option wird angegeben, dass die `VIEW DEFINITION`-Berechtigung für `EricKurjan` ebenfalls für die Prinzipale verweigert wird, denen diese Berechtigung von `RMeyyappan` erteilt wurde.  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. Verweigern der VIEW DEFINITION-Berechtigung für eine Serverrolle  
 Im folgenden Beispiel wird `VIEW DEFINITION` für die Serverrolle `Sales` in der Serverrolle `Auditors` verweigert.  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Gespeicherte Sicherheitsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
