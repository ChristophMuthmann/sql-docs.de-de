---
title: "Verfügbarkeitsgruppe REVOKE-Berechtigungen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
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
- Availability Groups [SQL Server], permissions
- REVOKE statement, availability groups
- revoking permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 02c77378-a36d-4286-9235-d8867a2b92ad
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1573f866cec3105cde4eeab59c230ede46144ac3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-availability-group-permissions-transact-sql"></a>Aufheben von Verfügbarkeitsgruppenberechtigungen mit REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Hebt Berechtigungen für eine Always On-verfügbarkeitsgruppe. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON AVAILABILITY GROUP :: availability_group_name  
    { FROM | TO } < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für eine Verfügbarkeitsgruppe aufgehoben werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 FÜR die VERFÜGBARKEITSGRUPPE **::***Availability_group_name*  
 Gibt die Verfügbarkeitsgruppe an, für die die Berechtigung aufgehoben wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 {AUS | AN} \<Server_principal > Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, die für die die Berechtigung aufgehoben wird.  
  
 *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_Windows_login*  
 Gibt einen aus einem Windows-Anmeldenamen erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_certificate*  
 Gibt einen einem Zertifikat zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_AsymKey*  
 Gibt einen einem asymmetrischen Schlüssel zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 GRANT OPTION  
 Gibt an, dass das Recht zum Erteilen der angegebenen Berechtigung für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!IMPORTANT]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *SQL_Server_login*  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können nur, wenn die aktuelle Datenbank ist gesperrt werden **master**.  
  
 Informationen zu Verfügbarkeitsgruppen werden in der [availability_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) -Katalogsicht angezeigt. Informationen zu Serverberechtigungen werden in der [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen werden in der [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt.  
  
 Eine Verfügbarkeitsgruppe ist ein sicherungsfähiges Element auf Serverebene. Die spezifischsten und restriktivsten Berechtigungen, die für eine Verfügbarkeitsgruppe aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Verfügbarkeitsgruppenberechtigung|Impliziert durch die Verfügbarkeitsgruppenberechtigung|Impliziert durch die Serverberechtigung|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Verfügbarkeitsgruppe oder die ALTER ANY AVAILABILTIY GROUP-Berechtigung für den Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-revoking-view-definition-permission-on-an-availability-group"></a>A. Aufheben der VIEW DEFINITION-Berechtigung für eine Verfügbarkeitsgruppe  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung für die Verfügbarkeitsgruppe `MyAg` für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `ZArifin` aufgehoben.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade"></a>B. Aufheben der TAKE OWNERSHIP-Berechtigung mit CASCADE  
 Im folgenden Beispiel wird die `TAKE OWNERSHIP`-Berechtigung für die Verfügbarkeitsgruppe `MyAg` für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer `PKomosinski` und für alle Prinzipale aufgehoben, denen von `PKomosinski` die TAKE OWNERSHIP-Berechtigung für MyAg erteilt wurde.  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
### <a name="c-revoking-a-previously-granted-with-grant-option-clause"></a>C. Aufheben einer zuvor mit der WITH GRANT OPTION-Klausel erteilten Berechtigung  
 Wenn eine Berechtigung mit der WITH GRANT OPTION erteilt wurde, verwenden Sie REVOKE GRANT OPTION FOR... So entfernen Sie die WITH GRANT OPTION Im folgenden Beispiel wird die Berechtigung erteilt, und dann wird der WITH GRANT-Teil der Berechtigung entfernt.  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
REVOKE GRANT OPTION FOR CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski  
CASCADE  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Verfügbarkeitsgruppenberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [Verweigern von Verfügbarkeitsgruppenberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Katalogsichten Always On-Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


