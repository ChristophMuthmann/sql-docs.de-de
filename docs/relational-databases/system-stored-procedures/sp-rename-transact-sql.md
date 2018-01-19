---
title: "\"Sp_rename\" (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_rename_TSQL
- sp_rename
dev_langs: TSQL
helpviewer_keywords:
- renaming indexes
- renaming columns
- sp_rename
- renaming tables
ms.assetid: bc3548f0-143f-404e-a2e9-0a15960fc8ed
caps.latest.revision: "54"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 158974d93e031d689318ea22f3bd0ba8189553ee
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sprename-transact-sql"></a>sp_rename (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ändert den Namen eines vom Benutzer erstellten Objekts in der aktuellen Datenbank. Dieses Objekt kann eine Tabelle, Index, Spalte Aliasdatentyp oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common Language Runtime (CLR) den benutzerdefinierten Typ.  
  
> [!CAUTION]  
>  Wenn Sie Teile eines Objektnamens ändern, können Skripts und gespeicherte Prozeduren funktionsunfähig werden. Es ist empfehlenswert, diese Anweisung nicht zum Umbenennen von gespeicherten Prozeduren, Triggern, benutzerdefinierten Funktionen oder Sichten zu verwenden. Löschen Sie stattdessen das Objekt, und erstellen Sie es neu mit dem neuen Namen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    [ , [ @objtype = ] 'object_type' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ @objname =] '*Object_name*"  
 Der aktuelle qualifizierte oder nicht qualifizierte Name des Benutzerobjekts oder Datentyps. Wenn es sich bei das umzubenennenden Objekt um eine Spalte in einer Tabelle ist *Object_name* muss im Format *table.column* oder *schema.table.column*. Wenn es sich bei das umzubenennenden Objekt um einen Index, muss *Object_name* muss im Format *table.index* oder *schema.table.index*. Wenn es sich bei das umzubenennenden Objekt um eine Einschränkung ist *Object_name* muss im Format *schema.constraint*.  
  
 Anführungszeichen sind nur dann notwendig, wenn ein qualifiziertes Objekt angegeben wird. Bei Angabe eines vollqualifizierten Namens, einschließlich eines Datenbanknamens, muss es sich bei dem Datenbanknamen um den Namen der aktuellen Datenbank handeln. *Object_name* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [ @newname = ] '*new_name*'  
 Der neue Name für das angegebene Objekt. *New_name* muss ein einteiliger Name sein und müssen den Regeln für Bezeichner entsprechen. *Newname* ist **Sysname**, hat keinen Standardwert.  
  
> [!NOTE]  
>  Namen von Triggern können nicht mit # oder ## beginnen.  
  
 [ @objtype = ] '*object_type*'  
 Der Typ des Objekts, das umbenannt wird. *Object_type* ist **varchar(13)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|COLUMN|Eine umzubenennende Spalte.|  
