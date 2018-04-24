---
title: STDEVP (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/13/2017
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
- STDEVP
- STDEVP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDEVP function [Transact-SQL]
- expressions [SQL Server], statistical standard deviation
- statistical standard deviation
ms.assetid: 29f2a906-d084-4464-abc3-4b275ed19442
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1e4a234c179fb4530acd3fbef5bf7beecfaa7853
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stdevp-transact-sql"></a>STDEVP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die statistische Standardabweichung für die Grundgesamtheit (Population) aller Werte des angegebenen Ausdrucks zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
STDEVP ( [ ALL | DISTINCT ] expression )   
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
STDEVP ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax   
STDEVP (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>Argumente  
 **ALL**  
 Wendet die Funktion auf alle Werte an. ALL ist die Standardeinstellung.  
  
 DISTINCT  
 Gibt an, dass jeder eindeutige Wert berücksichtigt wird.  
  
 *expression*  
 Ein numerischer [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md). Aggregatfunktionen und Unterabfragen sind nicht zulässig. Bei *expression* handelt es sich um einen Ausdruck der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme des **bit**-Datentyps.  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* unterteilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *order_by_clause* bestimmt die logische Reihenfolge, in der der Vorgang ausgeführt wird. *order_by_clause* ist erforderlich. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **float**  
  
## <a name="remarks"></a>Remarks  
 Falls STDEVP für alle Elemente einer SELECT-Anweisung verwendet wird, werden alle Werte im Resultset in die Berechnung eingeschlossen. STDEVP kann nur bei numerischen Spalten verwendet werden. NULL-Werte werden ignoriert.  
  
 STDEVP ist eine deterministische Funktion, wenn sie ohne die OVER- und ORDER BY-Klauseln angegeben wird. Sie ist nicht deterministisch, wenn sie mit den OVER- und ORDER BY-Klauseln angegeben wird. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stdevp"></a>A: Verwenden von STDEVP  
 Im folgenden Beispiel wird die Standardabweichung für die Grundgesamtheit aller Bonuswerte in der `SalesPerson`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
SELECT STDEVP(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="b-using-stdevp"></a>B: Verwenden von STDEVP  
 Das folgende Beispiel gibt in der Tabelle `dbo.FactSalesQuota` die `STDEVP` der Sollvorgabenwerte für den Verkauf zurück. Die erste Spalte enthält die Standardabweichung aller eindeutigen Werte. Die zweite Spalte enthält die Standardabweichung aller Werte, einschließlich aller doppelten Werte.  
  
```  
-- Uses AdventureWorks  
  
SELECT STDEVP(DISTINCT SalesAmountQuota)AS Distinct_Values, STDEVP(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;SELECT STDEVP(DISTINCT Quantity)AS Distinct_Values, STDEVP(Quantity) AS All_Values  
FROM ProductInventory;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values  
----------------  ----------------  
397676.79         397226.44
```  
  
### <a name="c-using-stdevp-with-over"></a>C. Verwenden von STDEVP mit OVER  
 Das folgende Beispiel gibt für jedes Quartal eines Kalenderjahrs die `STDEVP` der Sollvorgabenwerte für den Verkauf zurück. Beachten Sie, dass `ORDER BY` in der `OVER`-Klausel `STDEVP` sortiert und dass `ORDER BY` der `SELECT`-Anweisung das Resultset sortiert.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       STDEVP(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS StdDeviation  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              StdDeviation  
----  -------  ----------------------  -------------------  
2002  1         91000.0000             0.00  
2002  2        140000.0000             24500.00  
2002  3         70000.0000             29329.55  
2002  4        154000.0000             34426.55
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aggregate Functions &#40;Transact-SQL&#41; (Aggregatfunktionen (Transact-SQL))](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

