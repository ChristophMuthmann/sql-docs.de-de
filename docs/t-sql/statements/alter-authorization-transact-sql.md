---
title: ALTER AUTHORIZATION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_AUTHORIZATION_TSQL
- ALTER AUTHORIZATION
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], transferring
- modifying entity ownership
- full-text search [SQL Server], permissions
- owners [SQL Server], entities
- ALTER AUTHORIZATION statement
- entity ownership [SQL Server]
- transferring ownership
- search property lists [SQL Server], permissions
- TAKE OWNERSHIP
ms.assetid: 8c805ae2-91ed-4133-96f6-9835c908f373
caps.latest.revision: 84
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 21d2654f72fca0a136a9369190b73edada80b316
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-authorization-transact-sql"></a>ALTER AUTHORIZATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert den Besitz eines sicherungsfähigen Elements.    
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
-- Syntax for SQL Server  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
        OBJECT | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP | CERTIFICATE     
      | CONTRACT | TYPE | DATABASE | ENDPOINT | FULLTEXT CATALOG     
      | FULLTEXT STOPLIST | MESSAGE TYPE | REMOTE SERVICE BINDING    
      | ROLE | ROUTE | SCHEMA | SEARCH PROPERTY LIST | SERVER ROLE     
      | SERVICE | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

