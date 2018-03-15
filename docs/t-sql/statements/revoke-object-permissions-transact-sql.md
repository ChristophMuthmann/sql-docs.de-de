---
title: REVOKE (Objektberechtigungen) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/10/2017
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
- table permissions [SQL Server], revoking
- REVOKE statement, objects
- revoking permissions to access tables
- object permissions [SQL Server], revoking
ms.assetid: 99c7146e-d2e7-4f1a-80ff-21a05bc5e8bb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1d75af81016de00d7d76b95a1ea721b3c9ac87e3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-object-permissions-transact-sql"></a>REVOKE-Objektberechtigungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hebt Berechtigungen für eine Tabelle, Sicht, Tabellenwertfunktion, gespeicherte Prozedur, erweiterte gespeicherte Prozedur, Skalarfunktion, Aggregatfunktion, Dienstwarteschlange oder für ein Synonym auf. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        { FROM | TO } <database_principal> [ ,...n ]   
    [ CASCADE ]  
    [ AS <database_principal> ]  
  
<permission> ::=  
    ALL [ PRIVILEGES ] | permission [ ( column [ ,...n ] ) ]  
  
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
 *permission*  
 Gibt eine Berechtigung an, die für Objekte, die Schemas als Bereiche besitzen, aufgehoben werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 ALL  
 Mit ALL werden nicht alle möglichen Berechtigungen aufgehoben. Das Aufheben von Berechtigungen mit ALL entspricht dem Aufheben aller [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92-Berechtigungen, die für das angegebene Objekt gelten. Die Bedeutung von ALL variiert wie folgt:  
  
 Berechtigungen für Skalarfunktionen: EXECUTE, REFERENCES.  
  
 Berechtigungen für Tabellenwertfunktionen: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
 Berechtigungen für gespeicherte Prozeduren: EXECUTE.  
  
 Berechtigungen für Tabellen: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
 Berechtigungen für Sichten: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
 PRIVILEGES  
 Dient zur Kompatibilität mit [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92. Ändert das Verhalten von ALL nicht.  
  
 *column*  
 Gibt den Namen einer Spalte in einer Tabelle, Sicht oder Tabellenwertfunktion an, für die die Berechtigung aufgehoben wird. Die Klammern () sind erforderlich. Für eine Spalte können nur die Berechtigungen SELECT, REFERENCES und UPDATE verweigert werden. *column* kann in der Berechtigungsklausel oder nach dem Namen des sicherungsfähigen Elements angegeben werden.  
  
 ON [ OBJECT :: ] [ *schema_name* ] . *object_name*  
 Gibt das Objekt an, für das die Berechtigung aufgehoben wird. Der OBJECT-Ausdruck ist optional, wenn *schema_name* angegeben ist. Wird der OBJECT-Ausdruck verwendet, ist der Bereichsqualifizierer (::) erforderlich. Wenn *schema_name* nicht angegeben ist, wird das Standardschema verwendet. Wenn *schema_name* angegeben ist, ist der Schemabereichsqualifizierer (.) erforderlich.  
  
 { FROM | TO } \<database_principal> Gibt den Prinzipal an, für den die Berechtigung aufgehoben wird.  
  
 GRANT OPTION  
 Gibt an, dass das Recht zum Erteilen der angegebenen Berechtigung für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS \<database_principal> Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet.  
  
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
  
## <a name="remarks"></a>Remarks  
 Informationen zu Objekten werden in unterschiedlichen Katalogsichten angezeigt. Weitere Informationen finden Sie unter [Object Catalog Views &#40;Transact-SQL&#41; (Katalogsichten für Objekte &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Ein Objekt ist ein sicherungsfähiges Element auf Schemaebene in dem Schema, das das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für ein Objekt aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Objektberechtigung|Impliziert durch die Objektberechtigung|Impliziert durch die Schemaberechtigung|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|Delete|CONTROL|Delete|  
|Führen Sie|CONTROL|Führen Sie|  
|INSERT|CONTROL|INSERT|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für das Objekt.  
  
 Falls die AS-Klausel verwendet wird, muss der angegebene Prinzipal der Besitzer des Objekts sein, für das Berechtigungen aufgehoben werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-revoking-select-permission-on-a-table"></a>A. Aufheben der SELECT-Berechtigung für eine Tabelle  
 Im folgenden Beispiel wird die `SELECT`-Berechtigung für den Benutzer `RosaQdM` für die `Person.Address`-Tabelle in der `AdventureWorks2012`-Datenbank aufgehoben.  
  
```  
USE AdventureWorks2012;  
REVOKE SELECT ON OBJECT::Person.Address FROM RosaQdM;  
GO  
```  
  
### <a name="b-revoking-execute-permission-on-a-stored-procedure"></a>B. Aufheben der EXECUTE-Berechtigung für eine gespeicherte Prozedur  
 Im folgenden Beispiel wird die `EXECUTE`-Berechtigung für die gespeicherte Prozedur `HumanResources.uspUpdateEmployeeHireInfo` für die Anwendungsrolle `Recruiting11` aufgehoben.  
  
```  
USE AdventureWorks2012;  
REVOKE EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    FROM Recruiting11;  
GO   
```  
  
### <a name="c-revoking-references-permission-on-a-view-with-cascade"></a>C. Aufheben der REFERENCES-Berechtigung für eine Sicht mit CASCADE  
 Im folgenden Beispiel wird die `REFERENCES`-Berechtigung für die `BusinessEntityID`-Spalte in der `HumanResources.vEmployee`-Sicht für den Benutzer `Wanida` mit `CASCADE` aufgehoben.  
  
```  
USE AdventureWorks2012;  
REVOKE REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    FROM Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

