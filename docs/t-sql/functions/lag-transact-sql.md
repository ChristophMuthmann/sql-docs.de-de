---
title: "Verzögerung (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAG_TSQL
- LAG
dev_langs:
- TSQL
helpviewer_keywords:
- LAG function
- analytic functions, LAG
ms.assetid: a9a90bdb-3f80-4c97-baca-b7407bcdc7f0
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 77598feb87f6766f6c24c454dace2c138315e69b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lag-transact-sql"></a>LAG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Greift im gleichen Resultset auf Daten in einer vorherigen Zeile zu, ohne dass ein Selbstjoin in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendet wird. LAG ermöglicht den Zugriff auf eine Zeile mit einem bestimmten physischen Offset vor der aktuellen Zeile. Verwenden Sie diese analytische Funktion in einer SELECT-Anweisung, um Werte in der aktuellen Zeile mit Werten in einer vorherigen Zeile zu vergleichen.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
LAG (scalar_expression [,offset] [,default])  
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumente  
 *"scalar_expression"*  
 Der zurückzugebende Wert auf Grundlage des angegebenen Offsets. Dies ist ein Ausdruck eines beliebigen Typs, der einen einzelnen Skalarwert zurückgibt. *"scalar_expression"* darf nicht keine analytische Funktion sein.  
  
 *Offset*  
 Die Anzahl der Zeilen vor der aktuellen Zeile, aus der ein Wert abgerufen werden soll. Wenn nichts angegeben ist, wird der Standardwert 1 verwendet. *Offset* kann eine Spalte, Unterabfrage oder ein anderer Ausdruck, der eine positive ganze Zahl ergibt oder implizit umgewandelt werden kann **"bigint"**. *Offset* darf nicht negativ oder keine analytische Funktion sein.  
  
 *Standardwert*  
 Der zurückzugebende Wert, wenn *"scalar_expression"* am *Offset* ist NULL. Wenn kein Standardwert angegeben ist, wird NULL zurückgegeben. *standardmäßige* kann eine Spalte, Unterabfrage oder ein anderer Ausdruck sein, jedoch keine analytische Funktion. *standardmäßige* typkompatibel sein muss mit *"scalar_expression"*.  
  
 ÜBER **(** [ *Partition_by_clause* ] *Order_by_clause***)**  
 *Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *Order_by_clause* bestimmt die Reihenfolge der Daten, bevor die Funktion angewendet wird. Wenn *Partition_by_clause* angegeben wird, bestimmt die Reihenfolge der Daten in der Partition. Die *Order_by_clause* ist erforderlich. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Der Datentyp des angegebenen *"scalar_expression"*. NULL wird zurückgegeben, wenn *"scalar_expression"* NULL-Werte zulässt oder *Standard* auf NULL festgelegt ist.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 LAG ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-compare-values-between-years"></a>A. Vergleichen von Werten aus verschiedenen Jahren  
 Im folgenden Beispiel wird mithilfe der LAG-Funktion die Differenz der Verkaufszahlen für einen bestimmten Mitarbeiter im Verlauf der Vorjahre zurückgegeben. Beachten Sie, dass der Standardwert 0 (null) zurückgegeben wird, da für die erste Zeile kein LAG-Wert verfügbar ist.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
       LAG(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS PreviousQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 and YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
BusinessEntityID SalesYear   CurrentQuota          PreviousQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             0.00  
275              2005        556000.00             367000.00  
275              2006        502000.00             556000.00  
275              2006        550000.00             502000.00  
275              2006        1429000.00            550000.00  
275              2006        1324000.00            1429000.00  
  
```  
  
### <a name="b-compare-values-within-partitions"></a>B. Vergleichen von Werten innerhalb von Partitionen  
 Im folgenden Beispiel werden mithilfe der LAG-Funktion die Verkaufszahlen des laufenden Jahres verschiedener Mitarbeiter verglichen. Um die Zeilen im Resultset nach Vertriebsgebiet zu unterteilen, wird die PARTITION BY-Klausel angegeben. Die LAG-Funktion wird auf jede Partition einzeln angewendet, und die Berechnung wird für jede Partition neu gestartet. Die ORDER BY-Klausel in der OVER-Klausel sortiert die Zeilen in jeder Partition. Die ORDER BY-Klausel in der SELECT-Anweisung sortiert die Zeilen im gesamten Resultset. Beachten Sie, dass der Standardwert 0 (null) zurückgegeben wird, da für die erste Zeile jeder Partition kein LAG-Wert verfügbar ist.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LAG (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS PrevRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
TerritoryName            BusinessEntityID SalesYTD              PrevRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          0.00  
Canada                   278              1453719.4653          2604540.7172  
Northwest                284              1576562.1966          0.00  
Northwest                283              1573012.9383          1576562.1966  
Northwest                280              1352577.1325          1573012.9383  
  
```  
  
### <a name="c-specifying-arbitrary-expressions"></a>C. Angeben willkürlicher Ausdrücke  
 Im folgenden Beispiel wird das Angeben verschiedener willkürlicher Ausdrücke in der Syntax der LAG-Funktion veranschaulicht.  
  
```  
CREATE TABLE T (a int, b int, c int);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LAG(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
b           c           i  
----------- ----------- -----------  
1           -3          1  
2           4           -2  
1           NULL        8  
3           1           -6  
2           NULL        NULL  
1           5           NULL  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-compare-values-between-quarters"></a>D: vergleicht Werte verschiedener Quartale  
 Das folgende Beispiel veranschaulicht die LAG-Funktion. Die Abfrage verwendet die LAG-Funktion, um die Differenz der Verkaufszahlen für einen bestimmten Mitarbeiter über vorherige Kalenderquartale zurückzugeben. Beachten Sie, dass der Standardwert 0 (null) zurückgegeben wird, da für die erste Zeile kein LAG-Wert verfügbar ist.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear, CalendarQuarter, SalesAmountQuota AS SalesQuota,  
       LAG(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS PrevQuota,  
       SalesAmountQuota - LAG(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001, 2002)  
ORDER BY CalendarYear, CalendarQuarter;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year Quarter  SalesQuota  PrevQuota  Diff  
---- -------  ----------  ---------  -------------  
2001 3        28000.0000      0.0000   28000.0000  
2001 4         7000.0000  28000.0000  -21000.0000  
2001 1        91000.0000   7000.0000   84000.0000  
2002 2       140000.0000  91000.0000   49000.0000  
2002 3         7000.0000 140000.0000  -70000.0000  
2002 4       154000.0000   7000.0000   84000.0000
```  
  
## <a name="see-also"></a>Siehe auch  
 [LEAD &#40; Transact-SQL &#41;](../../t-sql/functions/lead-transact-sql.md)  
  
  



