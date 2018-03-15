---
title: OVER-Klausel (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OVER_TSQL
- OVER
dev_langs:
- TSQL
helpviewer_keywords:
- order of rowsets [SQL Server]
- rowsets [SQL Server], windowing
- window function
- partitions [SQL Server], rowsets
- clauses [SQL Server], OVER
- rowsets [SQL Server], partitioning
- rowsets [SQL Server], ordering
- OVER clause
ms.assetid: ddcef3a6-0341-43e0-ae73-630484b7b398
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1144e82253c5e9d2988ec9ff4a8aa47bb3cb2fb1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select---over-clause-transact-sql"></a>SELECT - OVER-Klausel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bestimmt die Partitionierung und Reihenfolge eines Rowsets vor der Anwendung der zugehörigen Fensterfunktion. Demnach definiert die OVER-Klausel ein Fenster oder eine benutzerdefinierte Reihe von Zeilen innerhalb eines Abfrageresultsets. Eine Fensterfunktion berechnet dann einen Wert für jede Zeile im Fenster. Sie können die OVER-Klausel mit Funktionen verwenden, um aggregierte Werte wie gleitende Durchschnitte, kumulierte Aggregate, laufende Gesamtbeträge oder Ergebnisse vom Typ "Erste n pro Gruppe" berechnen.  
  
-   [Rangfolgefunktionen](../../t-sql/functions/ranking-functions-transact-sql.md)  
  
-   [Aggregatfunktionen](../../t-sql/functions/aggregate-functions-transact-sql.md)  
  
-   [Analytische Funktionen](../../t-sql/functions/analytic-functions-transact-sql.md)  
  
-   [NEXT VALUE FOR-Funktion](../../t-sql/functions/next-value-for-transact-sql.md)  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, and Azure SQL Data Warehouse  
  
OVER (   
       [ <PARTITION BY clause> ]  
       [ <ORDER BY clause> ]   
       [ <ROW or RANGE clause> ]  
      )  
  
<PARTITION BY clause> ::=  
PARTITION BY value_expression , ... [ n ]  
  
<ORDER BY clause> ::=  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]  
  
<ROW or RANGE clause> ::=  
{ ROWS | RANGE } <window frame extent>  
  
<window frame extent> ::=   
{   <window frame preceding>  
  | <window frame between>  
}  
<window frame between> ::=   
  BETWEEN <window frame bound> AND <window frame bound>  
  
<window frame bound> ::=   
{   <window frame preceding>  
  | <window frame following>  
}  
  
<window frame preceding> ::=   
{  
    UNBOUNDED PRECEDING  
  | <unsigned_value_specification> PRECEDING  
  | CURRENT ROW  
}  
  
<window frame following> ::=   
{  
    UNBOUNDED FOLLOWING  
  | <unsigned_value_specification> FOLLOWING  
  | CURRENT ROW  
}  
  
