---
title: Verwenden von PIVOT und UNPIVOT | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
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
- PIVOT_TSQL
helpviewer_keywords:
- FROM clause, UNPIVOT operator
- unpivoting tables
- table pivoting [SQL Server]
- UNPIVOT operator
- crosstab query
- PIVOT operator
- rotating table-valued expressions
- pivoting tables
- FROM clause, PIVOT operator
- rotating columns
ms.assetid: 24ba54fc-98f7-4d35-8881-b5158aac1d66
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1feee91c251b5c1f326e8e69569186c049007d9e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="from---using-pivot-and-unpivot"></a>FROM: Verwenden von PIVOT und UNPIVOT
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Verwenden Sie die relationalen Operatoren `PIVOT` und `UNPIVOT`, um einen Tabellenwertausdruck in einer andere Tabelle zu ändern. Mit dem `PIVOT`-Operator wird ein Tabellenwertausdruck gedreht, indem die eindeutigen Werte einer Spalte des Ausdrucks in mehrere Spalten der Ausgabe versetzt werden und dabei gegebenenfalls Aggregationen für verbliebene Spaltenwerte erfolgen, die in der endgültigen Ausgabe erwünscht sind. Der `UNPIVOT`-Operator führt den umgekehrten Vorgang aus, d.h., er setzt Spalten eines Tabellenwertausdrucks in Spaltenwerte zurück.  
  
 Die von `PIVOT` bereitgestellte Syntax ist einfacher und lesbarer als die Syntax, die andernfalls durch eine komplexe Reihe von `SELECT...CASE`-Anweisungen angegeben werden müsste. Eine vollständige Beschreibung der Syntax für `PIVOT` finden Sie unter [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
 Die folgende Syntax fasst die Verwendung des `PIVOT`-Operators zusammen.  
  
```  
SELECT <non-pivoted column>,  
    [first pivoted column] AS <column name>,  
    [second pivoted column] AS <column name>,  
    ...  
    [last pivoted column] AS <column name>  
FROM  
    (<SELECT query that produces the data>)   
    AS <alias for the source query>  
PIVOT  
(  
    <aggregation function>(<column being aggregated>)  
FOR   
[<column that contains the values that will become column headers>]   
    IN ( [first pivoted column], [second pivoted column],  
    ... [last pivoted column])  
) AS <alias for the pivot table>  
<optional ORDER BY clause>;  
```  

## <a name="remarks"></a>Remarks  
Die Spaltenbezeichner in der `UNPIVOT`-Klausel folgen der Katalogsortierung. Bei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] wird immer die Sortierung `SQL_Latin1_General_CP1_CI_AS` verwendet. Bei teilweise eigenständigen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Datenbanken wird immer die Sortierung `Latin1_General_100_CI_AS_KS_WS_SC` verwendet. Wenn die Spalte mit anderen Spalten kombiniert wird, ist eine COLLATE-Klausel (`COLLATE DATABASE_DEFAULT`) erforderlich, um Konflikte zu vermeiden.  

  
## <a name="basic-pivot-example"></a>Elementares Beispiel für PIVOT  
 Im folgenden Codebeispiel wird eine zweispaltige Tabelle mit vier Zeilen erstellt.  
  
```  
USE AdventureWorks2014 ;  
GO  
SELECT DaysToManufacture, AVG(StandardCost) AS AverageCost   
FROM Production.Product  
GROUP BY DaysToManufacture;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 DaysToManufacture AverageCost
 ----------------- -----------
 0                 5.0885
 1                 223.88
 2                 359.1082
 4                 949.4105
 ```
  
 Es sind keine Produkte mit drei `DaysToManufacture` definiert.  
  
 Im folgenden Code wird dasselbe Ergebnis pivotiert angezeigt, sodass die `DaysToManufacture`-Werte als Spaltenüberschriften verwendet werden. Es wird eine Spalte für drei `[3]` Tage bereitgestellt, auch wenn die Ergebnisse `NULL` betragen.  
  
```  
-- Pivot table with one row and five columns  
SELECT 'AverageCost' AS Cost_Sorted_By_Production_Days,   
[0], [1], [2], [3], [4]  
FROM  
(SELECT DaysToManufacture, StandardCost   
    FROM Production.Product) AS SourceTable  
PIVOT  
(  
AVG(StandardCost)  
FOR DaysToManufacture IN ([0], [1], [2], [3], [4])  
) AS PivotTable;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Cost_Sorted_By_Production_Days 0           1           2           3           4         
------------------------------ ----------- ----------- ----------- ----------- -----------
AverageCost                    5.0885      223.88      359.1082    NULL        949.4105
```
  
## <a name="complex-pivot-example"></a>Komplexes PIVOT-Beispiel  
 Ein häufiges Szenario, in dem sich `PIVOT` als nützlich erweisen kann, ist das Generieren von Kreuztabellenberichten zum Zusammenfassen von Daten. Nehmen Sie z. B. an, Sie möchten die `PurchaseOrderHeader`-Tabelle in der `AdventureWorks2014`-Beispieldatenbank abfragen, um die Anzahl an von bestimmten Mitarbeitern aufgenommenen Bestellungen zu bestimmen. Mit der folgenden Abfrage wird dieser Bericht geordnet nach Verkäufern bereitgestellt:  
  
