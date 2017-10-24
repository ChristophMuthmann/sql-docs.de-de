---
title: VAR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VAR
- VAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VAR function [Transact-SQL]
ms.assetid: 71dfc339-16c8-42f9-8555-ad45400f7f9b
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 677b8eae4863b18d5e94e8c7f577d13ebfe01031
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="var-transact-sql"></a>VAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die statistische Varianz aller Werte im angegebenen Ausdruck zurück. Gefolgt von der [OVER-Klausel](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
VAR ( [ ALL | DISTINCT ] expression )   
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
VAR ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VAR (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>Argumente  
 **ALL**  
 Wendet die Funktion auf alle Werte an. ALL ist die Standardeinstellung.  
  
 DISTINCT  
 Gibt an, dass jeder eindeutige Wert berücksichtigt wird.  
  
 *expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme der **Bit** -Datentyp. Aggregatfunktionen und Unterabfragen sind nicht zulässig.  
  
 ÜBER **(** [ *Partition_by_clause* ] *Order_by_clause***)**  
 *Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *Order_by_clause* bestimmt die logische Reihenfolge, in dem der Vorgang ausgeführt wird. *Order_by_clause* ist erforderlich. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **float**  
  
## <a name="remarks"></a>Hinweise  
 Falls VAR für alle Elemente einer SELECT-Anweisung verwendet wird, werden alle Werte im Resultset in die Berechnung eingeschlossen. VAR kann nur bei numerischen Spalten verwendet werden. NULL-Werte werden ignoriert.  
  
 VAR ist eine deterministische Funktion, wenn sie ohne die OVER- und ORDER BY-Klauseln angegeben wird. Sie ist nicht deterministisch, wenn sie mit den OVER- und ORDER BY-Klauseln angegeben wird. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-var"></a>A: verwenden VAR.  
 Im folgenden Beispiel wird die Varianz aller Bonuswerte in der `SalesPerson`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
SELECT VAR(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-var"></a>B: verwenden VAR.  
 Im folgende Beispiel gibt die statistische Varianz der sales Quota-Werte in der Tabelle `dbo.FactSalesQuota`. Die erste Spalte enthält die Varianz der unterschiedlichen Werte und die zweite Spalte enthält die Varianz aller Werte, einschließlich aller Duplikate-Werte.  
  
```  
-- Uses AdventureWorks  
  
SELECT VAR(DISTINCT SalesAmountQuota)AS Distinct_Values, VAR(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
159180469909.18   158762853821.10
 ```  
  
### <a name="c-using-var-with-over"></a>C. Verwenden VAR mit Failover  
 Im folgende Beispiel gibt die statistische Varianz der sollvorgaben für jedes Quartal in ein Kalenderjahr zurück. Beachten Sie, dass die ORDER BY in der OVER-Klausel die statistische Varianz und der ORDER BY der SELECT-Anweisung sortiert sortiert das Resultset.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VAR(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             1200500000.00
2002  3         70000.0000             1290333333.33
2002  4        154000.0000             1580250000.00
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Aggregatfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [Failover-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


