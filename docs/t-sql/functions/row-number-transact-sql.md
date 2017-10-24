---
title: ROW_NUMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 820acddf7de1282501caf2fcaa43dbc757b98b7a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legen Sie die Zahlen die Ausgabe eines Ergebnisses. Genauer gesagt, gibt die laufende Nummer einer Zeile innerhalb einer Partition eines Resultsets, beginnend mit 1 für die erste Zeile in jeder Partition ein. 
  
`ROW_NUMBER`und `RANK` ähneln. `ROW_NUMBER`Zahlen, die alle Zeilen sequenziell (z. B. 1, 2, 3, 4, 5). `RANK`Stellt den gleichen Wert für Ties (z. B. 1, 2, 2, 4, 5) bereit.   
  
> [!NOTE]
> `ROW_NUMBER`ein temporärer Wert wird berechnet, wenn die Abfrage ausgeführt wird. Um Zahlen in eine Tabelle dauerhaft zu speichern, finden Sie unter [IDENTITY-Eigenschaft](../../t-sql/statements/create-table-transact-sql-identity-property.md) und [SEQUENZ](../../t-sql/statements/create-sequence-transact-sql.md). 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>Syntax  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumente  
 PARTITION BY *Value_expression*  
 Teilt das Resultset erzeugt, indem Sie die [FROM](../../t-sql/queries/from-transact-sql.md) -Klausel in Partitionen, auf die die ROW_NUMBER-Funktion angewendet wird. *Value_expression* gibt die Spalte, nach der das Resultset partitioniert wird. Wenn `PARTITION BY` nicht angegeben ist, behandelt die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 Die `ORDER BY` -Klausel bestimmt die Reihenfolge, in der die Zeilen ihren eindeutigen zugewiesen sind `ROW_NUMBER` innerhalb einer angegebenen Partition. Sie ist erforderlich. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **bigint**  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Es gibt keine Garantie, die die zurückgegebenen Zeilen mithilfe einer Abfrage `ROW_NUMBER()` angeordnet genauso bei jeder Ausführung, wenn Folgendes zutrifft.  
  
1.  Werte der partitionierten Spalte sind eindeutig.  
  
2.  Der Werte der `ORDER BY` Spalten sind eindeutig.  
  
3.  Kombinationen von Werten für die Partitionsspalte und `ORDER BY` Spalten sind eindeutig.  
  
 `ROW_NUMBER()`ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-examples"></a>A. Einfache Beispiele 

Die folgende Abfrage gibt die vier Systemtabellen in alphabetischer Reihenfolge zurück.

```t-sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|name    |recovery_model_desc |  
|-----------  |------------ |  
|master |SIMPLE |
|model |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

Um eine Zeilennummernspalte vor jede Zeile hinzuzufügen, fügen Sie eine Spalte mit dem `ROW_NUMBER` Funktion, die in diesem Fall mit dem Namen `Row#`. Sie verschieben, müssen die `ORDER BY` Klausel bis zu der `OVER` Klausel.

```t-sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Zeilennr. |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |master |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

Hinzufügen einer `PARTITION BY` -Klausel für die `recovery_model_desc` Spalte wird neu gestartet, wenn die Nummerierung der `recovery_model_desc` -Wert ändert. 
 
```t-sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Zeilennr. |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |model |FULL |
|1 |master |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. Zurückgeben der Zeilennummer für Vertriebsmitarbeiter  
 Im folgenden Beispiel wird eine Zeilennummer für die Vertriebsmitarbeiter in [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] auf Grundlage der Verkaufszahlen des laufenden Jahres berechnet.  
  
```t-sql  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>C. Zurückgeben einer Teilmenge von Zeilen  
 Im folgenden Beispiel werden Zeilennummern für alle Zeilen in der `SalesOrderHeader`-Tabelle in der Reihenfolge des `OrderDate` berechnet und nur die Zeilen `50` bis `60` (einschließlich) zurückgegeben.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-rownumber-with-partition"></a>D. Verwenden von ROW_NUMBER () mit PARTITION  
 Im folgenden Beispiel wird das Argument `PARTITION BY` zum Partitionieren des Abfrageresultset nach der Spalte `TerritoryName` verwendet. Durch die `ORDER BY`-Klausel in der `OVER`-Klausel werden die Zeilen in jeder Partition nach der Spalte `SalesYTD` sortiert. Die `ORDER BY`-Klausel in der `SELECT`-Anweisung sortiert das gesamte Abfrageresultset nach `TerritoryName`.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. Zurückgeben der Zeilennummer für Vertriebsmitarbeiter  
 Das folgende Beispiel gibt die `ROW_NUMBER` für Vertriebsmitarbeiter, die basierend auf ihren zugewiesenen Vorgabe.  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
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

### <a name="f-using-rownumber-with-partition"></a>F. Verwenden von ROW_NUMBER () mit PARTITION  
 Im folgenden Beispiel wird die Verwendung der `ROW_NUMBER`-Funktion mit dem `PARTITION BY`-Argument dargestellt. Dies bewirkt, dass die `ROW_NUMBER` Funktion, um die Anzahl der Zeilen in jeder Partition.  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
 
```  
 
RowNumber  LastName            Territory  SalesQuota  
---------  ------------------  ---------  -------------  
1          Campbell            1           4,025,000.00  
2          Ansman-Wolfe        1           3,551,000.00  
3          Mensa-Annan         1           2,275,000.00  
1          Blythe              2          11,162,000.00  
1          Carson              3          12,198,000.00  
1          Mitchell            4          11,786,000.00  
2          Ito                 4           7,804,000.00  
```
  
## <a name="see-also"></a>Siehe auch  
 [Rang &#40; Transact-SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40; Transact-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40; Transact-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  



