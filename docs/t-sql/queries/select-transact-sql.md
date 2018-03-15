---
title: SELECT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/24/2017
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
- SELECT_TSQL
- SELECT
dev_langs:
- TSQL
helpviewer_keywords:
- retrieving rows
- SELECT statement [SQL Server]
- SELECT statement [SQL Server], about SELECT statement
- row retrieval [SQL Server], SELECT statement
- DML [SQL Server], SELECT statement
- data manipulation language [SQL Server], SELECT statement
- row retrieval [SQL Server]
- queries [SQL Server], results
ms.assetid: dc85caea-54d1-49af-b166-f3aa2f3a93d0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b8cca7419cce15dcbb83b4aa72dc551e5eb89eb1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ruft Zeilen aus der Datenbank ab und ermöglicht die Auswahl einer oder vieler Zeilen oder Spalten aus einer Tabelle oder aus zahlreichen Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die vollständige Syntax der SELECT-Anweisung ist komplex, die Hauptklauseln können jedoch wie folgt zusammengefasst werden:  
  
[ WITH { [ XMLNAMESPACES ,] [ \<common_table_expression> ] } ]
  
 SELECT *select_list* [ INTO *new_table* ]  
  
 [ FROM *table_source* ] [ WHERE *search_condition* ]  
  
 [ GROUP BY *group_by_expression* ]  
  
 [ HAVING *search_condition* ]  
  
 [ ORDER BY *order_expression* [ ASC | DESC ] ]  
  
 Die Operatoren UNION, EXCEPT und INTERSECT können zwischen Abfragen verwendet werden, um deren Ergebnisse in einem Resultset zu kombinieren oder zu vergleichen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<SELECT statement> ::=    
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]  
    <query_expression>   
    [ ORDER BY { order_by_expression | column_position [ ASC | DESC ] }   
  [ ,...n ] ]   
    [ <FOR Clause>]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]   
<query_expression> ::=   
    { <query_specification> | ( <query_expression> ) }   
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }  
        <query_specification> | ( <query_expression> ) [...n ] ]   
