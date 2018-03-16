---
title: GROUP BY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
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
- GROUP
- CUBE
- ROLLUP
- GROUPING_SETS_TSQL
- GROUP BY
- GROUPING SETS
- GROUP_BY_TSQL
- GROUP_TSQL
- CUBE_TSQL
- ROLLUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5e99efe49620003de40659dd4bfd959dacef986c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select---group-by--transact-sql"></a>SELECT – GROUP BY – Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Die Klausel der SELECT-Anweisung, die die Abfrageergebnisse in Gruppen von Zeilen unterteilt. Wird in der Regel für das Ausführen einer oder mehrerer Aggregationen für jede Gruppe verwendet. Die SELECT-Anweisung gibt eine Zeile pro Gruppe zurück.  
  
## <a name="syntax"></a>Syntax  

 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```  
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
 
<group_by_expression> ::=  
      column-expression  
    | ( column-expression [ ,...n ] )    
   
<grouping_set> ::=  
      () --calculates the grand total  
    | <grouping_set_item>  
    | ( <grouping_set_item> [ ,...n ] )  
  
<grouping_set_item> ::=  
      <group_by_expression>  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
  

-- For backward compatibility only.
-- Non-ISO-Compliant Syntax for SQL Server and Azure SQL Database 
  
GROUP BY 
      [ ALL ] column-expression [ ,...n ] 
    | column-expression [ ,...n ] [ WITH { CUBE | ROLLUP } ]   

```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
  
## <a name="arguments"></a>Argumente 
 
### <a name="column-expression"></a>*column-expression*  
Gibt eine Spalte oder eine nicht-aggregierbare Berechnung für eine Spalte an. Diese Spalte kann zu einer (abgeleiteten) Tabelle oder Sicht gehören. Die Spalte muss in der FROM-Klausel der SELECT-Anweisung angezeigt werden. Es ist jedoch nicht erforderlich, dass sie auch in der SELECT-Liste angezeigt wird. 

Gültige Ausdrücke finden Sie unter [expression](~/t-sql/language-elements/expressions-transact-sql.md).    

Die Spalte muss in der FROM-Klausel der SELECT-Anweisung angezeigt werden. Es ist jedoch nicht erforderlich, dass sie auch in der SELECT-Liste angezeigt wird. Allerdings muss jede Tabellen- oder Sichtspalte in einem nicht aggregierten Ausdruck in der \<select>-Liste in die GROUP BY-Liste aufgenommen werden.  
  
Die folgenden Anweisungen sind zulässig:  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
    ```  
  
Die folgenden Anweisungen sind nicht zulässig:  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    ```  
Folgendes darf nicht im Spaltenausdruck enthalten sein:

- Ein Spaltenalias, der in der SELECT-Liste definiert wird. Es kann ein Spaltenalias für eine abgeleitete Tabelle verwendet werden, die in der FROM-Klausel definiert ist.
- Eine Spalte vom Typ **text**, **ntext** oder **image**. Allerdings können Sie Spalten vom Typ „text“, „ntext“ oder „image“ als Argumente für eine Funktion verwenden, die einen Wert eines gültigen Datentyps zurückgibt. Der Ausdruck kann beispielsweise SUBSTRING() und CAST() verwenden. Dies gilt auch für Ausdrücke in der HAVING-Klausel.
- XML-Datentypmethoden. Eine benutzerdefinierte Funktion, die XML-Datentypmethoden verwendet, darf enthalten sein. Eine berechnete Spalte, die XML-Datentypmethoden verwendet, darf enthalten sein. 
- Eine Unterabfrage. Fehler 144 wird zurückgegeben. 
- Eine Spalte aus einer indizierten Sicht. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *column-expression* [ ,...n ] 

Gruppiert die Ergebnisse der SELECT-Anweisung basierend auf den Werten in einer Liste mit mindestens einem Spaltenausdruck. 

Diese Abfrage erstellt z.B. eine Sales-Tabelle mit Spalten für das Land, die Region und die Verkäufe. Sie fügt vier Zeilen ein. Bei zwei dieser Zeilen stimmen die Werte für Land und Region überein.  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
Die Sales-Tabelle enthält folgende Zeilen:

| Country | Region | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 200 |
| Canada | British Columbia | 300 |
| United States | Montana | 100 |

