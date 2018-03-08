---
title: "GRANT-Berechtigungen für Datenbankprinzipal (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
- database roles [SQL Server], permissions
- permissions [SQL Server], database roles
- granting permissions [SQL Server], database users
- granting permissions [SQL Server], application roles
- granting permissions [SQL Server], database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- GRANT statement, users
- GRANT statement, roles
- application roles [SQL Server], permissions
ms.assetid: 012588a2-cbe1-48f0-a731-b4a2b83203d5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 58f66a871299d85c8ee9bce59b696cec2668ae9f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-database-principal-permissions-transact-sql"></a>GRANT (Berechtigungen für Datenbankprinzipal) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erteilt Berechtigungen für einen Datenbankbenutzer, eine Datenbankrolle oder Anwendungsrolle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GRANT permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
    TO <database_principal> [ ,...n ]  
       [ WITH GRANT OPTION ]  
       [ AS <database_principal> ]  
  
<database_principal> ::=  
    Database_user   
  | Database_role   
  | Application_role   
  | Database_user_mapped_to_Windows_User   
  | Database_user_mapped_to_Windows_Group   
  | Database_user_mapped_to_certificate   
  | Database_user_mapped_to_asymmetric_key   
  | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für den Datenbankprinzipal erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 USER::*Database_user*  
 Gibt die Klasse und den Namen des Benutzers an, für den die Berechtigung erteilt wird. Der Bereichsqualifizierer (::) ist erforderlich.  
  
 Rolle::*Database_role*  
 Gibt die Klasse und den Namen der Rolle an, für die die Berechtigung erteilt wird. Der Bereichsqualifizierer (::) ist erforderlich.  
  
 ANWENDUNGSROLLE::*Application_role*  
   
 Gibt die Klasse und den Namen der Anwendungsrolle an, für die die Berechtigung erteilt wird. Der Bereichsqualifizierer (::) ist erforderlich.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 AS \<Database_principal >  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet.  
  
 *Database_user*  
 Gibt einen Datenbankbenutzer an.  
  
 *Database_role*  
 Gibt eine Datenbankrolle an.  
  
 *Application_role*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt eine Anwendungsrolle an.  
  
 *Database_user_mapped_to_Windows_User*  
 Gibt einen Datenbankbenutzer für einen Windows-Benutzer zugeordnet.  
  
 *Database_user_mapped_to_Windows_Group*  
  
 Gibt einen Datenbankbenutzer an, der einer Windows-Gruppe zugeordnet ist.  
  
 *Database_user_mapped_to_certificate*  
  
 Gibt einen Datenbankbenutzer an, der einem Zertifikat zugeordnet ist.  
  
 *Database_user_mapped_to_asymmetric_key*  
  
 Gibt einen Datenbankbenutzer an, der einem asymmetrischen Schlüssel zugeordnet ist.  
  
 *Database_user_with_no_login*  
 Gibt einen Datenbankbenutzer ohne entsprechenden Prinzipal auf Serverebene an.  
  
## <a name="remarks"></a>Hinweise  
 Informationen zu datenbankprinzipalen werden in der [Sys. database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) -Katalogsicht angezeigt. Informationen zu Berechtigungen auf Datenbankebene ist sichtbar, in der [database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="database-user-permissions"></a>Berechtigungen für Datenbankbenutzer  
 Ein Datenbankbenutzer ist ein sicherungsfähiges Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die einem Datenbankbenutzer erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Berechtigung für Datenbankbenutzer|Impliziert durch die Berechtigung für Datenbankbenutzer|Impliziert durch Datenbankberechtigung|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>Berechtigungen für Datenbankrollen  
 Eine Datenbankrolle ist ein sicherungsfähiges Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die einer Datenbankrolle erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Berechtigung für Datenbankrollen|Impliziert durch die Berechtigung für Datenbankrollen|Impliziert durch Datenbankberechtigung|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>Berechtigungen für Anwendungsrollen  
 Eine Anwendungsrolle ist ein sicherungsfähiges Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die einer Anwendungsrolle erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Berechtigung für Anwendungsrollen|Impliziert durch die Berechtigung für Anwendungsrollen|Impliziert durch Datenbankberechtigung|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Falls die AS-Option verwendet wird, gelten die folgenden zusätzlichen Anforderungen.  
  
|AS *Granting_principal*|Zusätzliche Berechtigung erforderlich|  
|------------------------------|------------------------------------|  
|Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Windows-Benutzer zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einer Windows-Gruppe zugeordneter Datenbankbenutzer|Mitgliedschaft in der Windows-Gruppe, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Zertifikat zugeordneter Datenbankbenutzer|Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer|Mitgliedschaft in Datenbankrolle Db_securityadminfixed, festen Mitgliedschaft in der "Db_owner"-Datenbankrolle oder die Mitgliedschaft in der festen Serverrolle "Sysadmin".|  
|Einem Serverprinzipal zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Datenbankrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in Datenbankrolle Db_securityadminfixed, Mitgliedschaft in der festen Datenbankrolle Db_owner oder Mitgliedschaft in der festen Serverrolle "Sysadmin".|  
|Anwendungsrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
  
 Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  
  
 Empfänger der CONTROL-Berechtigung in einer Datenbank, z. B. Mitglieder der festen Datenbankrolle db_owner, können jede Berechtigung für ein beliebiges sicherungsfähiges Element in der Datenbank erteilen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-granting-control-permission-on-a-user-to-another-user"></a>A. Erteilen der CONTROL-Berechtigung für einen Benutzer an einen anderen Benutzer  
 Im folgenden Beispiel wird die `CONTROL`-Berechtigung für den `AdventureWorks2012`-Benutzer `Wanida` an den Benutzer `RolandX` erteilt.  
  
```  
GRANT CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-granting-view-definition-permission-on-a-role-to-a-user-with-grant-option"></a>B. Erteilen der VIEW DEFINITION-Berechtigung für eine Rolle an einen Benutzer mit GRANT OPTION  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung für die `AdventureWorks2012`-Rolle `SammamishParking` zusammen mit `GRANT OPTION` an den Datenbankbenutzer `JinghaoLiu` erteilt.  
  
```  
GRANT VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-impersonate-permission-on-a-user-to-an-application-role"></a>C. Erteilen der IMPERSONATE-Berechtigung für einen Benutzer an eine Anwendungsrolle  
 Im folgenden Beispiel wird die `IMPERSONATE`-Berechtigung für den Benutzer `HamithaL` an die `AdventureWorks2012`-Anwendungsrolle `AccountsPayable17` erteilt.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
```  
GRANT IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verweigern von Berechtigungen für Datenbankprinzipal &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [REVOKE-Berechtigungen für Datenbankprinzipal &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Erstellen Sie die Rolle "" &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
