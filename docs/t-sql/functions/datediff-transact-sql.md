---
title: DATEDIFF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEDIFF_TSQL
- DATEDIFF
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATEDIFF function [SQL Server]
- time [SQL Server], crossed boundaries
- differences in date and time [SQL Server]
- counting crossed date time boundaries [SQL Server]
- date and time [SQL Server], DATEDIFF
- dates [SQL Server], crossed boundaries
- boundary differences date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- interval dates [SQL Server]
- time [SQL Server], functions
- crossing date time boundaries [SQL Server]
- calculating dates times [SQL Server]
ms.assetid: eba979f2-1a8d-4cce-9d75-b74f9b519b37
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8231f0207ed1b0575327ac85f31604132acb590
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Anzahl (Ganzzahl mit Vorzeichen) der angegebenen *Datepart* Grenzen überschritten, zwischen dem angegebenen *"StartDate"* und *Enddate*.
  
Größere Unterschiede finden Sie unter [DATEDIFF_BIG &#40; Transact-SQL &#41; ](../../t-sql/functions/datediff-big-transact-sql.md). Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Ist der Teil des *"StartDate"* und *Enddate* , die den Typ der überschrittenen Begrenzung angibt. Die folgende Tabelle enthält alle gültigen *Datepart* Argumente. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**Jahr**|**Yy, yyyy**|  
|**Quartal**|**Qq, q**|  
|**Monat**|**mm, m**|  
|**DayOfYear**|**dy, y**|  
|**Tag**|**tt, d**|  
|**Woche**|**wk weltweit**|  
|**Stunde**|**hh**|  
|**Minute**|**Mi, n**|  
|**Sekunde**|**ss, s**|  
|**Millisekunde**|**MS**|  
|**in Mikrosekunden**|**MCS**|  
|**Nanosekunden**|**Notification Services**|  
  
*startdate*  
Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. *Datum* kann ein Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolge literal. *"StartDate"* abgezogen *Enddate*.
  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [konfigurieren two Digit Year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*EndDate*  
Finden Sie unter *"StartDate"*.
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
  
-   Jede *Datepart* und zugehörigen Abkürzungen geben denselben Wert zurück.  
  
Wenn der Rückgabewert außerhalb des gültigen Bereichs für **Int** (-2,147,483,648 bis + 2,147,483,647), wird ein Fehler zurückgegeben. Für **Millisekunde**, der maximale Unterschied zwischen *"StartDate"* und *Enddate* beträgt 24 Tage, 20 Stunden, 31 Minuten und 23,647 Sekunden. Für **zweite**, der maximale Unterschied 68 Jahre liegt.
  
Wenn *"StartDate"* und *Enddate* sowohl nur einen Uhrzeitwert zugeordnet werden und die *Datepart* ist nicht *Datepart*, wird 0 zurückgegeben.
  
Ein Zeitzonenoffset Komponente des *"StartDate"* oder *Endate* wird bei der Berechnung des Rückgabewerts nicht verwendet.
  
Da [Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) wird nur auf die Minute, wenn eine **Smalldatetime** Wert wird zum *"StartDate"* oder *Enddate*, Sekunden und Millisekunden immer in der zurückgegebene Wert auf 0 festgelegt sind.
  
Wenn zu einer Variablen eines Datumsdatentyps nur ein Uhrzeitwert zugeordnet wird, wird für den Wert des fehlenden Datumsteils der Standardwert festgelegt: 1900-01-01. Wenn zu einer Variablen eines Uhrzeit- oder Datumsdatentyps nur ein Datumswert zugeordnet wird, wird für den Wert des fehlenden Uhrzeitteils der Standardwert festgelegt: 00-00-00. Wenn entweder *"StartDate"* oder *Enddate* haben nur einen Uhrzeitteil und der andere nur einen Date-Teil, die fehlenden Uhrzeit- und Datumsteile werden auf die Standardwerte festgelegt.
  
Wenn *"StartDate"* und *Enddate* sind von anderen Date-Datentypen und eine mehr Uhrzeitteile oder die Genauigkeit der Sekundenbruchteile als das andere ist, werden die fehlenden Teile des anderen auf 0 festgelegt.
  
## <a name="datepart-boundaries"></a>datepart-Begrenzungen  
Die folgenden Anweisungen verfügen über denselben *"StartDate"* und demselben *Endate*. Die Datumsangaben folgen aufeinander und unterscheiden sich in der Uhrzeit um 0,0000001 Sekunden. Der Unterschied zwischen der *"StartDate"* und *Endate* in jeder Anweisung überschreitet eine Kalender- oder uhrzeitbegrenzung des seine *Datepart*. Jede Anweisung gibt 1 zurück. Wenn für dieses Beispiel unterschiedliche Jahre verwendet werden, und wenn die beiden *"StartDate"* und *Endate* befinden sich in derselben Kalenderwoche, der Rückgabewert für **Woche** würde "0" sein.
  
`SELECT DATEDIFF(year, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(quarter, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(month, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(dayofyear, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(day, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(week, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(hour, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(minute, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(second, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
`SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999'`
  
`, '2006-01-01 00:00:00.0000000');`
  
## <a name="remarks"></a>Hinweise  
DATEDIFF kann in den Klauseln WHERE, HAVING, GROUP BY und ORDER BY der Auswahlliste verwendet werden.
  
DATEDIFF wandelt Zeichenfolgenliterale als implizit eine **datetime2** Typ. Daher unterstützt DATEDIFF das Format YDM nicht, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge, die explizit Umwandeln einer **"DateTime"** oder **Smalldatetime** Typ das YDM-Format verwendet.
  
Das Angeben von SET DATEFIRST hat keine Auswirkungen auf DATEDIFF. DATEDIFF verwendet immer Sonntag als ersten Wochentag, um zu gewährleisten, dass die Funktion deterministisch ist.
  
## <a name="examples"></a>Beispiele  
In den folgenden Beispielen wird mit verschiedenen Arten von Ausdrücken als Argumente für die *"StartDate"* und *Enddate* Parameter.
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. Angeben von Spalten für startdate und enddate  
Im folgenden Beispiel wird die Anzahl der Tagesbegrenzungen berechnet, die von den Datumsangaben in zwei Spalten in einer Tabelle überschritten wurden.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. Angeben von benutzerdefinierten Variablen für startdate und enddate  
Im folgenden Beispiel wird eine benutzerdefinierte Variablen als Argumente für *"StartDate"* und *Enddate*.
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. Angeben von skalaren Systemfunktionen für startdate und enddate  
Im folgenden Beispiel wird die skalaren Systemfunktionen als Argumente für *"StartDate"* und *Enddate*.
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. Angeben von skalaren Unterabfragen und skalaren Funktionen für startdate und enddate  
Im folgende Beispiel werden skalare Unterabfragen und skalaren Funktionen als Argumente für verwendet *"StartDate"* und *Enddate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. Angeben von Konstanten für startdate und enddate  
Im folgenden Beispiel wird Zeichenkonstanten als Argumente für *"StartDate"* und *Enddate*.
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. Angeben von numerischen Ausdrücken und skalaren Systemfunktionen für enddate  
Im folgenden Beispiel wird einen numerischen Ausdruck `(GETDATE ()+ 1)`, und skalare Systemfunktionen `GETDATE` und `SYSDATETIME`, als Argumente für *Enddate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE()+ 1)   
    AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day,1,SYSDATETIME())) AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. Angeben von Rangfolgefunktionen für startdate  