Die nächste Abfrage gruppiert Land und Region und gibt die aggregierte Summe für jede Wertkombination zurück.  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
Das Abfrageergebnis enthält 3 Zeilen, da 3 Wertkombinationen für Land und Region möglich sind. Die Spalte TotalSales für Canada und British Columbia ist die Summe aus zwei Zeilen. 

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| United States | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY ROLLUP

Erstellt eine Gruppe für jede Kombination von Spaltenausdrücken. Darüber hinaus wird ein „Rollup“ der Ergebnisse in Teilergebnisse und Gesamtergebnisse durchgeführt. Zu diesem Zweck bewegt sich der Vorgang von rechts nach links und verringert die Anzahl der Spaltenausdrücke, für die er Gruppen erstellt, und die Aggregation(en). 

Die Reihenfolge der Spalten wirkt sich auf die Ausgabe von ROLLUP und möglicherweise auch auf die Anzahl der Zeilen im Resultset aus.  

`GROUP BY ROLLUP (col1, col2, col3, col4)` erstellt z.B. Gruppen für jede Kombination von Spaltenausdrücken in den folgenden Listen.  

- col1, col2, col3, col4 
- col1, col2, col3, NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- NULL, NULL, NULL, NULL: Dies ist die Gesamtsumme

Unter Verwendung der Tabelle aus dem vorherigen Beispiel führt dieser Code anstelle eines GROUP BY-Vorgangs einen GROUP BY ROLLUP-Vorgang aus.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

Das Abfrageergebnis enthält die gleichen Aggregationen wie der einfache GROUP BY-Vorgang ohne ROLLUP. Außerdem erstellt er Teilergebnisse für jeden Wert von Country. Schließlich gibt er ein Gesamtergebnis für alle Zeilen zurück. Das Ergebnis sieht wie folgt aus:

| Country | Region | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| Canada | NULL | 600 |
| United States | Montana | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE ( )  

GROUP BY CUBE erstellt Gruppen für alle möglichen Kombinationen von Spalten. Für GROUP BY CUBE (a, b) enthalten die Ergebnisse über Gruppen für eindeutige Werte von (a, b), (NULL, B) (a, NULL) und (NULL, NULL).

Unter Verwendung der Tabelle aus dem vorherigen Beispiel führt dieser Code einen GROUP BY CUBE-Vorgang für Land und Region aus. 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

Das Abfrageergebnis enthält Gruppen für eindeutige Werte von (Land, Region), (NULL, Region), (Land, NULL) und (NULL, NULL). Das Ergebnis sieht folgendermaßen aus:

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | British Columbia | 500 |
| NULL | British Columbia | 500 |
| United States | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>GROUP BY GROUPING SETS ( )  
 
Die Option GROUPING SETS bietet Ihnen die Möglichkeit, mehrere GROUP BY-Klauseln in einer einzigen GROUP BY-Klausel zu vereinen. Die Ergebnisse entsprechen denen von UNION ALL für die angegebenen Gruppen. 

`GROUP BY ROLLUP (Country, Region)` und `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` geben z.B. die gleichen Ergebnisse zurück. 

Wenn GROUPING SETS über zwei oder mehr Elemente verfügt, sind die Ergebnisse eine Vereinigung der Elemente. Dieses Beispiel gibt die Union der ROLLUP- und CUBE-Ergebnisse für Land und Region zurück.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

