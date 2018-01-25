---
title: GROUP BY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
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
dev_langs: TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
caps.latest.revision: "80"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5e99efe49620003de40659dd4bfd959dacef986c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select---group-by--transact-sql"></a>Wählen Sie-GROUP BY - Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine SELECT-Anweisung-Klausel, die das Abfrageergebnis in Gruppen von Zeilen, in der Regel für das Ausführen ein oder mehrere Aggregationen für jede Gruppe unterteilt. Die SELECT-Anweisung gibt eine Zeile pro Gruppe zurück.  
  
## <a name="syntax"></a>Syntax  

 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
Gibt eine Spalte oder eine nicht-aggregierbare Berechnung für eine Spalte an. Diese Spalte kann auf eine Tabelle, abgeleitete Tabelle oder Sicht gehören. Die Spalte muss in der FROM-Klausel der SELECT-Anweisung angezeigt werden, ist jedoch nicht erforderlich, die in der Auswahlliste angezeigt werden. 

Gültige Ausdrücke finden Sie unter [Ausdruck](~/t-sql/language-elements/expressions-transact-sql.md).    

Die Spalte muss in der FROM-Klausel der SELECT-Anweisung angezeigt werden, ist jedoch nicht erforderlich, die in der Auswahlliste angezeigt werden. Jedoch jede Tabelle oder Spalte in einem Nichtaggregatausdruck in Anzeigen der \<auswählen > Liste in der GROUP BY-Liste enthalten sein muss:  
  
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
Der Ausdruck für die Spalte darf nicht enthalten:

- Einen Spaltenalias, der in der Auswahlliste definiert ist. Sie können einen Spaltenalias für eine abgeleitete Tabelle, die in der FROM-Klausel definiert ist.
- Eine Spalte vom Typ **Text**, **Ntext**, oder **Image**. Allerdings können Sie eine Spalte mit Text, Ntext oder Image als Argument an eine Funktion verwenden, die einen Wert, der einen gültigen Datentyp zurückgibt. Der Ausdruck kann beispielsweise SUBSTRING() und CAST() verwenden. Dies gilt auch für Ausdrücke in der HAVING-Klausel.
- XML-Datentypmethoden. Es kann eine benutzerdefinierte Funktion enthalten, die Xml-Datentypmethoden verwendet. Er kann eine berechnete Spalte enthalten, die Xml-Datentypmethoden verwendet. 
- Eine Unterabfrage. Fehler 144 zurückgegeben. 
- Eine Spalte aus einer indizierten Sicht. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *Spaltenausdruck* [,... ...n] 

Gruppiert die Ergebnisse SELECT-Anweisung nach den Werten in einer Liste von Spaltenausdrücken für mindestens eine an. 

Diese Abfrage erstellt z. B. eine Sales-Tabelle mit Spalten für das Land, Region und Sales. Fügt vier Zeilen und zwei Zeilen verfügen übereinstimmenden Werte für Land und Region.  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
Die Sales-Tabelle werden diese Zeilen enthält:

| Country | Region | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 200 |
| Canada | British Columbia | 300 |
| United States | Montana | 100 |

Der nächsten Abfrage gruppiert, Land und Region und gibt die aggregierte Summe für jede Kombination von Werten zurück.  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
Das Abfrageergebnis enthält 3 Zeilen an, da es sich um 3 Kombinationen von Werten für Land und Region. Der TotalSales für Kanada und British Columbia ist die Summe von zwei Zeilen. 

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| United States | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY ROLLUP

Erstellt eine Gruppe für jede Kombination von Spaltenausdrücke. Darüber hinaus Rollup"es" die Ergebnisse in Teil- und Gesamtergebnisse. Zu diesem Zweck wird von rechts nach links, verringern die Anzahl der über die Gruppen und die Aggregation(s) erstellt Spaltenausdrücke verschoben. 

Die Spaltenreihenfolge wirkt sich auf die ROLLUP-Ausgabe und die Anzahl der Zeilen im Resultset auswirken kann.  

Beispielsweise `GROUP BY ROLLUP (col1, col2, col3, col4)` Gruppen für jede Kombination von Spaltenausdrücke in den folgenden Listen erstellt.  

- col1, col2, col3, col4 
- col1, col2, col3 NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- NULL, NULL, NULL, NULL – ist dies die Gesamtsumme

Verwenden die Tabelle aus dem vorherigen Beispiel, wird dieser Code anstelle einer einfachen GROUP BY einen GROUP BY ROLLUP-Vorgang ausgeführt.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

Das Ergebnis der Abfrage hat die gleichen Aggregationen als das einfache GROUP BY ohne den ROLLUP. Außerdem erstellt es Teilergebnisse für jeden Wert des Landes. Schließlich gibt es ein Gesamtergebnis für alle Zeilen. Das Ergebnis sieht wie folgt:

