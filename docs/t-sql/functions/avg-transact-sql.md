---
title: AVG (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG_TSQL
- AVG
dev_langs:
- TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 40240e2c06055d61eb047c319349f4869b9979df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt den Mittelwert der Werte in einer Gruppe zurück. NULL-Werte werden ignoriert.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>Argumente  
ALL  
Wendet die Aggregatfunktion auf alle Werte an. ALL ist die Standardeinstellung.
  
DISTINCT  
Gibt an, dass AVG nur für jede eindeutige Instanz eines Werts ausgeführt werden soll, unabhängig davon, wie oft der Wert vorkommt.
  
*expression*  
Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme des **bit**-Datentyps. Aggregatfunktionen und Unterabfragen sind nicht zulässig.
  
OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* unterteilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *order_by_clause* bestimmt die logische Reihenfolge, in der der Vorgang ausgeführt wird. *order_by_clause* ist erforderlich. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Rückgabetypen
Der Rückgabetyp wird durch den Typ des ausgewerteten Ergebnisses von *expression* bestimmt.
  
|Ausdrucksergebnis|Rückgabetyp|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**decimal**-Kategorie (p, s)|**decimal(38, s)** geteilt durch **decimal(10, 0)**|  
|**money**- und **smallmoney**-Kategorie|**money**|  
|**float**- und **real**-Kategorie|**float**|  
  
## <a name="remarks"></a>Remarks  
Wenn der Datentyp von *expression* ein Aliasdatentyp ist, ist der Rückgabetyp ebenfalls ein Aliasdatentyp. Wird der Basisdatentyp des Aliasdatentyps jedoch heraufgestuft, beispielsweise von **tinyint** zu **int**, handelt es sich beim Rückgabetyp um den heraufgestuften Datentyp und nicht um den Aliasdatentyp.
  
AVG () berechnet den Durchschnitt einer Menge von Werten, indem die Summe dieser Werte durch die Anzahl der Nicht-NULL-Werte dividiert wird. Wenn die Summe größer als der vom Datentyp des Rückgabewerts unterstützte Höchstwert ist, wird ein Fehler zurückgegeben.
  
AVG ist eine deterministische Funktion, wenn sie ohne die OVER- und ORDER BY-Klauseln angegeben wird. Sie ist nicht deterministisch, wenn sie mit den OVER- und ORDER BY-Klauseln angegeben wird. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>A. Verwenden der Funktionen SUM und AVG für Berechnungen  
Im folgenden Beispiel werden die durchschnittlichen Urlaubstage und die Summe der Krankheitstage (in Stunden) der stellvertretenden Direktoren von [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] berechnet. Beide Aggregatfunktionen erzeugen jeweils einen zusammenfassenden Wert aller abgerufenen Zeilen. Im Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Average vacation hours       Total sick leave hours
 ----------------------       ----------------------
25                           97
  
(1 row(s) affected)
```
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>B. Verwenden der Funktionen SUM und AVG mit einer GROUP BY-Klausel  
In Verbindung mit einer `GROUP BY`-Klausel erzeugt jede Aggregatfunktion einen einzelnen Wert für jede Gruppe anstelle eines Werts für die gesamte Tabelle. Im folgenden Beispiel werden für alle Vertriebsgebiete in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank Zusammenfassungswerte erzeugt. In der Zusammenfassung werden die durchschnittlichen Bonusleistungen von Vertriebsmitarbeitern der einzelnen Regionen und die Summe der Verkaufszahlen für das laufende Jahr pro Region aufgelistet.
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>C. Verwenden von AVG mit DISTINCT  
Mit der folgenden Anweisung wird der durchschnittliche Listenpreis der Produkte in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. Durch Angabe von DISTINCT werden nur eindeutige Werte in der Berechnung berücksichtigt.
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
437.4042
  
(1 row(s) affected)
```
  
### <a name="d-using-avg-without-distinct"></a>D. Verwenden von AVG ohne DISTINCT  
Ohne DISTINCT wird mithilfe der `AVG`-Funktion der durchschnittliche Listenpreis aller Produkte in der `Product`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank gesucht, einschließlich aller doppelten Werte.
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
438.6662
  
(1 row(s) affected)
```
  
### <a name="e-using-the-over-clause"></a>E. Verwenden der OVER-Klausel  
Im folgenden Beispiel wird die AVG-Funktion mit der OVER-Klausel verwendet, um einen gleitenden Durchschnitt des Jahresumsatzes für jedes Gebiet in der `Sales.SalesPerson`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank bereitzustellen. Die Daten werden nach `TerritoryID` partitioniert und logisch nach `SalesYTD` sortiert. Folglich wird die AVG-Funktion auf Grundlage des Verkaufsjahres für jedes Gebiet berechnet. Beachten Sie, dass für `TerritoryID` 1 zwei Zeilen für das Verkaufsjahr 2005 vorhanden sind, die die beiden Vertriebsmitarbeiter mit dem Umsatz aus diesem Jahr darstellen. Der durchschnittliche Umsatz für diese zwei Zeilen wird berechnet, und anschließend wird die dritte Zeile, die den Umsatz für das Jahr 2006 darstellt, in die Berechnung einbezogen.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
In diesem Beispiel ist PARTITION BY nicht in der OVER-Klausel enthalten. Folglich wird die Funktion auf alle von der Abfrage zurückgegebenen Zeilen angewendet. Die in der OVER-Klausel angegebene ORDER BY-Klausel bestimmt die logische Reihenfolge, auf die die AVG-Funktion angewendet wird. Die Abfrage gibt einen gleitenden Durchschnitt der Jahresumsätze für alle Vertriebsgebiete zurück, die in der WHERE-Klausel angegeben sind. Die in der SELECT-Anweisung angegebene ORDER BY-Klausel bestimmt die Reihenfolge, in der die Zeilen der Abfrage angezeigt werden.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[Aggregate Functions &#40;Transact-SQL&#41; (Aggregatfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
