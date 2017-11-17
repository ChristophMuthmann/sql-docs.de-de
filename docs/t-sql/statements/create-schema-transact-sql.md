---
title: Erstellen von SCHEMAS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/01/2016
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
- CREATE_SCHEMA_TSQL
- SCHEMA
- CREATE SCHEMA
- SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], schemas
- table creation [SQL Server], CREATE SCHEMA statement
- permissions [SQL Server], schemas
- schemas [SQL Server], creating
- CREATE SCHEMA statement
ms.assetid: df74fc36-20da-4efa-b412-c4e191786695
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 58eaf0c325ab4884dfe1e67ae0b0889a2ca6769a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-schema-transact-sql"></a>CREATE SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt ein Schema in der aktuellen Datenbank. Mit der CREATE SCHEMA-Transaktion können auch Tabellen und Sichten innerhalb des neuen Schemas erstellt und GRANT-, DENY- oder REVOKE-Berechtigungen für diese Objekte festgelegt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE SCHEMA schema_name_clause [ <schema_element> [ ...n ] ]  
  
<schema_name_clause> ::=  
    {  
    schema_name  
    | AUTHORIZATION owner_name  
    | schema_name AUTHORIZATION owner_name  
    }  
  
<schema_element> ::=   
    {   
        table_definition | view_definition | grant_statement |   
        revoke_statement | deny_statement   
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE SCHEMA schema_name [ AUTHORIZATION owner_name ] [;]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name, mit dem das Schema innerhalb der Datenbank identifiziert wird.  
  
 Autorisierung *Owner_name*  
 Gibt den Namen des Prinzipals auf Datenbankebene an, der der Besitzer des Schemas ist. Dieser Prinzipal kann andere Schemas besitzen und verwendet das aktuelle Schema möglicherweise nicht als Standardschema.  
  
 *Table_Definition*  
 Gibt eine CREATE TABLE-Anweisung an, die eine Tabelle in dem Schema erstellt. Der Prinzipal, der diese Anweisung ausführt, benötigt die CREATE TABLE-Berechtigung für die aktuelle Datenbank.  
  
 *view_definition*  
 Gibt eine CREATE VIEW-Anweisung an, die eine Sicht in dem Schema erstellt. Der Prinzipal, der diese Anweisung ausführt, benötigt die CREATE VIEW-Berechtigung für die aktuelle Datenbank.  
  
 *grant_statement*  
 Gibt eine GRANT-Anweisung an, die Berechtigungen für jedes sicherungsfähige Element außer dem neuen Schema erteilt.  
  
 *revoke_statement*  
 Gibt eine REVOKE-Anweisung an, die Berechtigungen für jedes sicherungsfähige Element außer dem neuen Schema aufhebt.  
  
 *deny_statement*  
 Gibt eine DENY-Anweisung an, die Berechtigungen für jedes sicherungsfähige Element außer dem neuen Schema verweigert.  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]  
>  Anweisungen, die CREATE SCHEMA AUTHORIZATION enthalten, aber kein Name angegeben ist, sind nur für Abwärtskompatibilität zulässig. Die Anweisung verursacht zwar keinen Fehler, erstellt aber auch kein Schema.  
  
 Mit CREATE SCHEMA können ein Schema und die darin enthaltenen Tabellen und Sichten sowie die Berechtigungen GRANT, REVOKE oder DENY für jedes sicherungsfähige Element in einer einzelnen Anweisung erstellt werden. Diese Anweisung muss als separater Batch ausgeführt werden. Mit der CREATE SCHEMA-Anweisung erstellte Objekte werden innerhalb des zu erstellenden Schemas erstellt.  
  
 CREATE SCHEMA-Transaktionen sind atomar. Wenn während der Ausführung einer CREATE SCHEMA-Anweisung ein Fehler auftritt, werden keine der angegebenen sicherungsfähigen Elemente erstellt, und es werden keine Berechtigungen erteilt.  
  
 Die von CREATE SCHEMA zu erstellenden sicherungsfähigen Elemente können in einer beliebigen Reihenfolge aufgelistet werden, außer bei Sichten, die auf andere Sichten verweisen. In diesem Fall muss die Sicht, auf die verwiesen wird, vor der verweisenden Sicht erstellt werden.  
  
 Deshalb kann eine GRANT-Anweisung eine Berechtigung für ein Objekt erteilen, bevor das Objekt selbst erstellt wird. Ebenso kann eine CREATE VIEW-Anweisung vor den entsprechenden CREATE TABLE-Anweisungen auftreten, die die Tabellen erstellen, auf die die Sicht verweist. CREATE TABLE-Anweisungen können darüber hinaus Fremdschlüssel für Tabellen deklarieren, die später in der CREATE SCHEMA-Anweisung definiert werden.  
  