```
-- Syntax for SQL Database  
  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
      OBJECT | ASSEMBLY | ASYMMETRIC KEY | CERTIFICATE     
    | TYPE | DATABASE | FULLTEXT CATALOG     
    | FULLTEXT STOPLIST     
    | ROLE | SCHEMA | SEARCH PROPERTY LIST     
    | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

    
```    
-- Syntax for Azure SQL Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
```    
-- Syntax for Parallel Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      DATABASE     
    | SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      database_name 
    | schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
## <a name="arguments"></a>Argumente    
\<class_type> ist die sicherungsfähige Klasse der Entität, für die der Besitzer geändert wird. OBJECT ist der Standardwert.    
    
|||    
|-|-|    
|OBJECT|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|    
|ASSEMBLY|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|ASYMMETRIC KEY|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|AVAILABILITY GROUP |**GILT FÜR:** SQL Server 2012 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|
|CERTIFICATE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|CONTRACT|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|DATABASE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Weitere Informationen finden Sie weiter unten im Abschnitt [ALTER AUTHORIZATION für Datenbanken](#AlterDB).|    
|ENDPOINT|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|FULLTEXT CATALOG|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|FULLTEXT STOPLIST|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|MESSAGE TYPE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|REMOTE SERVICE BINDING|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|ROLE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|ROUTE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|SCHEMA|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|    
|SEARCH PROPERTY LIST|**GILT FÜR:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|SERVER ROLE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|SERVICE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|    
|SYMMETRIC KEY|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|TYPE|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
|XML SCHEMA COLLECTION|**GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|    
    
 *entity_name*    
 Der Name der Entität.    
    
 *principal_name* | SCHEMA OWNER    
 Name des Sicherheitsprinzipals, der die Entität besitzt. Datenbankobjekte müssen im Besitz eines Datenbankprinzipals sein, also ein Datenbankbenutzer oder eine Datenbankrolle. Serverobjekte (beispielsweise Datenbanken) müssen im Besitz eines Serverprinzipals (eines Anmeldenamens) sein. Geben Sie **SCHEMA OWNER** als *principal_name* an, um anzugeben, dass das Objekt im Besitz des Prinzipals sein sollte, der das Schema des Objekts besitzt.    
    
## <a name="remarks"></a>Remarks    
 Mit ALTER AUTHORIZATION kann der Besitz einer Entität, die einen Besitzer aufweist, geändert werden. Der Besitz von in der Datenbank enthaltenen Entitäten kann an jeden Prinzipal auf Datenbankebene übertragen werden. Der Besitz von Entitäten auf Serverebene kann nur an Prinzipale auf Serverebene übertragen werden.    
    
> [!IMPORTANT]    
>  Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] kann der Benutzer Besitzer eines Objekts oder Typs sein, das bzw. der in einem Schema enthalten ist, dessen Besitzer ein anderer Datenbankbenutzer ist. Dieses Verhalten unterscheidet sich von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [OBJECTPROPERTY &#40;Transact-SQL&#41; ](../../t-sql/functions/objectproperty-transact-sql.md) und [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md).    
    
 Der Besitz der folgenden in einem Schema enthaltenen Entitäten vom Typ "object" kann übertragen werden: Tabellen, Sichten, Funktionen, Prozeduren, Warteschlangen und Synonyme.    
    
 Der Besitz der folgenden Entitäten kann nicht übertragen werden: Verbindungsserver, Statistiken, Einschränkungen, Regeln, Standardwerte, Trigger, [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Warteschlangen, Anmeldeinformationen, Partitionsfunktionen, Partitionsschemas, Datenbank-Hauptschlüssel, Diensthauptschlüssel und Ereignisbenachrichtigungen.    
    
 Der Besitz von Mitgliedern der folgenden sicherungsfähigen Klassen kann nicht übertragen werden: Server, Anmeldename, Benutzer, Anwendungsrolle und Spalte.    
    
 Die SCHEMA OWNER-Option ist nur gültig, wenn Sie den Besitz einer in einem Schema enthaltenen Entität übertragen. Mit SCHEMA OWNER wird der Besitz der Entität an den Besitzer des Schemas übertragen, in dem sie sich befindet. Nur Entitäten der Klasse OBJECT, TYPE oder XML SCHEMA COLLECTION sind in Schemas enthalten.    
    
 Falls es sich bei der Zielentität nicht um eine Datenbank handelt und die Entität an einen neuen Besitzer übertragen wird, werden alle Berechtigungen für das Ziel gelöscht.    
    
> [!CAUTION]    
>  Das Verhalten der Schemas in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] unterscheidet sich von dem in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Code, in dem vorausgesetzt wird, dass Schemas Datenbankbenutzern entsprechen, gibt möglicherweise nicht die richtigen Ergebnisse zurück. Alte Katalogsichten, einschließlich sysobjects, sollten nicht in einer Datenbank verwendet werden, in der eine der folgenden DDL-Anweisungen bereits verwendet wurde: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. In einer Datenbank, in der jemals eine dieser Anweisungen verwendet wurde, müssen Sie die neuen Katalogsichten verwenden. In den neuen Katalogsichten wird die Trennung zwischen Prinzipalen und Schemas berücksichtigt, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführt wurde. Weitere Informationen zu Katalogansichten finden Sie unter [Catalog Views &#40;Transact-SQL&#41; (Katalogansichten (Transact-SQL))](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).    
    
 Beachten Sie dabei außerdem Folgendes:    
    
> [!IMPORTANT]    
>  Die einzig zuverlässige Möglichkeit, den Besitzer eines Objekts zu finden, besteht darin, die **sys.objects**-Katalogsicht abzufragen. Die einzige zuverlässige Möglichkeit, den Besitzer eines Typs zu finden, besteht in der Verwendung der TYPEPROPERTY-Funktion.    
    
## <a name="special-cases-and-conditions"></a>Spezialfälle und Bedingungen    
 In der folgenden Tabelle sind Spezialfälle, Ausnahmen und Bedingungen aufgeführt, die beim Ändern der Autorisierung gelten.    
    
|Klasse|Bedingung|    
|-----------|---------------|    
|OBJECT|Der Besitz von Triggern, Einschränkungen, Regeln, Standardwerten, Statistiken, Systemobjekten, Warteschlangen, indizierten Sichten oder Tabellen mit indizierten Sichten kann nicht geändert werden.|    
|SCHEMA|Wenn der Besitz übertragen wird, werden Berechtigungen für in einem Schema enthaltene Objekte, die keine expliziten Besitzer aufweisen, gelöscht. Der Besitzer von sys, dbo oder information_schema kann nicht geändert werden.|    
|TYPE|Der Besitz eines TYPE-Objekts, das zu sys oder information_schema gehört, kann nicht geändert werden.|    
|CONTRACT, MESSAGE TYPE oder SERVICE|Der Besitz von Systementitäten kann nicht geändert werden.|    
|SYMMETRIC KEY|Der Besitz von globalen temporären Schlüsseln kann nicht geändert werden.|    
|CERTIFICATE oder ASYMMETRIC KEY|Der Besitz dieser Entitäten kann nicht an eine Rolle oder Gruppe übertragen werden.|    
|ENDPOINT|Der Prinzipal muss ein Anmeldename sein.|    
  
## <a name="AlterDB"></a> ALTER AUTHORIZATION für Datenbanken  
**GILT FÜR:** [!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
### <a name="for-sql-server"></a>Für SQL Server:  
**Anforderungen für den neuen Besitzer:**   
Der neue Besitzerprinzipal muss einer der folgenden sein:  
-   Ein Anmeldename für die SQL Server-Authentifizierung  
-   Ein Anmeldename für die Windows-Authentifizierung, der einen Windows-Benutzer (keine Gruppe) darstellt  
-   Ein Windows-Benutzer, der sich über einen Anmeldenamen für die Windows-Authentifizierung authentifiziert, der eine Windows-Gruppe darstellt  
  
**Anforderungen an die Person, die die ALTER AUTHORIZATION-Anweisung ausführt:**  
Wenn Sie kein Mitglied der festen Serverrolle **sysadmin** sind, benötigen Sie mindestens die Berechtigung TAKE OWNERSHIP für die Datenbank und die Berechtigung IMPERSONATE für den neuen Besitzeranmeldenamen.   

### <a name="for-azure-sql-database"></a>Für Azure SQL-Datenbank:  
**Anforderungen für den neuen Besitzer:**   
Der neue Besitzerprinzipal muss einer der folgenden sein:  
-   Ein Anmeldename für die SQL Server-Authentifizierung  
-   Ein Verbundbenutzer (keine Gruppe) in Azure AD  
-   Ein verwalteter Benutzer (keine Gruppe) oder eine Anwendung in Azure AD    

> [!NOTE]  
> Wenn der neue Besitzer ein Azure Active Directory-Benutzer ist, darf dieser Benutzer nicht in der Datenbank vorhanden sein, für die der neue Besitzer der DBO werden soll. Der Azure AD-Benutzer muss zunächst aus der Datenbank entfernt werden, bevor die ALTER AUTHORIZATION-Anweisung ausgeführt wird, die den Datenbankbesitz auf den neuen Benutzer überträgt. Weitere Informationen zum Konfigurieren eines Azure Active Directory-Benutzers finden Sie unter [Verwenden der Azure Active Directory-Authentifizierung für die Authentifizierung mit SQL-Datenbank oder SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
**Anforderungen an die Person, die die ALTER AUTHORIZATION-Anweisung ausführt:**  
Sie müssen eine Verbindung zur Zieldatenbank herstellen, um den Besitzer der Datenbank zu ändern.  

Die folgenden Kontotypen können den Besitzer einer Datenbank ändern. 
* Der Prinzipalanmeldename auf Serverebene (Der SQL Azure-Administrator, der bei der Erstellung des logischen Servers bereitgestellt wird.)  
* Der Active Directory-Administrator für den Azure SQL-Server   
* Der aktuelle Besitzer der Datenbank   
 
  
In der folgenden Tabelle werden die Anforderungen zusammengefasst:  
  
Ausführendes Konto  |Ziel  |Ergebnis    
---------|---------|---------  
Ein Anmeldename für die SQL Server-Authentifizierung     |Ein Anmeldename für die SQL Server-Authentifizierung         |Success  
Ein Anmeldename für die SQL Server-Authentifizierung     |Azure AD-Benutzer         |Fehler           
Azure AD-Benutzer     |Ein Anmeldename für die SQL Server-Authentifizierung         |Success           
Azure AD-Benutzer     |Azure AD-Benutzer         |Success           
  
Um den Azure AD-Besitzer der Datenbank zu bestätigen, führen Sie den folgenden Transact-SQL-Befehl in einer Benutzerdatenbank aus (in diesem Beispiel `testdb`).  
    
```    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
Die Ausgabe besteht aus einem Bezeichner (z.B. 6D8B81F6-7C79-444C-8858-4AF896C03C67), der der `richel@cqclinic.onmicrosoft.com` zugewiesenen Azure AD-ObjectID entspricht.  
Wenn ein Benutzeranmeldename für die SQL Server-Authentifizierung der Datenbankbesitzer ist, führen Sie die folgende Anweisung in der Masterdatenbank aus, um den Datenbankbesitzer zu bestätigen:  
    
