---
title: ALTER SCHEMA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs: TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 30ef553ccfba1f30be9b75f8d0290115be395925
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Überträgt ein sicherungsfähiges Element zwischen Schemas.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name eines Schemas in der aktuellen Datenbank, in das das sicherungsfähige Element verschoben wird. Kann weder SYS noch INFORMATION_SCHEMA sein.  
  
 \<entity_type>  
 Die Klasse der Entität, für die der Besitzer geändert wird. Object ist der Standardwert.  
  
 *securable_name*  
 Ist die einteiligen oder zweiteiligen Namen von einem Schemabereich sicherungsfähigen Elements, das in das Schema verschoben werden.  
  
## <a name="remarks"></a>Hinweise  
 Benutzer und Schemas vollkommen voneinander getrennt.  
  
 ALTER SCHEMA kann nur zum Verschieben von sicherungsfähigen Elementen zwischen Schemas in derselben Datenbank verwendet werden. Zum Ändern oder Löschen eines sicherungsfähigen Elements in einem Schema verwenden Sie die für das sicherungsfähige Element spezifische ALTER- oder DROP-Anweisung.  
  
 Wenn ein einteiliger Name verwendet wird, für die *Securable_name*, die Regeln für die Auflösung von Namen derzeit gültigen werden verwendet, um das sicherungsfähige Element zu suchen.  
  
 Alle dem sicherungsfähigen Element zugeordneten Berechtigungen werden gelöscht, wenn das sicherungsfähige Element in das neue Schema verschoben wird. Wurde der Besitzer des sicherungsfähigen Elements explizit festgelegt, bleibt der Besitzer unverändert. Wenn der Besitzer des sicherungsfähigen Elements auf SCHEMA OWNER festgelegt wurde, bleibt diese Einstellung zunächst erhalten. Nach dem Verschieben wird SCHEMA OWNER jedoch zum Besitzer des neuen Schemas aufgelöst. principal_id des neuen Besitzers ist NULL.  
  
 Verschieben eine gespeicherte Prozedur, Funktion, Sicht oder Trigger wird der Schemaname nicht ändern, wenn vorhanden, der das entsprechende entweder in der definitionsspalte der Objekt der [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht oder erhalten hat, mithilfe der [ OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) integrierte Funktion. Aus diesem Grund wird empfohlen, ALTER SCHEMA nicht verwendet werden, um diese Objekttypen zu verschieben. Löschen Sie stattdessen auf, und das Objekt in das neue Schema neu erstellen.  
  
 Das Verschieben eines Objekts, z. B. eine Tabelle oder ein Synonym werden Verweise auf dieses Objekt nicht automatisch aktualisiert. Sie müssen Objekte ändern, die das übertragene Objekt, manuell verweisen. Wenn Sie eine Tabelle verschieben, und diese Tabelle in einem Trigger verwiesen wird, müssen Sie z. B. den Trigger entsprechend den neuen Schemanamen ändern. Verwendung [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) für eine Liste der Abhängigkeiten für das Objekt vor dem verschieben.  

 So ändern Sie das Schema einer Tabelle mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Objekt-Explorer mit der Maustaste auf die Tabelle, und klicken Sie dann auf **Entwurf**. Drücken Sie **F4** um das Eigenschaftenfenster zu öffnen. In der **Schema** wählen ein neues Schema.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Übertragung eines sicherungsfähigen Elements aus einem anderen Schema benötigt der aktuelle Benutzer die CONTROL-Berechtigung für das sicherungsfähige Element (nicht das Schema) sowie die ALTER-Berechtigung für das Zielschema.  
  
 Wenn das sicherungsfähige Element weist eine EXECUTE AS OWNER-Spezifikation auf, und der Besitzer auf SCHEMA OWNER festgelegt ist, muss der Benutzer auch auf den Besitzer des Zielschemas IMPERSONATE-Berechtigung verfügen.  
  
 Alle dem sicherungsfähigen Element, das übertragen wird, zugeordneten Berechtigungen werden gelöscht, wenn es verschoben wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-transferring-ownership-of-a-table"></a>A. Übertragen des Besitzes einer Tabelle  
 Im folgenden Beispiel wird das `HumanResources`-Schema durch Übertragen der `Address`-Tabelle aus dem `Person`-Schema in das Schema geändert.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>B. Übertragen des Besitzes eines Typs  
 Im folgenden Beispiel wird ein Typ im `Production`-Schema erstellt und dann an das `Person`-Schema übertragen.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [varchar](10) NOT NULL ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
  
-- Change the type to the Person schema.  
ALTER SCHEMA Person TRANSFER type::Production.TestType ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>C. Übertragen des Besitzes einer Tabelle  
 Im folgende Beispiel wird eine Tabelle erstellt `Region` in der `dbo` Schema erstellt eine `Sales` Schema, und klicken Sie dann wechselt der `Region` Tabelle aus der `dbo` Schema, um die `Sales` Schema.  
  
```  
CREATE TABLE dbo.Region   
    (Region_id int NOT NULL,  
    Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

