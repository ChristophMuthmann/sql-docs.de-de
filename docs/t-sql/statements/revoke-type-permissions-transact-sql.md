---
title: REVOKE (Typberechtigungen) (Transact-SQL) | Microsoft Docs
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
- REVOKE statement, types
- permissions [SQL Server], types
- type permissions [SQL Server]
ms.assetid: 3969c7e9-ca10-4c67-971b-25d2dfccf650
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7421493593b931d8178e2b4b3377ef7d9fcdd80
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-type-permissions-transact-sql"></a>REVOKE (Typberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Hebt die Berechtigungen für einen Typ auf.  
  
  ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON TYPE :: [ schema_name ]. type_name   
    { FROM | TO } <database_principal> [ ,...n ]   
    [ CASCADE ]  
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
 Gibt eine Berechtigung an, die für einen Typ aufgehoben werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 FÜR den Typ **::** [ *Schema_name* ] **.** *TYPE_NAME*  
 Gibt den Typ an, für den die Berechtigung aufgehoben wird. Der bereichsqualifizierer (**::**) ist erforderlich. Wenn *Schema_name* nicht angegeben ist, wird das Standardschema verwendet. Wenn *Schema_name* angegeben wird, der schemabereichsqualifizierer (**.**) ist erforderlich.  
  
 {AUS | AN} \<Database_principal > Gibt den Prinzipal, von dem die Berechtigung aufgehoben wird.  
  
 GRANT OPTION  
 Gibt an, dass das Recht zum Erteilen der angegebenen Berechtigung für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS \<Database_principal > Gibt einen Prinzipal aus dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet.  
  
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
  
 Die spezifischsten und restriktivsten Berechtigungen, die für einen Typ aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Typberechtigung|Impliziert durch die Typberechtigung|Impliziert durch die Schemaberechtigung|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|EXECUTE|CONTROL|EXECUTE|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den Typ. Falls die AS-Klausel verwendet wird, muss der angegebene Prinzipal den Typ besitzen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung für den benutzerdefinierten Typ `PhoneNumber` für den Benutzer `KhalidR` aufgehoben. Mit der `CASCADE`-Option wird angegeben, dass die `VIEW DEFINITION`-Berechtigung für die Prinzipale aufgehoben wird, denen diese Berechtigung von `KhalidR` gewährt wurde. `PhoneNumber` befindet sich im Schema `Telemarketing`.  
  
```  
REVOKE VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    FROM KhalidR CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)   
 [DENY (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Sicherungsfähige Elemente](../../relational-databases/security/securables.md)  
  
  


