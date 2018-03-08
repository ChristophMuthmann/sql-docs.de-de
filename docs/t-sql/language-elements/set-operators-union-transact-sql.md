---
title: UNION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7c71b2eae1c0c3e55d09cdc5af2dfd7740df143f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="set-operators---union-transact-sql"></a>Mengenoperatoren Sie - UNION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Kombiniert die Ergebnisse von mindestens zwei Abfragen zu einem Resultset, das alle Zeilen enthält, die zu allen Abfragen der Vereinigung gehören. Der UNION-Vorgang unterscheidet sich von dem Verwenden von Joins, die Spalten aus zwei Tabellen kombinieren.  
  
 Für die Kombination der Resultsets von zwei Abfragen mit UNION gelten die folgenden Grundregeln:  
  
-   Die Anzahl und die Reihenfolge der Spalten müssen für alle Abfragen identisch sein.  
  
-   Die Datentypen müssen kompatibel sein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
    { <query_specification> | ( <query_expression> ) }   
  UNION [ ALL ]   
  <query_specification | ( <query_expression> )   
 [ UNION [ ALL ] <query_specification> | ( <query_expression> )   
    [ ...n ] ]   
```  
  
## <a name="arguments"></a>Argumente  
\<query_specification> | ( \<query_expression> ) Is a query specification or query expression that returns data to be combined with the data from another query specification or query expression. Die Definitionen der Spalten, die Bestandteil eines UNION-Vorgangs sind, müssen nicht identisch, jedoch durch implizite Konvertierung kompatibel sein. Datentypen unterschiedlich sind, das der resultierenden Datentyp bestimmt, in gemäß den Regeln für [Rangfolge der Datentypen](../../t-sql/data-types/data-type-precedence-transact-sql.md). Wenn die Typen identisch sind, diese sich aber in der Genauigkeit, Dezimalstellenanzahl oder Länge unterscheiden, wird das Ergebnis basierend auf denselben Regeln wie für das Kombinieren von Ausdrücken bestimmt. Weitere Informationen finden Sie unter [Genauigkeit, Dezimalstellen und Länge &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 Spalten mit den **Xml** -Datentyp muss äquivalent sein. Alle Spalten müssen entweder einen XML-Schematyp aufweisen oder nicht typisiert sein. Wenn sie typisiert sein, müssen sie derselben XML-Schemaauflistung zugeordnet werden.  
  
 UNION  
 Gibt an, dass mehrere Resultsets kombiniert und als ein einzelnes Resultset zurückgegeben werden sollen.  
  
 ALL  
 Bezieht alle Zeilen in das Ergebnis ein. Hierzu zählen auch Duplikate. Ohne diese Option werden doppelte Zeilen gelöscht.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-a-simple-union"></a>A. Verwenden einer einfachen UNION-Klausel  
 Das Resultset im folgenden Beispiel enthält den Inhalt der Spalten `ProductModelID` und `Name` der Tabellen `ProductModel` und `Gloves`.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Here is the simple union.  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="b-using-select-into-with-union"></a>B. Verwenden von SELECT INTO mit UNION  
 Im folgenden Beispiel gibt die `INTO`-Klausel in der zweiten `SELECT`-Anweisung an, dass die `ProductResults`-Tabelle das endgültige Resultset der Union der angegebenen Spalten aus den Tabellen `ProductModel` und `Gloves` enthält. Beachten Sie, dass die `Gloves`-Tabelle in der ersten `SELECT`-Anweisung erstellt wird.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.ProductResults', 'U') IS NOT NULL  
DROP TABLE dbo.ProductResults;  
GO  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
INTO dbo.ProductResults  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
SELECT ProductModelID, Name   
FROM dbo.ProductResults;  
  
```  
  
### <a name="c-using-union-of-two-select-statements-with-order-by"></a>C. Verwenden von UNION in zwei SELECT-Anweisungen mit ORDER BY  
 Die Reihenfolge bestimmter Parameter, die mit der UNION-Klausel verwendet werden, ist von Bedeutung. Im folgenden Beispiel werden die ordnungsgemäße und die falsche Verwendung von `UNION` in zwei `SELECT`-Anweisungen veranschaulicht, in denen eine Spalte in der Ausgabe umbenannt werden soll.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
/* INCORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
ORDER BY Name  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
/* CORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
  
```  
  
### <a name="d-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>D. Verwenden von UNION mit drei SELECT-Anweisungen, wobei die Auswirkung von ALL und Klammern gezeigt wird  
 In den folgenden Beispielen wird `UNION` verwendet, um die Ergebnisse aus drei Tabellen zu kombinieren, wobei in allen Tabellen 5 identische Datenzeilen vorhanden sind. Im ersten Beispiel wird `UNION ALL` verwendet, um doppelte Datensätze anzuzeigen, und alle 15 Zeilen zurückgegeben. Im zweiten Beispiel wird `UNION` ohne `ALL` verwendet, um die doppelten Zeilen aus den kombinierten Ergebnissen der drei `SELECT`-Anweisungen zu löschen, und 5 Zeilen zurückgegeben.  
  
 Im dritten Beispiel wird `ALL` mit dem ersten `UNION` verwendet; das zweite `UNION` verwendet `ALL` nicht und ist in Klammern eingeschlossen. Da die zweite `UNION`-Anweisung in Klammern steht, wird sie zuerst verarbeitet; sie gibt 5 Zeilen zurück, weil die Option `ALL` nicht verwendet wird und Duplikate gelöscht werden. Diese 5 Zeilen werden mit den Ergebnissen der ersten `SELECT`-Anweisung mithilfe der `UNION ALL`-Schlüsselwörter kombiniert. Dabei werden die Duplikate in den beiden aus 5 Zeilen bestehenden Resultsets nicht gelöscht. Das Endergebnis enthält 10 Zeilen.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.EmployeeOne', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeOne;  
GO  
IF OBJECT_ID ('dbo.EmployeeTwo', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeTwo;  
GO  
IF OBJECT_ID ('dbo.EmployeeThree', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeThree;  
GO  
  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeOne  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeTwo  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeThree  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
-- Union ALL  
SELECT LastName, FirstName, JobTitle  
FROM dbo.EmployeeOne  
UNION ALL  
SELECT LastName, FirstName ,JobTitle  
FROM dbo.EmployeeTwo  
UNION ALL  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle  
FROM dbo.EmployeeOne  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeOne  
UNION ALL  
(  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree  
);  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. Verwenden einer einfachen UNION-Klausel  
 Im folgenden Beispiel enthält das Resultset auf den Inhalt der `CustomerKey` Spalten beider der `FactInternetSales` und `DimCustomer` Tabellen. Da das ALL-Schlüsselwort nicht verwendet wird, werden Duplikate aus den Ergebnissen ausgeschlossen.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="f-using-union-of-two-select-statements-with-order-by"></a>F. Verwenden von UNION in zwei SELECT-Anweisungen mit ORDER BY  
 Wenn eine SELECT-Anweisung in einer UNION-Anweisung eine ORDER BY-Klausel enthält, sollte dieser Klausel nach allen SELECT-Anweisungen gespeichert werden. Das folgende Beispiel zeigt die falschen und richtige Verwendung des `UNION` in zwei `SELECT` Anweisungen, die in dem eine Spalte mit ORDER BY sortiert ist.  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT  
SELECT CustomerKey   
FROM FactInternetSales    
ORDER BY CustomerKey  
UNION   
SELECT CustomerKey   
FROM DimCustomer  
ORDER BY CustomerKey;  
  
-- CORRECT   
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. Verwenden von UNION mit zwei SELECT-Anweisungen mit WHERE und ORDER BY  
 Das folgende Beispiel zeigt die falschen und richtige Verwendung des `UNION` in zwei `SELECT` Anweisungen, wobei und ORDER BY erforderlich sind.  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT   
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
ORDER BY CustomerKey   
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
  
-- CORRECT  
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. Verwenden von UNION mit drei SELECT-Anweisungen, die Auswirkung von ALL und Klammern gezeigt wird  
 Verwenden Sie die folgenden Beispielen `UNION` kombiniert die Ergebnisse der **derselben Tabelle** um die Auswirkung von ALL und Klammern zu veranschaulichen, bei Verwendung `UNION`.  
  
 Im ersten Beispiel wird `UNION ALL` anzuzeigende doppelte Datensätze und gibt jede Zeile in der Quelltabelle dreimal aufgerufen. Im zweiten Beispiel wird `UNION` ohne `ALL` entfernen die doppelten Zeilen aus den kombinierten Ergebnissen der drei `SELECT` Anweisungen und gibt nur die keine Duplikate Zeilen aus der Quelltabelle.  
  
 Im dritten Beispiel wird `ALL` mit dem ersten `UNION` und Klammern einschließen der zweiten `UNION` , der nicht mit `ALL`. Die zweite `UNION` wird zuerst verarbeitet, da er in Klammern angegeben ist. Es gibt nur die keine Duplikate Zeilen aus der Tabelle zurück, da die `ALL` Option wird nicht verwendet und Duplikate entfernt werden. Diese Zeilen werden mit den Ergebnissen des ersten kombiniert `SELECT` mithilfe der `UNION ALL` Schlüsselwörter. Die Duplikate zwischen den beiden Sätzen wird nicht entfernt.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL  
(  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Wählen Sie die Beispiele &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
  
  

