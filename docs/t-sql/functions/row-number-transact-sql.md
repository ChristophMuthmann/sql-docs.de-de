---
title: ROW_NUMBER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/11/2017
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 35d962e66f23200635087f2416ad2fb5079bbdfa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Nummeriert die Ausgabe eines Resultsets. Genauer gesagt wird die fortlaufende Nummer einer Zeile innerhalb einer Partition eines Resultsets zurückgegeben, beginnend mit 1 für die erste Zeile in jeder Partition. 
  
`ROW_NUMBER` und `RANK` sind ähnlich. `ROW_NUMBER` nummeriert alle Zeilen sequenziell (z.B. 1, 2, 3, 4, 5). `RANK` stellt den gleichen numerischen Wert für gleichwertige Werte bereit (z.B. 1, 2, 3, 4, 5).   
  
> [!NOTE]
> `ROW_NUMBER` ist ein temporärer Wert, der berechnet wird, wenn die Abfrage ausgeführt wird. Unter [IDENTITY-Eigenschaft](../../t-sql/statements/create-table-transact-sql-identity-property.md) und [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) finden Sie weitere Informationen zum dauerhaften Speichern von Zahlen in einer Tabelle. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>Syntax  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumente  
 PARTITION BY *value_expression*  
 Teilt das von der [FROM](../../t-sql/queries/from-transact-sql.md)-Klausel erzeugte Resultset in Partitionen, auf die die ROW_NUMBER-Funktion angewendet wird. *value_expression* gibt die Spalte an, nach der das Resultset partitioniert wird. Wird `PARTITION BY` nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 Die `ORDER BY`-Klausel bestimmt die Reihenfolge, in der den Zeilen die eindeutige `ROW_NUMBER` innerhalb einer angegebenen Partition zugewiesen wird. Sie ist erforderlich. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **bigint**  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Es gibt keine Garantie, dass die mithilfe von `ROW_NUMBER()` zurückgegebenen Zeilen bei jeder Ausführung exakt gleich sind, es sei denn, die folgenden Bedingungen treffen zu.  
  
1.  Werte der partitionierten Spalte sind eindeutig.  
  
2.  Werte der `ORDER BY`-Spalten sind eindeutig.  
  
3.  Kombinationen der Werte der Partitionsspalte und `ORDER BY`-Spalten sind eindeutig.  
  
 `ROW_NUMBER()` ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-examples"></a>A. Einfache Beispiele 

Die folgende Abfrage gibt vier Systemtabellen in alphabetischer Reihenfolge zurück.

```sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|NAME    |recovery_model_desc |  
|-----------  |------------ |  
|master |SIMPLE |
|model |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

Fügen Sie mit der `ROW_NUMBER`-Funktion eine Spalte namens `Row#` (in diesem Fall) hinzu, um eine Spalte für Zeilennummern vor jeder Zeile hinzuzufügen. Sie müssen die `ORDER BY`-Klausel bis zur `OVER`-Klausel verschieben.

```sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Row# |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |master |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

Durch das Hinzufügen einer `PARTITION BY`-Klausel zur `recovery_model_desc`-Spalte wird die Nummerierung neu gestartet, wenn der `recovery_model_desc`-Wert sich verändert. 
 
```sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Row# |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |model |FULL |
|1 |master |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. Zurückgeben der Zeilennummer für Vertriebsmitarbeiter  
 Im folgenden Beispiel wird eine Zeilennummer für die Vertriebsmitarbeiter in [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] auf Grundlage der Verkaufszahlen des laufenden Jahres berechnet.  
  
```sql  
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
  
```sql  
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
  
```sql  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. Zurückgeben der Zeilennummer für Vertriebsmitarbeiter  
 Im folgenden Beispiel wird `ROW_NUMBER` für die Vertriebsmitarbeiter (basierend auf der zugewiesenen Sollvorgabe für den Verkauf) zurückgegeben.  
  
```sql  
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
 Im folgenden Beispiel wird die Verwendung der `ROW_NUMBER`-Funktion mit dem `PARTITION BY`-Argument dargestellt. Dadurch nummeriert die `ROW_NUMBER`-Funktion die Zeilen in jeder Partition.  
  
```sql  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RANK &#40;Transact-SQL&#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40;Transact-SQL&#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  


