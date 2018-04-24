---
title: LEAD (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/09/2017
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
- LEAD_TSQL
- LEAD
dev_langs:
- TSQL
helpviewer_keywords:
- LEAD function
- analytic functions, LEAD
ms.assetid: 21f66bbf-d1ea-4f75-a3c4-20dc7fc1c69e
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 255f5ab3de4d7a9f045df6179f43da8b16bd6f31
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="lead-transact-sql"></a>LEAD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Greift im selben Resultset auf Daten in einer nachfolgenden Zeile zu, ohne dass ein Selbstjoin ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] verwendet wird. LEAD ermöglicht den Zugriff auf eine Zeile mit einem bestimmten physischen Offset nach der aktuellen Zeile. Verwenden Sie diese analytische Funktion in einer SELECT-Anweisung, um Werte in der aktuellen Zeile mit Werten in einer nachfolgenden Zeile zu vergleichen.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
LEAD ( scalar_expression [ ,offset ] , [ default ] )   
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumente  
 *scalar_expression*  
 Der zurückzugebende Wert auf Grundlage des angegebenen Offsets. Dies ist ein Ausdruck eines beliebigen Typs, der einen einzelnen Skalarwert zurückgibt. *scalar_expression* darf keine analytische Funktion sein.  
  
 *offset*  
 Die Anzahl der Zeilen nach der aktuellen Zeile, aus der ein Wert abgerufen werden soll. Wenn nichts angegeben ist, wird der Standardwert 1 verwendet. *offset* kann eine Spalte, eine Unterabfrage oder ein anderer Ausdruck sein, der eine positive ganze Zahl ergibt, kann aber auch implizit in einen Wert vom Typ **bigint** konvertiert werden. *offset* darf kein negativer Wert bzw. keine analytische Funktion sein.  
  
 *default*  
 Der zurückzugebende Wert, wenn *scalar_expression* bei *offset* NULL ist. Wenn kein Standardwert angegeben ist, wird NULL zurückgegeben. *default* kann eine Spalte, eine Unterabfrage oder ein anderer Ausdruck sein, jedoch keine analytische Funktion. *default* muss mit *scalar_expression* typkompatibel sein.  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* unterteilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *order_by_clause* bestimmt die Reihenfolge der Daten, bevor die Funktion angewendet wird. Wenn *partition_by_clause* angegeben wird, wird hierdurch die Reihenfolge der Daten in jeder Partition bestimmt. *order_by_clause* ist erforderlich. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Der Datentyp des angegebenen *scalar_expression*-Ausdrucks. NULL wird zurückgegeben, wenn *scalar_expression* auf NULL festgelegt werden kann oder *default* auf NULL festgelegt ist.  
  
 LEAD ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-compare-values-between-years"></a>A. Vergleichen von Werten aus verschiedenen Jahren  
 Die Abfrage gibt mithilfe der LEAD-Funktion die Differenz zwischen den Umsatzzahlen eines bestimmten Mitarbeiters in Folgejahren zurück. Beachten Sie, dass der Standardwert 0 (null) zurückgegeben wird, da für die letzte Zeile kein LEAD-Wert verfügbar ist.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
    LEAD(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS NextQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 and YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID SalesYear   CurrentQuota          NextQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             556000.00  
275              2005        556000.00             502000.00  
275              2006        502000.00             550000.00  
275              2006        550000.00             1429000.00  
275              2006        1429000.00            1324000.00  
275              2006        1324000.00            0.00  
```  
  
### <a name="b-compare-values-within-partitions"></a>B. Vergleichen von Werten innerhalb von Partitionen  
 Im folgenden Beispiel werden mithilfe der LEAD-Funktion die Verkaufszahlen des laufenden Jahres verschiedener Mitarbeiter verglichen. Um die Zeilen im Resultset nach Vertriebsgebiet zu partitionieren, wird die PARTITION BY-Klausel angegeben. Die LEAD-Funktion wird auf jede Partition einzeln angewendet, und die Berechnung wird für jede Partition neu gestartet. Durch die in der OVER-Klausel angegebene ORDER BY-Klausel werden die Zeilen in jeder Partition sortiert, bevor die Funktion angewendet wird. Die ORDER BY-Klausel in der SELECT-Anweisung sortiert die Zeilen im gesamten Resultset. Beachten Sie, dass der Standardwert 0 (null) zurückgegeben wird, da für die letzte Zeile jeder Partition kein LEAD-Wert verfügbar ist.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LEAD (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS NextRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```   
TerritoryName            BusinessEntityID SalesYTD              NextRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          1453719.4653  
Canada                   278              1453719.4653          0.00  
Northwest                284              1576562.1966          1573012.9383  
Northwest                283              1573012.9383          1352577.1325  
Northwest                280              1352577.1325          0.00  
  
```  
  
### <a name="c-specifying-arbitrary-expressions"></a>C. Angeben willkürlicher Ausdrücke  
 Im folgenden Beispiel wird das Angeben verschiedener willkürlicher Ausdrücke in der Syntax der LEAD-Funktion veranschaulicht.  
  
```sql  
CREATE TABLE T (a int, b int, c int);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LEAD(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
b           c           i  
----------- ----------- -----------  
1           -3          8  
2           4           2  
1           NULL        2  
3           1           0  
2           NULL        NULL  
1           5           -2  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-compare-values-between-quarters"></a>D: Vergleichen von Werten aus verschiedenen Quartalen  
 Im folgenden Beispiel wird die LEAD-Funktion vorgestellt. Die Abfrage ruft den Unterschied in den Sollvorgabenwerten für den Verkauf für einen angegebenen Mitarbeiter über nachfolgende Kalenderquartale ab. Beachten Sie, dass der Standardwert 0 (null) verwendet wird, da nach der letzten Zeile kein LEAD-Wert verfügbar ist.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       LEAD(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS NextQuota,  
   SalesAmountQuota - LEAD(Sale sAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001,2002)  
ORDER BY CalendarYear, CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year Quarter  SalesQuota  NextQuota  Diff  
---- -------  ----------  ---------  -------------  
2001 3        28000.0000   7000.0000   21000.0000 
2001 4         7000.0000  91000.0000  -84000.0000  
2001 1        91000.0000 140000.0000  -49000.0000  
2002 2       140000.0000   7000.0000    7000.0000  
2002 3         7000.0000 154000.0000   84000.0000  
2002 4       154000.0000      0.0000  154000.0000
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LAG &#40;Transact-SQL&#41;](../../t-sql/functions/lag-transact-sql.md)  
  
  


