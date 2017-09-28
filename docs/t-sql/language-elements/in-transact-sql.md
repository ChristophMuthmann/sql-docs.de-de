---
title: IN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IN_TSQL
- IN
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], matching
- NOT IN keyword
- 8623 (Database Engine error)
- matching values in subquery or list [SQL Server]
- IN keyword
- 8632 (Database Engine error)
ms.assetid: 4419de73-96b1-4dfe-8500-f4507915db04
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70b186107966791e29ccb76ea9c310724b76e3b6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ermittelt, ob ein angegebener Wert mit einem Wert aus einer Unterabfrage oder Liste übereinstimmt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>Argumente  
 *test_expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *Unterabfrage*  
 Ist eine Unterabfrage mit einem Resultset, das aus einer Spalte besteht. Diese Spalte muss denselben Datentyp wie aufweisen *Test_expression*.  
  
 *Ausdruck*[ **,**... *n* ]  
 Eine Liste mit Ausdrücken, die auf Übereinstimmungen geprüft werden sollen. Alle Ausdrücke müssen vom gleichen Typ wie sein *Test_expression*.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 Wenn der Wert der *Test_expression* gleich zurückgegebenen Wert *Unterabfrage* oder einem beliebigen anderen *Ausdruck* aus der Liste durch Trennzeichen getrennte ist der Ergebniswert TRUE; der Ergebniswert ist, andernfalls "false".  
  
 Verwenden von NOT IN negiert die *Unterabfrage* Wert oder *Ausdruck*.  
  
> [!CAUTION]  
>  Null-Werten zurückgegebenes *Unterabfrage* oder *Ausdruck* , sind im Vergleich zu *Test_expression* mithilfe von IN oder nicht IN "UNKNOWN" zurückgegeben. Werden NULL-Werte zusammen mit IN oder NOT IN verwendet, kann dies zu unerwarteten Ergebnissen führen.  
  
## <a name="remarks"></a>Hinweise  
 Einschließlich explizit innerhalb der Klammern eine IN-Klausel eine extrem hohe Zahl von Werten (viele Tausende von Werte durch Kommas getrennt) kann verbrauchen Ressourcen und die Fehler 8623 oder 8632 auftreten. Um dieses Problem zu umgehen, speichern Sie die Elemente in der Liste IN einer Tabelle, und Verwenden einer SELECT-Unterabfrage in einer IN-Klausel.  
  
 Fehler 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 Fehler 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-comparing-or-and-in"></a>A. Vergleichen von OR und IN  
 Im folgenden Beispiel wird eine Liste der Namen von Mitarbeitern ausgewählt, die Konstruktionsingenieure, Werkzeugkonstrukteure oder Marketingassistenten sind.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle = 'Design Engineer'   
   OR e.JobTitle = 'Tool Designer'   
   OR e.JobTitle = 'Marketing Assistant';  
GO  
```  
  
 Sie können jedoch dieselben Ergebnisse mithilfe von IN abrufen.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle IN ('Design Engineer', 'Tool Designer', 'Marketing Assistant');  
GO  
```  
  
 Hier ist das Resultset aus beiden Abfragen.  
  
```  
FirstName   LastName      Title  
---------   ---------   ---------------------  
Sharon      Salavaria   Design Engineer                                     
Gail        Erickson    Design Engineer                                     
Jossef      Goldberg    Design Engineer                                     
Janice      Galvin      Tool Designer                                       
Thierry     D'Hers      Tool Designer                                       
Wanida      Benshoof    Marketing Assistant                                 
Kevin       Brown       Marketing Assistant                                 
Mary        Dempsey     Marketing Assistant                                 
  
(8 row(s) affected)  
```  
  
### <a name="b-using-in-with-a-subquery"></a>B. Verwenden von IN mit einer Unterabfrage  
 Im folgenden Beispiel werden alle IDs der Vertriebsmitarbeiter in der `SalesPerson`-Tabelle der Mitarbeiter ermittelt, deren jährliche Sollvorgabe über 250.000 EUR liegt, und aus der `Employee`-Tabelle die Namen aller Mitarbeiter ausgewählt, bei denen `EmployeeID` mit den Ergebnissen der `SELECT`-Unterabfrage übereinstimmt.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName   LastName                                             
---------   --------   
Tsvi         Reiter                                              
Michael      Blythe                                              
Tete         Mensa-Annan                                         
  
(3 row(s) affected)  
```  
  
### <a name="c-using-not-in-with-a-subquery"></a>C. Verwenden von NOT IN mit einer Unterabfrage  
 Im folgenden Beispiel werden die Vertriebsmitarbeiter gesucht, deren Quote 250.000 $ nicht übersteigt. `NOT IN` sucht die Vertriebsmitarbeiter, die nicht den Elementen in der Werteliste entsprechen.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID NOT IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. IN und nicht IN Verwendung  
 Das folgende Beispiel findet alle Einträge in der `FactInternetSales` Tabelle, bei denen `SalesReasonKey` Werte in der `DimSalesReason` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 Das folgende Beispiel findet alle Einträge in der `FactInternetSalesReason` Tabelle, die nicht übereinstimmen `SalesReasonKey` Werte in der `DimSalesReason` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. Verwenden sich mit einer Liste der Ausdrücke  
 Das folgende Beispiel findet alle IDs der Vertriebsmitarbeiter in die `DimEmployee` Tabelle für Mitarbeiter, die eine erste haben also entweder Namen `Mike` oder `Michael`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Groß-/KLEINSCHREIBUNG &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [Alle &#40; Transact-SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [Einige &#124; Alle &#40; Transact-SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  




