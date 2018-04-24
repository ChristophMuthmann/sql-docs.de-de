---
title: RANK (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RANK
- RANK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- tied rows [SQL Server]
- ranking rows
- RANK function [Transact-SQL]
ms.assetid: 2d96f6d2-5db7-4b3c-a63e-213c58e4af55
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c746f3ba206e548b78a50a02221f690be6fe8e2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="rank-transact-sql"></a>RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Rang jeder Zeile innerhalb der Partition eines Resultsets zurück. Der Rang einer Zeile ergibt sich, indem 1 zur Anzahl von Rängen vor der fraglichen Zeile addiert wird.  

  ROW_NUMBER und RANK sind ähnlich. ROW_NUMBER nummeriert alle Zeilen sequenziell (z.B. 1, 2, 3, 4, 5). RANK stellt den gleichen numerischen Wert für gleichwertige Werte bereit (z.B. 1, 2, 3, 4, 5).   
  
> [!NOTE]
> RANK ist ein temporärer Wert, der berechnet wird, wenn die Abfrage ausgeführt wird. Unter [IDENTITY-Eigenschaft](../../t-sql/statements/create-table-transact-sql-identity-property.md) und [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) finden Sie weitere Informationen zum dauerhaften Speichern von Zahlen in einer Tabelle. 
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
RANK ( ) OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumente  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* unterteilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *order_by_clause* bestimmt die Reihenfolge der Daten, bevor die Funktion angewendet wird. *order_by_clause* ist erforderlich. Die \<Zeilen- oder Bereichsklausel> der OVER-Klausel kann für die RANK-Funktion nicht angegeben werden. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **bigint**  
  
## <a name="remarks"></a>Remarks  
 Wenn zwei oder mehr Zeilen gleichwertig sind, erhält jede gleichwertige Zeile denselben Rang. Wenn beispielsweise zwei Vertriebsmitarbeiter denselben SalesYTD-Wert aufweisen, erhalten beide den Rang 1. Der Vertriebsmitarbeiter mit dem nächsthöheren SalesYTD-Wert erhält den Rang 3, da es bereits zwei Zeilen mit einem höheren Rang gibt. Aus diesem Grund gibt die RANK-Funktion nicht immer aufeinander folgende ganze Zahlen zurück.  
  
 Die Sortierreihenfolge, die für die ganze Abfrage verwendet wird, bestimmt die Reihenfolge, mit der die Zeilen in einem Resultset aufgeführt sind.  
  
 RANK ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-ranking-rows-within-a-partition"></a>A. Ordnen von Zeilen innerhalb einer Partition  
 Im folgenden Beispiel wird die Rangfolge der Produkte im Bestand für die angegebenen Lagerstandorte gemäß ihren Mengen bestimmt. Das Resultset wird nach `LocationID` partitioniert und logisch nach `Quantity` sortiert. Beachten Sie, dass die Produkte 494 und 495 die gleiche Menge haben. Da sie verbunden sind, wird beiden Rang 1 zugeordnet.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,RANK() OVER   
    (PARTITION BY i.LocationID ORDER BY i.Quantity DESC) AS Rank  
FROM Production.ProductInventory AS i   
INNER JOIN Production.Product AS p   
    ON i.ProductID = p.ProductID  
WHERE i.LocationID BETWEEN 3 AND 4  
ORDER BY i.LocationID;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
ProductID   Name                   LocationID   Quantity Rank  
----------- ---------------------- ------------ -------- ----  
494         Paint - Silver         3            49       1  
495         Paint - Blue           3            49       1  
493         Paint - Red            3            41       3  
496         Paint - Yellow         3            30       4  
492         Paint - Black          3            17       5  
495         Paint - Blue           4            35       1  
496         Paint - Yellow         4            25       2  
493         Paint - Red            4            24       3  
492         Paint - Black          4            14       4  
494         Paint - Silver         4            12       5  
 (10 row(s) affected)  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>B. Ordnen aller Zeilen in einem Resultset  
 Im folgenden Beispiel werden die ersten zehn nach ihrem Gehalt geordneten Mitarbeiter zurückgegeben. Da keine PARTITION BY-Klausel angegeben wurde, wurde die RANK-Funktion auf alle Zeilen im Resultset angewendet.  
  
```  
USE AdventureWorks2012  
SELECT TOP(10) BusinessEntityID, Rate,   
       RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory AS eph1  
WHERE RateChangeDate = (SELECT MAX(RateChangeDate)   
                        FROM HumanResources.EmployeePayHistory AS eph2  
                        WHERE eph1.BusinessEntityID = eph2.BusinessEntityID)  
ORDER BY BusinessEntityID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
2                63.4615               4  
3                43.2692               8  
4                29.8462               19  
5                32.6923               16  
6                32.6923               16  
7                50.4808               6  
8                40.8654               10  
9                40.8654               10  
10               42.4808               9  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-ranking-rows-within-a-partition"></a>C: Ordnen von Zeilen innerhalb einer Partition  
 Im folgenden Beispiel wird die Rangfolge der Vertriebsmitarbeiter in jedem Vertriebsgebiet auf Grundlage von deren Gesamtumsatz bestimmt. Das Rowset wird auf der Grundlage von `SalesTerritoryGroup` partitioniert und nach `SalesAmountQuota` sortiert.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
LastName          TotalSales     SalesTerritoryGroup  RankResult
----------------  -------------  -------------------  --------
Tsoflias          1687000.0000   Australia            1
Saraiva           7098000.0000   Canada               1
Vargas            4365000.0000   Canada               2
Carson            12198000.0000  Central              1
Varkey Chudukatil 5557000.0000   France               1
Valdez            2287000.0000   Germany              1
Blythe            11162000.0000  Northeast            1
Campbell          4025000.0000   Northwest            1
Ansman-Wolfe      3551000.0000   Northwest            2
Mensa-Annan       2753000.0000   Northwest            3
Reiter            8541000.0000   Southeast            1
Mitchell          11786000.0000  Southwest            1
Ito               7804000.0000   Southwest            2
Pak               10514000.0000  United Kingdom       1
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DENSE_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [ROW_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE &#40;Transact-SQL&#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [Rangfolgefunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