<unsigned value specification> ::=   
{  <unsigned integer literal> }  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
OVER ( [ PARTITION BY value_expression ] [ order_by_clause ] )  
```  
  
## <a name="arguments"></a>Argumente  
 PARTITION BY  
 Teilt das Abfrageresultset in Partitionen. Die Fensterfunktion wird auf jede Partition einzeln angewendet, und die Berechnung wird für jede Partition neu gestartet.  
  
 *value_expression*  
 Gibt die Spalte an, nach der das Rowset partitioniert wird. *value_expression* kann nur auf von der FROM-Klausel bereitgestellte Spalten verweisen. *value_expression* kann in der Auswahlliste nicht auf Ausdrücke oder Aliase verweisen. *value_expression* kann ein Spaltenausdruck, eine skalare Unterabfrage, eine Skalarfunktion oder eine benutzerdefinierte Variable sein.  
  
 \<ORDER BY-Klausel>  
 Definiert die logische Reihenfolge der Zeilen innerhalb jeder Partition des Resultsets. Demnach gibt sie die logische Reihenfolge an, in der die Fensterfunktionsberechnung ausgeführt wird.  
  
 *order_by_expression*  
 Gibt eine Spalte oder einen Ausdruck für die Sortierung an. *order_by_expression* kann nur auf von der FROM-Klausel bereitgestellte Spalten verweisen. Eine ganze Zahl kann nicht angegeben werden, um einen Spaltennamen oder einen Alias darzustellen.  
  
 COLLATE *collation_name*  
 Gibt an, dass der ORDER BY-Vorgang gemäß der in *collation_name* angegebenen Sortierung ausgeführt werden soll. *collation_name* kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname sein. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md). COLLATE ist nur für Spalten vom Typ **char**, **varchar**, **nchar** und **nvarchar** anwendbar.  
  
 **ASC** | DESC  
 Gibt an, dass die Werte in der angegebenen Spalte in aufsteigender oder absteigender Reihenfolge sortiert werden sollen. ASC ist die Standardsortierreihenfolge. NULL-Werte werden als die niedrigsten Werte behandelt, die möglich sind.  
  
 ROWS | RANGE  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Grenzt die Zeilen innerhalb der Partition weiter ein, indem Start- und Endpunkte innerhalb der Partition angegeben werden. Dies erfolgt durch die Angabe einer Reihe von Zeilen unter Berücksichtigung aktuellen Zeile – entweder anhand der logischen oder physischen Zuordnung. Die physische Zuordnung wird erreicht, indem die ROWS-Klausel verwendet wird.  
  
 Die ROWS-Klausel schränkt die Zeilen innerhalb einer Partition ein, indem eine feste Anzahl an Zeilen angegeben wird, die der aktuellen Zeile vorausgehen oder dieser folgen. Alternativ schränkt die RANGE-Klausel die Zeilen innerhalb einer Partition logisch ein, indem eine Reihe von Werten unter Berücksichtigung des Werts der aktuellen Zeile angegeben wird. Vorausgehende und folgende Zeilen werden auf Grundlage der Reihenfolge in der ORDER BY-Klausel definiert. Der Fensterrahmen "RANGE … CURRENT ROW …“ beinhaltet alle Zeilen, die im ORDER BY-Ausdruck über die gleichen Werte wie die aktuelle Zeile verfügen. Beispielsweise bedeutet ROWS BETWEEN 2 PRECEDING AND CURRENT ROW, dass das Zeilenfenster, über das die Funktion ausgeführt wird, drei Zeilen umfasst – beginnend mit zwei vorausgehenden Zeilen bis zur und einschließlich der aktuellen Zeile.  
  
> [!NOTE]  
>  ROWS oder RANGE erfordert die Angabe der ORDER BY-Klausel. Wenn ORDER BY mehrere Reihenfolgenausdrücke enthält, berücksichtigt CURRENT ROW FOR RANGE beim Ermitteln der aktuellen Zeile alle Spalten in der ORDER BY-Liste.  
  
 UNBOUNDED PRECEDING  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass das Fenster bei der ersten Zeile der Partition startet. UNBOUNDED PRECEDING kann nur als Fensterstartpunkt angegeben werden.  
  
 \<unsigned value specification> PRECEDING  
 Wird mit \<unsigned value specification> angegeben, um die Anzahl der Zeilen oder Werte anzugeben, die der aktuellen Zeile vorausgehen sollen. Diese Spezifikation ist für RANGE nicht zulässig.  
  
 CURRENT ROW  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt an, dass das Fenster bei Verwendung mit ROWS oder auf Basis des aktuellen Werts bei Verwendung mit RANGE bei der aktuellen Zeile startet oder endet. CURRENT ROW kann als Start- und Endpunkt angegeben werden.  
  
 BETWEEN \<window frame bound > AND \<window frame bound >  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Wird mit ROWS oder RANGE verwendet, um den unteren Grenzpunkt (Startpunkt) oder oberen Grenzpunkt (Endpunkt) des Fensters anzugeben. \<window frame bound> definiert den Startgrenzpunkt, und \<window frame bound> definiert den Endgrenzpunkt. Die Obergrenze kann nicht kleiner als die Untergrenze sein.  
  
 UNBOUNDED FOLLOWING  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt an, dass das Fenster bei der letzten Zeile der Partition endet. UNBOUNDED FOLLOWING kann nur als Fensterendpunkt angegeben werden. Beispielsweise definiert RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING ein Fenster, das mit der aktuellen Zeile startet und mit der letzten Zeile der Partition endet.  
  
 \<unsigned value specification> FOLLOWING  
 Wird mit \<unsigned value specification> angegeben, um die Anzahl der Zeilen oder Werte anzugeben, die der aktuellen Zeile folgen sollen. Wenn \<unsigned value specification> FOLLOWING als Fensterstartpunkt angegeben ist, muss der Endpunkt \<unsigned value specification>FOLLOWING lauten. Beispielsweise definiert ROWS BETWEEN 2 FOLLOWING AND 10 FOLLOWING ein Fenster, das mit der zweiten Zeile startet, die der aktuellen Zeile folgt, und mit der zehnten Zeile endet, die der aktuellen Zeile folgt. Diese Spezifikation ist für RANGE nicht zulässig.  
  
 unsigned integer literal  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ist ein positives ganzzahliges Literal (einschließlich 0), das die Anzahl an Zeilen oder Werten angibt, die der aktuellen Zeile oder dem aktuellen Wert vorausgehen oder folgen. Diese Spezifikation ist nur für ROWS gültig.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Mehrere Fensterfunktionen können in einer einzelnen Abfrage mit einer einzelnen FROM-Klausel verwendet werden. Die OVER-Klausel für jede Funktion kann sich in der Partitionierung und Reihenfolge unterscheiden.  
  
 Wird PARTITION BY nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. 
 
### <a name="important"></a>Wichtig!

Bei Angabe von ROWS/RANGE und Verwendung von \<window frame preceding> für \<window frame extent> (kurze Syntax) wird diese Spezifikation für den Startgrenzpunkt des Fensterrahmens und CURRENT ROW für den Endgrenzpunkt verwendet. Beispielsweise ist "ROWS 5 PRECEDING" gleich "ROWS BETWEEN 5 PRECEDING AND CURRENT ROW".  
  
> [!NOTE]
> Wenn ORDER BY nicht angegeben ist, wird die ganze Partition für einen Fensterrahmen verwendet. Dies gilt für nur Funktionen, die keine ORDER BY-Klausel erfordern. Wenn ROWS/RANGE nicht angegeben und ORDER BY angegeben ist, wird RANGE UNBOUNDED PRECEDING AND CURRENT ROW für Fensterrahmen als Standard verwendet. Dies gilt für nur Funktionen, die eine optionale ROWS/RANGE-Spezifikation akzeptieren. Beispielsweise können Rangfolgefunktionen ROWS/RANGE nicht akzeptieren. Daher wird dieser Fensterrahmen nicht übernommen, obwohl ORDER BY angegeben und ROWS/RANGE nicht angegeben ist.  
    
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Die OVER-Klausel kann nicht mit der CHECKSUM-Aggregatfunktion verwendet werden.  
  
 RANGE kann nicht mit \<unsigned value specification> PRECEDING oder \<unsigned value specification> FOLLOWING verwendet werden.  
  
 Je nach Rangfolge-, Aggregat- oder Analysefunktion, die mit der OVER-Klausel verwendet wird, wird die \<ORDER BY-Klausel> bzw. die \<ROWS/RANGE-Klausel> u.U. nicht unterstützt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-over-clause-with-the-rownumber-function"></a>A. Verwenden der OVER-Klausel mit der ROW_NUMBER-Funktion  
 Das folgende Beispiel zeigt die Verwendung der OVER-Klausel mit der ROW_NUMBER-Funktion, um eine Zeilennummer für jede Zeile innerhalb einer Partition anzuzeigen. Durch die ORDER BY-Klausel in der OVER-Klausel werden die Zeilen in jeder Partition nach der Spalte `SalesYTD` sortiert. Die ORDER BY-Klausel in der SELECT-Anweisung bestimmt die Reihenfolge, in der das gesamte Abfrageresultset zurückgegeben wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT ROW_NUMBER() OVER(PARTITION BY PostalCode ORDER BY SalesYTD DESC) AS "Row Number",   
    p.LastName, s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0  
ORDER BY PostalCode;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Row Number      LastName                SalesYTD              PostalCode 
 --------------- ----------------------- --------------------- ---------- 
 1               Mitchell                4251368.5497          98027 
 2               Blythe                  3763178.1787          98027 
 3               Carson                  3189418.3662          98027 
 4               Reiter                  2315185.611           98027 
 5               Vargas                  1453719.4653          98027  
 6               Ansman-Wolfe            1352577.1325          98027  
 1               Pak                     4116871.2277          98055  
 2               Varkey Chudukatil       3121616.3202          98055  
 3               Saraiva                 2604540.7172          98055  
 4               Ito                     2458535.6169          98055  
 5               Valdez                  1827066.7118          98055  
 6               Mensa-Annan             1576562.1966          98055  
 7               Campbell                1573012.9383          98055  
 8               Tsoflias                1421810.9242          98055
 ```  
  