Die Ergebnisse sind identisch mit dieser Abfrage, die eine Union der beiden GROUP BY-Anweisungen zurückgibt.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region)
;
```

SQL konsolidiert keine doppelten Gruppen, die für eine GROUPING SETS-Liste generiert werden. In `GROUP BY ( (), CUBE (Country, Region) )` geben z.B. beide Elemente eine Zeile für die Gesamtsumme zurück, die beide in den Ergebnissen aufgeführt werden. 

 ### <a name="group-by-"></a>GROUP BY ()  
Gibt die leere Gruppe an, die die Gesamtsumme generiert. Dies ist als eines der Elemente von GROUPING SET sinnvoll. Diese Anweisung gibt z.B. den Gesamtumsatz (total sales) für jedes Land und anschließend die Gesamtsumme aller Länder zurück.

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ ALL ] column-expression [ ,...n ] 

Gilt für: SQL Server und Azure SQL-Datenbank

HINWEIS: Diese Syntax wird nur aus Gründen der Abwärtskompatibilität bereitgestellt. Sie wird in einer zukünftigen Version entfernt. Vermeiden Sie die Verwendung dieser Syntax bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen diese Syntax zurzeit verwendet wird.

Gibt an, alle Gruppen in den Ergebnissen einzubeziehen, unabhängig davon, ob diese den Suchkriterien in der WHERE-Klausel entsprechen. Gruppen, die den Suchkriterien nicht entsprechen, haben NULL als Aggregation. 

GROUP BY ALL:
- GROUP BY ALL wird für Abfragen nicht unterstützt, die auf Remotetabellen zugreifen und eine WHERE-Klausel enthalten.
- Diese Funktion scheitert bei Spalten, die über das FILESTREAM-Attribut verfügen.
  
### <a name="with-distributedagg"></a>WITH (DISTRIBUTED_AGG)
Gilt für: SQL Data Warehouse und Parallel Data Warehouse

Der Abfragehinweis DISTRIBUTED_AGG zwingt das MPP-System (Massively Parallel Processing), eine Tabelle in einer bestimmten Spalte neu zu verteilen, bevor eine Aggregation durchgeführt wird. Nur eine Spalte in der GROUP BY-Klausel kann über einen DISTRIBUTED_AGG-Abfragehinweis verfügen. Nachdem die Abfrage abgeschlossen ist, wird die neu verteilte Tabelle gelöscht. Die ursprüngliche Tabelle wird nicht geändert.  

HINWEIS: Der DISTRIBUTED_AGG-Abfragehinweis dient zur Abwärtskompatibilität mit früheren Versionen von Parallel Data Warehouse und verbessert die Leistung für die meisten Abfragen nicht. Standardmäßig verteilt MPP bereits bei Bedarf Daten zur Verbesserung der Leistung für Aggregationen. 
  
## <a name="general-remarks"></a>Allgemeine Hinweise

### <a name="how-group-by-interacts-with-the-select-statement"></a>So interagiert GROUP BY mit der SELECT-Anweisung
SELECT-Liste:
- Vektoraggregate. GROUP BY berechnet einen Summenwert für jede Gruppe, wenn Aggregatfunktionen in der SELECT-Klausel enthalten sind. Diese Ausdrücke werden als Vektoraggregate bezeichnet. 
- DISTINCT-Aggregate. Die Aggregate AVG (DISTINCT *column_name*), COUNT (DISTINCT *column_name*) und SUM (DISTINCT *column_name*) werden zusammen mit ROLLUP, CUBE und GROUPING SETS unterstützt.
  
WHERE-Klausel:
- SQL entfernt Zeilen, die die Bedingungen der WHERE-Klausel nicht erfüllen, bevor Gruppierungsvorgänge ausgeführt werden.  
  
HAVING-Klausel:
- SQL verwendet die HAVING-Klausel, um Gruppen im Resultset zu filtern. 
  
ORDER BY-Klausel:
- Verwenden Sie die ORDER BY-Klausel, um das Resultset zu sortieren. Die GROUP BY-Klausel sortiert das Resultset nicht. 
  
NULL-Werte:
- Wenn eine Gruppierungsspalte NULL-Werte enthält, werden alle NULL-Werte als gleich betrachtet und in einer Gruppe zusammengefasst.   
  
## <a name="limitations-and-restrictions"></a>Einschränkungen

Gilt für: SQL Server (ab 2008), und Azure SQL Data Warehouse

### <a name="maximum-capacity"></a>Maximale Kapazität

Für eine GROUP BY-Klausel, die ROLLUP, CUBE oder GROUPING SETS verwendet, ist die maximale Anzahl von Ausdrücken 32. Die maximale Anzahl von Gruppen ist 4096 (2<sup>12</sup>). Die folgenden Beispiele schlagen fehl, weil die GROUP BY-Klausel mehr als 4096 Gruppen enthält.  
 
-   Im folgenden Beispiel werden 4097 (2<sup>12</sup> + 1) Gruppierungssätze generiert und schlagen fehl.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   Im folgenden Beispiel werden 4097 (2<sup>12</sup> + 1) Gruppen generiert und schlagen fehl. Sowohl die `CUBE ()`- als auch die `()`-Gruppierungssätze generieren eine Gesamtergebniszeile, und doppelte Gruppierungssätze werden nicht entfernt.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   Dieses Beispiel verwendet die abwärtskompatible Syntax. Es werden 8192 (2<sup>13</sup>) Gruppierungssätze generiert und schlagen fehl.  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    Bei abwärtskompatiblen GROUP BY-Klauseln, die weder CUBE noch ROLLUP enthalten, ist die Anzahl von GROUP BY-Elementen durch die GROUP BY-Spaltengrößen, die Aggregatspalten und die Aggregatwerte der Abfrage beschränkt. Diese Beschränkung ergibt sich aus der maximalen Größe von 8.060 Byte der temporären Arbeitstabelle, die für die zwischenzeitlich erstellten Abfrageergebnisse benötigt wird. Bei Angabe von CUBE oder ROLLUP sind höchstens 12 Gruppierungsausdrücke zulässig.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>Unterstützung für ISO und ANSI SQL 2006 GROUP BY-Funktionen

Die GROUP BY-Klausel unterstützt alle GROUP BY-Features, die in SQL 2006-Standard enthalten sind, außer den folgenden Syntaxausnahmen:  
  
-   Gruppierungssätze sind in einer GROUP BY-Klausel nicht zugelassen, es sei denn, sie sind Teil einer expliziten GROUPING SETS-Liste. Beispielsweise ist `GROUP BY Column1, (Column2, ...ColumnN`) in der Standardversion zulässig, in Transact-SQL allerdings nicht.  Transact-SQL unterstützt `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` und `GROUP BY Column1, Column2, ... ColumnN`, die semantisch gleichwertig sind. Diese Klauseln sind mit dem vorherigen `GROUP BY`-Beispiel semantisch gleichwertig. Damit soll die Möglichkeit vermieden werden, dass `GROUP BY Column1, (Column2, ...ColumnN`) als `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` fehlinterpretiert wird. Diese beiden sind semantisch nicht gleichwertig.  
  
-   Gruppierungssätze sind in Gruppierungssätzen nicht zulässig. Beispielsweise ist `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` in SQL-2006 Standard zulässig, in Transact-SQL allerdings nicht. Transact-SQL lässt `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` oder `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )` zu, die semantisch gleichwertig mit dem ersten GROUP BY-Beispiel sind und über eine klarere Syntax verfügen.  
  
-   GROUP BY [ALL/DISTINCT] ist nur in einer einfachen GROUP BY-Klausel zulässig, die Spaltenausdrücke enthält. Mit GROUPING SETS, ROLLUP, CUBE, WITH CUBE oder WITH ROLLUP-Konstrukten ist es nicht zulässig. ALL ist der Standard und ist implizit. Es ist ebenso nur in der abwärtskompatiblen Syntax zulässig.
  
### <a name="comparison-of-supported-group-by-features"></a>Vergleich der unterstützten GROUP BY- Funktionen  
 In der folgenden Tabelle werden die GROUP BY-Features beschrieben, die abhängig von den SQL-Versionen und dem Datenbankkompatibilitätsgrad unterstützt werden.  
  
|Funktion|SQL Server Integration Services|SQL Server, Kompatibilitätsgrad 100 oder höher|SQL Server 2008 oder höher, mit Kompatibilitätsgrad 90.|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT-Aggregate|Nicht unterstützt für WITH CUBE oder WITH ROLLUP.|Unterstützt für WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE oder ROLLUP.|Wie bei Kompatibilitätsgrad 100|  
|Benutzerdefinierte Funktion mit CUBE- oder ROLLUP-Namen in der GROUP BY-Klausel|Benutzerdefinierte Funktionen **dbo.cube(***arg1***,***...argN***)** oder **dbo.rollup(***arg1***,**...*argN***)** in der GROUP BY-Klausel sind zulässig.<br /><br /> Beispiel: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|Benutzerdefinierte Funktionen **dbo.cube (***arg1***,**...argN**)** oder **dbo.rollup(**arg1**,***...argN***)** in der GROUP BY-Klausel sind nicht zulässig.<br /><br /> Beispiel: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> Es wird folgende Fehlermeldung zurückgegeben: "Incorrect syntax near the keyword 'cube'&#124;'rollup'." (Falsche Syntax in der Nähe des 'cube'&#124;'rollup'-Schlüsselworts.).<br /><br /> Ersetzen Sie `dbo.cube` durch `[dbo].[cube]` oder `dbo.rollup` durch `[dbo].[rollup]`, um dieses Problem zu vermeiden.<br /><br /> Das folgende Beispiel ist zulässig: `SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|Benutzerdefinierte Funktionen *dbo.cube ***(arg1***,***...argN*) oder **dbo.rollup(***arg1***,***...argN***)** in der GROUP BY-Klausel sind zulässig.<br /><br /> Beispiel: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
|GROUPING SETS|Nicht unterstützt|Supported|Supported|  
|CUBE|Nicht unterstützt|Supported|Nicht unterstützt|  
|ROLLUP|Nicht unterstützt|Supported|Nicht unterstützt|  
|Gesamtergebnis, z. B. GROUP BY ()|Nicht unterstützt|Supported|Supported|  
|GROUPING_ID-Funktion|Nicht unterstützt|Supported|Supported|  
|GROUPING-Funktion|Supported|Supported|Supported|  
|WITH CUBE|Supported|Supported|Supported|  
|WITH ROLLUP|Supported|Supported|Supported|  
|WITH CUBE- oder WITH ROLLUP-Entfernung "doppelter" Gruppierungen|Supported|Supported|Supported| 
 
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-use-a-simple-group-by-clause"></a>A. Verwenden einer einfachen GROUP BY-Klausel  
 Im folgenden Beispiel wird die Summe für jede `SalesOrderID` aus der `SalesOrderDetail`-Tabelle abgerufen. In diesem Beispiel wird AdventureWorks verwendet.  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. Verwenden einer GROUP BY-Klausel mit mehreren Tabellen  
 Im folgenden Beispiel wird die Anzahl von Mitarbeitern für die einzelnen `City`-Spalten der `Address`-Tabelle abgerufen, die mit der `EmployeeAddress`-Tabelle verknüpft ist. In diesem Beispiel wird AdventureWorks verwendet. 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. Verwenden einer GROUP BY-Klausel mit einem Ausdruck  
 Im folgenden Beispiel wird der Gesamtumsatz für jedes Jahr mithilfe der `DATEPART`-Funktion abgerufen. Derselbe Ausdruck muss sowohl in der `SELECT`-Liste als auch in der `GROUP BY`-Klausel vorhanden sein.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. Verwenden einer GROUP BY-Klausel mit einer HAVING-Klausel  
 Im folgenden Beispiel wird die `HAVING`-Klausel verwendet, um anzugeben, welche der in der `GROUP BY`-Klausel generierten Gruppen in das Resultset aufgenommen werden soll.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>Beispiele: SQL Data Warehouse und Parallel Data Warehouse  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. Grundlegende Verwendung der GROUP BY-Klausel  
 Im folgenden Beispiel wird die Gesamtsumme aller Verkäufe pro Tag gesucht. Für jeden Tag wird eine Zeile mit der Summe aller Verkäufe pro Tag zurückgegeben.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. Grundlegende Verwendung des DISTRIBUTED_AGG-Hinweises  
 Dieses Beispiel verwendet den DISTRIBUTED_AGG-Abfragehinweis, um die Anwendung zu zwingen, die Tabelle an der `CustomerKey`-Spalte umzusortieren, bevor die Aggregation durchgeführt wird.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. Variationen der Syntax für GROUP BY  
 Wenn die SELECT-Liste nicht über Aggregationen verfügt, muss jede Spalte in der SELECT-Liste in die GROUP BY-Liste aufgenommen werden. Berechnete Spalten in der SELECT-Liste können zwar in der GROUP BY-Liste angezeigt werden, dies ist jedoch nicht erforderlich. Beispiele für syntaktisch gültige SELECT-Anweisungen:  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. Verwenden von GROUP BY mit mehreren GROUP BY-Ausdrücken  
 Im folgenden Beispiel werden die Ergebnisse mithilfe mehrerer `GROUP BY`-Kriterien gruppiert. Wenn sich innerhalb jeder `OrderDateKey`-Gruppe Untergruppen befinden, die von `DueDateKey` unterschieden werden können, wird für jedes Resultset eine neue Gruppierung definiert.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. Verwenden einer GROUP BY-Klausel mit einer HAVING-Klausel  
 Im folgenden Beispiel wird die `HAVING`-Klausel verwendet, um anzugeben, welche der in der `GROUP BY`-Klausel generierten Gruppen in das Resultset aufgenommen werden soll. Nur die Gruppen mit Bestelldaten im Jahr 2004 oder später werden in die Ergebnisse aufgenommen.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GROUPING_ID &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [GROUPING &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [SELECT-Klausel &#40;Transact-SQL&#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




