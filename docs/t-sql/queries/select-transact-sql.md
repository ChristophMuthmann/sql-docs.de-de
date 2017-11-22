---
title: "Wählen Sie (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 10/24/2017
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
- SELECT_TSQL
- SELECT
dev_langs: TSQL
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
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 012853c97e01250bf5aee62d95ae7971549f5094
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ruft Zeilen aus der Datenbank ab und ermöglicht die Auswahl einer oder vieler Zeilen oder Spalten aus einem oder mehreren Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die vollständige Syntax der SELECT-Anweisung ist komplex, die Hauptklauseln können jedoch wie folgt zusammengefasst werden:  
  
[Mit {[XMLNAMESPACES,] [ \<Common_table_expression >]}]
  
 Wählen Sie *Select_list* [INTO *New_table* ]  
  
 [Aus *Table_source* ] [, in denen *Search_condition* ]  
  
 [GROUP BY *Group_by_expression* ]  
  
 [Müssen *Search_condition* ]  
  
 [ORDER BY *Order_expression* [ASC | "DESC"]]  
  
 Die UNION, EXCEPT und INTERSECT-Operatoren können zwischen Abfragen zu kombinieren oder vergleichen Sie ihre Ergebnisse in einem Resultset verwendet werden.  
  
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
  
## <a name="remarks"></a>Hinweise  
 Da die SELECT-Anweisung relativ komplex ist, werden ausführliche Syntaxelemente und Argumente nach Klauseln zusammengefasst aufgeführt:  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[HAVING](../../t-sql/queries/select-having-transact-sql.md)|  
