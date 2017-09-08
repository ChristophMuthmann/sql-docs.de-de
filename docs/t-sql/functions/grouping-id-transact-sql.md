---
title: GROUPING_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GROUPING_ID_TSQL
- GROUPING_ID
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, GROUPING_ID
- GROUPING_ID function
ms.assetid: c1050658-b19f-42ee-9a05-ecd6a73b896c
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5cb5b4ba4925661797760e906e36ddcec1526747
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="groupingid-transact-sql"></a>GROUPING_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ist eine Funktion, die die Ebene der Gruppierung berechnet. GROUPING_ID kann nur in die SELECT-Anweisung verwendet werden \<auswählen > aufzulisten, HAVING oder ORDER BY-Klauseln, wenn GROUP BY angegeben ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GROUPING_ID ( <column_expression>[ ,...n ] )  
```  
  
## <a name="arguments"></a>Argumente  
 \<Spaltenausdruck >  
 Ist eine *Spaltenausdruck* in einem [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) Klausel.  
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Der GROUPING_ID \<Spaltenausdruck > muss den Ausdruck in der GROUP BY-Liste genau entsprechen. Angenommen, Sie nach DATEPART gruppieren (Yyyy, \< *Spaltenname*>), verwenden Sie GROUPING_ID (DATEPART (Yyyy, \< *Spaltenname*>)); oder wenn Sie von Gruppieren\< *Spaltenname*>, verwenden Sie GROUPING_ID (\<*Spaltenname*>).  
  
## <a name="comparing-groupingid--to-grouping-"></a>Vergleichen von GROUPING_ID () mit GROUPING ()  
 GROUPING_ID (\<Spaltenausdruck > [ **,**...  *n*  ]) gibt die Entsprechung der Gruppierung (\<Spaltenausdruck >) für jede Spalte in seiner Spaltenliste in jeder Ausgabezeile als Zeichenfolge aus Einsen und Nullen zurück. GROUPING_ID interpretiert diese Zeichenfolge als Basis-2-Nummer und gibt die entsprechende ganze Zahl zurück. Betrachten Sie beispielsweise die folgende Anweisung: `SELECT a, b, c, SUM(d),``GROUPING_ID(a,b,c)``FROM T GROUP BY <group by list>`. Die folgende Tabelle zeigt die Ein- und Ausgabewerte für GROUPING_ID ().  
  
|Aggregierte Spalten|GROUPING_ID (a, b, c) Eingabe = GROUPING(a) + GROUPING(b) + GROUPING(c)|GROUPING_ID () Ausgabe|  
|------------------------|---------------------------------------------------------------------------------------|------------------------------|  
|`a`|`100`|`4`|  
|`b`|`010`|`2`|  
|`c`|`001`|`1`|  
|`ab`|`110`|`6`|  
|`ac`|`101`|`5`|  
|`bc`|`011`|`3`|  
|`abc`|`111`|`7`|  
  
## <a name="technical-definition-of-groupingid-"></a>Technische Definition von GROUPING_ID ()  
 Jedes GROUPING_ID-Argument muss ein Element der GROUP BY-Liste sein. GROUPING_ID () gibt eine **Ganzzahl** Bitmap, deren niedrigste N-Bit hervorgehoben sein können. Ein hervorgehobenes **Bit** gibt an, das entsprechende Argument keine Gruppierungsspalte für die entsprechende Ausgabezeile ist. Der niedrigsten Ordnung **Bit** entspricht Argument N und die n-1<sup>ten</sup> niederwertigsten **Bit** entspricht Argument 1.  
  
## <a name="groupingid--equivalents"></a>GROUPING_ID ()-Entsprechungen  
 Für eine einzelne gruppierungsabfrage GRUPPIEREN (\<Spaltenausdruck >) GROUPING_ID entspricht (\<Spaltenausdruck >), und beide geben 0 zurück.  
  
 Beispielsweise sind die folgenden Anweisungen äquivalent:  
  
 Anweisung A:  
  
```  
SELECT GROUPING_ID(A,B)  
FROM T   
GROUP BY CUBE(A,B)   
```  
  
 Anweisung B:  
  
```  
SELECT 3 FROM T GROUP BY ()  
UNION ALL  
SELECT 1 FROM T GROUP BY A  
UNION ALL  
SELECT 2 FROM T GROUP BY B  
UNION ALL  
SELECT 0 FROM T GROUP BY A,B  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-groupingid-to-identify-grouping-levels"></a>A. Verwenden von GROUPING_ID zur Identifizierung von Gruppierungsebenen  
 Im folgenden Beispiel wird die Anzahl der Mitarbeiter nach `Name` und `Title` sowie nach `Name,` und Unternehmen insgesamt aus der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. `GROUPING_ID()` wird verwendet, um einen Wert für jede Zeile in der `Title`-Spalte zu erstellen, die die Aggregationsebene angibt.  
  
