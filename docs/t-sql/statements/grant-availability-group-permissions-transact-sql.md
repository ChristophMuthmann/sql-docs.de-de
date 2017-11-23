---
title: "Verfügbarkeitsgruppe GRANT-Berechtigungen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
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
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2138d0fb0b3e6066af9452a033dcf042fa1f5ca6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-availability-group-permissions-transact-sql"></a>Erteilen von Verfügbarkeitsgruppenberechtigungen mit GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für eine Always On-verfügbarkeitsgruppe.  
  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für eine Verfügbarkeitsgruppe erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 FÜR die VERFÜGBARKEITSGRUPPE **::***Availability_group_name*  
 Gibt die Verfügbarkeitsgruppe an, der die Berechtigung erteilt wird. Der bereichsqualifizierer (**::**) ist erforderlich.  
  
 UM \<Server_principal >  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, dem die Berechtigung erteilt wird.  
  
 *SQL_Server_login*  
 Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_Windows_login*  
 Gibt einen aus einem Windows-Anmeldenamen erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_certificate*  
 Gibt einen einem Zertifikat zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 *SQL_Server_login_from_AsymKey*  
 Gibt einen einem asymmetrischen Schlüssel zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 AS *SQL_Server_login*  
 Gibt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet.  
  
## <a name="remarks"></a>Hinweise  
 Berechtigungen im Serverbereich können erteilt werden, nur, wenn die aktuelle Datenbank ist **master**.  
  
 Informationen zu Verfügbarkeitsgruppen werden in der [availability_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) -Katalogsicht angezeigt. Informationen zu Serverberechtigungen werden in der [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) -Katalogsicht und Informationen zu serverprinzipalen werden in der [Sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) -Katalogsicht angezeigt.  
  
 Eine Verfügbarkeitsgruppe ist ein sicherungsfähiges Element auf Serverebene. Die spezifischsten und restriktivsten Berechtigungen, die für eine Verfügbarkeitsgruppe erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Verfügbarkeitsgruppenberechtigung|Impliziert durch die Verfügbarkeitsgruppenberechtigung|Impliziert durch die Serverberechtigung|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 Für ein Diagramm aller [!INCLUDE[ssDE](../../includes/ssde-md.md)] Berechtigungen finden Sie unter [Datenbankmodulberechtigungen](http://go.microsoft.com/fwlink/?LinkId=229142).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Verfügbarkeitsgruppe oder die ALTER ANY AVAILABILTIY GROUP-Berechtigung für den Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>A. Erteilen der VIEW DEFINITION-Berechtigung für eine Verfügbarkeitsgruppe  
 Im folgenden Beispiel wird dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `VIEW DEFINITION` die `MyAg`-Berechtigung für die Verfügbarkeitsgruppe `ZArifin` erteilt.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. Gewähren der TAKE OWNERSHIP-Berechtigung mit der GRANT OPTION  
 Im folgenden Beispiel wird dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer `TAKE OWNERSHIP` die `MyAg`-Berechtigung für die Verfügbarkeitsgruppe `PKomosinski` mit `GRANT OPTION` erteilt.  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. Erteilen der CONTROL-Berechtigung für eine Verfügbarkeitsgruppe  
 Im folgenden Beispiel wird dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer `CONTROL` die `MyAg`-Berechtigung für die Verfügbarkeitsgruppe `PKomosinski` erteilt. CONTROL ermöglicht dem Anmeldenamen die umfassende Kontrolle der Verfügbarkeitsgruppe, auch wenn er nicht der Besitzer der Verfügbarkeitsgruppe ist. Zum Ändern des Besitzes finden Sie unter [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verfügbarkeitsgruppenberechtigungen mit REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [Verweigern von Verfügbarkeitsgruppenberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn-Verfügbarkeitsgruppen-Katalogsichten &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [Berechtigungen &#40; Datenbankmodul &#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
