---
title: DENY (Typberechtigungen) (Transact-SQL) | Microsoft Docs
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
- DENY statement, types
- permissions [SQL Server], types
- type permissions [SQL Server]
- denying permissions [SQL Server], types
ms.assetid: 564e3500-c567-43dc-993b-9ab50e99cf3f
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1fab44dfa4778f222965453a16ed052adc640bc
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deny-type-permissions-transact-sql"></a>DENY (Typberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verweigert die Berechtigungen für einen Typ in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DENY permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
        TO <database_principal> [ ,...n ]  
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
 Gibt eine Berechtigung an, die für einen Typ verweigert werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 FÜR den Typ **::** [ *Schema_name***.** ] *Type_name*  
 Gibt den Typ an, für den die Berechtigung verweigert wird. Der bereichsqualifizierer (**::**) ist erforderlich. Wenn *Schema_name* nicht angegeben ist, wird das Standardschema verwendet. Wenn *Schema_name* angegeben wird, der schemabereichsqualifizierer (**.**) ist erforderlich.  
  
 UM \<Database_principal >  
 Gibt den Prinzipal an, für den die Berechtigung verweigert wird.  
  
 CASCADE  
 Gibt an, dass die verweigerte Berechtigung auch anderen Prinzipalen verweigert wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde.  
  
 AS \<Database_principal >  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, das Recht zum Verweigern der Berechtigung ableitet.  
  
 *Database_user*  
 Gibt einen Datenbankbenutzer an.  
  
 *Database_role*  
 Gibt eine Datenbankrolle an.  
  
 *Application_role*  
   
 Gibt eine Anwendungsrolle an.  
  
 *Database_user_mapped_to_Windows_User*  
 
 Gibt einen Datenbankbenutzer an, der einem Windows-Benutzer zugeordnet ist.  
  
 *Database_user_mapped_to_Windows_Group*  
 
 Gibt einen Datenbankbenutzer an, der einer Windows-Gruppe zugeordnet ist.  
  
 *Database_user_mapped_to_certificate*  
 
 Gibt einen Datenbankbenutzer an, der einem Zertifikat zugeordnet ist.  
  
 *Database_user_mapped_to_asymmetric_key*  
  
 Gibt einen Datenbankbenutzer an, der einem asymmetrischen Schlüssel zugeordnet ist.  
  
 *Database_user_with_no_login*  
 Gibt einen Datenbankbenutzer ohne entsprechenden Prinzipal auf Serverebene an.  
  
## <a name="remarks"></a>Hinweise  
 Ein Typ ist ein sicherungsfähiges Element auf Schemaebene in dem Schema, das das übergeordnete Element in der Berechtigungshierarchie ist.  
  
> [!IMPORTANT]  
>  **GRANT**, **verweigern,** und **widerrufen** Berechtigungen gelten nicht für Systemtypen. Benutzerdefinierten Typen können Berechtigungen erteilt werden. Weitere Informationen zu benutzerdefinierten Typen finden Sie unter [arbeiten mit benutzerdefinierten Typen in SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md).  
  
 Die spezifischsten und restriktivsten Berechtigungen, die für einen Typ verweigert werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Typberechtigung|Impliziert durch die Typberechtigung|Impliziert durch die Schemaberechtigung|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|EXECUTE|CONTROL|EXECUTE|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den Typ. Falls die AS-Klausel verwendet wird, muss der angegebene Prinzipal der Besitzer des Typs sein, für den Berechtigungen verweigert werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `VIEW DEFINITION`-Berechtigung mit der `CASCADE` im benutzerdefinierten `PhoneNumber`-Typ für den Benutzer `KhalidR` verweigert. `PhoneNumber` befindet sich im Schema `Telemarketing`.  
  
```  
DENY VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)   
 [REVOKE (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Sicherungsfähige Elemente](../../relational-databases/security/securables.md)  
  
  

