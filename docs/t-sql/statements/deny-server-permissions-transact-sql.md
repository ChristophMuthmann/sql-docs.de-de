---
title: "Verweigern von Serverberechtigungen für (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/09/2017
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
- denying permissions [SQL Server], servers
- servers [SQL Server], permissions
- DENY statement, servers
ms.assetid: 68d6b2a9-c36f-465a-9cd2-01d43a667e99
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 424e0188b20d15831debf1e19ff17179fa3472c7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deny-server-permissions-transact-sql"></a>DENY (Serverberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verweigert Berechtigungen für einen Server.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DENY permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ]  
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
 Gibt eine Berechtigung an, die für einen Server verweigert werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 CASCADE  
 Gibt an, dass die verweigerte Berechtigung auch anderen Prinzipalen verweigert wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde.  
  
 UM \<Server_principal >  
 Gibt den Prinzipal an, für den die Berechtigung verweigert wird.  
  
 AS \<Grantor_principal >  
 Gibt den Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Verweigern der Berechtigung ableitet.  
  
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
 Gibt eine Serverrolle an.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können nur verweigert werden, wenn master als aktuelle Datenbank verwendet wird.  
  
 Informationen zu Serverberechtigungen kann angezeigt werden, der [Sys. server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen in angezeigt werden können die [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt. Informationen zur Mitgliedschaft von Serverrollen kann angezeigt werden, der [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) -Katalogsicht angezeigt.  
  
 Ein Server stellt die höchste Ebene der Berechtigungshierarchie dar. Die spezifischsten und restriktivsten Berechtigungen, die für einen Server verweigert werden können, sind in der folgenden Tabelle aufgeführt.  
  
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
 Erfordert die CONTROL SERVER-Berechtigung oder den Besitz des sicherungsfähigen Elements. Falls die AS-Klausel verwendet wird, muss der angegebene Prinzipal der Besitzer des sicherungsfähigen Elements sein, für das Berechtigungen verweigert werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-denying-connect-sql-permission-to-a-sql-server-login-and-principals-to-which-the-login-has-regranted-it"></a>A. Verweigern der CONNECT SQL-Berechtigung für einen SQL Server-Anmeldenamen und für Prinzipale, denen der Anmeldename diese Berechtigung erteilt hat  
 Im folgenden Beispiel wird die `CONNECT SQL`-Berechtigung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `Annika` und für die Prinzipale verweigert, denen diese Benutzerin die Berechtigung erteilt hat.  
  
```  
USE master;  
DENY CONNECT SQL TO Annika CASCADE;  
GO  
```  
  
### <a name="b-denying-create-endpoint-permission-to-a-sql-server-login-using-the-as-option"></a>B. Verweigern der CREATE ENDPOINT-Berechtigung für einen SQL Server-Anmeldenamen mit der AS-Option  
 Im folgenden Beispiel wird die `CREATE ENDPOINT`-Berechtigung für den Benutzer `ArifS` verweigert. Im Beispiel wird die `AS`-Option verwendet, um `MandarP` als Prinzipal anzugeben, von dem der ausführende Prinzipal die Berechtigung zum Erteilen oder Verweigern der Berechtigung ableitet.  
  
```  
USE master;  
DENY CREATE ENDPOINT TO ArifS AS MandarP;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Verweigern von Serverberechtigungen für (Transact-SQL)](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [WIDERRUFEN Sie Serverberechtigungen für &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