<query_specification> ::=   
SELECT [ ALL | DISTINCT ]   
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]   
    < select_list >   
    [ INTO new_table ]   
    [ FROM { <table_source> } [ ,...n ] ]   
    [ WHERE <search_condition> ]   
    [ <GROUP BY> ]   
    [ HAVING < search_condition > ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
SELECT <select_criteria>  
[;]  
  
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
  
```  
  
## <a name="remarks"></a>Remarks  
 Da die SELECT-Anweisung relativ komplex ist, werden ausführliche Syntaxelemente und Argumente nach Klauseln zusammengefasst aufgeführt:  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[HAVING](../../t-sql/queries/select-having-transact-sql.md)|  
|[SELECT Clause (SELECT-Klausel)](../../t-sql/queries/select-clause-transact-sql.md)|[UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[INTO-Klausel](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT und INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[FOR-Klausel](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md)|[OPTION Clause (OPTION-Klausel)](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 Die Reihenfolge der Klauseln in der SELECT-Anweisung ist wichtig. Jede der optionalen Klauseln kann ausgelassen werden. Wenn sie jedoch verwendet werden, müssen sie in der richtigen Reihenfolge stehen.  
  
 SELECT-Anweisungen sind in benutzerdefinierten Funktionen nur dann zulässig, wenn die Auswahllisten dieser Anweisungen Ausdrücke enthalten, die lokalen Variablen der Funktionen Werte zuweisen.  
  
 Ein mit der OPENDATASOURCE-Funktion als Servername konstruierter vierteiliger Name kann als Tabellenquelle überall dort verwendet werden, wo ein Tabellenname in einer SELECT-Anweisung vorkommen kann. Für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] kann kein vierteiliger Name angegeben werden.  
  
 Für SELECT-Anweisungen, die Remotetabellen einbeziehen, gelten einige Syntaxeinschränkungen.  
  
## <a name="logical-processing-order-of-the-select-statement"></a>Logische Verarbeitungsreihenfolge der SELECT-Anweisung  
 Die folgenden Schritte beschreiben die logische Verarbeitungs- oder Bindungsreihenfolge der SELECT-Anweisung. Diese Reihenfolge bestimmt, wann die in einem Schritt definierten Objekte in nachfolgenden Schritten für die Klauseln verfügbar gemacht werden. Wenn der Abfrageprozessor z. B. eine Bindung mit den in der FROM-Klausel definierten Tabellen oder Sichten herstellen (bzw. darauf zugreifen) kann, werden diese Objekte und die dazugehörigen Spalten für alle nachfolgenden Schritten verfügbar gemacht. Umgekehrt kann auf die in dieser Klausel definierten Spaltenaliase oder abgeleiteten Spalten nicht durch vorhergehende Klauseln verwiesen werden, da die SELECT-Klausel Schritt 8 ist. Allerdings kann durch nachfolgende Klauseln wie der ORDER BY-Klausel darauf verwiesen werden. Die tatsächliche physische Ausführung der Anweisung wird durch den Abfrageprozessor bestimmt, und die Reihenfolge kann von dieser Liste abweichen.  
  
1.  FROM  
2.  ON  
3.  JOIN  
4.  WHERE  
5.  GROUP BY  
6.  WITH CUBE oder WITH ROLLUP  
7.  HAVING  
8.  SELECT  
9. DISTINCT  
10. ORDER BY  
11. NACH OBEN  

> [!WARNING]
> Die oben dargestellte Reihenfolge ist in der Regel zutreffend. Es gibt jedoch Ausnahmefälle, in denen die Reihenfolge abweichen kann.
>
> Nehmen wir als Beispiel einen gruppierten Index für eine Sicht, die manche Tabellenzeilen ausschließt und deren SELECT-Spaltenliste CONVERT verwendet, wodurch ein Datentyp von *varchar* in *integer* geändert wird. In diesem Fall kann CONVERT ausgeführt werden, bevor die WHERE-Klausel ausgeführt wird. Dies ist wirklich ein Ausnahmefall. Es gibt meistens eine Möglichkeit, die Sicht zu ändern, um die veränderte Reihenfolge zu vermeiden, falls dies in Ihrem Fall relevant ist. 

## <a name="permissions"></a>Berechtigungen  
 Die Auswahl von Daten erfordert die Berechtigung **SELECT** für die Tabelle oder Sicht, die über einen höheren Bereich, beispielsweise über die Berechtigung **SELECT** für das Schema oder die Berechtigung **CONTROL** für die Tabelle, vererbt werden kann. Oder sie erfordert die Mitgliedschaft in der festen Datenbankrolle **db_datareader** oder **db_owner** oder der festen Serverrolle **sysadmin**. Das Erstellen einer neuen Tabelle mit **SELECTINTO** erfordert auch die Berechtigungen **CREATETABLE** und **ALTERSCHEMA** für das Schema, das die neue Tabelle besitzt.  
  
## <a name="examples"></a>Beispiele:   
In den folgenden Beispielen wird die [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank verwendet.
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. Verwenden von SELECT zum Abrufen von Zeilen und Spalten  
 In diesem Abschnitt werden drei Codebeispiele aufgeführt. Im ersten Codebeispiel werden alle Zeilen (es ist keine WHERE-Klausel angegeben) und alle Spalten (mit `*`) aus der `DimEmployee`-Tabelle zurückgegeben.  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 Im nächsten Beispiel wird Aliasing von Tabellen verwendet, um das gleiche Ergebnis zu erzielen.  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 In diesem Beispiel werden alle Zeilen (keine WHERE-Klausel angegeben) und eine Teilmenge der Spalten (`FirstName`, `LastName`, `StartDate`) aus der `DimEmployee`-Tabelle in der `AdventureWorksPDW2012`-Datenbank zurückgegeben. Die Überschrift der dritten Spalte wird in `FirstDay` umbenannt.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 In diesem Beispiel werden nur die Zeilen für `DimEmployee` zurückgegeben, die über ein `EndDate` verfügen, das nicht NULL ist und über einen `MaritalStatus` von „M“ (married = verheiratet) verfügen.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>B. Verwenden von SELECT mit Spaltenüberschriften und Berechnungen  
 Das folgende Beispiel gibt alle Zeilen aus der `DimEmployee`-Tabelle zurück und berechnet das Bruttogehalt für jeden Mitarbeiter basierend auf `BaseRate` und einer 40-Stunden-Woche.  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. Verwenden von DISTINCT mit SELECT  
 Im folgenden Beispiel wird `DISTINCT` zum Generieren einer Liste aller eindeutigen Titel in der `DimEmployee`-Tabelle verwendet.  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. Verwenden von GROUP BY  
 Im folgenden Beispiel wird die Gesamtsumme aller Verkäufe pro Tag gesucht.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 Aufgrund der `GROUP BY`-Klausel wird für jeden Tag nur eine Zeile zurückgegeben, die die Summe aller Verkäufe enthält.  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. Verwenden von GROUP BY mit mehreren Gruppen  
 Im folgenden Beispiel wird der Durchschnittspreis und die Summe aller Internetverkäufe pro Tag gesucht und nach Bestelldatum und Promotion Key gruppiert.  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. Verwenden von GROUP BY und WHERE  
 In diesem Beispiel werden die Ergebnisse in Gruppen zusammengefasst, nachdem nur die Zeilen mit Bestelldaten nach dem 1. August 2002 abgerufen wurden.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
WHERE OrderDateKey > '20020801'  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="g-using-group-by-with-an-expression"></a>G. Verwenden von GROUP BY mit einem Ausdruck  
 Im folgenden Beispiel wird nach einem Ausdruck gruppiert. Sie können nach einem Ausdruck gruppieren, wenn dieser keine Aggregatfunktionen enthält.  
  
```sql  
SELECT SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY (OrderDateKey * 10);  
```  
  
### <a name="h-using-group-by-with-order-by"></a>H. Verwenden von GROUP BY mit ORDER BY  
 Im folgenden Beispiel wird die Summe der Verkäufe und Bestellungen pro Tag gesucht.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>I. Verwenden der HAVING-Klausel  
 Diese Abfrage verwendet die `HAVING`-Klausel, um Ergebnisse zu beschränken.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SELECT-Beispiele &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)
  

