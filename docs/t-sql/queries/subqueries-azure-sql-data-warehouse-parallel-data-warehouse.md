---
title: Unterabfragen (Azure SQL Datawarehouse, Parallel Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 351d559bde6300d9f746d68a802ae0a61202f8b8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>Unterabfragen (Azure SQL Datawarehouse, Parallel Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Dieses Thema enthält Beispiele für die Verwendung von Unterabfragen in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 Die SELECT-Anweisung finden Sie unter [SELECT &#40; Transact-SQL &#41;](../../t-sql/queries/select-transact-sql.md)  
  
## <a name="contents"></a>Inhalt  
  
-   [Grundlagen](#Basics)  
  
-   [Beispiele: SQL Datawarehouse und Parallel Datawarehouse](#Examples)  
  
##  <a name="Basics"></a>Grundlagen  
 Unterabfrage  
 Eine Unterabfrage ist eine Abfrage, die in einer SELECT-, INSERT-, UPDATE- oder DELETE-Anweisung bzw. in einer anderen Unterabfrage geschachtelt ist. Dies wird auch innere Abfrage oder innere Select-Ausdruck bezeichnet.  
  
 Äußere Abfrage  
 Die Anweisung, die die Unterabfrage enthält. Dies ist auch eine äußere Select bezeichnet.  
  
 Korrelierte Unterabfrage  
 Eine Unterabfrage, die auf eine Tabelle in der äußeren Abfrage verweist.  
  
##  <a name="Examples"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Dieser Abschnitt enthält Beispiele von Unterabfragen unterstützt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. TOP und ORDER BY in einer Unterabfrage  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. HAVING-Klausel mit einer korrelierten Unterabfrage  
  
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
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. Korrelierte Unterabfragen mit analytics  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. Korrelierte union-Anweisungen in einer Unterabfrage  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. Verknüpfen von Prädikaten in einer Unterabfrage  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. Korrelierte Join-Prädikaten in einer Unterabfrage  
  
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
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. Korrelierte Unterabfragen in die Datenwerte mit Aggregaten verwendet  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. Mithilfe einer korrelierten Unterabfrage  
 Im folgenden Beispiel wird `IN` in einer abhängigen oder sich wiederholenden Unterabfrage verwendet. Die Werte dieser Abfrage sind von der äußeren Abfrage abhängig. Die innere Abfrage wird wiederholt ausgeführt werden, einmal für jede Zeile, die ausgewählt werden von der äußeren Abfrage. Diese Abfrage ruft eine Instanz des der `EmployeeKey` plus vor- und Nachnamen der Mitarbeiter für die der `OrderQuantity` in der `FactResellerSales` Tabelle ist `5` und für die in der Angestellten-IDs entsprechen den `DimEmployee` und `FactResellerSales` Tabellen.  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. Verwenden von EXISTS im Vergleich zu einer Unterabfrage  
 Das folgende Beispiel zeigt Abfragen, die semantisch äquivalent veranschaulicht den Unterschied zwischen der Verwendung der `EXISTS` Schlüsselwort und die `IN` Schlüsselwort. Beides sind Beispiele für eine Unterabfrage, eine Instanz von jedem Produktnamen abruft, für die die Produktunterkategorie ist `Road Bikes`. `ProductSubcategoryKey`zwischen entspricht der `DimProduct` und `DimProductSubcategory` Tabellen.  
  
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
  
  
