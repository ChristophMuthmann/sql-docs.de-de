---
title: SET IDENTITY_INSERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET IDENTITY_INSERT
- SET_IDENTITY_INSERT_TSQL
- IDENTITY_INSERT_TSQL
- IDENTITY_INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY_INSERT option
- SET IDENTITY_INSERT statement
- identity values [SQL Server], explicit values
- identity columns [SQL Server], explicit values
ms.assetid: a5dd49f2-45c7-44a8-b182-e0a5e5c373ee
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9725d774075f21fc86d5276c91ed281fa34eba7d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-identityinsert-transact-sql"></a>SET IDENTITY_INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ermöglicht das Einfügen expliziter Werte in die Identitätsspalte einer Tabelle.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET IDENTITY_INSERT [ database_name . [ schema_name ] . ] table { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Name der Datenbank, in der sich die angegebene Tabelle befindet.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle gehört.  
  
 *table*  
 Name einer Tabelle mit einer Identitätsspalte.  
  
## <a name="remarks"></a>Hinweise  
 Die IDENTITY_INSERT-Eigenschaft kann in einer Sitzung zu jedem Zeitpunkt nur für eine einzige Tabelle auf ON festgelegt sein. Wenn diese Eigenschaft bereits für eine Tabelle auf ON festgelegt ist und eine SET IDENTITY_INSERT ON-Anweisung für eine andere Tabelle ausgegeben wird, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung zurück, die besagt, dass SET IDENTITY_INSERT bereits den Wert ON hat, und die angibt, für welche Tabelle der Wert ON festgelegt ist.  
  
 Wenn der eingefügte Wert größer als der aktuelle Identitätswert für die Tabelle ist, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch den neu eingefügten Wert als aktuellen Identitätswert.  
  
 Die Einstellung von SET IDENTITY_INSERT wird beim Ausführen bzw. zur Laufzeit festgelegt, nicht beim Analysieren.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss der Besitzer der Tabelle sein oder die ALTER-Berechtigung für die Tabelle besitzen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Tabelle mit einer Identitätsspalte erstellt. Es zeigt, wie mithilfe der `SET IDENTITY_INSERT`-Einstellung eine aufgrund einer `DELETE`-Anweisung entstandene Lücke in den Identitätswerten gefüllt werden kann.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create tool table.  
CREATE TABLE dbo.Tool(  
   ID INT IDENTITY NOT NULL PRIMARY KEY,   
   Name VARCHAR(40) NOT NULL  
);  
GO  
-- Inserting values into products table.  
INSERT INTO dbo.Tool(Name)   
VALUES ('Screwdriver')  
        , ('Hammer')  
        , ('Saw')  
        , ('Shovel');  
GO  
  
-- Create a gap in the identity values.  
DELETE dbo.Tool  
WHERE Name = 'Saw';  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
  
-- Try to insert an explicit ID value of 3;  
-- should return a warning.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
-- SET IDENTITY_INSERT to ON.  
SET IDENTITY_INSERT dbo.Tool ON;  
GO  
  
-- Try to insert an explicit ID value of 3.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
-- Drop products table.  
DROP TABLE dbo.Tool;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SCOPE_IDENTITY &#40; Transact-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

