---
title: ALTER SCHEMA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad157c7d4d7b92bc199c4a490d4387acc0af0908
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
  
 \<Entity_type >  
 Die Klasse der Entität, für die der Besitzer geändert wird. Object ist der Standardwert.  
  
 *securable_name*  
 Bezeichnet den ein- oder zweiteiligen Namen eines sicherungsfähigen Elements mit Schemabereich, das in das Schema verschoben werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Benutzer und Schemas vollkommen voneinander getrennt.  
  
 ALTER SCHEMA kann nur zum Verschieben von sicherungsfähigen Elementen zwischen Schemas in derselben Datenbank verwendet werden. Zum Ändern oder Löschen eines sicherungsfähigen Elements in einem Schema verwenden Sie die für das sicherungsfähige Element spezifische ALTER- oder DROP-Anweisung.  
  
 Wenn ein einteiliger Name verwendet wird, für die *Securable_name*, die Regeln für die Auflösung von Namen derzeit gültigen werden verwendet, um das sicherungsfähige Element zu suchen.  
  
 Alle dem sicherungsfähigen Element zugeordneten Berechtigungen werden gelöscht, wenn das sicherungsfähige Element in das neue Schema verschoben wird. Wurde der Besitzer des sicherungsfähigen Elements explizit festgelegt, bleibt der Besitzer unverändert. Wenn der Besitzer des sicherungsfähigen Elements auf SCHEMA OWNER festgelegt wurde, bleibt diese Einstellung zunächst erhalten. Nach dem Verschieben wird SCHEMA OWNER jedoch zum Besitzer des neuen Schemas aufgelöst. principal_id des neuen Besitzers ist NULL.  
  
 So ändern Sie das Schema einer Tabelle oder Sicht mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], im Objekt-Explorer mit der Maustaste die Tabelle oder Sicht, und klicken Sie dann auf **Entwurf**. Drücken Sie **F4** um das Eigenschaftenfenster zu öffnen. In der **Schema** wählen ein neues Schema.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Übertragung eines sicherungsfähigen Elements aus einem anderen Schema benötigt der aktuelle Benutzer die CONTROL-Berechtigung für das sicherungsfähige Element (nicht das Schema) sowie die ALTER-Berechtigung für das Zielschema.  
  
 Verfügt das sicherungsfähige Element über eine EXECUTE AS OWNER-Spezifikation und der Benutzer ist als SCHEMA OWNER festgelegt, benötigt der Benutzer auch die IMPERSONATION-Berechtigung für den Besitzer des Zielschemas.  
  
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
 [Erstellen Sie SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


