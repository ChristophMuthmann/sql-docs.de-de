---
title: ALTER AUTHORIZATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31738dcb4eaf4676b4c0a34b13ee400e89333428
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

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
\<Class_type > ist der sicherungsfähige Klasse der Entität, für die der Besitzer geändert werden. OBJECT ist der Standardwert.    
    
|||    
|-|-|    
|OBJECT|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Datawarehouse, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|    
|ASSEMBLY|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|ASYMMETRIC KEY|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|AVAILABILITY GROUP |**GILT für**: SQLServer 2012 durch [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|CERTIFICATE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|CONTRACT|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|DATABASE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Weitere Informationen finden Sie unter [ALTER AUTHORIZATION für Datenbanken](#AlterDB) Abschnitt weiter unten.|    
|ENDPOINT|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|FULLTEXT CATALOG|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|FULLTEXT STOPLIST|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|MESSAGE TYPE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|REMOTE SERVICE BINDING|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|ROLE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|ROUTE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|SCHEMA|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Datawarehouse, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|    
|SEARCH PROPERTY LIST|**GILT für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|SERVER ROLE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|SERVICE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|    
|SYMMETRIC KEY|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|TYPE|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|XML SCHEMA COLLECTION|**GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
    
 *entity_name*    
 Der Name der Entität.    
    
 *Principal_name* | SCHEMABESITZER    
 Name des Sicherheitsprinzipals, der die Entität besitzt. Datenbankobjekte müssen im Besitz eines Datenbankprinzipals sein, also ein Datenbankbenutzer oder eine Datenbankrolle. Serverobjekte (beispielsweise Datenbanken) müssen im Besitz eines Serverprinzipals (eines Anmeldenamens) sein. Geben Sie **SCHEMABESITZER** als die *Principal_name* um anzugeben, dass der Prinzipal Besitzer des Objekts werden sollte, der das Schema des Objekts besitzt.    
    
## <a name="remarks"></a>Hinweise    
 Mit ALTER AUTHORIZATION kann der Besitz einer Entität, die einen Besitzer aufweist, geändert werden. Der Besitz von in der Datenbank enthaltenen Entitäten kann an jeden Prinzipal auf Datenbankebene übertragen werden. Der Besitz von Entitäten auf Serverebene kann nur an Prinzipale auf Serverebene übertragen werden.    
    
> [!IMPORTANT]    
>  Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] kann der Benutzer Besitzer eines Objekts oder Typs sein, das bzw. der in einem Schema enthalten ist, dessen Besitzer ein anderer Datenbankbenutzer ist. Dieses Verhalten unterscheidet sich von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [OBJECTPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/objectproperty-transact-sql.md) und [TYPEPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/typeproperty-transact-sql.md).    
    
 Der Besitz der folgenden in einem Schema enthaltenen Entitäten vom Typ "object" kann übertragen werden: Tabellen, Sichten, Funktionen, Prozeduren, Warteschlangen und Synonyme.    
    
 Der Besitz der folgenden Entitäten kann nicht übertragen werden: Verbindungsserver, Statistiken, Einschränkungen, Regeln, Standardwerte, Trigger, [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Warteschlangen, Anmeldeinformationen, Partitionsfunktionen, Partitionsschemas, Datenbank-Hauptschlüssel, Diensthauptschlüssel und Ereignisbenachrichtigungen.    
    
 Der Besitz von Mitgliedern der folgenden sicherungsfähigen Klassen kann nicht übertragen werden: Server, Anmeldename, Benutzer, Anwendungsrolle und Spalte.    
    
 Die SCHEMA OWNER-Option ist nur gültig, wenn Sie den Besitz einer in einem Schema enthaltenen Entität übertragen. Mit SCHEMA OWNER wird der Besitz der Entität an den Besitzer des Schemas übertragen, in dem sie sich befindet. Nur Entitäten der Klasse OBJECT, TYPE oder XML SCHEMA COLLECTION sind in Schemas enthalten.    
    
 Falls es sich bei der Zielentität nicht um eine Datenbank handelt und die Entität an einen neuen Besitzer übertragen wird, werden alle Berechtigungen für das Ziel gelöscht.    
    
> [!CAUTION]    
>  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], das Verhalten der Schemas geändert wird, vom Verhalten in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Code, in dem vorausgesetzt wird, dass Schemas Datenbankbenutzern entsprechen, gibt möglicherweise nicht die richtigen Ergebnisse zurück. Alte Katalogsichten, einschließlich Sysobjects, sollten nicht verwendet werden, in einer Datenbank, in denen eine der folgenden DDL jemals Anweisungen verwendet wurde: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. In einer Datenbank, in der jemals eine dieser Anweisungen verwendet wurde, müssen Sie die neuen Katalogsichten verwenden. Die neuen Katalogsichten berücksichtigen die Trennung zwischen Prinzipalen und Schemas, das in eingeführte [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Weitere Informationen zu Katalogansichten finden Sie unter [Catalog Views &#40;Transact-SQL&#41; (Katalogansichten (Transact-SQL))](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).    
    
 Beachten Sie dabei außerdem Folgendes:    
    
> [!IMPORTANT]    
>  Die einzig zuverlässige Möglichkeit, den Besitzer eines Objekts zu finden ist, um Abfrage der **sys.objects** -Katalogsicht angezeigt. Die einzige zuverlässige Möglichkeit, den Besitzer eines Typs zu finden, besteht in der Verwendung der TYPEPROPERTY-Funktion.    
    
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
  
## <a name="AlterDB"></a>ALTER AUTHORIZATION für Datenbanken  
**GILT FÜR**: [!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
### <a name="for-sql-server"></a>Für SQLServer:  
**Anforderungen für den neuen Besitzer:**   
Der neue Prinzipal der Besitzer muss eine der folgenden sein:  
-   Eine SQL Server-authentifizierungsanmeldung.  
-   Eine Windows-authentifizierungsanmeldung, die einen Windows-Benutzer (und keiner Gruppe) darstellt.  
-   Ein Windows-Benutzer, der für die Authentifizierung über eine Windows-Anmeldung, Authentifizierung, die eine Windows-Gruppe darstellt.  
  
**Anforderungen für die Person, die die ALTER AUTHORIZATION-Anweisung ausführen:**  
Wenn Sie nicht Mitglied der sind die **Sysadmin** festen Serverrolle, benötigen Sie mindestens TAKE OWNERSHIP-Berechtigung für die Datenbank und benötigen IMPERSONATE-Berechtigung für den neuen Besitzer Anmeldenamen.   

### <a name="for-azure-sql-database"></a>Für Azure SQL-Datenbank:  
**Anforderungen für den neuen Besitzer:**   
Der neue Prinzipal der Besitzer muss eine der folgenden sein:  
-   Eine SQL Server-authentifizierungsanmeldung.  
-   Ein Verbundbenutzer (keine Gruppe) in Azure AD vorhanden.  
-   Ein verwalteter Benutzer (keine Gruppe) oder eine Anwendung in Azure AD vorhanden.    

> [!NOTE]  
> Wenn der neue Besitzer, Azure Active Directory-Benutzer ist, nicht als Benutzer in der Datenbank vorhanden sein, in dem der neue Besitzer der neuen DBO werden soll. Derartige Azure AD-Benutzer muss vor dem Ausführen der ALTER AUTHORIZATION-Anweisung, die den Datenbankbesitz ändern, auf den neuen Benutzer zunächst aus der Datenbank entfernt werden. Weitere Informationen zum Konfigurieren einer Azure Active Directory-Benutzer mit SQL-Datenbank finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank oder SQL Data Warehouse durch Verwenden von Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
**Anforderungen für die Person, die die ALTER AUTHORIZATION-Anweisung ausführen:**  
Sie müssen in die Zieldatenbank zum Ändern des Besitzers der Datenbank verbinden.  

Die folgenden Kontotypen können den Besitzer einer Datenbank ändern. 
* Der Dienst serverebenenprinzipal-Anmeldung. (Der SQL Azure-Administrator bereitgestellt werden, wenn der logische Server erstellt wurde.)  
* Der Azure Active Directory-Administrator für den Azure SQL-Server.   
* Der aktuelle Besitzer der Datenbank.   
 
  
In der folgenden Tabelle werden die Anforderungen zusammengefasst:  
  
Executor  |Target  |Ergebnis    
---------|---------|---------  
SQL Server-authentifizierungsanmeldung     |SQL Server-authentifizierungsanmeldung         |Success  
SQL Server-authentifizierungsanmeldung     |Azure AD-Benutzer         |Fehler           
Azure AD-Benutzer     |SQL Server-authentifizierungsanmeldung         |Success           
Azure AD-Benutzer     |Azure AD-Benutzer         |Success           
  
So überprüfen ein Azure AD-Besitzer der Datenbank, führen Sie den folgenden Transact-SQL-Befehl in einer Benutzerdatenbank (in diesem Beispiel `testdb`).  
    
```    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
Die Ausgabe ist ein Bezeichner (z. B. 6D8B81F6-7C79-444C-8858-4AF896C03C67) die zugewiesene Azure AD-ObjectID entspricht`richel@cqclinic.onmicrosoft.com`  
Wenn eine SQL Server-Authentifizierung angemeldeter Benutzer der Besitzer der Datenbank ist, führen Sie die folgende Anweisung in der Masterdatenbank, um zu überprüfen, ob den Datenbankbesitzer ein:  
    
```    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>Bewährte Methoden  
  
Verwenden Sie anstelle von Azure AD-Benutzer als einzelne Besitzer der Datenbank, eine Azure AD-Gruppe als Mitglied der **Db_owner** festen Datenbankrolle "". Die folgenden Schritte zeigen, wie zum Konfigurieren einer deaktivierten Anmeldung als Besitzer der Datenbank, und stellen eine Azure Active Directory-Gruppe (`mydbogroup`) ein Mitglied der **Db_owner** Rolle. 
1.  Melden Sie sich an SQL Server mit Azure AD-Administrator, und ändern Sie den Besitzer der Datenbank, die ein deaktivierter Anmeldename der SQL Server-Authentifizierung an. Führen Sie z. B. aus der Benutzerdatenbank:  
  ```    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```    
2.  Erstellen einer Azure AD-Gruppe, die Besitzer der Datenbank und als ein Benutzer mit der Benutzerdatenbank hinzufügen sollten. Beispiel:  
  ```    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```    
3.  Fügen Sie den Benutzer, die die Azure AD-Gruppe zu darstellt, in der Benutzerdatenbank die **Db_owner** festen Datenbankrolle "". Beispiel:  
  ```    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
Jetzt die `mydbogroup` Mitglieder können zentral verwalten die Datenbank als Mitglied der **Db_owner** Rolle.  
- Mitglieder dieser Gruppe aus der Azure AD-Gruppe entfernt werden, verlieren sie automatisch die Dbo-Berechtigungen für diese Datenbank.  
- Auf ähnliche Weise, wenn neue Elemente hinzugefügt werden `mydbogroup` Azure AD-Gruppe, sie erhalten automatisch die Dbo-Zugriff für diese Datenbank.  
  
Um festzustellen, ob ein bestimmter Benutzer die effektive Dbo-Berechtigungen verfügt, haben Sie den Benutzer die folgende Anweisung ausführen:  
    
```    
SELECT IS_MEMBER ('db_owner');  
```    
  
Der Rückgabewert 1 gibt an, dass der Benutzer ein Mitglied der Rolle ist.  
   
    
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
    
 Wenn das Schema Objekte nicht Bestandteil der Anweisung, ist der [!INCLUDE[ssDE](../../includes/ssde-md.md)] für das Objekt im Standardschema Benutzer sieht. Beispiel:    
    
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
    
### <a name="e-changing-the-owner-of-a-table"></a>E. Das Ändern des Besitzers einer Tabelle    
 Jede der in den folgenden Beispielen ändert den Besitzer der `Sprockets` -Tabelle in der `Parts` Datenbank dem Datenbankbenutzer `MichikoOsada`.    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>F. Das Ändern des Besitzers einer Datenbank    
 **GILT für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].    
    
 Im folgende Beispiel Ändern des Besitzers der `Parts` Datenbank für die Anmeldung `MichikoOsada`.    
    
```    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>G. Das Ändern des Besitzers einer SQL-Datenbank in einem Azure AD-Benutzer  
Im folgenden Beispiel wird ein Azure Active Directory-Administrator für SQL Server in einer Organisation mit einer active Directory mit dem Namen `cqclinic.onmicrosoft.com`, kann der aktuelle Besitzer einer Datenbank ändern `targetDB` und einen AAD-Benutzer stellen `richel@cqclinic.onmicorsoft.com` die neue Datenbank der Besitzer mit dem folgenden Befehl:  
    
```    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 Beachten Sie, dass für Azure AD-Benutzer die Klammern um den Benutzernamen verwendet werden müssen.  
  
    
## <a name="see-also"></a>Siehe auch    
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 