> [!NOTE]  
>  DENY und REVOKE werden in CREATE SCHEMA-Anweisungen unterstützt. DENY- und REVOKE-Klauseln werden in der Reihenfolge ausgeführt, in der sie in der CREATE SCHEMA-Anweisung angezeigt werden.  
  
 Der Prinzipal, der CREATE SCHEMA ausführt, kann einen anderen Datenbankprinzipal als Besitzer des erstellten Schemas angeben. Dies erfordert zusätzliche Berechtigungen, die im Abschnitt "Berechtigungen" weiter unten in diesem Thema beschrieben werden.  
  
 Das neue Schema ist im Besitz einer der folgenden Prinzipale auf Datenbankebene: Datenbankbenutzer, Datenbankrolle oder Anwendungsrolle. Objekte, die innerhalb eines Schemas erstellt werden, gehören dem Besitzer des Schemas und haben für **principal_id** in **sys.objects**einen NULL-Wert. Der Besitz von Objekten, die Schemas als Bereich aufweisen, kann an jeden Prinzipal auf Datenbankebene übertragen werden, aber der Schemabesitzer behält immer die CONTROL-Berechtigung für Objekte innerhalb des Schemas.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 **Implizites Schema und Benutzererstellung**  
  
 In bestimmten Fällen kann ein Benutzer eine Datenbank verwenden, ohne ein Datenbankbenutzerkonto (einen Datenbankprinzipal in der Datenbank) zu besitzen. Das ist in den folgenden Situationen möglich:  
  
-   Eine Anmeldung besitzt **CONTROL SERVER** Berechtigungen.  
  
-   Ein Windows-Benutzer hat kein individuelles Datenbankbenutzerkonto (einen Datenbankprinzipal in der Datenbank), greift jedoch als Mitglied einer Windows-Gruppe, die ein Datenbankbenutzerkonto (einen Datenbankprinzipal für die Windows-Gruppe) besitzt, auf eine Datenbank zu.  
  
 Wenn ein Benutzer ohne Datenbankbenutzerkonto ein Objekt erstellt, ohne ein vorhandenes Schema anzugeben, werden für diesen Benutzer automatisch ein Datenbankprinzipal und ein Standardschema in der Datenbank erstellt. Der erstellte Datenbankprinzipal und das erstellte Schema weisen den Namen auf, den der Benutzer bei der Herstellung der Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet hat (der Anmeldenamen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung oder der Windows-Benutzername).  
  
 Dieses Verhalten ist erforderlich, damit auf Windows-Gruppen basierende Benutzer Objekte erstellen und besitzen können. Es kann jedoch zur unbeabsichtigten Erstellung von Schemata und Benutzern führen. Um das implizite Erstellen von Benutzern und Schemata tu vermeiden, sollten Sie soweit möglich Datenbankprinzipale explizit erstellen und ein Standardschema zuweisen. Oder geben Sie bei der Erstellung von Objekten in einer Datenbank explizit ein vorhandenes Schema anhand von zwei- oder dreiteiligen Objektnamen an.  