```    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>Bewährte Methoden  
  
Statt Azure AD-Benutzer als einzelne Datenbankbesitzer zu verwenden, verwenden Sie eine Azure AD-Gruppe als Mitglied der festen Datenbankrolle **db_owner**. In den folgenden Schritten wird gezeigt, wie ein deaktivierter Anmeldename als Datenbankbesitzer und eine Azure Active Directory-Gruppe (`mydbogroup`) als Mitglied der **db_owner**-Rolle konfiguriert wird. 
1.  Melden Sie sich als Azure AD-Administrator bei SQL Server an, und ändern Sie den Datenbankbesitzer in einen deaktivierten Anmeldenamen für die SQL Server-Authentifizierung. Führen Sie über die Benutzerdatenbank z.B. Folgendes aus:  
  ```    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```    
2.  Erstellen Sie eine Azure AD-Gruppe, die Datenbankbesitzer werden soll, und fügen Sie sie als Benutzer zur Benutzerdatenbank hinzu. Zum Beispiel:  
  ```    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```    
3.  Fügen Sie den Benutzer, der die Azure AD-Gruppe darstellt, in der Benutzerdatenbank zur festen Datenbankrolle **db_owner** hinzu. Zum Beispiel:  
  ```    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
Nun können die `mydbogroup`-Mitglieder die Datenbank als Mitglieder der **db_owner**-Rolle zentral verwalten.  
- Wenn Mitglieder dieser Gruppe aus der Azure AD-Gruppe entfernt werden, verlieren sie automatisch die DBO-Berechtigungen für diese Datenbank.  
- Auch wenn neue Mitglieder zur `mydbogroup`-Azure AD-Gruppe hinzugefügt werden, erhalten sie automatisch DBO-Zugriff auf diese Datenbank.  
  
