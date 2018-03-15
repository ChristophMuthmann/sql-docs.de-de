---
title: GRANT (Objektberechtigungen) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/10/2017
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
- granting permissions [SQL Server], objects
- GRANT statement, objects
ms.assetid: c001c2e7-d092-43d4-8fa6-693b3ec4c3ea
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7346cb0ddd69277fd9a7336feaba766fb1ec5b0b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-object-permissions-transact-sql"></a>GRANT (Objektberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erteilt Berechtigungen für eine Tabelle, Sicht, Tabellenwertfunktion, gespeicherte Prozedur, erweiterte gespeicherte Prozedur, Skalarfunktion, Aggregatfunktion, Dienstwarteschlange oder für ein Synonym.  
  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GRANT <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
    TO <database_principal> [ ,...n ]   
    [ WITH GRANT OPTION ]  
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
 Gibt eine Berechtigung an, die für Objekte, die Schemas als Bereiche besitzen, erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 ALL  
 Mit ALL werden nicht alle möglichen Berechtigungen erteilt. Das Erteilen von Berechtigungen mit ALL entspricht dem Erteilen aller [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92-Berechtigungen, die für das angegebene Objekt gelten. Die Bedeutung von ALL variiert wie folgt:  
  
- Berechtigungen für Skalarfunktionen: EXECUTE, REFERENCES.  
- Berechtigungen für Tabellenwertfunktionen: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
- Berechtigungen für gespeicherte Prozeduren: EXECUTE.  
- Berechtigungen für Tabellen: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
- Berechtigungen für Sichten: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
PRIVILEGES  
 Dient zur Kompatibilität mit [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92. Ändert das Verhalten von ALL nicht.  
  
*column*  
 Gibt den Namen einer Spalte in einer Tabelle, Sicht oder Tabellenwertfunktion an, für die die Berechtigung erteilt wird. Die Klammern () sind erforderlich. Für eine Spalte können nur die Berechtigungen SELECT, REFERENCES und UPDATE gewährt werden. *column* kann in der Berechtigungsklausel oder nach dem Namen des sicherungsfähigen Elements angegeben werden.  
  
> [!CAUTION]  
>  Eine DENY-Anweisung auf Tabellenebene hat keinen Vorrang vor einer GRANT-Anweisung auf Spaltenebene. Diese Inkonsistenz in der Berechtigungshierarchie wurde aus Gründen der Abwärtskompatibilität beibehalten.  
  
 ON [ OBJECT :: ] [ *schema_name* ] . *object_name*  
 Gibt das Objekt an, für das die Berechtigung erteilt wird. Der OBJECT-Ausdruck ist optional, wenn *schema_name* angegeben ist. Wird der OBJECT-Ausdruck verwendet, ist der Bereichsqualifizierer (::) erforderlich. Wenn *schema_name* nicht angegeben ist, wird das Standardschema verwendet. Wenn *schema_name* angegeben ist, ist der Schemabereichsqualifizierer (.) erforderlich.  
  
 TO \<database_principal>  
 Gibt den Prinzipal an, für den die Berechtigung erteilt wird.  
  
 WITH GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 AS \<database_principal> Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet.  
  
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
  
> [!IMPORTANT]  
>  Durch eine Kombination von ALTER- und REFERENCE-Berechtigungen würde in manchen Fällen zugelassen, dass der Empfänger Daten anzeigt oder Funktionen ausführt, für die er nicht autorisiert ist. Beispiel: Ein Benutzer mit ALTER-Berechtigung für eine Tabelle und REFERENCE-Berechtigung für eine Funktion kann eine berechnete Spalte über eine Funktion erstellen und ausführen lassen. In diesem Fall benötigt der Benutzer auch die SELECT-Berechtigung für die berechnete Spalte.  
  
 Informationen zu Objekten werden in unterschiedlichen Katalogsichten angezeigt. Weitere Informationen finden Sie unter [Object Catalog Views &#40;Transact-SQL&#41; (Katalogsichten für Objekte &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Ein Objekt ist ein sicherungsfähiges Element auf Schemaebene in dem Schema, das das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für ein Objekt erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
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
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Falls die AS-Option verwendet wird, gelten die folgenden zusätzlichen Anforderungen.  
  
|AS|Zusätzliche Berechtigung erforderlich|  
|--------|------------------------------------|  
|Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einer Windows-Gruppe zugeordneter Datenbankbenutzer|Mitgliedschaft in der Windows-Gruppe, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Zertifikat zugeordneter Datenbankbenutzer|Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer|Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Serverprinzipal zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Datenbankrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Anwendungsrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-granting-select-permission-on-a-table"></a>A. Erteilen der SELECT-Berechtigung für eine Tabelle  
 Im folgenden Beispiel wird die `SELECT`-Berechtigung dem Benutzer `RosaQdM` für die `Person.Address`-Tabelle in der `AdventureWorks2012`-Datenbank erteilt.  
  
```  
GRANT SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-a-stored-procedure"></a>B. Erteilen der EXECUTE-Berechtigung für eine gespeicherte Prozedur  
 Im folgenden Beispiel wird die `EXECUTE`-Berechtigung für die gespeicherte Prozedur `HumanResources.uspUpdateEmployeeHireInfo` der Anwendungsrolle `Recruiting11` erteilt.  
  
```  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-granting-references-permission-on-a-view-with-grant-option"></a>C. Erteilen der REFERENCES-Berechtigung für eine Sicht mit GRANT OPTION  
 Im folgenden Beispiel wird die `REFERENCES`-Berechtigung für die `BusinessEntityID`-Spalte in der `HumanResources.vEmployee`-Sicht dem Benutzer `Wanida` mit `GRANT OPTION` erteilt.  
  
```  
GRANT REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida WITH GRANT OPTION;  
GO  
```  
  
### <a name="d-granting-select-permission-on-a-table-without-using-the-object-phrase"></a>D. Erteilen der SELECT-Berechtigung für eine Tabelle ohne Verwendung des OBJECT-Ausdrucks  
 Im folgenden Beispiel wird die `SELECT`-Berechtigung dem Benutzer `RosaQdM` für die `Person.Address`-Tabelle in der `AdventureWorks2012`-Datenbank erteilt.  
  
```  
GRANT SELECT ON Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="e-granting-select-permission-on-a-table-to-a-domain-account"></a>E. Erteilen der SELECT-Berechtigung für eine Tabelle an ein Domänenkonto  
 Im folgenden Beispiel wird die `SELECT`-Berechtigung dem Benutzer `AdventureWorks2012\RosaQdM` für die `Person.Address`-Tabelle in der `AdventureWorks2012`-Datenbank erteilt.  
  
```  
GRANT SELECT ON Person.Address TO [AdventureWorks2012\RosaQdM];  
GO  
```  
  
### <a name="f-granting-execute-permission-on-a-procedure-to-a-role"></a>F. Erteilen der EXECUTE-Berechtigung für eine Prozedur an eine Rolle  
 Im folgenden Beispiel wird eine Rolle erstellt; anschließend wird der Rolle die `EXECUTE`-Berechtigung für die `uspGetBillOfMaterials`-Prozedur in der `AdventureWorks2012`-Datenbank erteilt.  
  
```  
CREATE ROLE newrole ;  
GRANT EXECUTE ON dbo.uspGetBillOfMaterials TO newrole ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