```  
SELECT D.Name  
    ,CASE   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 0 THEN E.JobTitle  
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 1 THEN N'Total: ' + D.Name   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 3 THEN N'Company Total:'  
        ELSE N'Unknown'  
    END AS N'Job Title'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle);  
```  
  
### <a name="b-using-groupingid-to-filter-a-result-set"></a>B. Verwenden von GROUPING_ID zum Filtern eines Resultsets  
  
#### <a name="simple-example"></a>Einfaches Beispiel  
 Um nur die Zeilen zurückzugeben, die die Anzahl der Mitarbeiter nach Titel enthalten, entfernen Sie im folgenden Code in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank die Kommentierungszeichen von `HAVING GROUPING_ID(D.Name, E.JobTitle); = 0`. Um nur die Zeilen zurückzugeben, die die Anzahl der Mitarbeiter nach Abteilung enthalten, entfernen Sie die Kommentierungszeichen aus `HAVING GROUPING_ID(D.Name, E.JobTitle) = 1;`.  
  
```  
SELECT D.Name  
    ,E.JobTitle  
    ,GROUPING_ID(D.Name, E.JobTitle) AS 'Grouping Level'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee AS E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department AS D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle)  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 0; --All titles  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 1; --Group by Name;  
```  
  
 Das ungefilterte Resultset sieht folgendermaßen aus.  
  
|Name|Title|Gruppierungsebene|Anzahl der Mitarbeiter|Name|  
|----------|-----------|--------------------|--------------------|----------|  
|Dokumentsteuerung|Steuerungsspezialist|0|2|Dokumentsteuerung|  
|Dokumentsteuerung|Dokumentsteuerungs-Assistent|0|2|Dokumentsteuerung|  
|Dokumentsteuerung|Dokumentsteuerungs-Manager|0|1|Dokumentsteuerung|  
|Dokumentsteuerung|NULL|1|5|Dokumentsteuerung|  
|Einrichtungen und Wartung|Einrichtungen-Verwaltungs-Assistent|0|1|Einrichtungen und Wartung|  
|Einrichtungen und Wartung|Einrichtungs-Manager|0|1|Einrichtungen und Wartung|  
|Einrichtungen und Wartung|Pförtner|0|4|Einrichtungen und Wartung|  
|Einrichtungen und Wartung|Wartungsleiter|0|1|Einrichtungen und Wartung|  
|Einrichtungen und Wartung|NULL|1|7|Einrichtungen und Wartung|  
|NULL|NULL|3|12|NULL|  
  
#### <a name="complex-example"></a>Komplexes Beispiel  
 Im folgenden Beispiel wird `GROUPING_ID()` verwendet, um ein Resultset mit mehreren Gruppierungsebenen nach Gruppierungsebene zu filtern. Der gleiche Code kann verwendet werden, um eine Sicht mit mehreren Gruppierungsebenen zu erstellen sowie eine gespeicherte Prozedur, die die Sicht aufruft, indem ein Parameter übergeben wird, der die Sicht nach Gruppierungsebene filtert. Im Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.  
  