| Country | Region | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| Canada | NULL | 600 |
| United States | Montana | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE)  

GROUP BY CUBE erstellt Gruppen für alle möglichen Kombinationen von Spalten. Für GROUP BY CUBE (a, b) hat die Ergebnisse Gruppen für eindeutige Werte (a, b), (NULL, b), (a, NULL) und (NULL, NULL).

Verwenden die Tabelle aus den vorherigen Beispielen, führt diesen Code eine GROUP BY CUBE-Operation für Land und Region. 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

Das Abfrageergebnis enthält Gruppen für eindeutige Werte (Land, Region), (NULL, Region), (Land, NULL) und (NULL, NULL). Die Ergebnisse aussehen wie folgt:

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
   
 ### <a name="group-by-grouping-sets--"></a>GROUP BY GROUPING SETS)  
 
Die GROUPING SETS-Option bietet Ihnen die Möglichkeit, mehrere GROUP BY-Klauseln in einer GROUP BY-Klausel zu kombinieren. Die Ergebnisse entsprechen denen von UNION ALL für die angegebenen Gruppen. 

Beispielsweise `GROUP BY ROLLUP (Country, Region)` und `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` die gleichen Ergebnisse zurück. 

Wenn GROUPING SETS zwei oder mehr Elemente enthält, sind die Ergebnisse einer Union der Elemente an. In diesem Beispiel gibt die Union der Ergebnisse ROLLUP und CUBE für Land und Region zurück.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

Die Ergebnisse sind identisch mit dieser Abfrage, die eine Kombination der beiden GROUP BY-Anweisungen zurückgibt.

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

Doppelte Gruppen generiert eine GROUPING SETS-Liste ist nicht von SQL konsolidiert werden. Beispielsweise ist in `GROUP BY ( (), CUBE (Country, Region) )`, beide Elemente geben eine Zeile für die Gesamtsumme zurück, und beide Zeilen werden in den Ergebnissen aufgeführt. 

 ### <a name="group-by-"></a>GROUP BY ()  
Gibt an, die leere Gruppe, die die Gesamtsumme generiert. Dies ist hilfreich, als eines der Elemente einer Gruppierung festlegen. Beispielsweise wird diese Anweisung gibt den Gesamtumsatz für jedes Land und gibt dann die Gesamtsumme für alle Länder.

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ALL]-Spalte-Ausdruck [,... ...n] 

Gilt für: SQLServer und Azure SQL-Datenbank

Hinweis: Diese Syntax wird nur für Abwärtskompatibilität bereitgestellt. Es wird in einer zukünftigen Version entfernt. Mithilfe dieser Syntax bei neuen Entwicklungen, und Planen von Anwendungen zu ändern, die diese Syntax verwenden.

Gibt an, um alle Gruppen einbeziehen, in den Ergebnissen unabhängig davon, ob sie die Suchkriterien in der WHERE-Klausel erfüllen. Gruppen, die die Suchkriterien entsprechen, nicht enthalten, NULL für die Aggregation. 

GROUP BY ALL:
- Wird nicht in Abfragen unterstützt, die auf Remotetabellen zugreifen, wenn es auch eine WHERE-Klausel in der Abfrage gibt.
- Scheitert bei Spalten, die mit dem FILESTREAM-Attribut enthalten.
  
### <a name="with-distributedagg"></a>MIT DER DISTRIBUTED_AGG-(HINWEIS)
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse

Der DISTRIBUTED_AGG-Abfragehinweis erzwingt den massive parallelverarbeitung (MPP) eine Tabelle für eine bestimmte Spalte vor dem Ausführen einer Aggregations verteilt. Darf nur eine Spalte in der GROUP BY-Klausel einen Abfrage DISTRIBUTED_AGG-Hinweis. Nachdem die Abfrage abgeschlossen ist, wird die weiterverteilten Tabelle gelöscht. Die ursprüngliche Tabelle wird nicht geändert.  

Hinweis: Der DISTRIBUTED_AGG-Abfragehinweis dient zur Abwärtskompatibilität mit früheren Versionen von Parallel Data Warehouse und verbessert die Leistung für die meisten Abfragen nicht. Standardmäßig verteilt MPP bereits Daten nach Bedarf zur Verbesserung der Leistung für Aggregationen. 
  
## <a name="general-remarks"></a>Allgemeine Hinweise

