---
title: Heben Sie die Serverberechtigungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], servers
- REVOKE statement, server permissions
- servers [SQL Server], permissions
ms.assetid: 7b9a56b3-face-452e-a655-147dac306ba1
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e77a5ec0e9e17ca414076035f7361ba21dde5e9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-server-permissions-transact-sql"></a>REVOKE (Serverberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt die GRANT- und DENY-Berechtigungen auf Serverebene.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    { TO | FROM } <grantee_principal> [ ,...n ]  
        [ CASCADE ]  
    [ AS <grantor_principal> ]   
  
<grantee_principal> ::= SQL_Server_login   
        | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
  
<grantor_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für einen Server erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 {UM | FROM} \<Grantee_principal > Gibt den Prinzipal, von dem die Berechtigung aufgehoben wird.  
  
 AS \<Grantor_principal > Gibt den Prinzipal an, aus dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet.  
  
 GRANT OPTION FOR  
 Gibt an, dass das Recht zum Erteilen der angegebenen Berechtigung für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 *SQL_Server_login*  
 Gibt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung.  
  
 *SQL_Server_login_mapped_to_Windows_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, der einem Windows-Anmeldenamen zugeordnet ist.  
  
 *SQL_Server_login_mapped_to_Windows_group*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, der einer Windows-Gruppe zugeordnet ist.  
  
 *SQL_Server_login_mapped_to_certificate*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, der einem Zertifikat zugeordnet ist.  
  
 *SQL_Server_login_mapped_to_asymmetric_key*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, der einem asymmetrischen Schlüssel zugeordnet ist.  
  
 *server_role*  
 Gibt eine benutzerdefinierte Serverrolle an.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können nur aufgehoben werden, wenn master als aktuelle Datenbank verwendet wird.  
  
 Mit REVOKE wird sowohl die GRANT- als auch die DENY-Berechtigung entfernt.  
  
 Verwenden Sie REVOKE GRANT OPTION FOR, um das Recht, die angegebene Berechtigung anderen Prinzipalen zu erteilen, ebenfalls aufzuheben. Falls der Prinzipal die Berechtigung mit dem Recht zum Erteilen der Berechtigung an andere Prinzipale besitzt, wird das Recht zum Erteilen der Berechtigung aufgehoben, die Berechtigung selbst wird jedoch nicht aufgehoben. Falls der Prinzipal die angegebene Berechtigung jedoch ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 Informationen zu Serverberechtigungen kann angezeigt werden, der [Sys. server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen in angezeigt werden können die [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt. Informationen zur Mitgliedschaft von Serverrollen kann angezeigt werden, der [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) -Katalogsicht angezeigt.  
  
 Ein Server stellt die höchste Ebene der Berechtigungshierarchie dar. Die spezifischsten und restriktivsten Berechtigungen, die für einen Server aufgehoben werden können, sind in der folgenden Tabelle aufgeführt.  
  
|Serverberechtigung|Impliziert durch die Serverberechtigung|  
|-----------------------|----------------------------------|  
|ADMINISTER BULK OPERATIONS|CONTROL SERVER|  
|ALTER ANY AVAILABILITY GROUP<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER ANY CONNECTION|CONTROL SERVER|  
|ALTER ANY CREDENTIAL|CONTROL SERVER|  
|ALTER ANY DATABASE|CONTROL SERVER|  
|ALTER ANY ENDPOINT|CONTROL SERVER|  
|ALTER ANY EVENT NOTIFICATION|CONTROL SERVER|  
|ALTER ANY EVENT SESSION|CONTROL SERVER|  
|ALTER ANY LINKED SERVER|CONTROL SERVER|  
|ALTER ANY LOGIN|CONTROL SERVER|  
|ALTER ANY SERVER AUDIT|CONTROL SERVER|  
|ALTER ANY SERVER ROLE<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER RESOURCES|CONTROL SERVER|  
|ALTER SERVER STATE|CONTROL SERVER|  
|ALTER SETTINGS|CONTROL SERVER|  
|ALTER TRACE|CONTROL SERVER|  
|AUTHENTICATE SERVER|CONTROL SERVER|  
|CONNECT ANY DATABASE<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|CONNECT SQL|CONTROL SERVER|  
|CONTROL SERVER|CONTROL SERVER|  
|CREATE ANY DATABASE|ALTER ANY DATABASE|  
|CREATE AVAILABILITY GROUP<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY AVAILABILITY GROUP|  
|CREATE DDL EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|CREATE ENDPOINT|ALTER ANY ENDPOINT|  
|CREATE SERVER ROLE<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY SERVER ROLE|  
|CREATE TRACE EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|EXTERNAL ACCESS ASSEMBLY|CONTROL SERVER|  
|IMPERSONATE ANY LOGIN<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SELECT ALL USER SECURABLES<br /><br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SHUTDOWN|CONTROL SERVER|  
|UNSAFE ASSEMBLY|CONTROL SERVER|  
|VIEW ANY DATABASE|VIEW ANY DEFINITION|  
|VIEW ANY DEFINITION|CONTROL SERVER|  
|VIEW SERVER STATE|ALTER SERVER STATE|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung oder die Mitgliedschaft in der festen Serverrolle sysadmin.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-revoking-a-permission-from-a-login"></a>A. Aufheben einer Berechtigung für einen Anmeldenamen  
 Im folgenden Beispiel wird die `VIEW SERVER STATE`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `WanidaBenshoof` aufgehoben.  
  
```  
USE master;  
REVOKE VIEW SERVER STATE FROM WanidaBenshoof;  
GO  
```  
  
### <a name="b-revoking-the-with-grant-option"></a>B. Aufheben der WITH GRANT OPTION  
 Im folgenden Beispiel wird das Recht zum Erteilen der `CONNECT SQL`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `JanethEsteves` aufgehoben.  
  
```  
USE master;  
REVOKE GRANT OPTION FOR CONNECT SQL FROM JanethEsteves;  
GO  
```  
  
 Der Anmeldename besitzt weiterhin die CONNECT SQL-Berechtigung, er kann diese Berechtigung jedoch anderen Prinzipalen nicht mehr erteilen.  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Verweigern von Serverberechtigungen für &#40; Transact-SQL &#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [Heben Sie die Serverberechtigungen (Transact-SQL)](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  


