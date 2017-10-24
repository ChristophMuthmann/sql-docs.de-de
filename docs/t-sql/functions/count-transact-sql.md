---
title: COUNT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_TSQL
- COUNT
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT function
- totals [SQL Server]
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT function [Transact-SQL]
ms.assetid: 28d39da6-bc2e-46c7-858c-b1721c938830
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: e2d11d2cc57d275e952ff371ddf99c34dcae323d
ms.contentlocale: de-de
ms.lasthandoff: 10/05/2017

---
# <a name="count-transact-sql"></a>COUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Anzahl von Elementen in einer Gruppe zurück. COUNT funktioniert wie die [COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md) Funktion. Der einzige Unterschied zwischen den beiden Funktionen sind die Rückgabewerte. COUNT gibt immer zurück ein **Int** -Datentypwert. COUNT_BIG gibt immer eine **"bigint"** -Datentypwert.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )   
    [ OVER (   
        [ partition_by_clause ]   
        [ order_by_clause ]   
        [ ROW_or_RANGE_clause ]  
    ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumente  
**ALL**  
Wendet die Aggregatfunktion auf alle Werte an. ALL ist die Standardeinstellung.
  
DISTINCT  
Gibt an, dass COUNT die Anzahl von eindeutigen Werten, die nicht NULL sind, zurückgibt.
  
*expression*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs außer **Text**, **Image**, oder **Ntext**. Aggregatfunktionen und Unterabfragen sind nicht zulässig.
  
\*  
Gibt an, dass alle Zeilen gezählt werden müssen, um die Gesamtzahl der Zeilen einer Tabelle zurückzugeben. COUNT (\*) besitzt keine Parameter und kann nicht zusammen mit DISTINCT verwendet werden. COUNT (\*) erfordert kein *Ausdruck* Parameter, da definitionsgemäß keine Informationen zu einer bestimmten Spalte verwendet wird. COUNT(*) gibt die Anzahl von Zeilen in der angegebenen Tabelle zurück, ohne Duplikate zu entfernen. Dabei werden alle Zeilen einzeln gezählt. Dies schließt Zeilen mit NULL-Werten ein.
  
ÜBER **(** [ *Partition_by_clause* ] [ *Order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
*Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *Order_by_clause* bestimmt die logische Reihenfolge, in dem der Vorgang ausgeführt wird. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Rückgabetypen
 **int**  
  
## <a name="remarks"></a>Hinweise  
COUNT(*) gibt die Anzahl von Elementen in einer Gruppe zurück. Dies schließt NULL-Werte und Duplikate ein.
  
COUNT (alle *Ausdruck*) ergibt *Ausdruck* für jede Zeile in einer Gruppe und die Anzahl der Werte ungleich NULL zurückgegeben.
  
COUNT (DISTINCT *Ausdruck*) ergibt *Ausdruck* für jede Zeile in einer Gruppe und die Anzahl der eindeutigen Werte ungleich NULL zurückgegeben.
  
Bei Rückgabewerten größer als 2^31-1 erzeugt COUNT einen Fehler. Verwenden Sie stattdessen COUNT_BIG.
  
COUNT ist eine deterministische Funktion, wenn sie ohne die OVER- und ORDER BY-Klauseln angegeben wird. Sie ist nicht deterministisch, wenn sie mit den OVER- und ORDER BY-Klauseln angegeben wird. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-count-and-distinct"></a>A. Verwenden von COUNT und DISTINCT  
Im folgenden Beispiel wird die Anzahl der verschiedenen Berufsbezeichnungen aufgelistet, die ein Mitarbeiter haben kann, der bei [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] arbeitet.
  
```sql
SELECT COUNT(DISTINCT Title)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67  
  
(1 row(s) affected)
```
  
### <a name="b-using-count"></a>B. Verwenden von COUNT(*)  
Im folgenden Beispiel wird die Gesamtzahl der Mitarbeiter ermittelt, die bei [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] arbeiten.
  
```sql
SELECT COUNT(*)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
290  
  
(1 row(s) affected)
```
  
### <a name="c-using-count-with-other-aggregates"></a>C. Verwenden von COUNT(*) mit anderen Aggregaten  
Im folgenden Beispiel wird gezeigt, wie `COUNT(*)` mit anderen Aggregatfunktionen in der SELECT-Liste kombiniert werden kann. Im Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.
  
```sql
SELECT COUNT(*), AVG(Bonus)  
FROM Sales.SalesPerson  
WHERE SalesQuota > 25000;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- ---------------------
14            3472.1428
  
(1 row(s) affected)
```
  
### <a name="d-using-the-over-clause"></a>D. Verwenden der OVER-Klausel  
Im folgenden Beispiel werden die Funktionen MIN, MAX, AVG und COUNT mit der OVER-Klausel verwendet, um aggregierte Werte für jede Abteilung in der `HumanResources.Department`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank bereitzustellen.
  
```sql
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
ON d.DepartmentID = edh.DepartmentID
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
(16 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-count-and-distinct"></a>E. Verwenden von COUNT und DISTINCT  
Das folgende Beispiel listet die Anzahl der verschiedenen Softwaretitel an, denen ein Mitarbeiter, die auf einen bestimmten Mandanten arbeitet aufnehmen kann.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(DISTINCT Title)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67
```  
  
### <a name="f-using-count"></a>F. Verwenden von COUNT(*)  
Im folgende Beispiel gibt die Gesamtanzahl der Zeilen in der `dbo.DimEmployee` Tabelle.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(*)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------
296
```  
  
### <a name="g-using-count-with-other-aggregates"></a>G. Verwenden von COUNT(*) mit anderen Aggregaten  
Das folgende Beispiel kombiniert `COUNT(*)` mit anderen Aggregatfunktionen in der SELECT-Liste. Die Abfrage gibt die Anzahl von Vertriebsmitarbeitern mit einer jährlichen sollvorgaben größer als 500.000 Euro und die durchschnittliche Vertriebsvorgaben zurück.
  
```sql
USE ssawPDW;  
  
SELECT COUNT(EmployeeKey) AS TotalCount, AVG(SalesAmountQuota) AS [Average Sales Quota]  
FROM dbo.FactSalesQuota  
WHERE SalesAmountQuota > 500000 AND CalendarYear = 2001;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
TotalCount  Average Sales Quota
----------  -------------------
10          683800.0000
```
  
### <a name="h-using-count-with-having"></a>H. Verwenden von COUNT mit HAVING  
Im folgenden Beispiel wird die Anzahl der mit der HAVING-Klausel zurückzugebenden Abteilungen in einem Unternehmen, die mehr als 15 Mitarbeiter haben.
  
```sql
USE ssawPDW;  
  
SELECT DepartmentName,   
       COUNT(EmployeeKey)AS EmployeesInDept  
FROM dbo.DimEmployee  
GROUP BY DepartmentName  
HAVING COUNT(EmployeeKey) > 15;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
DepartmentName  EmployeesInDept
--------------  ---------------
Sales           18
Production      179
```
  
### <a name="i-using-count-with-over"></a>I. Verwenden von COUNT mit Failover  
Im folgenden Beispiel wird die Anzahl mit der OVER-Klausel, um die Anzahl der Produkte, die enthalten sind in jedem der angegebenen Aufträge zurückzugeben.
  
```sql
USE ssawPDW;  
  
SELECT DISTINCT COUNT(ProductKey) OVER(PARTITION BY SalesOrderNumber) AS ProductCount  
    ,SalesOrderNumber  
FROM dbo.FactInternetSales  
WHERE SalesOrderNumber IN (N'SO53115',N'SO55981');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
ProductCount   SalesOrderID`
------------   -----------------
3              SO53115
1              SO55981
```
  
## <a name="see-also"></a>Siehe auch
[Aggregatfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG &#40; Transact-SQL &#41;](../../t-sql/functions/count-big-transact-sql.md)  
[Failover-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  



