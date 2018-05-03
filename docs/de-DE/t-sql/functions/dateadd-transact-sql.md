---
title: DATEADD (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/29/2017
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
- DATEADD
- DATEADD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: 71
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dd7dd81f8e12b0c14048fd8ab550e7edfd780cf5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt einen angegebenen *date*-Wert zurück, wobei das angegebene *number*-Intervall (ganze Zahl mit Vorzeichen) einem angegebenen *datepart*-Wert für diesen *date*-Wert hinzugefügt wird.
  
Eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] finden Sie unter [Date and Time Data Types and Functions &#40;Transact-SQL&#41; (Datums- und Uhrzeitdatentypen und zugehörige Funktionen)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Ist Teil von *date*, zu dem ein **ganzzahliges** *number*-Intervall hinzugefügt wird. In der folgenden Tabelle werden alle gültigen *datepart*-Argumente aufgeführt. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**, **w**|  
|**hour**|**hh**|  
|**minute**|**mi**, **n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*number*  
Ein Ausdruck, der in einen [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)-Wert aufgelöst werden kann, der einem *datepart*-Wert vom Datentyp *date* hinzugefügt wird. Benutzerdefinierte Variablen sind gültig.  
Wenn Sie einen Wert mit einem Dezimalbruch angeben, wird der Bruch abgeschnitten und nicht gerundet.
  
*Datum*  
Ein Ausdruck, der in einen der folgenden Werte aufgelöst werden kann: **time**, **date**, **smalldatetime**, **datetime**, **datetime2** oder **datetimeoffset**. *date* kann ein Ausdruck, ein Spaltenausdruck, eine benutzerdefinierte Variable oder ein Zeichenfolgenliteral sein. Wenn der Ausdruck ein Zeichenfolgenliteral ist, muss er in **datetime** aufgelöst werden. Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Umstellungsjahr für Angaben mit zwei Ziffern“](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-types"></a>Rückgabetypen
Beim Rückgabedatentyp handelt es sich um den Datentyp des *date*-Arguments. Eine Ausnahme bilden hier Zeichenfolgenliterale.
Der Rückgabedatentyp für ein Zeichenfolgenliteral ist **datetime**. Wenn die Dezimalstellen für die Sekunden des Zeichenfolgenliterals mehr als drei Positionen (.nnn) umfassen oder einen Zeitzonenoffset-Teil enthalten, wird ein Fehler ausgelöst.
  
## <a name="return-value"></a>Rückgabewert  
  
## <a name="datepart-argument"></a>datepart-Argument  
**dayofyear**, **day** und **weekday** geben den gleichen Wert zurück.
  
Jedes *datepart*-Argument und die zugehörigen Abkürzungen geben den gleichen Wert zurück.
  
Wenn *datepart* den Wert **month** aufweist, der für *date* angegebene Monat mehr Tage umfasst als der Rückgabemonat und der für *date* angegebene Tag nicht im Rückgabemonat vorhanden ist, wird der letzte Tag des Rückgabemonats zurückgegeben. Beispiel: Der September hat 30 Tage. Daher geben die beiden folgenden Anweisungen 2006-09-30 00:00:00.000 zurück:
  
```sql
SELECT DATEADD(month, 1, '20060830');
SELECT DATEADD(month, 1, '20060831');
```
  
## <a name="number-argument"></a>number-Argument  
Das *number*-Argument kann den Bereich von **int** nicht überschreiten. In den folgenden Anweisungen überschreitet das Argument für *number* den Bereich von **int** um 1. Die folgende Fehlermeldung wird zurückgegeben: "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '20060731');  
SELECT DATEADD(year,-2147483649, '20060731');  
```  
  
## <a name="date-argument"></a>date-Argument  
Das *date*-Argument kann nicht zu einem Wert außerhalb des Bereichs seines Datentyps inkrementiert werden. In den folgenden Anweisungen überschreitet der *number*-Wert, der dem *date*-Wert hinzugefügt wird, den Bereich des *date*-Datentyps. Die folgende Fehlermeldung wird zurückgegeben: "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '20060731');  
SELECT DATEADD(year,-2147483647, '20060731');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>Rückgabewerte für ein Datum vom Typ smalldatetime und einen datepart-Wert in Sekunden oder Sekundenbruchteilen  
Die Sekundenangabe eines [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)-Werts ist immer 00. Wenn *date* ein **smalldatetime**-Wert ist, gilt Folgendes:
-   Wenn *datepart* ein **second**-Wert ist und *number* zwischen –30 und +29 liegt, wird keine Addition durchgeführt.  
-   Wenn *datepart* ein **second**-Wert ist und *number* kleiner als –30 oder größer als +29 ist, wird die Addition beginnend bei einer Minute durchgeführt.  
-   Wenn *datepart* ein **millisecond**-Wert ist und *number* zwischen –30001 und +29998 liegt, wird keine Addition durchgeführt.  
-   Wenn *datepart* ein **millisecond**-Wert ist und *number* kleiner als –30001 oder größer als +29998 ist, wird die Addition beginnend bei einer Minute durchgeführt.  
  
## <a name="remarks"></a>Remarks  
DATEADD kann in den Klauseln SELECT \<list>, WHERE, HAVING, GROUP BY und ORDER BY verwendet werden.
  
## <a name="fractional-seconds-precision"></a>Genauigkeit in Millisekunden
Die Addition ist für *datepart* mit **microsecond**- oder **nanosecond**-Werten für die *date*-Datentypen **smalldatetime**, **date** und **datetime** nicht zulässig.
  
Millisekunden besitzen drei Dezimalstellen (.123). Mikrosekunden besitzen sechs Dezimalstellen (.123456). Nanosekunden besitzen neun Dezimalstellen (.123456789). Die Datentypen **time**, **datetime2** und **datetimeoffset** weisen maximal 7 Dezimalstellen (,1234567) auf. Wenn *datepart* ein **nanosecond**-Wert ist, muss *number* den Wert 100 aufweisen, bevor die Sekundenbruchteile von *date* erhöht werden. Hat *number* einen Wert zwischen 1 und 49, wird auf 0 abgerundet. Eine Zahl zwischen 50 und 99 wird auf 100 aufgerundet.
  
Die folgende Anweisung fügt *datepart* mit einem **millisecond**-, **microsecond**- oder **nanosecond**-Wert hinzu.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>Zeitzonenoffset
Für einen Zeitzonenoffset ist Addition nicht zulässig.
  
## <a name="examples"></a>Beispiele  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>A. Inkrementieren von datepart mit einem Intervall von 1  
Jede der folgenden Anweisungen inkrementiert *datepart* mit einem Intervall von 1.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>B. Inkrementieren mehrerer Ebenen von datepart in einer Anweisung  
Jede der folgenden Anweisungen inkrementiert *datepart* um einen *number*-Wert, der hoch genug ist, um auch den nächsthöheren *datepart*-Wert von *date* zu inkrementieren.
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>C. Verwenden von Ausdrücken als Argumente für den number-Parameter und den date-Parameter  
In den folgenden Beispielen werden verschiedene Typen von Ausdrücken als Argumente für den *number*- und den *date*-Parameter verwendet. In den Beispielen wird die Datenbank „AdventureWorks“ verwendet.
  
#### <a name="specifying-a-column-as-date"></a>Angeben einer Spalte als date-Parameter  
Im folgenden Beispiel werden zu jedem Wert in der `2`-Spalte `OrderDate` Tage hinzuaddiert, um eine neue Spalte mit dem Namen `PromisedShipDate` abzuleiten.
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
Dies ist ein Auszug aus dem Resultset.
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>Angeben von benutzerdefinierten Variablen als Argumente für number und date  
Im folgenden Beispiel werden benutzerdefinierte Variablen als Argumente für *number* und *date* angegeben.
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>Angeben einer skalaren Systemfunktion als Argument für date  
Im folgenden Beispiel wird `SYSDATETIME` für *date* angegeben.
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>Angeben von skalaren Unterabfragen und skalaren Funktionen als Argumente für number und date  
Im folgenden Beispiel werden skalare Unterabfragen (`MAX(ModifiedDate)`) als Argumente für *number* und *date* verwendet. `(SELECT TOP 1 BusinessEntityID FROM Person.Person)` ist ein Beispielargument für den number-Parameter, das veranschaulicht, wie ein *number*-Argument aus einer Werteliste ausgewählt wird.
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>Angeben von numerischen Ausdrücken und skalaren Systemfunktionen als Argumente für number und date  
Im folgenden Beispiel werden numerische Ausdrücke (–`(10/2))`, [unäre Operatoren](../../mdx/unary-operators.md) (`-`), ein [arithmetischer Operator](../../mdx/arithmetic-operators.md) (`/`) und skalare Systemfunktionen (`SYSDATETIME`) als Argumente für *number* und *date* verwendet.
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>Angeben von Rangfolgefunktionen als Argumente für number  
Im folgenden Beispiel wird eine Rangfolgefunktion als Argument für *number* verwendet.
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>Angeben einer Aggregatfensterfunktion als Argument für number  
Im folgenden Beispiel wird eine Aggregatfensterfunktion als Argument für *number* verwendet.
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

