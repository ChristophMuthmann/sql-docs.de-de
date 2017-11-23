---
title: LAST_VALUE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAST_VALUE
- LAST_VALUE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- analytic functions, LAST_VALUE
- LAST_VALUE function
ms.assetid: fd833e34-8092-42b7-80fc-95ca6b0eab6b
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0ae5fbf63898d56e9af53a096c666a30d9fb1b77
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="lastvalue-transact-sql"></a>LAST_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Gibt den letzten Wert in einer geordneten Wertemenge in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LAST_VALUE ( [scalar_expression )   
    OVER ( [ partition_by_clause ] order_by_clause rows_range_clause )   
```  
  
## <a name="arguments"></a>Argumente  
 *"scalar_expression"*  
 Der zurückzugebende Wert. *"scalar_expression"* kann eine Spalte, Unterabfrage oder ein anderer Ausdruck, der sich in einem einzelnen Wert ergibt. Andere analytische Funktionen sind nicht zulässig.  
  
 ÜBER **(** [ *Partition_by_clause* ] *Order_by_clause* [ *Rows_range_clause* ] **)**  
 *Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe.  
  
 *Order_by_clause* bestimmt die Reihenfolge der Daten, bevor die Funktion angewendet wird. Die *Order_by_clause* ist erforderlich. *Rows_range_clause* weiter schränkt die Zeilen in der Partition durch Angabe der Start- und Endpunkt. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Ist vom selben Typ wie *"scalar_expression"*.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 LAST_VALUE ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-lastvalue-over-partitions"></a>A. Partitionsweise Verwendung von LAST_VALUE  
 Im folgenden Beispiel wird das Einstellungsdatum des letzten Mitarbeiters in jeder Abteilung für das angegebene Gehalt ("Rate") zurückgegeben. Die PARTITION BY-Klausel partitioniert die Mitarbeiter nach Abteilung, und die LAST_VALUE-Funktion wird auf jede Partition separat angewendet. Die in der OVER-Klausel angegebene ORDER BY-Klausel bestimmt die logische Reihenfolge, in der die LAST_VALUE-Funktion auf die Zeilen in jeder Partition angewendet wird.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate, HireDate,   
    LAST_VALUE(HireDate) OVER (PARTITION BY Department ORDER BY Rate) AS LastValue  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
INNER JOIN HumanResources.EmployeePayHistory AS eph    
    ON eph.BusinessEntityID = edh.BusinessEntityID  
INNER JOIN HumanResources.Employee AS e  
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department                  LastName                Rate         HireDate     LastValue  
--------------------------- ----------------------- ------------ ----------   ----------  
Document Control            Chai                    10.25        2003-02-23   2003-03-13  
Document Control            Berge                   10.25        2003-03-13   2003-03-13  
Document Control            Norred                  16.8269      2003-04-07   2003-01-17  
Document Control            Kharatishvili           16.8269      2003-01-17   2003-01-17  
Document Control            Arifin                  17.7885      2003-02-05   2003-02-05  
Information Services        Berg                    27.4038      2003-03-20   2003-01-24  
Information Services        Meyyappan               27.4038      2003-03-07   2003-01-24  
Information Services        Bacon                   27.4038      2003-02-12   2003-01-24  
Information Services        Bueno                   27.4038      2003-01-24   2003-01-24  
Information Services        Sharma                  32.4519      2003-01-05   2003-03-27  
Information Services        Connelly                32.4519      2003-03-27   2003-03-27  
Information Services        Ajenstat                38.4615      2003-02-18   2003-02-23  
Information Services        Wilson                  38.4615      2003-02-23   2003-02-23  
Information Services        Conroy                  39.6635      2003-03-08   2003-03-08  
Information Services        Trenary                 50.4808      2003-01-12   2003-01-12  
  
```  
  
### <a name="b-using-firstvalue-and-lastvalue-in-a-computed-expression"></a>B. Verwenden von FIRST_VALUE und LAST_VALUE in einem berechneten Ausdruck  
 Im folgenden Beispiel werden die FIRST_VALUE-Funktion und die LAST_VALUE-Funktion in berechneten Ausdrücken verwendet, um den Unterschied zwischen den Verkaufszahlen für das laufende Quartal und das erste bzw. letzte Quartal des Jahres für eine bestimmte Anzahl von Mitarbeitern aufzuzeigen. Die FIRST_VALUE-Funktion gibt den Verkaufszahlenwert für das erste Quartal des Jahres zurück und subtrahiert diesen von den Verkaufszahlen für das aktuelle Quartal. Der Wert wird in der abgeleiteten Spalte mit dem Titel "DifferenceFromFirstQuarter" zurückgegeben. Für das erste Quartal eines Jahres ist der Wert der Spalte "DifferenceFromFirstQuarter" 0. Die LAST_VALUE-Funktion gibt den Verkaufszahlenwert für das letzte Quartal des Jahres zurück und subtrahiert diesen von den Verkaufszahlen für das aktuelle Quartal. Der Wert wird in der abgeleiteten Spalte mit dem Titel "DifferenceFromLastQuarter" zurückgegeben. Für das letzte Quartal eines Jahres ist der Wert der Spalte "DifferenceFromLastQuarter" 0.  
  
 Die Klausel "RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING" muss in diesem Beispiel für die Werte ungleich NULL in der Spalte "DifferenceFromLastQuarter" zurückgegeben werden, wie unten dargestellt. Der Standardbereich lautet "RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW". In diesem Beispiel führt die Verwendung dieses Standardbereichs (oder ausschließlich eines Bereichs, wodurch der Standardbereich verwendet wird) dazu, dass Nullen (0) in der Spalte "DifferenceFromLastQuarter" zurückgegeben werden. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
SELECT BusinessEntityID, DATEPART(QUARTER,QuotaDate)AS Quarter, YEAR(QuotaDate) AS SalesYear,   
    SalesQuota AS QuotaThisQuarter,   
    SalesQuota - FIRST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate) ) AS DifferenceFromFirstQuarter,   
    SalesQuota - LAST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate)   
              RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING ) AS DifferenceFromLastQuarter   