>  [!NOTE]
>  Die implizite Erstellung von Azure Active Directory-Benutzer ist nicht möglich, auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. Da den Status der Benutzer in der AAD Erstellen eines Azure AD-Benutzers von externen Anbieter überprüfen muss, Erstellen des Benutzers schlägt fehl mit Fehler 2760: **der angegebene Schemaname "\<user_name@domain>" ist nicht vorhanden oder Sie verfügen nicht über die Berechtigung, ihn zu verwenden.** Und klicken Sie dann die Fehler 2759: **Fehler bei CREATE SCHEMA wegen vorheriger Fehler.** Um diese Fehler zu umgehen, erstellen Sie Azure AD-Benutzers vom externen Anbieter zunächst, und führen Sie die Anweisung, die beim Erstellen des Objekts.
 
  
## <a name="deprecation-notice"></a>Hinweis zur Abwärtskompatibilität  
 CREATE SCHEMA-Anweisungen, die keinen Schemanamen angeben, werden derzeit aus Gründen der Abwärtskompatibilität unterstützt. Solche Anweisungen erstellen kein Schema in der Datenbank, sondern Tabellen und Sichten, und sie erteilen Berechtigungen. Prinzipale benötigen die CREATE SCHEMA-Berechtigung nicht zum Ausführen dieser älteren Version von CREATE SCHEMA, weil kein Schema erstellt wird. Diese Funktionalität wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr bereitgestellt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE SCHEMA-Berechtigung für die Datenbank.  
  
 Zum Erstellen eines in der CREATE SCHEMA-Anweisung angegebenen Objekts muss der Benutzer über die entsprechende CREATE-Berechtigung verfügen.  
  
 Um einen anderen Benutzer als den Besitzer des zu erstellenden Schemas anzugeben, benötigt der Aufrufer die IMPERSONATE-Berechtigung für diesen Benutzer. Wenn eine Datenbankrolle als Besitzer angegeben wird, muss der Aufrufer entweder über eine Mitgliedschaft in der Rolle oder die ALTER-Berechtigung für die Rolle verfügen.  
  
> [!NOTE]  
>  Für die Abwärtskompatibilitätssyntax werden keine Berechtigungen für CREATE SCHEMA überprüft, weil kein Schema erstellt wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-schema-and-granting-permissions"></a>A. Erstellen eines Schemas und Benutzern Berechtigungen erteilen  
 Das folgende Beispiel erstellt das `Sprockets`-Schema, das im Besitz von `Annik` ist und die `NineProngs`-Tabelle enthält. Die Anweisung erteilt die `SELECT`-Berechtigung für `Mandar` und verweigert die `SELECT`-Berechtigung für `Prasanna`. Beachten Sie, dass `Sprockets` und `NineProngs` in einer einzigen Anweisung erstellt werden.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE SCHEMA Sprockets AUTHORIZATION Annik  
    CREATE TABLE NineProngs (source int, cost int, partnumber int)  
    GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
    DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
GO   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-creating-a-schema-and-a-table-in-the-schema"></a>B. Erstellen ein Schema und eine Tabelle im schema  
 Das folgende Beispiel erstellt ein Schema `Sales` und erstellt dann eine Tabelle `Sales.Region` in diesem Schema.  
  
```  
CREATE SCHEMA Sales;  
GO;  
  
CREATE TABLE Sales.Region   
(Region_id int NOT NULL,  
Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
```  
  
### <a name="c-setting-the-owner-of-a-schema"></a>C. Festlegen des Besitzers eines Schemas  
 Das folgende Beispiel erstellt ein Schema `Production` Besitz `Mary`.  
  
```  
CREATE SCHEMA Production AUTHORIZATION [Contoso\Mary];  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [DROP SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sys.Schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [Erstellen eines Datenbankschemas](../../relational-databases/security/authentication-access/create-a-database-schema.md)  
  
  



