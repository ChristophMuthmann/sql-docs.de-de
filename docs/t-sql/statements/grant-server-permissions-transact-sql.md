---
title: "Gewähren von Server-Berechtigungen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- GRANT statement, servers
- permissions [SQL Server], servers
- servers [SQL Server], permissions
- granting permissions [SQL Server], servers
ms.assetid: 7e880a5a-3bdc-491f-a167-7a9ed338be7f
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 424bb9cf8db72c399a733d1e4ffe3eb55bd14427
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-server-permissions-transact-sql"></a>GRANT (Serverberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für einen Server. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GRANT permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ] [ WITH GRANT OPTION ]  
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
  
 UM \<Grantee_principal > Gibt den Prinzipal an, die die Berechtigung erteilt wird.  
  
 AS \<Grantor_principal > Gibt den Prinzipal an, aus dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
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
 Berechtigungen im Serverbereich können nur erteilt werden, wenn master als aktuelle Datenbank verwendet wird.  
  
 Informationen zu Serverberechtigungen kann angezeigt werden, der [Sys. server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen in angezeigt werden können die [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt. Informationen zur Mitgliedschaft von Serverrollen kann Viewd in werden die [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) -Katalogsicht angezeigt.  
  
 Ein Server stellt die höchste Ebene der Berechtigungshierarchie dar. Die spezifischsten und restriktivsten Berechtigungen, die für einen Server erteilt werden können, sind in der folgenden Tabelle aufgeführt.  
  
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
  
## <a name="remarks"></a>Hinweise  
 Die folgenden drei Serverberechtigungen wurden in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hinzugefügt.  
  
 **Verbinden Sie eine beliebige Datenbank** Berechtigung  
 GRANT **CONNECT ANY DATABASE** eine Anmeldung, die eine Verbindung herstellen müssen, um alle derzeit vorhandenen Datenbanken und alle neuen Datenbanken, die möglicherweise in Zukunft erstellt werden. Gewährt keine Berechtigung für Datenbanken außer der Berechtigung zum Herstellen der Verbindung. Kombinieren mit **SELECT ALL USER SECURABLES** oder **VIEW SERVER STATE** ermöglichen einem Überwachungsprozess das Anzeigen aller Daten oder datenbankstatusangaben für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Identität einer beliebigen Anmeldung** Berechtigung  
 Wenn die Berechtigung erteilt wird, kann ein Prozess der mittleren Ebene beim Herstellen der Verbindung mit Datenbanken die Identität des Kontos von Clients annehmen, die eine Verbindung mit ihm herstellen. Wenn die Berechtigung verweigert wird, kann verhindert werden, dass ein Anmeldename mit hohen Privilegien die Identität anderer Anmeldenamen annimmt. Angenommen, eine Anmeldung mit **CONTROL SERVER** Berechtigung kann verhindert werden Identität anderer Anmeldenamen annimmt.  
  
 **Wählen Sie alle sicherungsfähigen BENUTZERELEMENTE** Berechtigung  
 Wenn sie erteilt wird, kann ein Anmeldename, z. B. ein Auditor, Daten in allen Datenbanken anzeigen, mit denen der Benutzer eine Verbindung herstellen kann. Wenn verweigert wird, verhindert den Zugriff auf Objekte, sofern werden die **Sys** Schema.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) muss entweder über die Berechtigung selbst mit GRANT OPTION oder über eine höhere Berechtigung verfügen, in der die erteilte Berechtigung impliziert ist. Mitglieder der festen Serverrolle sysadmin können beliebige Berechtigungen erteilen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-granting-a-permission-to-a-login"></a>A. Gewähren einer Berechtigung für einen Anmeldenamen  
 Im folgenden Beispiel wird die `CONTROL SERVER`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `TerryEminhizer` erteilt.  
  
```  
USE master;  
GRANT CONTROL SERVER TO TerryEminhizer;  
GO  
```  
  
### <a name="b-granting-a-permission-that-has-grant-permission"></a>B. Gewähren einer Berechtigung, die über die GRANT-Berechtigung verfügt  
 Im folgenden Beispiel wird die `ALTER ANY EVENT NOTIFICATION`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `JanethEsteves` mit dem Recht zum Erteilen der Berechtigung für andere Anmeldenamen erteilt.  
  
```  
USE master;  
GRANT ALTER ANY EVENT NOTIFICATION TO JanethEsteves WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-a-permission-to-a-server-role"></a>C. Gewähren einer Berechtigung für eine Serverrolle  
 Im folgenden Beispiel werden die beiden Serverrollen `ITDevAdmin` und `ITDevelopers` erstellt. Die `ALTER ANY DATABASE`-Berechtigung wird der benutzerdefinierten `ITDevAdmin`-Serverrolle mit der `WITH GRANT`-Option erteilt, sodass die `ITDevAdmin`-Berechtigung von der `ALTER ANY DATABASE`-Serverrolle neu zugewiesen werden kann. Anschließend wird im Beispiel `ITDevelopers` die Berechtigung zur Verwendung der `ALTER ANY DATABASE`-Berechtigung der `ITDevAdmin`-Serverrolle erteilt.  
  
```  
USE master;  
CREATE SERVER ROLE ITDevAdmin ;  
CREATE SERVER ROLE ITDevelopers ;  
GRANT ALTER ANY DATABASE TO ITDevAdmin WITH GRANT OPTION ;  
GRANT ALTER ANY DATABASE TO ITDevelopers AS ITDevAdmin ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Verweigern von Serverberechtigungen für &#40; Transact-SQL &#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [WIDERRUFEN Sie Serverberechtigungen für &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