Im folgende Beispiel wird eine rangfolgefunktion als Argument für *"StartDate"*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. Angeben einer Aggregatfensterfunktion für startdate  
Im folgenden Beispiel wird eine aggregatfensterfunktion als Argument für *"StartDate"*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty,soh.OrderDate  
    ,DATEDIFF(day,MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID),SYSDATETIME() ) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659,58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
In den folgenden Beispielen wird mit verschiedenen Arten von Ausdrücken als Argumente für die *"StartDate"* und *Enddate* Parameter.
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>I. Angeben von Spalten für startdate und enddate  
Im folgenden Beispiel wird die Anzahl der Tagesbegrenzungen berechnet, die von den Datumsangaben in zwei Spalten in einer Tabelle überschritten wurden.
  
```sql
CREATE TABLE dbo.Duration (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT TOP(1) DATEDIFF(day,startDate,endDate) AS Duration  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>J. Angeben von skalaren Unterabfragen und skalaren Funktionen für startdate und enddate  
Im folgende Beispiel werden skalare Unterabfragen und skalaren Funktionen als Argumente für verwendet *"StartDate"* und *Enddate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. Angeben von Konstanten für startdate und enddate  
Im folgenden Beispiel wird Zeichenkonstanten als Argumente für *"StartDate"* und *Enddate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. Angeben von Rangfolgefunktionen für startdate  
Im folgende Beispiel wird eine rangfolgefunktion als Argument für *"StartDate"*.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. Angeben einer Aggregatfensterfunktion für startdate  
Im folgenden Beispiel wird eine aggregatfensterfunktion als Argument für *"StartDate"*.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>Siehe auch
[DATEDIFF_BIG &#40; Transact-SQL &#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



