---
title: Vorhanden ist (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXISTS_TSQL
- EXISTS
dev_langs:
- TSQL
helpviewer_keywords:
- existence testing [SQL Server]
- testing existence
- EXISTS keyword
- subqueries [SQL Server], EXISTS keyword
- queries [SQL Server], comparing
- comparing queries
- NOT EXISTS keyword
- row existence testing [SQL Server]
ms.assetid: b6510a65-ac38-4296-a3d5-640db0c27631
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c620baae23d9cab28142ee890ee103edbe2ee114
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="exists-transact-sql"></a>EXISTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Unterabfrage an, die testet, ob Zeilen vorhanden sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
EXISTS ( subquery )  
```  
  
## <a name="arguments"></a>Argumente  
 *Unterabfrage*  
 Eine eingeschränkte SELECT-Anweisung. Das INTO-Schlüsselwort ist nicht zulässig. Weitere Informationen finden Sie die Informationen zu Unterabfragen in [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-values"></a>Ergebniswerte  
 Gibt TRUE zurück, wenn eine Unterabfrage mindestens eine Zeile enthält.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-null-in-a-subquery-to-still-return-a-result-set"></a>A. Verwenden von NULL in Unterabfragen, um weiterhin ein Resultset zurückzugeben  
 Das folgende Beispiel gibt ein Resultset zurück, das mithilfe von `NULL` zu TRUE ausgewertet wird, obwohl `EXISTS` in der Unterabfrage angegeben wurde.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name   
FROM HumanResources.Department   
WHERE EXISTS (SELECT NULL)  
ORDER BY Name ASC ;  
```  
  
### <a name="b-comparing-queries-by-using-exists-and-in"></a>B. Vergleichen von Abfragen mit EXISTS und IN  
 Das folgende Beispiel vergleicht zwei semantisch gleichwertige Abfragen. Die erste Abfrage verwendet `EXISTS`, die zweite verwendet `IN`.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.FirstName, a.LastName  
FROM Person.Person AS a  
WHERE EXISTS  
(SELECT *   
    FROM HumanResources.Employee AS b  
    WHERE a.BusinessEntityID = b.BusinessEntityID  
    AND a.LastName = 'Johnson');  
GO  
```  
  
 Die folgende Abfrage verwendet `IN`.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.FirstName, a.LastName  
FROM Person.Person AS a  
WHERE a.LastName IN  
(SELECT a.LastName  
    FROM HumanResources.Employee AS b  
    WHERE a.BusinessEntityID = b.BusinessEntityID  
    AND a.LastName = 'Johnson');  
GO  
```  
  
 Hier wird das Resultset für die beiden Abfragen.  
  
 `FirstName                                          LastName`  
  
 `-------------------------------------------------- ----------`  
  
 `Barry                                              Johnson`  
  
 `David                                              Johnson`  
  
 `Willis                                             Johnson`  
  
 `(3 row(s) affected)`  
  
### <a name="c-comparing-queries-by-using-exists-and--any"></a>C. Vergleichen von Abfragen mit EXISTS und = ANY  
 Das folgende Beispiel zeigt zwei Abfragen zum Ermitteln von Läden, deren Namen dem Namen eines Lieferanten entsprechen. Die erste Abfrage verwendet `EXISTS` und die zweite verwendet `=``ANY`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT s.Name  
FROM Sales.Store AS s   
WHERE EXISTS  
(SELECT *  
    FROM Purchasing.Vendor AS v  
    WHERE s.Name = v.Name) ;  
GO  
```  
  
 Die folgende Abfrage verwendet `= ANY`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT s.Name  
FROM Sales.Store AS s   
WHERE s.Name = ANY  
(SELECT v.Name  
    FROM Purchasing.Vendor AS v ) ;  
GO  
```  
  
### <a name="d-comparing-queries-by-using-exists-and-in"></a>D. Vergleichen von Abfragen mit EXISTS und IN  
 Das folgende Beispiel zeigt Abfragen zum Ermitteln von Mitarbeitern in Abteilungen, die mit `P` beginnen.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p   
JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
WHERE EXISTS  
(SELECT *  
    FROM HumanResources.Department AS d  
    JOIN HumanResources.EmployeeDepartmentHistory AS edh  
       ON d.DepartmentID = edh.DepartmentID  
    WHERE e.BusinessEntityID = edh.BusinessEntityID  
    AND d.Name LIKE 'P%');  
GO  
```  
  
 Die folgende Abfrage verwendet `IN`.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
   ON e.BusinessEntityID = edh.BusinessEntityID   
WHERE edh.DepartmentID IN  
(SELECT DepartmentID  
   FROM HumanResources.Department  
   WHERE Name LIKE 'P%');  
GO  
```  
  
### <a name="e-using-not-exists"></a>E. Verwenden von NOT EXISTS  
 NOT EXISTS funktioniert genau umgekehrt wie EXISTS. Die WHERE-Klausel in NOT EXISTS wird erfüllt, wenn die Unterabfrage keine Zeilen zurückgibt. Im folgenden Beispiel werden Mitarbeiter ermittelt, die nicht in den Abteilungen arbeiten, deren Namen mit `P` beginnen.  
  
```  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p   
JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID   
WHERE NOT EXISTS  
(SELECT *  
   FROM HumanResources.Department AS d  
   JOIN HumanResources.EmployeeDepartmentHistory AS edh  
      ON d.DepartmentID = edh.DepartmentID  
   WHERE e.BusinessEntityID = edh.BusinessEntityID  
   AND d.Name LIKE 'P%')  
ORDER BY LastName, FirstName  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `FirstName                      LastName                       Title`  
  
 `------------------------------ ------------------------------ ------------`  
  
 `Syed                           Abbas                          Pacific Sales Manager`  
  
 `Hazem                          Abolrous                       Quality Assurance Manager`  
  
 `Humberto                       Acevedo                        Application Specialist`  
  
 `Pilar                          Ackerman                       Shipping & Receiving Superviso`  
  
 `François                       Ajenstat                       Database Administrator`  
  
 `Amy                            Alberts                        European Sales Manager`  
  
 `Sean                           Alexander                      Quality Assurance Technician`  
  
 `Pamela                         Ansman-Wolfe                   Sales Representative`  
  
 `Zainal                         Arifin                         Document Control Manager`  
  
 `David                          Barber                         Assistant to CFO`  
  
 `Paula                          Barreto de Mattos              Human Resources Manager`  
  
 `Shai                           Bassli                         Facilities Manager`  
  
 `Wanida                         Benshoof                       Marketing Assistant`  
  
 `Karen                          Berg                           Application Specialist`  
  
 `Karen                          Berge                          Document Control Assistant`  
  
 `Andreas                        Berglund                       Quality Assurance Technician`  
  
 `Matthias                       Berndt                         Shipping & Receiving Clerk`  
  
 `Jo                             Berry                          Janitor`  
  
 `Jimmy                          Bischoff                       Stocker`  
  
 `Michael                        Blythe                         Sales Representative`  
  
 `David                          Bradley                        Marketing Manager`  
  
 `Kevin                          Brown                          Marketing Assistant`  
  
 `David                          Campbell                       Sales Representative`  
  
 `Jason                          Carlson                        Information Services Manager`  
  
 `Fernando                       Caro                           Sales Representative`  
  
 `Sean                           Chai                           Document Control Assistant`  
  
 `Sootha                         Charncherngkha                 Quality Assurance Technician`  
  
 `Hao                            Chen                           HR Administrative Assistant`  
  
 `Kevin                          Chrisulis                      Network Administrator`  
  
 `Pat                            Coleman                        Janitor`  
  
 `Stephanie                      Conroy                         Network Manager`  
  
 `Debra                          Core                           Application Specialist`  
  
 `Ovidiu                         Crãcium                        Sr. Tool Designer`  
  
 `Grant                          Culbertson                     HR Administrative Assistant`  
  
 `Mary                           Dempsey                        Marketing Assistant`  
  
 `Thierry                        D'Hers                         Tool Designer`  
  
 `Terri                          Duffy                          VP Engineering`  
  
 `Susan                          Eaton                          Stocker`  
  
 `Terry                          Eminhizer                      Marketing Specialist`  
  
 `Gail                           Erickson                       Design Engineer`  
  
 `Janice                         Galvin                         Tool Designer`  
  
 `Mary                           Gibson                         Marketing Specialist`  
  
 `Jossef                         Goldberg                       Design Engineer`  
  
 `Sariya                         Harnpadoungsataya              Marketing Specialist`  
  
 `Mark                           Harrington                     Quality Assurance Technician`  
  
 `Magnus                         Hedlund                        Facilities Assistant`  
  
 `Shu                            Ito                            Sales Representative`  
  
 `Stephen                        Jiang                          North American Sales Manager`  
  
 `Willis                         Johnson                        Recruiter`  
  
 `Brannon                        Jones                          Finance Manager`  
  
 `Tengiz                         Kharatishvili                  Control Specialist`  
  
 `Christian                      Kleinerman                     Maintenance Supervisor`  
  
 `Vamsi                          Kuppa                          Shipping & Receiving Clerk`  
  
 `David                          Liu                            Accounts Manager`  
  
 `Vidur                          Luthra                         Recruiter`  
  
 `Stuart                         Macrae                         Janitor`  
  
 `Diane                          Margheim                       Research & Development Enginee`  
  
 `Mindy                          Martin                         Benefits Specialist`  
  
 `Gigi                           Matthew                        Research & Development Enginee`  
  
 `Tete                           Mensa-Annan                    Sales Representative`  
  
 `Ramesh                         Meyyappan                      Application Specialist`  
  
 `Dylan                          Miller                         Research & Development Manager`  
  
 `Linda                          Mitchell                       Sales Representative`  
  
 `Barbara                        Moreland                       Accountant`  
  
 `Laura                          Norman                         Chief Financial Officer`  
  
 `Chris                          Norred                         Control Specialist`  
  
 `Jae                            Pak                            Sales Representative`  
  
 `Wanda                          Parks                          Janitor`  
  
 `Deborah                        Poe                            Accounts Receivable Specialist`  
  
 `Kim                            Ralls                          Stocker`  
  
 `Tsvi                           Reiter                         Sales Representative`  
  
 `Sharon                         Salavaria                      Design Engineer`  
  
 `Ken                            Sanchez                        Chief Executive Officer`  
  
 `José                           Saraiva                        Sales Representative`  
  
 `Mike                           Seamans                        Accountant`  
  
 `Ashvini                        Sharma                         Network Administrator`  
  
 `Janet                          Sheperdigian                   Accounts Payable Specialist`  
  
 `Candy                          Spoon                          Accounts Receivable Specialist`  
  
 `Michael                        Sullivan                       Sr. Design Engineer`  
  
 `Dragan                         Tomic                          Accounts Payable Specialist`  
  
 `Lynn                           Tsoflias                       Sales Representative`  
  
 `Rachel                         Valdez                         Sales Representative`  
  
 `Garrett                        Vargar                         Sales Representative`  
  
 `Ranjit                         Varkey Chudukatil              Sales Representative`  
  
 `Bryan                          Walton                         Accounts Receivable Specialist`  
  
 `Jian Shuo                      Wang                           Engineering Manager`  
  
 `Brian                          Welcker                        VP Sales`  
  
 `Jill                           Williams                       Marketing Specialist`  
  
 `Dan                            Wilson                         Database Administrator`  
  
 `John                           Wood                           Marketing Specialist`  
  
 `Peng                           Wu                             Quality Assurance Supervisor`  
  
 `(91 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-using-exists"></a>F. Verwenden von EXISTS  
 Das folgende Beispiel gibt an, ob alle Zeilen in der `ProspectiveBuyer` Tabelle möglicherweise Übereinstimmungen, die Zeilen in der `DimCustomer` Tabelle. Die Abfrage gibt Zeilen zurück nur, wenn sowohl die `LastName` und `BirthDate` Werte in den beiden Tabellen übereinstimmen.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.LastName, a.BirthDate  
FROM DimCustomer AS a  
WHERE EXISTS  
(SELECT *   
    FROM dbo.ProspectiveBuyer AS b  
    WHERE (a.LastName = b.LastName) AND (a.BirthDate = b.BirthDate));  
```  
  
### <a name="g-using-not-exists"></a>G. Verwenden von NOT EXISTS  
 NOT EXISTS funktioniert als als EXISTS Gegenstück. Die WHERE-Klausel in NOT EXISTS wird erfüllt, wenn die Unterabfrage keine Zeilen zurückgibt. Das folgende Beispiel sucht nach Zeilen in der `DimCustomer` Tabelle die `LastName` und `BirthDate` entsprechen keine Einträge in der `ProspectiveBuyers` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
SELECT a.LastName, a.BirthDate  
FROM DimCustomer AS a  
WHERE NOT EXISTS  
(SELECT *   
    FROM dbo.ProspectiveBuyer AS b  
    WHERE (a.LastName = b.LastName) AND (a.BirthDate = b.BirthDate));  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  