### <a name="how-group-by-interacts-with-the-select-statement"></a>Interaktion GROUP BY mit der SELECT-Anweisung
SELECT-Liste:
- Vektoraggregate. Aggregatfunktionen in der SELECT-Liste enthalten sind, wird von GROUP BY einen Summenwert für jede Gruppe berechnet. Diese Ausdrücke werden als Vektoraggregate bezeichnet. 
- DISTINCT-Aggregate. Die Aggregate AVG (DISTINCT *Column_name*), COUNT (DISTINCT *Column_name*), und SUM (DISTINCT *Column_name*) mit ROLLUP, CUBE und GROUPING SETS unterstützt werden.
  
WHERE-Klausel:
- SQL entfernt Zeilen, die nicht entsprechen, die die Bedingungen der WHERE-Klausel, bevor irgendwelche Gruppierungsvorgänge ausgeführt wird.  
  
HAVING-Klausel:
- SQL ausführen verwendet die having-Klausel, um Filtergruppen im Resultset. 
  
ORDER BY-Klausel:
- Verwenden Sie die ORDER BY-Klausel, um das Resultset zu sortieren. Die GROUP BY-Klausel sortiert das Resultset nicht. 
  
NULL-Werte:
- Wenn eine Gruppierungsspalte NULL-Werte enthält, werden alle NULL-Werte als gleich betrachtet und in einer einzelnen Gruppe gesammelt werden.   
  
## <a name="limitations-and-restrictions"></a>Einschränkungen

Gilt für: SQLServer (ab 2008) und Azure SQL Data Warehouse

### <a name="maximum-capacity"></a>Maximale Kapazität

Für eine GROUP BY-Klausel, die ROLLUP, CUBE oder GROUPING SETS verwendet, ist die maximale Anzahl von Ausdrücken 32. Die maximale Anzahl von Gruppen ist 4096 (2<sup>12</sup>). In den folgenden Beispielen wird fehlschlagen, da die GROUP BY-Klausel mehr als 4096 Gruppen verfügt.  
 
-   Im folgenden Beispiel wird 4097 (2<sup>12</sup> + 1) gruppierungssätze und schlägt fehl.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   Im folgenden Beispiel wird 4097 (2<sup>12</sup> + 1) gruppiert und schlägt fehl. Sowohl die `CUBE ()`- als auch die `()`-Gruppierungssätze generieren eine Gesamtergebniszeile, und doppelte Gruppierungssätze werden nicht entfernt.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   Dieses Beispiel verwendet die abwärtskompatibler Syntax. Es generiert 8192 (2<sup>13</sup>) gruppierungssätze und schlägt fehl.  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    Die Anzahl der Gruppe von Elementen durch die GROUP BY-Spaltengrößen, die Aggregatspalten beschränkt ist abwärtskompatibel GROUP BY-Klauseln, die keine Cube- oder ROLLUP enthalten, und die Aggregatwerte der Abfrage beteiligten. Diese Beschränkung ergibt sich aus der maximalen Größe von 8.060 Byte der temporären Arbeitstabelle, die für die zwischenzeitlich erstellten Abfrageergebnisse benötigt wird. Bei Angabe von CUBE oder ROLLUP sind höchstens 12 Gruppierungsausdrücke zulässig.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>Unterstützung für ISO und ANSI SQL 2006 GROUP BY-Funktionen

Die GROUP BY-Klausel unterstützt alle GROUP BY-Funktionen, die in der SQL-2006-Standard, mit Ausnahme der folgenden Syntax enthalten sind:  
  
-   Gruppierungssätze sind in einer GROUP BY-Klausel nicht zugelassen, es sei denn, sie sind Teil einer expliziten GROUPING SETS-Liste. Deutet, `GROUP BY Column1, (Column2, ...ColumnN`) ist zulässig, in dem Standard jedoch nicht in Transact-SQL.  Transact-SQL unterstützt `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` und `GROUP BY Column1, Column2, ... ColumnN`, die semantisch gleichwertig sind. Diese Klauseln sind mit dem vorherigen `GROUP BY`-Beispiel semantisch gleichwertig. Wird verwendet, um zu vermeiden, `GROUP BY Column1, (Column2, ...ColumnN`) fehlinterpretiert wird als `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`, die beide nicht semantisch gleichwertig.  
  
-   Gruppierungssätze sind in Gruppierungssätzen nicht zulässig. Beispielsweise `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` ist zulässig, in der SQL-2006-Standard jedoch nicht in Transact-SQL. Transact-SQL können `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` oder `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`, die dem ersten GROUP BY-Beispiel semantisch gleichwertig sind und eine klare Syntax.  
  
-   GROUP BY [ALL/DISTINCT] ist nur in einer einfachen GROUP BY-Klausel zulässig, die Spaltenausdrücke enthält. Es ist mit den Konstrukten GROUPING SETS, ROLLUP, CUBE, WITH CUBE oder WITH ROLLUP nicht zulässig. ALL ist der Standard und ist implizit. Es ist auch nur in abwärtskompatibler Syntax zulässig.
  