```  
DECLARE @Grouping nvarchar(50);  
DECLARE @GroupingLevel smallint;  
SET @Grouping = N'CountryRegionCode Total';  
  
SELECT @GroupingLevel = (  
    CASE @Grouping  
        WHEN N'Grand Total'             THEN 15  
        WHEN N'SalesPerson Total'       THEN 14  
        WHEN N'Store Total'             THEN 13  
        WHEN N'Store SalesPerson Total' THEN 12  
        WHEN N'CountryRegionCode Total' THEN 11  
        WHEN N'Group Total'             THEN 7  
        ELSE N'Unknown'  
    END);  
  
SELECT   
    T.[Group]  
    ,T.CountryRegionCode  
    ,S.Name AS N'Store'  
    ,(SELECT P.FirstName + ' ' + P.LastName   
        FROM Person.Person AS P   
        WHERE P.BusinessEntityID = H.SalesPersonID)  
        AS N'Sales Person'  
    ,SUM(TotalDue)AS N'TotalSold'  
    ,CAST(GROUPING(T.[Group])AS char(1)) +   
        CAST(GROUPING(T.CountryRegionCode)AS char(1)) +   
        CAST(GROUPING(S.Name)AS char(1)) +   
        CAST(GROUPING(H.SalesPersonID)AS char(1))   
        AS N'GROUPING base-2'  
    ,GROUPING_ID((T.[Group])  
        ,(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
        ) AS N'GROUPING_ID'  
    ,CASE   
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 15 THEN N'Grand Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 14 THEN N'SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 13 THEN N'Store Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 12 THEN N'Store SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 11 THEN N'CountryRegionCode Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) =  7 THEN N'Group Total'  
        ELSE N'Error'  
        END AS N'Level'  
FROM Sales.Customer AS C  
    INNER JOIN Sales.Store AS S  
        ON C.StoreID  = S.BusinessEntityID   
    INNER JOIN Sales.SalesTerritory AS T  
        ON C.TerritoryID  = T.TerritoryID   
    INNER JOIN Sales.SalesOrderHeader AS H  
        ON C.CustomerID = H.CustomerID  
GROUP BY GROUPING SETS ((S.Name,H.SalesPersonID)  
    ,(H.SalesPersonID),(S.Name)  
    ,(T.[Group]),(T.CountryRegionCode),()  
    )  
HAVING GROUPING_ID(  
    (T.[Group]),(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
    ) = @GroupingLevel  
ORDER BY   
    GROUPING_ID(S.Name,H.SalesPersonID),GROUPING_ID((T.[Group])  
    ,(T.CountryRegionCode)  
    ,(S.Name)  
    ,(H.SalesPersonID))ASC;  
```  
  
### <a name="c-using-groupingid--with-rollup-and-cube-to-identify-grouping-levels"></a>C. Verwenden von GROUPING_ID () mit ROLLUP und CUBE, um Gruppierungsebenen zu ermitteln  
 Der Code in den folgenden Beispielen zeigt, wie `GROUPING()` zum Berechnen der `Bit Vector(base-2)`-Spalte verwendet wird. `GROUPING_ID()` wird verwendet, um die entsprechende `Integer Equivalent`-Spalte zu berechnen. Die Spaltenreihenfolge in der `GROUPING_ID()`-Funktion ist die umgekehrte Reihenfolge der Spalten, die durch die `GROUPING()`-Funktion verkettet sind.  
  
 In diesen Beispielen wird `GROUPING_ID()` verwendet, um einen Wert für jede Zeile in der `Grouping Level`-Spalte zu erstellen, um die Gruppierungsebene zu ermitteln. Gruppierungsebenen sind nicht immer eine aufeinander folgende Liste von ganzen Zahlen, die beginnen mit 1 (0, 1, 2... *n*).  
  
> [!NOTE]  
>  GROUPING und GROUPING_ID können in einer HAVING-Klausel verwendet werden, um ein Resultset zu filtern.  
  