|DATABASE|Eine benutzerdefinierte Datenbank. Dieser Objekttyp ist erforderlich, wenn Sie eine Datenbank umbenennen.|  
|INDEX|Ein benutzerdefinierter Index. Beim Umbenennen eines Indizes mit Statistiken werden die Statistiken auch automatisch umbenannt.|  
|OBJECT|Ein Element eines Typs in nachverfolgte [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Beispielsweise könnte OBJECT zum Umbenennen von Objekten mit Einschränkungen (CHECK, FOREIGN KEY, PRIMARY/UNIQUE KEY), Benutzertabellen und Regeln verwendet werden.|  
|STATISTICS|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Explizit von einem Benutzer erstellte Statistiken oder implizit mit einem Index erstellt Beim Umbenennen der Statistiken eines Indizes wird der Index auch automatisch umbenannt.|  
|USERDATATYPE|Ein [CLR-benutzerdefinierte Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) dazu hinzugefügt [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) oder [Sp_addtype](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md).|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Zahl ungleich Null (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie können Objekte und Datentypen nur in der aktuellen Datenbank umbenennen. Die Namen der meisten Systemdatentypen und -objekte können nicht geändert werden.  
  
 sp_rename sorgt dafür, dass beim Umbenennen einer PRIMARY KEY- oder UNIQUE-Einschränkung automatisch auch der zugehörige Index umbenannt wird. Wenn ein umbenannter Index an eine PRIMARY KEY-Einschränkung gebunden ist, wird auch die PRIMARY KEY-Einschränkung automatisch von sp_rename umbenannt.  
  
 sp_rename kann zum Umbenennen von primären und sekundären XML-Indizes verwendet werden.  
  
 Umbenennen einer gespeicherten Prozedur, Funktion, Sicht oder Trigger ändert nicht dem Namen des entsprechenden Objekts in der definitionsspalte der der [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht oder erhalten hat, mithilfe der [OBJECT_ DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) integrierte Funktion. Daher ist es empfehlenswert, sp_rename nicht zum Umbenennen dieser Objekttypen zu verwenden. Löschen Sie stattdessen das Objekt, und erstellen Sie es neu mit dem neuen Namen.  
  
 Beim Umbenennen eines Objekts, wie z. B. einer Tabelle oder Spalte, werden Verweise auf das Objekt nicht automatisch umbenannt. Sie müssen Objekte, die auf das umbenannte Objekt verweisen, manuell ändern. Wenn Sie z. B. eine Tabellenspalte umbenennen und in einem Trigger auf diese Spalte verwiesen wird, müssen Sie den Trigger ändern, sodass er den neuen Spaltennamen wiedergibt. Verwenden Sie [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) , um Abhängigkeiten vom Objekt aufzulisten, bevor Sie es umbenennen.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Umbenennen von Objekten, Spalten und Indizes ist die ALTER-Berechtigung für das entsprechende Objekt erforderlich. Zum Umbenennen von Benutzertypen ist die CONTROL-Berechtigung für den entsprechenden Typ erforderlich. Zum Umbenennen einer Datenbank ist die Mitgliedschaft in der festen Serverrolle sysadmin oder dbcreator erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-renaming-a-table"></a>A. Umbenennen einer Tabelle  
 Im folgenden Beispiel wird die `SalesTerritory` -Tabelle im Schema `SalesTerr` in `Sales` umbenannt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
GO  
```  
  
### <a name="b-renaming-a-column"></a>B. Das Umbenennen einer Spalte  
 Im folgenden Beispiel wird die `TerritoryID` Spalte in der `SalesTerritory` Tabelle `TerrID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
GO  
```  
  
### <a name="c-renaming-an-index"></a>C. Umbenennen eines Indexes  
 Im folgenden Beispiel wird der `IX_ProductVendor_VendorID`-Index in `IX_VendorID` umbenannt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';  
GO  
```  
  
### <a name="d-renaming-an-alias-data-type"></a>D. Umbenennen eines Aliasdatentyps  
 Im folgenden Beispiel wird der `Phone`-Aliasdatentyp in `Telephone` umbenannt.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Phone', N'Telephone', N'USERDATATYPE';  
GO  
```  
  
### <a name="e-renaming-constraints"></a>E. Umbenennen von Einschränkungen  
 In den folgenden Beispielen wird eine PRIMARY KEY-Einschränkung, CHECK-Einschränkung und FOREIGN KEY-Einschränkung umbenannt. Beim Umbenennen einer Einschränkung muss das Schema angegeben werden, dem die Einschränkung angehört.  
  
```  
USE AdventureWorks2012;   
GO  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');   
GO  
  
-- Rename the primary key constraint.  
sp_rename 'HumanResources.PK_Employee_BusinessEntityID', 'PK_EmployeeID';  
GO  
  
-- Rename a check constraint.  
sp_rename 'HumanResources.CK_Employee_BirthDate', 'CK_BirthDate';  
GO  
  
-- Rename a foreign key constraint.  
sp_rename 'HumanResources.FK_Employee_Person_BusinessEntityID', 'FK_EmployeeID';  
  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');  
  
```  
  
```  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_Person_BusinessEntityID   HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_BusinessEntityID          HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_Employee_BirthDate                 HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_ID                        HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_ID                        HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_BirthDate                          HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
```  
  
### <a name="f-renaming-statistics"></a>F. Umbenennen von Statistiken  
 Im folgenden Beispiel erstellt eine Statistik-Objekt, das mit dem Namen contactMail1 und klicken Sie dann die Statistik zu NewContact mithilfe von "Sp_rename" umbenannt. Bei der Umbenennung von Statistiken muss das Objekt im Format schema.table.statistics_name angegeben werden.  
  
```  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
  
sp_rename 'Person.Person.ContactMail1', 'NewContact','Statistics';  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