### <a name="comparison-of-supported-group-by-features"></a>Vergleich der unterstützten GROUP BY- Funktionen  
 Die folgende Tabelle beschreibt die GROUP BY-Funktionen, die auf Grundlage der SQL-Versionen und Datenbankkompatibilitätsgrad unterstützt werden.  
  
|Funktion|SQL Server Integration Services|SQL Server, Kompatibilitätsgrad 100 oder höher|SQL Server 2008 oder höher, mit Kompatibilitätsgrad 90.|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT-Aggregate|Nicht unterstützt für WITH CUBE oder WITH ROLLUP.|Unterstützt für WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE oder ROLLUP.|Wie bei Kompatibilitätsgrad 100|  
|Benutzerdefinierte Funktion mit CUBE- oder ROLLUP-Namen in der GROUP BY-Klausel|User-defined Function, **dbo.cube (***arg1***,***.. ...argN***)** oder **dbo.rollup (***arg1***,**... *ArgN ***)* * in der GROUP BY-Klausel ist zulässig.<br /><br /> Beispiel: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|User-defined Function, **dbo.cube (***arg1***,**.. ...argN**)** oder **dbo.rollup (**arg1**,***.. ...argN*** )** in der GROUP BY-Klausel nicht zulässig.<br /><br /> Beispiel: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> Die folgende Fehlermeldung wird zurückgegeben: "falsche Syntax in der Nähe von Schlüsselwort 'Cube' &#124;" Rollup "."<br /><br /> Ersetzen Sie `dbo.cube` durch `[dbo].[cube]` oder `dbo.rollup` durch `[dbo].[rollup]`, um dieses Problem zu vermeiden.<br /><br /> Im folgende Beispiel ist zulässig:`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|User-defined Function, **dbo.cube (***arg1***, ***.. ...argN*) oder **dbo.rollup (***arg1***,***.. ...argN***)**in der GROUP BY-Klausel ist zulässig<br /><br /> Beispiel: `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
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
  
### <a name="a-use-a-simple-group-by-clause"></a>A. Verwenden Sie eine einfache GROUP BY-Klausel  
 Im folgenden Beispiel wird die Summe für jede `SalesOrderID` aus der `SalesOrderDetail`-Tabelle abgerufen. In diesem Beispiel wird die AdventureWorks verwendet.  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. Verwenden einer GROUP BY-Klausel mit mehreren Tabellen  
 Im folgenden Beispiel wird die Anzahl von Mitarbeitern für die einzelnen `City`-Spalten der `Address`-Tabelle abgerufen, die mit der `EmployeeAddress`-Tabelle verknüpft ist. In diesem Beispiel wird die AdventureWorks verwendet. 
  
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
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>Beispiele: SQL Datawarehouse und Parallel Datawarehouse  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. Grundlegende Verwendung von GROUP BY-Klausel  
 Das folgende Beispiel sucht die Gesamtmenge für alle Verkäufe pro Tag. Eine Zeile, die die Summe aller Kaufaufträge enthält, wird für jeden Tag zurückgegeben.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. Grundlegende Verwendung von der DISTRIBUTED_AGG-Hinweis  
 Dieses Beispiel verwendet den DISTRIBUTED_AGG-Abfragehinweis, um das Gerät auf die Tabelle auf zufällige Erzwingen der `CustomerKey` Spalte vor dem Ausführen der Aggregations.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. Variationen der Syntax für GRUPPIEREN nach  
 Wenn die select-Liste keine Aggregationen aufweist, muss jede Spalte in der select-Liste in der GROUP BY-Liste enthalten sein. Berechnete Spalten in der Auswahlliste aufgeführt werden können, sind jedoch nicht erforderlich ist, in der GROUP BY-Liste. Dies sind Beispiele für gültige Syntax SELECT-Anweisungen:  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. Verwenden einer GROUP BY mit mehreren GROUP BY-Ausdrücke  
 Im folgende Beispiel gruppiert die Ergebnisse, die mithilfe mehrerer `GROUP BY` Kriterien. Wenn es sich, in jeder `OrderDateKey` gruppieren, sind Untergruppen an, die von der unterschieden werden können `DueDateKey`, eine neue Gruppierung für das Resultset definiert werden.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. Verwenden einer GROUP BY-Klausel mit einer HAVING-Klausel  
 Im folgenden Beispiel wird die `HAVING` -Klausel zur Angabe der generierten Gruppen der `GROUP BY` -Klausel, die in das Resultset aufgenommen werden. Nur die Gruppen mit Bestelldaten in 2004 oder höher werden in den Ergebnissen enthalten sein.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GROUPING_ID &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [GROUPING &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [SELECT Clause &#40;Transact-SQL&#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




