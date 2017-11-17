---
title: Verwenden von PIVOT und UNPIVOT | Microsoft Docs
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
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 413e4e89679358f0c53c82340dcae5640387ddcb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="from---using-pivot-and-unpivot"></a>VON - Verwenden von PIVOT und UNPIVOT
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Sie können die `PIVOT` und `UNPIVOT` relationale Operatoren, um eine Tabellenwert-Ausdruck in einer anderen Tabelle zu ändern. `PIVOT`Aktivieren die eindeutigen Werte einer Spalte des Ausdrucks in mehrere Spalten in der Ausgabe dreht eine tabellenwertausdrucks, Aggregationen und führt, sind sie für verbliebene Spaltenwerte erforderlich, die in der endgültigen Ausgabe erwünscht sind. `UNPIVOT`Führt den entgegengesetzten Vorgang zu PIVOT er setzt Spalten eines tabellenwertausdrucks in Spaltenwerte zurück.  
  
 Die Syntax für `PIVOT` bietet ist einfacher und besser lesbar als die Syntax, die andernfalls in eine komplexe Reihe von angegeben werden kann `SELECT...CASE` Anweisungen. Eine vollständige Beschreibung der Syntax für `PIVOT`, finden Sie unter [aus (Transact-SQL)](../../t-sql/queries/from-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
 Die folgende Syntax werden zusammengefasst, wie die `PIVOT` Operator.  
  
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

## <a name="remarks"></a>Hinweise  
Die Spalten-IDs in der `UNPIVOT` -Klausel folgen die katalogsortierung. Für [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], die Sortierung ist immer `SQL_Latin1_General_CP1_CI_AS`. Für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] teilweise eigenständige Datenbanken, die Sortierung ist immer `Latin1_General_100_CI_AS_KS_WS_SC`. Wenn die Spalte mit den anderen Spalten, und klicken Sie dann auf eine Collate-Klausel kombiniert wird (`COLLATE DATABASE_DEFAULT`) ist erforderlich, um Konflikte zu vermeiden.  

  
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
>  Wenn Aggregatfunktionen verwendet werden, mit `PIVOT`, das Vorhandensein der null-Werte in der Wertspalte werden bei der Berechnung der Aggregation nicht berücksichtigt.  
  
 `UNPIVOT`führt nahezu den entgegengesetzten Vorgang `PIVOT`, indem Sie Spalten in Zeilen drehen. Angenommen, die im vorherigen Beispiel erstellte Tabelle wurde in der Datenbank als `pvt` gespeichert, und Sie möchten nun die Spalten-IDs `Emp1`, `Emp2`, `Emp3`, `Emp4` und `Emp5` zu Zeilenwerten umsetzen, sodass sie einem bestimmten Verkäufer entsprechen. Dies bedeutet, dass Sie zwei zusätzliche Spalten identifizieren müssen. Die Spalte, die die umzusetzenden Spaltenwerte erhalten soll (`Emp1`, `Emp2`, ...), wird `Employee` genannt, und die Spalte, die die Werte erhalten soll, die sich derzeit unter den umzusetzenden Spalten befinden, wird `Orders` genannt. Diese Spalten entsprechen den *Pivot_column* und *Value_column*bzw. in die [!INCLUDE[tsql](../../includes/tsql-md.md)] Definition. So sieht die Abfrage aus.  
  
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
  
 Beachten Sie, dass `UNPIVOT` ist nicht das exakte Gegenteil von `PIVOT`. `PIVOT`führt eine Aggregation, und daher fügt mehrere Zeilen zusammen möglich, in eine einzelne Zeile in der Ausgabe. `UNPIVOT`lässt sich nicht im ursprünglichen tabellenwertausdrucks Resultset reproduzieren, da Zeilen zusammengeführt wurden. Darüber hinaus null-Werte in der Eingabe des `UNPIVOT` nicht mehr in der Ausgabe angezeigt, während möglicherweise stattgefunden haben ursprünglichen null-Werte in der Eingabe vor der `PIVOT` Vorgang.  
  
 Die `Sales.vSalesPersonSalesByFiscalYears` anzeigen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispiel Datenbank verwendet `PIVOT` um den Gesamtumsatz jedes Vertriebsmitarbeiters pro Geschäftsjahr zurückzugeben. Die Ansicht im Skript [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im **Objekt-Explorer**, suchen Sie die Sicht der **Ansichten** Ordner für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank. Mit der rechten Maustaste des Ansichtsnamens aus, und wählen Sie dann **Skriptansicht als**.  
  
## <a name="see-also"></a>Siehe auch  
 [AUS (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [Fall (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  