|[SELECT Clause (SELECT-Klausel)](../../t-sql/queries/select-clause-transact-sql.md)|[UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[INTO-Klausel](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT und INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[FOR-Klausel](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[GRUPPIEREN NACH](../../t-sql/queries/select-group-by-transact-sql.md)|[OPTION Clause (OPTION-Klausel)](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 Die Reihenfolge der Klauseln in der SELECT-Anweisung ist wichtig. Jede der optionalen Klauseln kann ausgelassen werden. Wenn sie jedoch verwendet werden, müssen sie in der richtigen Reihenfolge stehen.  
  
 SELECT-Anweisungen sind in benutzerdefinierten Funktionen nur dann zulässig, wenn die Auswahllisten dieser Anweisungen Ausdrücke enthalten, die lokalen Variablen der Funktionen Werte zuweisen.  
  
 Ein mit der OPENDATASOURCE-Funktion als Servername konstruierter vierteiliger Name kann als Tabellenquelle überall dort verwendet werden, wo ein Tabellenname in einer SELECT-Anweisung vorkommen kann. Ein vierteiliger Name kann nicht angegeben werden, für die [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Für SELECT-Anweisungen, die Remotetabellen einbeziehen, gelten einige Syntaxeinschränkungen.  
  
## <a name="logical-processing-order-of-the-select-statement"></a>Logische Verarbeitungsreihenfolge der SELECT-Anweisung  
 Die folgenden Schritte beschreiben die logische Verarbeitungs- oder Bindungsreihenfolge der SELECT-Anweisung. Diese Reihenfolge bestimmt, wann die in einem Schritt definierten Objekte in nachfolgenden Schritten für die Klauseln verfügbar gemacht werden. Wenn der Abfrageprozessor z. B. eine Bindung mit den in der FROM-Klausel definierten Tabellen oder Sichten herstellen (bzw. darauf zugreifen) kann, werden diese Objekte und die dazugehörigen Spalten für alle nachfolgenden Schritten verfügbar gemacht. Umgekehrt kann auf die in dieser Klausel definierten Spaltenaliase oder abgeleiteten Spalten nicht durch vorhergehende Klauseln verwiesen werden, da die SELECT-Klausel Schritt 8 ist. Allerdings kann durch nachfolgende Klauseln wie der ORDER BY-Klausel darauf verwiesen werden. Die tatsächliche physische Ausführung der Anweisung wird durch den Abfrageprozessor bestimmt, und die Reihenfolge dieser Liste abweichen.  
  
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
> Die oben dargestellten Reihenfolge ist in der Regel "true". Es gibt jedoch ungewöhnliche Fälle, in die Reihenfolge abweichen.
>
> Nehmen wir beispielsweise an einen gruppierten Index für eine Sicht, stehen Ihnen die Ansicht schließt einige Tabellenzeilen und SELECT-Spaltenliste der Ansicht verwendet eine Konvertierung, die einen Datentyp aus ändert *Varchar* auf *Ganzzahl*. In diesem Fall kann die CONVERT führen Sie vor die WHERE-Klausel ausgeführt wird. Tatsächlich ungewöhnlich. Es ist häufig eine Möglichkeit, die Ansicht, um die verschiedenen Sequenz zu vermeiden zu ändern, wenn diese in Ihrem Fall so wichtig ist. 

## <a name="permissions"></a>Berechtigungen  
 Die Auswahl von Daten erfordert die Berechtigung **SELECT** für die Tabelle oder Sicht, die über einen höheren Bereich, beispielsweise über die Berechtigung **SELECT** für das Schema oder die Berechtigung **CONTROL** für die Tabelle, vererbt werden kann. Oder die Mitgliedschaft in der **"db_datareader"** oder **Db_owner** festen Datenbankrollen oder der **Sysadmin** festen Serverrolle "". Erstellen einer neuen Tabelle mit **SELECTINTO** erfordert auch die **CREATETABLE** Berechtigung und die **ALTERSCHEMA** -Berechtigung für das Schema, das die neue Tabelle besitzt.  
  
## <a name="examples"></a>Beispiele:   
In den folgenden Beispielen wird die [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank verwendet.
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. Verwenden von SELECT zum Abrufen von Zeilen und Spalten  
 In diesem Abschnitt werden drei Codebeispiele aufgeführt. Diesem erste Codebeispiel gibt alle Zeilen (keine WHERE-Klausel angegeben ist), und alle Spalten (mit der `*`) aus der `DimEmployee` Tabelle.  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 Im folgenden Beispiel Tabelle Aliasing verwenden, um dasselbe Ergebnis zu erzielen.  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 In diesem Beispiel gibt alle Zeilen (keine WHERE-Klausel angegeben ist) und eine Teilmenge der Spalten (`FirstName`, `LastName`, `StartDate`) aus der `DimEmployee` -Tabelle in der `AdventureWorksPDW2012` Datenbank. Die Überschrift der dritten Spalte wird in umbenannt `FirstDay`.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 In diesem Beispiel gibt nur die Zeilen für `DimEmployee` , auf denen ein `EndDate` , die nicht NULL ist und ein `MaritalStatus` von bin "(Verheiratet).  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>B. Verwenden von SELECT mit Spaltenüberschriften und Berechnungen  
 Das folgende Beispiel gibt alle Zeilen aus der `DimEmployee` Tabelle, und berechnet den Bruttogewinn bezahlen für jeden Mitarbeiter basierend auf ihren `BaseRate` und 40 Stunden pro Woche.  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. Verwenden von DISTINCT mit SELECT  
 Im folgenden Beispiel wird `DISTINCT` zum Generieren einer Liste aller eindeutigen Titel in der `DimEmployee` Tabelle.  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. Verwenden von GROUP BY  
 Das folgende Beispiel sucht die Gesamtmenge für alle Verkäufe pro Tag.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 Aufgrund der der `GROUP BY` -Klausel wird nur eine Zeile, die die Summe aller Kaufaufträge enthält für jeden Tag zurückgegeben.  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. Verwenden von GROUP BY mit mehreren Gruppen  
 Im folgende Beispiel ermittelt den Durchschnittspreis und die Summe der Internetverkäufe für jeden Tag gruppiert nach Bestelldatum und den Schlüssel für die heraufstufung.  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. Verwenden von GROUP BY und WHERE  
 Das folgende Beispiel fügt die Ergebnisse in Gruppen nach Abrufen der nur die Zeilen mit einem späteren Zeitpunkt vor dem 1. August 2002 Bestelldaten.  
  
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
 Das folgende Beispiel sucht die Summe der Verkäufe pro Tag und Aufträge nach dem Tag.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>I. Verwenden der HAVING-Klausel  
 Diese Abfrage verwendet die `HAVING` -Klausel, um Ergebnisse zu beschränken.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Wählen Sie die Beispiele &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [Tabellenhinweise &#40; Transact-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)
  

