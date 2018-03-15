---
title: IN (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/29/2016
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 86d03b96015869efb8ff2ab873b1c838c50387f8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 Ein gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *subquery*  
 Ist eine Unterabfrage mit einem Resultset, das aus einer Spalte besteht. Diese Spalte muss denselben Datentyp besitzen wie *test_expression*.  
  
 *expression*[ **,**... *n* ]  
 Eine Liste mit Ausdrücken, die auf Übereinstimmungen geprüft werden sollen. Alle Ausdrücke müssen denselben Datentyp besitzen wie *test_expression*.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 Wenn der Wert von *test_expression* einem von der *Unterabfrage* zurückgegebenen Wert oder einem *Ausdruck* aus der durch Trennzeichen getrennten Liste entspricht, ist der Ergebniswert TRUE. Andernfalls ist der Ergebniswert FALSE.  
  
 Die Verwendung von NOT IN negiert den Wert der *Unterabfrage* oder den *Ausdruck*.  
  
> [!CAUTION]  
>  Bei von der *Unterabfrage* oder dem *Ausdruck* zurückgegebenen NULL-Werten, die mithilfe von IN oder NOT IN mit *test_expression* verglichen werden, wird UNKNOWN zurückgegeben. Werden NULL-Werte zusammen mit IN oder NOT IN verwendet, kann dies zu unerwarteten Ergebnissen führen.  
  
## <a name="remarks"></a>Remarks  
 Wenn eine IN-Klausel eine extrem hohe Anzahl von Werten (viele Tausende durch Trennzeichen getrennte Werte) explizit in den Klammern enthält, können die Ressourcen überbeansprucht werden und die Fehler 8623 oder 8632 auftreten. Speichern Sie die Elemente in der IN-Liste in einer Tabelle, und verwenden Sie eine SELECT-Unterabfrage in einer IN-Klausel, um dieses Problem zu umgehen.  
  
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
  
 Im Folgenden wird das Resultset der beiden Abfragen aufgeführt.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-using-in-and-not-in"></a>D. Verwenden von IN und NOT IN  
 Im folgenden Beispiel werden alle Einträge in der Tabelle `FactInternetSales` gefunden, die den Werten von `SalesReasonKey` in der Tabelle `DimSalesReason` entsprechen.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 Im folgenden Beispiel werden alle Einträge in der Tabelle `FactInternetSalesReason` gefunden, die den Werten von `SalesReasonKey` in der Tabelle `DimSalesReason` nicht entsprechen.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. Verwendung von IN mit einer Ausdrucksliste  
 Im folgenden Beispiel werden alle IDs der Vertriebsmitarbeiter in der Tabelle `DimEmployee` gefunden, die den Vornamen `Mike` oder `Michael` haben.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  