```  
USE AdventureWorks2014;  
GO  
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5  
FROM   
(SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM Purchasing.PurchaseOrderHeader) p  
PIVOT  
(  
COUNT (PurchaseOrderID)  
FOR EmployeeID IN  
( [250], [251], [256], [257], [260] )  
) AS pvt  
ORDER BY pvt.VendorID;  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
```
VendorID    Emp1        Emp2        Emp3        Emp4        Emp5  
----------- ----------- ----------- ----------- ----------- -----------
1492        2           5           4           4           4
1494        2           5           4           5           4
1496        2           4           4           5           5
1498        2           5           4           4           4
1500        3           4           4           5           4
```
  
 Die von dieser untergeordneten SELECT-Anweisung zurückgegebenen Ergebnisse werden in die `EmployeeID`-Spalte pivotiert.  
  
```  
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 Dies bedeutet, dass die von der `EmployeeID`-Spalte zurückgegebenen eindeutigen Werte ihrerseits zu Feldern im endgültigen Resultset werden. Das Ergebnis ist eine Spalte für jede `EmployeeID`-Nummer, die in der PIVOT-Klausel angegeben war: In diesem Fall die Mitarbeiter `164`, `198`, `223`, `231` und `233`. Die `PurchaseOrderID`-Spalte dient als Wertspalte, für die die in der endgültigen Ausgabe zurückgegebenen Spalten, die auch als Gruppierungsspalten bezeichnet werden, gruppiert sind. In diesem Fall werden die Gruppierungsspalten durch die `COUNT`-Funktion aggregiert. Beachten Sie, dass eine Warnmeldung darauf hinweist, dass eventuell vorhandene NULL-Werte, die sich in der `PurchaseOrderID`-Spalte befinden, bei der Berechnung der `COUNT`-Funktion für die einzelnen Mitarbeiter nicht berücksichtigt werden.  
  
> [!IMPORTANT]  
>  Beim Verwenden der Aggregatfunktionen mit `PIVOT` werden eventuell vorhandene NULL-Werte in der Wertespalte bei der Berechnung der Aggregation nicht berücksichtigt.  
  
 `UNPIVOT` führt nahezu den entgegengesetzten Vorgang zu `PIVOT` aus, indem dabei die Spalten zu Zeilen umgesetzt werden. Angenommen, die im vorherigen Beispiel erstellte Tabelle wurde in der Datenbank als `pvt` gespeichert, und Sie möchten nun die Spalten-IDs `Emp1`, `Emp2`, `Emp3`, `Emp4` und `Emp5` zu Zeilenwerten umsetzen, sodass sie einem bestimmten Verkäufer entsprechen. Dies bedeutet, dass Sie zwei zusätzliche Spalten identifizieren müssen. Die Spalte, die die umzusetzenden Spaltenwerte erhalten soll (`Emp1`, `Emp2`, ...), wird `Employee` genannt, und die Spalte, die die Werte erhalten soll, die sich derzeit unter den umzusetzenden Spalten befinden, wird `Orders` genannt. Diese Spalten entsprechen jeweils *pivot_column* und *value_column* in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Definition. So sieht die Abfrage aus.  
  
```  
-- Create the table and insert values as portrayed in the previous example.  
CREATE TABLE pvt (VendorID int, Emp1 int, Emp2 int,  
    Emp3 int, Emp4 int, Emp5 int);  
GO  
INSERT INTO pvt VALUES (1,4,3,5,4,4);  
INSERT INTO pvt VALUES (2,4,1,5,5,5);  
INSERT INTO pvt VALUES (3,4,3,5,4,4);  
INSERT INTO pvt VALUES (4,4,2,5,5,4);  
INSERT INTO pvt VALUES (5,5,1,5,5,5);  
GO  
-- Unpivot the table.  
SELECT VendorID, Employee, Orders  
FROM   
   (SELECT VendorID, Emp1, Emp2, Emp3, Emp4, Emp5  
   FROM pvt) p  
UNPIVOT  
   (Orders FOR Employee IN   
      (Emp1, Emp2, Emp3, Emp4, Emp5)  
)AS unpvt;  
GO  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
```
VendorID    Employee    Orders
----------- ----------- ------
1            Emp1       4
1            Emp2       3 
1            Emp3       5
1            Emp4       4
1            Emp5       4
2            Emp1       4
2            Emp2       1
2            Emp3       5
2            Emp4       5
2            Emp5       5
...
```
  
 Beachten Sie, dass `UNPIVOT` nicht das exakte Gegenteil von `PIVOT` ist. `PIVOT` führt eine Aggregation aus, d.h., der Operator führt ggf. mehrere Zeilen in einer einzigen Zeile der Ausgabe zusammen. `UNPIVOT` ergibt keine Reproduktion des ursprünglichen Tabellenwertausdrucks, da Zeilen zusammengeführt wurden. Außerdem verschwinden NULL-Werte in der Eingabe von `UNPIVOT` in der Ausgabe, auch wenn beim ursprünglichen `PIVOT`-Vorgang NULL-Werte vorhanden waren.  
  
 Für die Sicht `Sales.vSalesPersonSalesByFiscalYears` in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank wird `PIVOT` verwendet, um den Gesamtumsatz jedes Vertriebsmitarbeiters pro Geschäftsjahr zurückzugeben. Um die Sicht in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] skripten zu können, suchen Sie diese im **Objekt-Explorer** im Ordner **Sichten** für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank. Klicken Sie mit der rechten Maustaste auf den Namen der Sicht, und klicken Sie auf **Script View as** (Skript für Sicht als).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [CASE (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
