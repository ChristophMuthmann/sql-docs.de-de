---
title: OPTION-Klausel (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPTION clause
- OPTION_TSQL
- OPTION
- OPTION_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- clauses [SQL Server], OPTION
- OPTION clause
ms.assetid: f47e2f3f-9302-4711-9d66-16b1a2a7ffe3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a2455ed114ec558c5707a867c04c7cc038fa349f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="option-clause-transact-sql"></a>OPTION-Klausel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt an, dass der angezeigte Abfragehinweis in der gesamten Abfrage verwendet werden soll. Jeder Abfragehinweis kann nur einmal angegeben werden, obwohl mehrere Abfragehinweise zulässig sind. Es kann nur eine OPTION-Klausel pro Anweisung angegeben werden.  
  
 Diese Klausel kann in den Anweisungen SELECT, DELETE, UPDATE und MERGE angegeben werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ OPTION ( <query_hint> [ ,...n ] ) ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
OPTION ( <query_option> [ ,...n ] )  
  
<query_option> ::=  
    LABEL = label_name |  
    <query_hint>  
  
<query_hint> ::=  
    HASH JOIN   
    | LOOP JOIN   
    | MERGE JOIN  
    | FORCE ORDER  
    | { FORCE | DISABLE } EXTERNALPUSHDOWN  
```  
  
## <a name="arguments"></a>Argumente  
 *query_hint*  
 Schlüsselwörter, die angeben, dass Hinweise für den Optimierer verwendet werden, um die Verarbeitung der Anweisung durch das Datenbankmodul anzupassen. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-an-option-clause-with-a-group-by-clause"></a>A. Verwenden einer OPTION-Klausel mit einer GROUP BY-Klausel  
 Im folgenden Beispiel wird gezeigt, wie die `OPTION`-Klausel in Verbindung mit einer `GROUP BY`-Klausel verwendet wird.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="b-select-statement-with-a-label-in-the-option-clause"></a>B. SELECT-Anweisung mit einer Bezeichnung in der OPTION-Klausel  
 Im folgenden Beispiel wird eine einfache [!INCLUDE[ssDW](../../includes/ssdw-md.md)]-SELECT-Anweisung mit einer Bezeichnung in der OPTION-Klausel dargestellt.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactResellerSales  
  OPTION ( LABEL = 'q17' );  
```  
  
### <a name="c-select-statement-with-a-query-hint-in-the-option-clause"></a>C. SELECT-Anweisung mit einem Abfragehinweis in der OPTION-Klausel  
 Im folgenden Beispiel wird eine SELECT-Anweisung in der OPTION-Klausel dargestellt, die einen HASH JOIN-Abfragehinweis verwendet.  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
```  
  
### <a name="d-select-statement-with-a-label-and-multiple-query-hints-in-the-option-clause"></a>D. SELECT-Anweisung mit einer Bezeichnung und mehreren Abfragehinweisen in der OPTION-Klausel  
 Beim folgenden Beispiel handelt es sich um eine [!INCLUDE[ssDW](../../includes/ssdw-md.md)]-SELECT-Anweisung, die eine Bezeichnung und mehrere Abfragehinweise enthält. Bei der Ausführung der Abfrage auf den Computeknoten wendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Hashjoin oder Merge Join an, je nachdem, welche Strategie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als optimal auswählt.  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION ( Label = 'CustJoin', HASH JOIN, MERGE JOIN);  
```  
  
### <a name="e-using-a-query-hint-when-querying-a-view"></a>E. Verwenden eines Abfragehinweises beim Abfragen einer Sicht  
 Im folgenden Beispiel wird eine Sicht mit dem Namen CustomerView erstellt und anschließend ein HASH JOIN-Abfragehinweis in einer Abfrage verwendet, die auf eine Sicht und eine Tabelle verweist.  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView  
AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT COUNT (*) FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
  
DROP VIEW CustomerView;  
  
```  
  
### <a name="f-query-with-a-subselect-and-a-query-hint"></a>F. Abfrage mit einer untergeordneten SELECT-Anweisung und einem Abfragehinweis  
 Im folgenden Beispiel wird eine Abfrage dargestellt, die sowohl eine untergeordnete SELECT-Anweisung als auch einen Abfragehinweis enthält. Der Abfragehinweis wird global angewendet. Abfragehinweise dürfen nicht an die untergeordnete SELECT-Anweisung angefügt werden.  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT * FROM (  
SELECT COUNT (*) AS a FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON ( a.CustomerKey = b.CustomerKey )) AS t  
OPTION (HASH JOIN);  
```  
  
### <a name="g-force-the-join-order-to-match-the-order-in-the-query"></a>G. Erzwingen der Übereinstimmung der Joinreihenfolge mit der Reihenfolge in der Abfrage  
 Im folgenden Beispiel wird der FORCE ORDER-Hinweis verwendet, um zu erzwingen, dass der Abfrageplan die von der Abfrage angegebene Joinreihenfolge verwendet. Dies verbessert die Leistung einiger Abfragen, jedoch nicht aller.  
  
```  
-- Uses AdventureWorks  
  
-- Obtain partition numbers, boundary values, boundary value types, and rows per boundary  
-- for the partitions in the ProspectiveBuyer table of the ssawPDW database.  
SELECT sp.partition_number, prv.value AS boundary_value, lower(sty.name) AS boundary_value_type, sp.rows   
FROM sys.tables st JOIN sys.indexes si ON st.object_id = si.object_id AND si.index_id <2  
JOIN sys.partitions sp ON sp.object_id = st.object_id AND sp.index_id = si.index_id  
JOIN sys.partition_schemes ps ON ps.data_space_id = si.data_space_id   
JOIN sys.partition_range_values prv ON prv.function_id = ps.function_id   
JOIN sys.partition_parameters pp ON pp.function_id = ps.function_id   
JOIN sys.types sty ON sty.user_type_id = pp.user_type_id AND prv.boundary_id = sp.partition_number   
WHERE st.object_id = (SELECT object_id FROM sys.objects WHERE name = 'FactResellerSales')   
ORDER BY sp.partition_number  
OPTION ( FORCE ORDER )  
;  
```  
  
### <a name="h-using-externalpushdown"></a>H. Verwenden von EXTERNALPUSHDOWN  
 Im folgenden Beispiel wird die Weitergabe der WHERE-Klausel an den MapReduce-Auftrag in der externen Hadoop-Tabelle erzwungen.  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 1000000  
OPTION (FORCE EXTERNALPUSHDOWN);  
```  
  
 Im folgenden Beispiel wird die Weitergabe der WHERE-Klausel an den MapReduce-Auftrag in der externen Hadoop-Tabelle verhindert. Wo die WHERE-Klausel angewendet wird, werden alle Zeilen an PDW zurückgegeben.  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 10  
OPTION (DISABLE EXTERNALPUSHDOWN);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
  
  

