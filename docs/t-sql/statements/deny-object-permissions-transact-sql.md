---
title: "Verweigern von Berechtigungen für Modellobjekte (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- DENY statement, objects
- table permissions [SQL Server]
ms.assetid: 0b8d3ddc-38c0-4241-b7bb-ee654a5081aa
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dc405b480d063ff6990182f9a66cc6f4e35c3a5a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="deny-object-permissions-transact-sql"></a>DENY (Objektberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verweigert Berechtigungen für ein Element der OBJECT-Klasse sicherungsfähiger Elemente. Folgende Elemente gehören zur OBJECT-Klasse: Tabellen, Sichten, Tabellenwertfunktionen, gespeicherte Prozeduren, erweiterte gespeicherte Prozeduren, Skalarfunktionen, Aggregatfunktionen, Dienstwarteschlangen und Synonyme.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DENY <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        TO <database_principal> [ ,...n ]   
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
 *Berechtigung*  
 Gibt eine Berechtigung an, die für Objekte, die Schemas als Bereiche besitzen, verweigert werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 ALL  
 Mit ALL werden nicht alle möglichen Berechtigungen verweigert. Das Verweigern mit ALL entspricht dem Verweigern aller ANSI-92-Berechtigungen, die für das angegebene Objekt gelten. Die Bedeutung von ALL variiert wie folgt:  
  
 - Berechtigungen für Skalarfunktionen: EXECUTE, REFERENCES.  
 - Berechtigungen für Tabellenwertfunktionen: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
 - Berechtigungen für gespeicherte Prozeduren: AUSZUFÜHREN.  
 - Berechtigungen für Tabellen: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
 - Berechtigungen für Sichten: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
PRIVILEGES  
 Aus Gründen der Kompatibilität mit ANSI-92 eingeschlossen. Ändert das Verhalten von ALL nicht.  
  
*Spalte*  
 Gibt den Namen einer Spalte in einer Tabelle, Sicht oder Tabellenwertfunktion an, für die die Berechtigung verweigert wird. Die Klammern **()** erforderlich sind. Für eine Spalte können nur die Berechtigungen SELECT, REFERENCES und UPDATE verweigert werden. *Spalte* kann in der berechtigungsklausel oder nach dem Namen des sicherungsfähigen Elements angegeben werden.  
  
> [!CAUTION]  
>  Eine DENY-Anweisung auf Tabellenebene hat keinen Vorrang vor einer GRANT-Anweisung auf Spaltenebene. Diese Inkonsistenz in der Berechtigungshierarchie wurde aus Gründen der Abwärtskompatibilität beibehalten.  
  
 ON [OBJECT **::** ] [ *Schema_name* ] **.** *object_name*  
 Gibt das Objekt, auf dem die Berechtigung verweigert wird. Der OBJECT-Ausdruck ist optional Wenn *Schema_name* angegeben ist. Wenn der OBJECT-Ausdruck verwendet wird, der bereichsqualifizierer (**::**) ist erforderlich. Wenn *Schema_name* nicht angegeben ist, wird das Standardschema verwendet. Wenn *Schema_name* angegeben wird, der schemabereichsqualifizierer (**.**) ist erforderlich.  
  
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
 Informationen zu Objekten werden in unterschiedlichen Katalogsichten angezeigt. Weitere Informationen finden Sie unter [Objekt Katalogsichten &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Ein Objekt ist ein sicherungsfähiges Element auf Schemaebene in dem Schema, das das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für ein Objekt verweigert werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Objektberechtigung|Impliziert durch die Objektberechtigung|Impliziert durch die Schemaberechtigung|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|DELETE|CONTROL|DELETE|  
|EXECUTE|CONTROL|EXECUTE|  
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
  
 Falls die AS-Klausel verwendet wird, muss der angegebene Prinzipal der Besitzer des Objekts sein, für das Berechtigungen verweigert werden.  
  
## <a name="examples"></a>Beispiele  
Die folgenden Beispiele verwenden die AdventureWorks-Datenbank.
  
### <a name="a-denying-select-permission-on-a-table"></a>A. Verweigern der SELECT-Berechtigung für eine Tabelle  
 Im folgenden Beispiel wird verweigert `SELECT` Berechtigung für den Benutzer `RosaQdM` für die Tabelle `Person.Address`.  
  
```  
DENY SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-denying-execute-permission-on-a-stored-procedure"></a>B. Verweigern der EXECUTE-Berechtigung für eine gespeicherte Prozedur  
 Im folgenden Beispiel wird die `EXECUTE`-Berechtigung für die gespeicherte Prozedur `HumanResources.uspUpdateEmployeeHireInfo` für die Anwendungsrolle `Recruiting11` verweigert.  
  
```  
DENY EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-denying-references-permission-on-a-view-with-cascade"></a>C. Verweigern der REFERENCES-Berechtigung für eine Sicht mit CASCADE  
 Im folgenden Beispiel wird die `REFERENCES`-Berechtigung für die `BusinessEntityID`-Spalte in der `HumanResources.vEmployee`-Sicht für den Benutzer `Wanida` mit `CASCADE` verweigert.  
  
```  
DENY REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [REVOKE-Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  