### <a name="b-using-the-over-clause-with-aggregate-functions"></a>B. Verwenden der OVER-Klausel mit Aggregatfunktionen  
 Im folgenden Beispiel wird die `OVER`-Klausel mit Aggregatfunktionen für alle von der Abfrage zurückgegebenen Zeilen verwendet. In diesem Beispiel ist die Verwendung der `OVER`-Klausel effizienter als die Verwendung von Unterabfragen, um die Aggregatwerte abzuleiten.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,AVG(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Avg"  
    ,COUNT(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Count"  
    ,MIN(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Min"  
    ,MAX(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Max"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
SalesOrderID ProductID   OrderQty Total       Avg         Count       Min    Max  
------------ ----------- -------- ----------- ----------- ----------- ------ ------  
43659        776         1        26          2           12          1      6  
43659        777         3        26          2           12          1      6  
43659        778         1        26          2           12          1      6  
43659        771         1        26          2           12          1      6  
43659        772         1        26          2           12          1      6  
43659        773         2        26          2           12          1      6  
43659        774         1        26          2           12          1      6  
43659        714         3        26          2           12          1      6  
43659        716         1        26          2           12          1      6  
43659        709         6        26          2           12          1      6  
43659        712         2        26          2           12          1      6  
43659        711         4        26          2           12          1      6  
43664        772         1        14          1           8           1      4  
43664        775         4        14          1           8           1      4  
43664        714         1        14          1           8           1      4  
43664        716         1        14          1           8           1      4  
43664        777         2        14          1           8           1      4  
43664        771         3        14          1           8           1      4  
43664        773         1        14          1           8           1      4  
43664        778         1        14          1           8           1      4  
```  
  
 Im folgenden Beispiel wird die Verwendung der `OVER`-Klausel mit einer Aggregatfunktion in einem berechneten Wert dargestellt.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,CAST(1. * OrderQty / SUM(OrderQty) OVER(PARTITION BY SalesOrderID)   
        *100 AS DECIMAL(5,2))AS "Percent by ProductID"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Beachten Sie, dass die Aggregate nach `SalesOrderID` berechnet werden und `Percent by ProductID` für jede Zeile von `SalesOrderID` berechnet wird.  
  
```  
SalesOrderID ProductID   OrderQty Total       Percent by ProductID  
------------ ----------- -------- ----------- ---------------------------------------  
43659        776         1        26          3.85  
43659        777         3        26          11.54  
43659        778         1        26          3.85  
43659        771         1        26          3.85  
43659        772         1        26          3.85  
43659        773         2        26          7.69  
43659        774         1        26          3.85  
43659        714         3        26          11.54  
43659        716         1        26          3.85  
43659        709         6        26          23.08  
43659        712         2        26          7.69  
43659        711         4        26          15.38  
43664        772         1        14          7.14  
43664        775         4        14          28.57  
43664        714         1        14          7.14  
43664        716         1        14          7.14  
43664        777         2        14          14.29  
43664        771         3        14          21.4  
43664        773         1        14          7.14  
43664        778         1        14          7.14  
  
 (20 row(s) affected)  
```  
  
### <a name="c-producing-a-moving-average-and-cumulative-total"></a>C. Erzeugen eines gleitenden Durchschnitts und kumulierten Gesamtbetrags  
 Im folgenden Beispiel werden die AVG- und SUM-Funktion mit der OVER-Klausel verwendet, um einen gleitenden Durchschnitt und kumulierten Gesamtbetrag von jährlichen Verkäufen für jedes Gebiet in der `Sales.SalesPerson`-Tabelle bereitzustellen. Die Daten werden nach `TerritoryID` partitioniert und logisch nach `SalesYTD` sortiert. Folglich wird die AVG-Funktion auf Grundlage des Verkaufsjahres für jedes Gebiet berechnet. Beachten Sie, dass für `TerritoryID` 1 zwei Zeilen für das Verkaufsjahr 2005 vorhanden sind, die die beiden Vertriebsmitarbeiter mit dem Umsatz aus diesem Jahr darstellen. Der durchschnittliche Umsatz für diese zwei Zeilen wird berechnet, und anschließend wird die dritte Zeile, die den Umsatz für das Jahr 2006 darstellt, in die Berechnung einbezogen.  
  
```sql  
USE AdventureWorks2012;  
GO  
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
  
```  
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
  
```  
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
  
### <a name="d-specifying-the-rows-clause"></a>D. Angeben der ROWS-Klausel  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird die ROWS-Klausel verwendet, um ein Fenster zu definieren, über das die Zeilen als aktuelle Zeile und die *N*-Anzahl an Zeilen, die folgen, berechnet werden (eine Zeile in diesem Beispiel).  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        1,079,603.50  
287              NULL        519,905.93           2006        692,430.38  
285              NULL        172,524.45           2007        172,524.45  
283              1           1,573,012.94         2005        2,925,590.07  
280              1           1,352,577.13         2005        2,929,139.33  
284              1           1,576,562.20         2006        1,576,562.20  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        6,709,904.17  
281              4           2,458,535.62         2005        2,458,535.62  
```  
  
 Im folgenden Beispiel wird die ROWS-Klausel mit UNBOUNDED PRECEDING angegeben. Das Ergebnis ist, dass das Fenster bei der ersten Zeile der Partition startet.  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS UNBOUNDED PRECEDING),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        559,697.56  
287              NULL        519,905.93           2006        1,079,603.50  
285              NULL        172,524.45           2007        1,252,127.95  
283              1           1,573,012.94         2005        1,573,012.94  
280              1           1,352,577.13         2005        2,925,590.07  
284              1           1,576,562.20         2006        4,502,152.27  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        4,251,368.55  
281              4           2,458,535.62         2005        6,709,904.17  
  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-the-over-clause-with-the-rownumber-function"></a>E. Verwenden der OVER-Klausel mit der ROW_NUMBER-Funktion  
 Im folgenden Beispiel wird ROW_NUMBER für die Vertriebsmitarbeiter (basierend auf der zugewiesenen Sollvorgabe für den Verkauf) zurückgegeben.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    FirstName, LastName,   
CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
 ```
 RowNumber  FirstName  LastName            SalesQuota  
 ---------  ---------  ------------------  -------------  
 1          Jillian    Carson              12,198,000.00  
 2          Linda      Mitchell            11,786,000.00  
 3          Michael    Blythe              11,162,000.00  
 4          Jae        Pak                 10,514,000.00  
 ```
 
### <a name="f-using-the-over-clause-with-aggregate-functions"></a>F. Verwenden der OVER-Klausel mit Aggregatfunktionen  
 In den folgenden Beispielen wird die Verwendung der OVER-Klausel mit Aggregatfunktionen dargestellt. In diesem Beispiel ist die Verwendung der OVER-Klausel effizienter als die Verwendung von Unterabfragen.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       AVG(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Avg,  
       COUNT(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Count,  
       MIN(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Min,  
       MAX(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Max  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 OrderNumber  Product  Qty  Total  Avg  Count  Min  Max  
 -----------  -------  ---  -----  ---  -----  ---  ---  
 SO43659      218      6    16     3    5      1    6  
 SO43659      220      4    16     3    5      1    6  
 SO43659      223      2    16     3    5      1    6  
 SO43659      229      3    16     3    5      1    6  
 SO43659      235      1    16     3    5      1    6  
 SO43664      229      1     2     1    2      1    1  
 SO43664      235      1     2     1    2      1    1  
 ```
 
 Im folgenden Beispiel wird die Verwendung der OVER-Klausel mit einer Aggregatfunktion in einem berechneten Wert dargestellt. Beachten Sie, dass die Aggregate nach `SalesOrderNumber` berechnet werden und der Prozentsatz der Auftragssumme für jede Zeile von `SalesOrderNumber` berechnet wird.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey AS Product,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       CAST(1. * OrderQuantity / SUM(OrderQuantity)   
        OVER(PARTITION BY SalesOrderNumber)   
            *100 AS DECIMAL(5,2)) AS PctByProduct  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 Das erste Ergebnis dieses Resultsets lautet wie folgt:  
  
 ```
 OrderNumber  Product  Qty  Total  PctByProduct  
 -----------  -------  ---  -----  ------------  
 SO43659      218      6    16     37.50  
 SO43659      220      4    16     25.00  
 SO43659      223      2    16     12.50  
 SO43659      229      2    16     18.75  
 ```
 
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aggregate Functions &#40;Transact-SQL&#41; (Aggregatfunktionen (Transact-SQL))](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [Analytische Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/analytic-functions-transact-sql.md)   
 [Hilreicher Blogbeitrag zu Fensterfunktionen und OVER unter sqlmag.com von Itzik Ben-Gan](http://sqlmag.com/sql-server-2012/how-use-microsoft-sql-server-2012s-window-functions-part-1)  
  
  
