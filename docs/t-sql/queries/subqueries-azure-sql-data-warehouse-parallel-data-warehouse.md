---
title: Unterabfragen (Azure SQL Data Warehouse, Parallel Data Warehouse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 39944bb4eeef8e2b7aca92fafd418eeb4afb78d7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>Unterabfragen (Azure SQL Data Warehouse, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Dieses Thema enthält Beispiele für die Verwendung von Unterabfragen in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 Informationen zur SELECT-Anweisung finden Sie unter [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="contents"></a>Inhalt  
  
-   [Grundlagen](#Basics)  
  
-   [Beispiele: SQL Data Warehouse und Parallel Data Warehouse](#Examples)  
  
##  <a name="Basics"></a> Grundlagen  
 Unterabfrage  
 Eine Unterabfrage ist eine Abfrage, die in einer SELECT-, INSERT-, UPDATE- oder DELETE-Anweisung bzw. in einer anderen Unterabfrage geschachtelt ist. Dies wird auch als innere Abfrage oder innerer Select-Ausdruck bezeichnet.  
  
 Äußere Abfrage  
 Die Anweisung, die die Unterabfrage enthält. Dies wird auch eine äußerer Select-Ausdruck bezeichnet.  
  
 Korrelierte Unterabfrage  
 Eine Unterabfrage, die auf eine Tabelle in der äußeren Abfrage verweist.  
  
##  <a name="Examples"></a> Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Dieser Abschnitt enthält Beispiele für in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] unterstützte Unterabfragen.  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. TOP und ORDER BY in einer Unterabfrage  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. Korrelierte Unterabfragen in einer HAVING-Klausel  
  
```  
SELECT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
GROUP BY dm.EmployeeKey, dm.FirstName, dm.LastName  
HAVING 5000 <=   
(SELECT sum(OrderQuantity)  
FROM FactResellerSales AS frs  
WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
  
```  
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. Korrelierte Unterabfragen mit Analyse  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. Korrelierte Union-Anweisungen in einer Unterabfrage  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. JOIN-Prädikate in einer Unterabfrage  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. Korrelierte JOIN-Prädikate in einer Unterabfrage  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. Korrelierte untergeordnete SELECT-Ausdrücke als Datenquellen  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. Korrelierte Unterabfragen in den mit Aggregaten verwendeten Datenwerten  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. Verwenden von IN mit einer korrelierten Unterabfrage  
 Im folgenden Beispiel wird `IN` in einer abhängigen oder sich wiederholenden Unterabfrage verwendet. Die Werte dieser Abfrage sind von der äußeren Abfrage abhängig. Die innere Abfrage wird wiederholt ausgeführt, und zwar einmal für jede Zeile, die von der äußeren Abfrage ausgewählt wird. Diese Abfrage ruft eine Instanz des `EmployeeKey` plus den Vor- und Nachnamen der einzelnen Mitarbeiter ab, für die die `OrderQuantity` in der `FactResellerSales`-Tabelle `5` beträgt und für die die Mitarbeiter-IDs in der `DimEmployee`- und `FactResellerSales`-Tabelle übereinstimmen.  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. Verwenden von EXISTS im Vergleich zu IN in einer Unterabfrage  
 Im folgenden Beispiel werden Abfragen, die semantisch ähnlich sind, gezeigt, und der Unterschied zwischen der Verwendung des `EXISTS`-Schlüsselworts und des `IN`-Schlüsselworts wird veranschaulicht. Beides sind Beispiele für eine Unterabfrage, die eine Instanz von jedem Produktnamen abruft, für die die Produktunterkategorie `Road Bikes` ist. `ProductSubcategoryKey` vergleicht die `DimProduct`- und die `DimProductSubcategory`-Tabelle.  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE EXISTS  
    (SELECT *  
     FROM DimProductSubcategory AS dps   
     WHERE dp.ProductSubcategoryKey = dps.ProductSubcategoryKey  
           AND dps.EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
 oder  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE dp.ProductSubcategoryKey IN  
    (SELECT ProductSubcategoryKey  
     FROM DimProductSubcategory   
     WHERE EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
### <a name="k-using-multiple-correlated-subqueries"></a>K. Verwenden von mehreren abhängigen Unterabfragen  
 In diesem Beispiel werden zwei abhängige Unterabfragen verwendet, um die Namen von Mitarbeitern zu finden, die ein bestimmtes Produkt verkauft haben.  
  
```  
SELECT DISTINCT LastName, FirstName, e.EmployeeKey  
FROM DimEmployee e JOIN FactResellerSales s ON e.EmployeeKey = s.EmployeeKey  
WHERE ProductKey IN  
(SELECT ProductKey FROM DimProduct WHERE ProductSubcategoryKey IN  
(SELECT ProductSubcategoryKey FROM DimProductSubcategory   
 WHERE EnglishProductSubcategoryName LIKE '%Bikes'))  
ORDER BY LastName  
;  
  
```  
  
  