Um festzustellen, ob ein bestimmter Benutzer über die effektive DBO-Berechtigung verfügt, muss der Benutzer folgende Anweisung ausführen:  
    
```    
SELECT IS_MEMBER ('db_owner');  
```    
  
Lautet der Rückgabewert 1, bedeutet dies, dass der Benutzer ein Mitglied der Rolle ist.  
   
    
## <a name="permissions"></a>Berechtigungen    
 Erfordert die TAKE OWNERSHIP-Berechtigung für die Entität. Falls der neue Besitzer nicht der Benutzer ist, der diese Anweisung ausführt, ist zudem eine der folgenden Berechtigungen erforderlich: 1) IMPERSONATE-Berechtigung für den neuen Besitzer, falls es sich um einen Benutzer oder einen Anmeldenamen handelt. Oder: 2) Falls der neue Besitzer eine Rolle ist, Mitgliedschaft in der Rolle oder ALTER-Berechtigung in der Rolle. Oder: 3) Falls der neue Besitzer eine Anwendungsrolle ist, ALTER-Berechtigung in der Anwendungsrolle.    
    
## <a name="examples"></a>Beispiele    
    
### <a name="a-transfer-ownership-of-a-table"></a>A. Übertragen des Besitzes einer Tabelle    
 Im folgenden Beispiel wird der Besitz der `Sprockets`-Tabelle an den Benutzer `MichikoOsada` übertragen. Die Tabelle befindet sich im `Parts`-Schema.    
    
