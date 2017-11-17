---
title: GRANT (Typberechtigungen) (Transact-SQL) | Microsoft Docs
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
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1e29ede5580418d1cbcb55d5a877196c3cabab92
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-type-permissions-transact-sql"></a>GRANT (Typberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erteilt die Berechtigungen für einen Typ.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GRANT permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
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
 Gibt eine Berechtigung an, die für einen Typ erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 FÜR den Typ **::** [ *Schema_name***.** ] *Type_name*  
 Gibt den Typ an, für den die Berechtigung erteilt wird. Der bereichsqualifizierer (**::**) ist erforderlich. Wenn *Schema_name* nicht angegeben ist, wird das Standardschema verwendet werden. Wenn *Schema_name* angegeben wird, der schemabereichsqualifizierer (**.**) ist erforderlich.  
  
 UM \<Database_principal > Gibt den Prinzipal an, die die Berechtigung erteilt wird.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 AS \<Database_principal > Gibt einen Prinzipal aus dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet.  
  
 *Database_user*  
 Gibt einen Datenbankbenutzer an.  
  
 *Database_role*  
 Gibt eine Datenbankrolle an.  
  
 *Application_role*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 Gibt eine Anwendungsrolle an.  
  
 *Database_user_mapped_to_Windows_User*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt einen Datenbankbenutzer an, der einem Windows-Benutzer zugeordnet ist.  
  
 *Database_user_mapped_to_Windows_Group*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt einen Datenbankbenutzer an, der einer Windows-Gruppe zugeordnet ist.  
  
 *Database_user_mapped_to_certificate*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt einen Datenbankbenutzer an, der einem Zertifikat zugeordnet ist.  
  
 *Database_user_mapped_to_asymmetric_key*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt einen Datenbankbenutzer an, der einem asymmetrischen Schlüssel zugeordnet ist.  
  
 *Database_user_with_no_login*  
 Gibt einen Datenbankbenutzer ohne entsprechenden Prinzipal auf Serverebene an.  
  
## <a name="remarks"></a>Hinweise  
 Ein Typ ist ein sicherungsfähiges Element auf Schemaebene in dem Schema, das das übergeordnete Element in der Berechtigungshierarchie ist.  
  
> [!IMPORTANT]  
>  **GRANT**, **verweigern,** und **widerrufen** Berechtigungen gelten nicht für Systemtypen. Benutzerdefinierten Typen können Berechtigungen erteilt werden. Weitere Informationen zu benutzerdefinierten Typen finden Sie unter [arbeiten mit benutzerdefinierten Typen in SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md).  
  
 Die spezifischsten und restriktivsten Berechtigungen, die für einen Typ erteilt werden können, sind in der folgenden Tabelle aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Typberechtigung|Impliziert durch die Typberechtigung|Impliziert durch die Schemaberechtigung|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|EXECUTE|CONTROL|EXECUTE|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Falls die AS-Option verwendet wird, gelten die folgenden zusätzlichen Anforderungen.  
  
|AS|Zusätzliche Berechtigung erforderlich|  
|--------|------------------------------------|  
|Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einer Windows-Gruppe zugeordneter Datenbankbenutzer|Mitgliedschaft in der Windows-Gruppe, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
|Einem Zertifikat zugeordneter Datenbankbenutzer|Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer|Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem Serverprinzipal zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Datenbankrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
|Anwendungsrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung mit der `GRANT OPTION` für den benutzerdefinierten `PhoneNumber`-Typ dem Benutzer `KhalidR` erteilt. `PhoneNumber`befindet sich im Schema `Telemarketing`.  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DENY (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [REVOKE (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