#### <a name="rollup-example"></a>ROLLUP-Beispiel  
 In diesem Beispiel werden die Gruppierungsebenen nicht so angezeigt, wie sie im folgenden CUBE-Beispiel dargestellt werden. Wenn die Reihenfolge der Spalten in der `ROLLUP`-Liste geändert wird, müssen auch die Ebenenwerte in der `Grouping Level`-Spalte geändert werden. Im Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
     AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY ROLLUP(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(mm,OrderDate)  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
|Year|Month|Day|Total Due|Bitvektor (Basis-2)|Ganzzahlige Entsprechung|Gruppierungsebene|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Jahr, Monat, Tag|  
|2007|1|2|21772.3494|000|0|Jahr, Monat, Tag|  
|2007|2|1|2705653.5913|000|0|Jahr, Monat, Tag|  
|2007|2|2|21684.4068|000|0|Jahr, Monat, Tag|  
|2008|1|1|1908122.0967|000|0|Jahr, Monat, Tag|  
|2008|1|2|46458.0691|000|0|Jahr, Monat, Tag|  
|2008|2|1|3108771.9729|000|0|Jahr, Monat, Tag|  
|2008|2|2|54598.5488|000|0|Jahr, Monat, Tag|  
|2007|1|NULL|1519224.956|100|1|Year Month|  
|2007|2|NULL|2727337.9981|100|1|Year Month|  
|2008|1|NULL|1954580.1658|100|1|Year Month|  
|2008|2|NULL|3163370.5217|100|1|Year Month|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|NULL|NULL|9364513.6416|111|7|Grand Total|  
  
#### <a name="cube-example"></a>CUBE-Beispiel  
 In diesen Beispielen wird die `GROUPING_ID()`-Funktion verwendet, um einen Wert für jede Zeile in der `Grouping Level`-Spalte zu erstellen, über den die Gruppierungsebene ermittelt wird.  
  
 Im Gegensatz zu `ROLLUP` im vorherigen Beispiel gibt `CUBE` alle Gruppierungsebenen aus. Wenn die Reihenfolge der Spalten in der `CUBE`-Liste geändert wird, müssen auch die Ebenenwerte in der `Grouping Level`-Spalte geändert werden. Im Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
        AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'Year Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY CUBE(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
|Year|Month|Day|Total Due|Bitvektor (Basis-2)|Ganzzahlige Entsprechung|Gruppierungsebene|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Jahr, Monat, Tag|  
|2007|1|2|21772.3494|000|0|Jahr, Monat, Tag|  
|2007|2|1|2705653.5913|000|0|Jahr, Monat, Tag|  
|2007|2|2|21684.4068|000|0|Jahr, Monat, Tag|  
|2008|1|1|1908122.0967|000|0|Jahr, Monat, Tag|  
|2008|1|2|46458.0691|000|0|Jahr, Monat, Tag|  
|2008|2|1|3108771.9729|000|0|Jahr, Monat, Tag|  
|2008|2|2|54598.5488|000|0|Jahr, Monat, Tag|  
|2007|1|NULL|1519224.956|100|1|Year Month|  
|2007|2|NULL|2727337.9981|100|1|Year Month|  
|2008|1|NULL|1954580.1658|100|1|Year Month|  
|2008|2|NULL|3163370.5217|100|1|Year Month|  
|2007|NULL|1|4203106.1979|010|2|Jahr und Tag|  
|2007|NULL|2|43456.7562|010|2|Jahr und Tag|  
|2008|NULL|1|5016894.0696|010|2|Jahr und Tag|  
|2008|NULL|2|101056.6179|010|2|Jahr und Tag|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|1|1|3405574.7033|001|4|Monat und Tag|  
|NULL|1|2|68230.4185|001|4|Monat und Tag|  
|NULL|2|1|5814425.5642|001|4|Monat und Tag|  
|NULL|2|2|76282.9556|001|4|Monat und Tag|  
|NULL|1|NULL|3473805.1218|101|5|Month|  
|NULL|2|NULL|5890708.5198|101|5|Month|  
|NULL|NULL|1|9220000.2675|011|6|Day|  
|NULL|NULL|2|144513.3741|011|6|Day|  
|NULL|NULL|NULL|9364513.6416|111|7|Grand Total|  
  
## <a name="see-also"></a>Siehe auch  
 [Gruppierung &#40; Transact-SQL &#41;](../../t-sql/functions/grouping-transact-sql.md)   
 [GROUP BY &#40; Transact-SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