```    
ALTER AUTHORIZATION ON OBJECT::Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 Die Abfrage kann auch folgendermaßen aussehen:    
    
```    
ALTER AUTHORIZATION ON Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 Wenn das Objektschema kein Bestandteil der Anweisung ist, sucht die [!INCLUDE[ssDE](../../includes/ssde-md.md)] das Objekt im Standardschema des Benutzers. Zum Beispiel:    
    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
```    
    
### <a name="b-transfer-ownership-of-a-view-to-the-schema-owner"></a>B. Übertragen des Besitzes einer Sicht an den Schemabesitzer    
 Im folgenden Beispiel wird der Besitz der `ProductionView06`-Sicht an den Besitzer des Schemas übertragen, das sie enthält. Die Sicht befindet sich im `Production`-Schema.    
    
```    
ALTER AUTHORIZATION ON OBJECT::Production.ProductionView06 TO SCHEMA OWNER;    
GO    
```    
    
### <a name="c-transfer-ownership-of-a-schema-to-a-user"></a>C. Übertragen des Besitzes eines Schemas an einen Benutzer    
 Im folgenden Beispiel wird der Besitz des `SeattleProduction11`-Schemas an den Benutzer `SandraAlayo` übertragen.    
    
```    
ALTER AUTHORIZATION ON SCHEMA::SeattleProduction11 TO SandraAlayo;    
GO    
```    
    
### <a name="d-transfer-ownership-of-an-endpoint-to-a-sql-server-login"></a>D. Übertragen des Besitzes für einen Endpunkt an einen SQL Server-Anmeldenamen    
 Im folgenden Beispiel wird der Besitz des `CantabSalesServer1`-Endpunkts auf `JaePak` übertragen. Da es sich bei dem Endpunkt um ein sicherungsfähiges Element auf Serverebene handelt, kann der Endpunkt nur an einen Prinzipal auf Serverebene übertragen werden.    
    
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].    
    
```    
ALTER AUTHORIZATION ON ENDPOINT::CantabSalesServer1 TO JaePak;    
GO    
```    
    
### <a name="e-changing-the-owner-of-a-table"></a>E. Ändern eines Tabellenbesitzers    
 In jedem der folgenden Beispiele wird der Besitzer der `Sprockets`-Tabelle in der `Parts`-Datenbank in den Datenbankbenutzer `MichikoOsada` geändert.    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>F. Ändern eines Datenbankbesitzers    
 **GILT FÜR:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]    
    
 Im folgenden Beispiel wird der Besitzer der `Parts`-Datenbank in den Anmeldenamen `MichikoOsada` geändert.    
    
```    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>G. Ändern des Besitzers einer SQL-Datenbank in einen Azure AD-Benutzer  
Im folgenden Beispiel kann ein Azure Active Directory-Administrator für SQL Server in einer Organisation mit einer Active Directory namens `cqclinic.onmicrosoft.com` den aktuellen Besitzer der Datenbank `targetDB` ändern und den AAD-Benutzer `richel@cqclinic.onmicorsoft.com` zum neuen Datenbankbesitzer machen. Dazu muss er den folgenden Befehl ausführen:  
    
```    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 Beachten Sie, dass die Klammern um den Benutzernamen bei Azure AD-Benutzern verwendet werden müssen.  
  
    
## <a name="see-also"></a>Weitere Informationen finden Sie unter    
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 