FROM Sales.SalesPersonQuotaHistory   
WHERE YEAR(QuotaDate) > 2005   
AND BusinessEntityID BETWEEN 274 AND 275   
ORDER BY BusinessEntityID, SalesYear, Quarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Quarter     SalesYear   QuotaThisQuarter      DifferenceFromFirstQuarter DifferenceFromLastQuarter  
---------------- ----------- ----------- --------------------- --------------------------- -----------------------  
274              1           2006        91000.00              0.00                        -63000.00  
274              2           2006        140000.00             49000.00                    -14000.00  
274              3           2006        70000.00              -21000.00                   -84000.00  
274              4           2006        154000.00             63000.00                    0.00  
274              1           2007        107000.00             0.00                        -9000.00  
274              2           2007        58000.00              -49000.00                   -58000.00  
274              3           2007        263000.00             156000.00                   147000.00  
274              4           2007        116000.00             9000.00                     0.00  
274              1           2008        84000.00              0.00                        -103000.00  
274              2           2008        187000.00             103000.00                   0.00  
275              1           2006        502000.00             0.00                        -822000.00  
275              2           2006        550000.00             48000.00                    -774000.00  
275              3           2006        1429000.00            927000.00                   105000.00  
275              4           2006        1324000.00            822000.00                   0.00  
275              1           2007        729000.00             0.00                        -489000.00  
275              2           2007        1194000.00            465000.00                   -24000.00  
275              3           2007        1575000.00            846000.00                   357000.00  
275              4           2007        1218000.00            489000.00                   0.00  
275              1           2008        849000.00             0.00                        -20000.00  
275              2           2008        869000.00             20000.00                    0.00  
  
(20 row(s) affected)  
  
```  
  
  
