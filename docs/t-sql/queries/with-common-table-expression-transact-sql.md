---
title: WITH allgemeiner_tabellenausdruck (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
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
- WITH common_table_expression
- WITH_TSQL
- WITH
- common table expression
dev_langs:
- TSQL
helpviewer_keywords:
- WITH common_table_expression clause
- CTEs
- hierarchical queries [SQL Server], WITH common_table_expression
- recursive CTEs [SQL Server]
- recursive queries [SQL Server]
- common table expressions
- MAXRECURSION hint
- clauses [SQL Server], WITH common_table_expression
ms.assetid: 27cfb819-3e8d-4274-8bbe-cbbe4d9c2e23
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8c77e9c97fd3d31b63e6e3938cbdab134554dd1c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="with-commontableexpression-transact-sql"></a>WITH common_table_expression (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt ein temporäres benanntes Resultset an, das als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bekannt ist. Dieser wird von einer einfachen Abfrage abgeleitet und innerhalb des Ausführungsbereichs einer einzelnen SELECT-, INSERT-, UPDATE- oder DELETE-Anweisung definiert. Diese Klausel kann auch in einer CREATE VIEW-Anweisung als Teil der definierenden SELECT-Anweisung verwendet werden. Ein allgemeiner Tabellenausdruck kann auch Verweise auf sich selbst enthalten. In diesem Fall handelt es sich um einen rekursiven allgemeinen Tabellenausdruck.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
[ WITH <common_table_expression> [ ,...n ] ]  
  
<common_table_expression>::=  
    expression_name [ ( column_name [ ,...n ] ) ]  
    AS  
    ( CTE_query_definition )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression_name*  
Ist ein gültiger Bezeichner für den allgemeinen Tabellenausdruck. *Expression_name* muss sich vom Namen des alle anderen allgemeinen Tabellenausdrucks in der gleichen WITH definiert \<Common_table_expression >-Klausel, aber *Expression_name* können den Namen der identisch sein ein Basistabelle oder Sicht. Jeder Verweis auf *Expression_name* in der Abfrage verwendet werden soll, der allgemeine Tabellenausdruck und nicht das Basisobjekt.
  
 *column_name*  
 Gibt einen Spaltennamen im allgemeinen Tabellenausdruck an. Innerhalb der Definition eines allgemeinen Tabellenausdrucks sind doppelte Namen nicht zulässig. Die Anzahl der angegebenen Spaltennamen muss die Anzahl der Spalten im Resultset entsprechen den *CTE*. Die Liste der Spaltennamen ist nur optional, wenn in der Abfragedefinition für alle Spalten verschiedene Namen angegeben werden.  
  
 *CTE_query_definition*  
 Gibt eine SELECT-Anweisung an, mit deren Resultset der allgemeine Tabellenausdruck aufgefüllt wird. Die SELECT-Anweisung für *CTE* erfüllt die gleichen Anforderungen an, wie für das Erstellen einer Ansicht mit der Ausnahme ein allgemeiner Tabellenausdruck einen weiteren allgemeinen Tabellenausdruck definieren kann. Weitere Informationen finden Sie im Abschnitt "Hinweise" und [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 Wenn mehr als ein *CTE* wird definiert, die Abfragedefinitionen müssen verknüpft werden, durch einen der folgenden Mengenoperatoren: UNION ALL, UNION, EXCEPT oder INTERSECT.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="guidelines-for-creating-and-using-common-table-expressions"></a>Richtlinien zum Erstellen und Verwenden allgemeiner Tabellenausdrücke  
 Die folgenden Richtlinien gelten für nicht rekursive allgemeine Tabellenausdrücke. Informationen zu Richtlinien für rekursive allgemeine Tabellenausdrücke finden Sie unter "Richtlinien zum Definieren und Verwenden rekursiver allgemeiner Tabellenausdrücke" weiter unten.  
  
-   Auf einen allgemeinen Tabellenausdruck muss eine einzelne SELECT-, INSERT-, UPDATE- oder DELETE-Anweisung folgen, die auf eine oder alle Spalten mit einem allgemeinen Tabellenausdruck verweist. Ein allgemeiner Tabellenausdruck kann auch in einer CREATE VIEW-Anweisung als Teil der definierenden SELECT-Anweisung der Sicht verwendet werden.  
  
-   In einem nicht rekursiven allgemeinen Tabellenausdruck können mehrere Abfragedefinitionen für allgemeine Tabellenausdrücke definiert werden. Die Definitionen müssen durch einen der folgenden Mengenoperatoren verbunden werden: UNION ALL, UNION, INTERSECT oder EXCEPT.  
  
-   Ein allgemeiner Tabellenausdruck kann in einer WITH-Klausel auf sich selbst und auf vorher definierte allgemeine Tabellenausdrücke verweisen. Ein Vorwärtsverweis ist nicht zulässig.  
  
-   Die Angabe mehrerer WITH-Klauseln in einem allgemeinen Tabellenausdruck ist nicht zulässig. Z. B. wenn ein *CTE* eine Unterabfrage enthält, diese Unterabfrage darf keine WITH-Klausel, die einen weiteren allgemeinen Tabellenausdruck definiert einen geschachtelten enthalten.  
  
-   Die folgenden Klauseln können nicht verwendet werden, der *CTE*:  
  
    -   ORDER BY (Ausnahme: wenn eine TOP-Klausel angegeben ist)  
  
    -   INTO  
  
    -   OPTION-Klausel mit Abfragehinweisen  
  
    -   FOR BROWSE  
  
-   Wird ein allgemeiner Tabellenausdruck in einer Anweisung verwendet, die zu einem Batch gehört, muss auf die vorangehende Anweisung ein Semikolon folgen.  
  
-   Eine Abfrage, die auf einen allgemeinen Tabellenausdruck verweist, kann zur Definition eines Cursors verwendet werden.  
  
-   In einem allgemeinen Tabellenausdruck kann auf Tabellen auf Remoteservern verwiesen werden.  
  
-   Wenn ein allgemeiner Tabellenausdruck ausgeführt wird, können Hinweise, die auf einen allgemeinen Tabellenausdruck verweisen, Konflikte mit anderen Hinweisen verursachen, die auftreten, wenn der allgemeine Tabellenausdruck auf die zugrunde liegenden Tabellen zugreift. Dies gilt auch für Hinweise, die auf Sichten in Abfragen verweisen. Wenn das passiert, gibt die Abfrage einen Fehler zurück.  
  
## <a name="guidelines-for-defining-and-using-recursive-common-table-expressions"></a>Richtlinien zum Definieren und Verwenden rekursiver allgemeiner Tabellenausdrücke  
 Die folgenden Richtlinien gelten für die Definition rekursiver allgemeiner Tabellenausdrücke:  
  
-   Die Definition des rekursiven allgemeinen Tabellenausdrucks muss mindestens zwei Abfragedefinitionen für allgemeine Tabellenausdrücke enthalten, und zwar ein Ankerelement und ein rekursives Element. Mehrere Ankerelemente und rekursive Elemente können definiert werden. Jedoch müssen alle Ankerelement-Abfragedefinitionen vor die erste Definition eines rekursiven Elements gesetzt werden. Alle Abfragedefinitionen für allgemeine Tabellenausdrücke sind Ankerelemente, es sei denn, sie verweisen auf den allgemeinen Tabellenausdruck selbst.  
  
-   Ankerelemente müssen durch einen der folgenden Mengenoperatoren verbunden werden: UNION ALL, UNION, INTERSECT oder EXCEPT. UNION ALL ist der einzige Mengenoperator, der zwischen dem letzten Ankerelement und dem ersten rekursiven Element sowie bei der Verbindung mehrerer rekursiver Elemente zulässig ist.  
  
-   Ankerelemente und rekursive Elemente müssen die gleiche Spaltenanzahl aufweisen.  
  
-   Der Datentyp einer Spalte im rekursiven Element und der Datentyp der entsprechenden Spalte im Ankerelement müssen übereinstimmen.  
  
-   Die FROM-Klausel eines rekursiven Elements muss nur einmal auf den allgemeinen Tabellenausdruck verweisen *Expression_name*.  
  
-   Die folgenden Elemente sind nicht zulässig, der *CTE* eines rekursiven Elements:  
  
    -   SELECT DISTINCT  
  
    -   GROUP BY  
  
    -   PIVOT (Wenn der Datenbank-Kompatibilitätsgrad 110 oder höher ist. Finden Sie unter [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQLServer 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).)  
  
    -   HAVING  
  
    -   Skalare Aggregation  
  
    -   NACH OBEN  
  
    -   LEFT, RIGHT, OUTER JOIN (INNER JOIN ist zulässig)  
  
    -   Unterabfragen  
  
    -   Ein Hinweis auf einen rekursiven Verweis für einen allgemeinen Tabellenausdruck innerhalb angewendet eine *CTE*.  
  
 Die folgenden Richtlinien gelten für die Verwendung rekursiver allgemeiner Tabellenausdrücke:  
  
-   Alle Spalten, die vom rekursiven allgemeinen Tabellenausdruck zurückgegeben werden, lassen NULL zu, unabhängig davon, ob die Spalten, die von den beteiligten SELECT-Anweisungen zurückgegeben werden, NULL zulassen.  
  
-   Ist ein rekursiver allgemeiner Tabellenausdruck falsch zusammengesetzt, kann dies zu einer Endlosschleife führen. Wenn beispielsweise die Abfragedefinition des rekursiven Elements für übergeordnete und untergeordnete Spalten die gleichen Werte zurückgibt, entsteht eine Endlosschleife. Um eine Endlosschleife zu verhindern, können Sie die Anzahl der für eine bestimmte Anweisung zulässigen Rekursionsebenen einschränken. Dazu verwenden Sie den MAXRECURSION-Hinweis und einen Wert zwischen 0 und 32.767 in der OPTION-Klausel der INSERT-, UPDATE-, DELETE- oder SELECT-Anweisung. Somit können Sie die Ausführung der Anweisung steuern, bis das Codeproblem behoben wurde, das die Schleife verursacht. Der serverweite Standardwert ist 100. Wenn 0 angegeben wird, wird keine Beschränkung angewendet. Pro Anweisung kann nur ein Wert für MAXRECURSION angegeben werden. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
-   Eine Sicht, die einen rekursiven allgemeinen Tabellenausdruck enthält, kann nicht zum Aktualisieren von Daten verwendet werden.  
  
-   Cursor können für Abfragen definiert werden, die allgemeine Tabellenausdrücke verwenden. Der allgemeine Tabellenausdruck ist die *Select_statement* Argument, das das Resultset des Cursors definiert. Für rekursive allgemeine Tabellenausdrücke sind nur schnelle Vorwärtscursor und statische (Momentaufnahme-)Cursor zulässig. Wird in einem rekursiven allgemeinen Tabellenausdruck ein anderer Cursortyp angegeben, wird der Cursortyp in einen statischen Typ konvertiert.  
  
-   Im allgemeinen Tabellenausdruck kann auf Tabellen auf Remoteservern verwiesen werden. Wenn im rekursiven Element des allgemeinen Tabellenausdrucks auf den Remoteserver verwiesen wird, wird für jede Remotetabelle ein Spoolvorgang erstellt, sodass auf die Tabellen wiederholt lokal zugegriffen werden kann. Wenn es sich um eine Abfrage für einen allgemeinen Tabellenausdruck handelt, wird im Abfrageplan Index Spool/Lazy Spool mit dem zusätzlichen WITH STACK-Prädikat angezeigt. Dies ist eine Möglichkeit, um eine ordnungsgemäße Rekursion zu gewährleisten.  
  
-   Analyse- und Aggregatfunktionen im rekursiven Teil des allgemeinen Tabellenausdrucks werden auf die Menge für die aktuelle Rekursionsebene und nicht auf die Menge für den allgemeinen Tabellenausdruck angewendet. Funktionen wie ROW_NUMBER werden nur für die von der aktuellen Rekursionsebene übergebene Teilmenge von Daten und nicht für die an den rekursiven Teil des allgemeinen Tabellenausdrucks übergebene gesamte Datenmenge ausgeführt. Weitere Informationen finden Sie unter Beispiel K. Verwenden von Analysefunktionen in einem rekursiven allgemeinen Tabellenausdrucks, das folgt.  
  
## <a name="features-and-limitations-of-common-table-expressions-in-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Funktionen und Einschränkungen von gemeinsamen Tabelle Ausdrücke in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Die aktuelle Implementierung von CTEs in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] haben die folgenden Features und Einschränkungen:  
  
-   Ein allgemeiner Tabellenausdruck kann angegeben werden, einem **wählen** Anweisung.  
  
-   Ein allgemeiner Tabellenausdruck kann angegeben werden, einem **CREATE VIEW** Anweisung.  
  
-   Ein allgemeiner Tabellenausdruck kann angegeben werden, einem **CREATE TABLE AS SELECT** (CTAS)-Anweisung.  
  
-   Ein allgemeiner Tabellenausdruck kann angegeben werden, einem **CREATE REMOTE TABLE AS SELECT** (CRTAS)-Anweisung.  
  
-   Ein allgemeiner Tabellenausdruck kann angegeben werden, einem **CREATE EXTERNAL TABLE AS SELECT** (CETAS)-Anweisung.  
  
-   Eine Remotetabelle kann über einen allgemeinen Tabellenausdruck verwiesen werden.  
  
-   Eine externe Tabelle kann aus einem allgemeinen Tabellenausdruck verwiesen werden.  
  
-   In einem allgemeinen Tabellenausdruck können mehrere Abfragedefinitionen definiert werden.  
  
-   Ein allgemeiner Tabellenausdruck muss eine einzelne folgen **wählen** Anweisung. **Fügen Sie**, **UPDATE**, **löschen**, und **MERGE** Anweisungen werden nicht unterstützt.  
  
-   Ein allgemeiner Tabellenausdruck, der Verweise auf sich selbst (eines rekursiven allgemeinen Tabellenausdrucks) enthält, wird nicht unterstützt.  
  
-   Mehrere angegeben **WITH** -Klausel in einem allgemeinen Tabellenausdruck ist nicht zulässig. Z. B. wenn ein CTE eine Unterabfrage enthält, diese Unterabfrage darf nicht enthalten eine geschachtelte **WITH** -Klausel, die einen weiteren allgemeinen Tabellenausdruck definiert.  
  
-   Ein **ORDER BY** -Klausel kann nicht verwendet werden, in dem CTE, außer wenn eine **oben** -Klausel angegeben ist.  
  
-   Wird ein allgemeiner Tabellenausdruck in einer Anweisung verwendet, die zu einem Batch gehört, muss auf die vorangehende Anweisung ein Semikolon folgen.  
  
-   Bei der Verwendung in von vorbereiteten Anweisungen **Sp_prepare**, allgemeine Tabellenausdrücke verhält sich genauso wie andere **wählen** Anweisungen in PDW. Jedoch wenn CTEs, im Rahmen des CETAS vorbereitet verwendet werden, indem **Sp_prepare**, kann das Verhalten von verzögern [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und andere Anweisungen PDW aufgrund der Weise Binden für implementiert **Sp_prepare**. Wenn **wählen** , dass Verweise CTE eine falsche Spalte verwendet wird, die in allgemeinen Tabellenausdruck, nicht vorhanden ist die **Sp_prepare** ohne erkennen des Fehlers, doch der Fehler während der ausgelöst wird, übergibt **Sp_execute**  stattdessen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-simple-common-table-expression"></a>A. Erstellen eines einfachen allgemeinen Tabellenausdrucks  
 Im folgenden Beispiel wird die Gesamtanzahl der Aufträge pro Jahr für jeden Vertriebsmitarbeiter von [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] angezeigt.  
  
```  
  
-- Define the CTE expression name and column list.  
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
AS  
-- Define the CTE query.  
(  
    SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
)  
-- Define the outer query referencing the CTE name.  
SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
FROM Sales_CTE  
GROUP BY SalesYear, SalesPersonID  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
### <a name="b-using-a-common-table-expression-to-limit-counts-and-report-averages"></a>B. Verwenden eines allgemeinen Tabellenausdrucks zum Einschränken von Anzahlen und Wiedergeben von Durchschnittswerten  
 Im folgenden Beispiel wird die durchschnittliche Anzahl der Verkaufsaufträge der Vertriebsmitarbeiter für alle Jahre veranschaulicht.  
  
```  
WITH Sales_CTE (SalesPersonID, NumberOfOrders)  
AS  
(  
    SELECT SalesPersonID, COUNT(*)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
    GROUP BY SalesPersonID  
)  
SELECT AVG(NumberOfOrders) AS "Average Sales Per Person"  
FROM Sales_CTE;  
GO  
```  
  
### <a name="c-using-multiple-cte-definitions-in-a-single-query"></a>C. Verwenden mehrerer Definitionen für allgemeine Tabellenausdrücke in einer einzelnen Abfrage  
 Im folgenden Beispiel wird veranschaulicht, wie mehrere allgemeine Tabellenausdrücke in einer einzelnen Abfrage definiert werden. Die Abfragedefinitionen für allgemeine Tabellenausdrücke werden durch ein Komma voneinander getrennt. Die FORMAT-Funktion, die verwendet wird, um die Geldbeträge in einem Währungsformat anzuzeigen, ist in SQL Server 2012 und höher verfügbar.  
  
```  
  
WITH Sales_CTE (SalesPersonID, TotalSales, SalesYear)  
AS  
-- Define the first CTE query.  
(  
    SELECT SalesPersonID, SUM(TotalDue) AS TotalSales, YEAR(OrderDate) AS SalesYear  
    FROM Sales.SalesOrderHeader  
    WHERE SalesPersonID IS NOT NULL  
       GROUP BY SalesPersonID, YEAR(OrderDate)  
  
)  
,   -- Use a comma to separate multiple CTE definitions.  
  
-- Define the second CTE query, which returns sales quota data by year for each sales person.  
Sales_Quota_CTE (BusinessEntityID, SalesQuota, SalesQuotaYear)  
AS  
(  
       SELECT BusinessEntityID, SUM(SalesQuota)AS SalesQuota, YEAR(QuotaDate) AS SalesQuotaYear  
       FROM Sales.SalesPersonQuotaHistory  
       GROUP BY BusinessEntityID, YEAR(QuotaDate)  
)  
  
-- Define the outer query by referencing columns from both CTEs.  
SELECT SalesPersonID  
  , SalesYear  
  , FORMAT(TotalSales,'C','en-us') AS TotalSales  
  , SalesQuotaYear  
  , FORMAT (SalesQuota,'C','en-us') AS SalesQuota  
  , FORMAT (TotalSales -SalesQuota, 'C','en-us') AS Amt_Above_or_Below_Quota  
FROM Sales_CTE  
JOIN Sales_Quota_CTE ON Sales_Quota_CTE.BusinessEntityID = Sales_CTE.SalesPersonID  
                    AND Sales_CTE.SalesYear = Sales_Quota_CTE.SalesQuotaYear  
ORDER BY SalesPersonID, SalesYear;  
GO  
  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
```  
  
SalesPersonID SalesYear   TotalSales    SalesQuotaYear SalesQuota  Amt_Above_or_Below_Quota  
------------- ---------   -----------   -------------- ---------- ----------------------------------   
  
274           2005        $32,567.92    2005           $35,000.00  ($2,432.08)  
274           2006        $406,620.07   2006           $455,000.00 ($48,379.93)  
274           2007        $515,622.91   2007           $544,000.00 ($28,377.09)  
274           2008        $281,123.55   2008           $271,000.00  $10,123.55  
  
```  
  
### <a name="d-using-a-recursive-common-table-expression-to-display-multiple-levels-of-recursion"></a>D. Verwenden eines rekursiven allgemeinen Tabellenausdrucks, um mehrere Rekursionsebenen anzuzeigen  
 Im folgenden Beispiel werden Vorgesetzte in einer Hierarchieliste sowie die Mitarbeiter angezeigt, die diesen unterstellt sind. In diesem Beispiel wird zunächst die `dbo.MyEmployees`-Tabelle erstellt und aufgefüllt.  
  
```  
-- Create an Employee table.  
CREATE TABLE dbo.MyEmployees  
(  
EmployeeID smallint NOT NULL,  
FirstName nvarchar(30)  NOT NULL,  
LastName  nvarchar(40) NOT NULL,  
Title nvarchar(50) NOT NULL,  
DeptID smallint NOT NULL,  
ManagerID int NULL,  
 CONSTRAINT PK_EmployeeID PRIMARY KEY CLUSTERED (EmployeeID ASC)   
);  
-- Populate the table with values.  
INSERT INTO dbo.MyEmployees VALUES   
 (1, N'Ken', N'Sánchez', N'Chief Executive Officer',16,NULL)  
,(273, N'Brian', N'Welcker', N'Vice President of Sales',3,1)  
,(274, N'Stephen', N'Jiang', N'North American Sales Manager',3,273)  
,(275, N'Michael', N'Blythe', N'Sales Representative',3,274)  
,(276, N'Linda', N'Mitchell', N'Sales Representative',3,274)  
,(285, N'Syed', N'Abbas', N'Pacific Sales Manager',3,273)  
,(286, N'Lynn', N'Tsoflias', N'Sales Representative',3,285)  
,(16,  N'David',N'Bradley', N'Marketing Manager', 4, 273)  
,(23,  N'Mary', N'Gibson', N'Marketing Specialist', 4, 16);  
```  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
ORDER BY ManagerID;  
GO  
```  
  
### <a name="e-using-a-recursive-common-table-expression-to-display-two-levels-of-recursion"></a>E. Verwenden eines rekursiven allgemeinen Tabellenausdrucks, um zwei Rekursionsebenen anzuzeigen  
 Im folgenden Beispiel werden Vorgesetzte sowie die Mitarbeiter angezeigt, die diesen unterstellt sind. Die Anzahl der zurückgegebenen Ebenen wird auf zwei Ebenen eingeschränkt.  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(ManagerID, EmployeeID, Title, EmployeeLevel) AS   
(  
    SELECT ManagerID, EmployeeID, Title, 0 AS EmployeeLevel  
    FROM dbo.MyEmployees   
    WHERE ManagerID IS NULL  
    UNION ALL  
    SELECT e.ManagerID, e.EmployeeID, e.Title, EmployeeLevel + 1  
    FROM dbo.MyEmployees AS e  
        INNER JOIN DirectReports AS d  
        ON e.ManagerID = d.EmployeeID   
)  
SELECT ManagerID, EmployeeID, Title, EmployeeLevel   
FROM DirectReports  
WHERE EmployeeLevel <= 2 ;  
GO  
  
```  
  
### <a name="f-using-a-recursive-common-table-expression-to-display-a-hierarchical-list"></a>F. Verwenden eines rekursiven allgemeinen Tabellenausdrucks, um eine Hierarchieliste anzuzeigen  
 Das folgende Beispiel baut auf Beispiel D auf, indem die Namen der Vorgesetzten und Mitarbeiter und deren Titel hinzugefügt werden. Die Hierarchieebenen von Vorgesetzten und Mitarbeitern werden zusätzlich hervorgehoben, indem die einzelnen Ebenen jeweils eingerückt werden.  
  
```  
USE AdventureWorks2012;  
GO  
WITH DirectReports(Name, Title, EmployeeID, EmployeeLevel, Sort)  
AS (SELECT CONVERT(varchar(255), e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        1,  
        CONVERT(varchar(255), e.FirstName + ' ' + e.LastName)  
    FROM dbo.MyEmployees AS e  
    WHERE e.ManagerID IS NULL  
    UNION ALL  
    SELECT CONVERT(varchar(255), REPLICATE ('|    ' , EmployeeLevel) +  
        e.FirstName + ' ' + e.LastName),  
        e.Title,  
        e.EmployeeID,  
        EmployeeLevel + 1,  
        CONVERT (varchar(255), RTRIM(Sort) + '|    ' + FirstName + ' ' +   
                 LastName)  
    FROM dbo.MyEmployees AS e  
    JOIN DirectReports AS d ON e.ManagerID = d.EmployeeID  
    )  
SELECT EmployeeID, Name, Title, EmployeeLevel  
FROM DirectReports   
ORDER BY Sort;  
GO  
```  
  
### <a name="g-using-maxrecursion-to-cancel-a-statement"></a>G. Verwenden von MAXRECURSION zum Abbrechen einer Anweisung  
 Mit `MAXRECURSION` kann verhindert werden, dass ein rekursiver allgemeiner Tabellenausdruck, der fehlerhaft formuliert ist, in eine Endlosschleife gerät. Im folgenden Beispiel wird absichtlich eine Endlosschleife erstellt. Außerdem wird `MAXRECURSION` verwendet, um die Anzahl der Rekursionsebenen auf zwei zu beschränken.  
  
```  
USE AdventureWorks2012;  
GO  
--Creates an infinite loop  
WITH cte (EmployeeID, ManagerID, Title) as  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT cte.EmployeeID, cte.ManagerID, cte.Title  
    FROM cte   
    JOIN  dbo.MyEmployees AS e   
        ON cte.ManagerID = e.EmployeeID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT EmployeeID, ManagerID, Title  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 Sobald der Fehler im Code behoben wurde, wird MAXRECURSION nicht mehr benötigt. Das folgende Beispiel zeigt den korrigierten Code.  
  
```  
USE AdventureWorks2012;  
GO  
WITH cte (EmployeeID, ManagerID, Title)  
AS  
(  
    SELECT EmployeeID, ManagerID, Title  
    FROM dbo.MyEmployees  
    WHERE ManagerID IS NOT NULL  
  UNION ALL  
    SELECT  e.EmployeeID, e.ManagerID, e.Title  
    FROM dbo.MyEmployees AS e  
    JOIN cte ON e.ManagerID = cte.EmployeeID  
)  
SELECT EmployeeID, ManagerID, Title  
FROM cte;  
GO  
```  
  
### <a name="h-using-a-common-table-expression-to-selectively-step-through-a-recursive-relationship-in-a-select-statement"></a>H. Verwenden eines allgemeinen Tabellenausdrucks, um eine rekursive Beziehung in einer SELECT-Anweisung selektiv zu durchlaufen  
 Im folgenden Beispiel wird die Hierarchie von Produktgruppen und Komponenten gezeigt, die erforderlich sind, um das Fahrrad für `ProductAssemblyID = 800` zu montieren.  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
SELECT AssemblyID, ComponentID, Name, PerAssemblyQty, EndDate,  
        ComponentLevel   
FROM Parts AS p  
    INNER JOIN Production.Product AS pr  
    ON p.ComponentID = pr.ProductID  
ORDER BY ComponentLevel, AssemblyID, ComponentID;  
GO  
```  
  
### <a name="i-using-a-recursive-cte-in-an-update-statement"></a>I. Verwenden eines rekursiven allgemeinen Tabellenausdrucks in einer UPDATE-Anweisung  
 Das folgende Beispiel aktualisiert die `PerAssemblyQty` Wert für alle Teile, die verwendet werden, um das Produkt "Road-550-W Yellow, 44" erstellen `(ProductAssemblyID``800`). Der allgemeine Tabellenausdruck gibt eine hierarchische Liste mit Teilen zurück, die zum Erstellen der `ProductAssemblyID 800` verwendet werden, sowie mit Komponenten, die zum Erstellen dieser Teile verwendet werden, usw. Nur die Zeilen, die vom allgemeinen Tabellenausdruck zurückgegeben werden, werden geändert.  
  
```  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
### <a name="j-using-multiple-anchor-and-recursive-members"></a>J. Verwenden mehrerer Ankerelemente und rekursiver Elemente  
 Im folgenden Beispiel werden mehrere Ankerelemente und rekursive Elemente verwendet, um alle Vorfahren einer bestimmten Person zurückzugeben. Eine Tabelle wird erstellt und mit Werten aufgefüllt, um den Familienstammbaum zu erstellen, der vom rekursiven allgemeinen Tabellenausdruck zurückgegeben wird.  
  
```  
-- Genealogy table  
IF OBJECT_ID('dbo.Person','U') IS NOT NULL DROP TABLE dbo.Person;  
GO  
CREATE TABLE dbo.Person(ID int, Name varchar(30), Mother int, Father int);  
GO  
INSERT dbo.Person   
VALUES(1, 'Sue', NULL, NULL)  
      ,(2, 'Ed', NULL, NULL)  
      ,(3, 'Emma', 1, 2)  
      ,(4, 'Jack', 1, 2)  
      ,(5, 'Jane', NULL, NULL)  
      ,(6, 'Bonnie', 5, 4)  
      ,(7, 'Bill', 5, 4);  
GO  
-- Create the recursive CTE to find all of Bonnie's ancestors.  
WITH Generation (ID) AS  
(  
-- First anchor member returns Bonnie's mother.  
    SELECT Mother   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION  
-- Second anchor member returns Bonnie's father.  
    SELECT Father   
    FROM dbo.Person  
    WHERE Name = 'Bonnie'  
UNION ALL  
-- First recursive member returns male ancestors of the previous generation.  
    SELECT Person.Father  
    FROM Generation, Person  
    WHERE Generation.ID=Person.ID  
UNION ALL  
-- Second recursive member returns female ancestors of the previous generation.  
    SELECT Person.Mother  
    FROM Generation, dbo.Person  
    WHERE Generation.ID=Person.ID  
)  
SELECT Person.ID, Person.Name, Person.Mother, Person.Father  
FROM Generation, dbo.Person  
WHERE Generation.ID = Person.ID;  
GO  
```  
  
###  <a name="bkmkUsingAnalyticalFunctionsInARecursiveCTE"></a> K. Verwenden von Analysefunktionen in einem rekursiven allgemeinen Tabellenausdruck  
 Im folgenden Beispiel wird ein Fehler gezeigt, der beim Verwenden einer Analyse- oder Aggregatfunktion im rekursiven Teil eines allgemeinen Tabellenausdrucks auftreten kann.  
  
```  
DECLARE @t1 TABLE (itmID int, itmIDComp int);  
INSERT @t1 VALUES (1,10), (2,10);   
  
DECLARE @t2 TABLE (itmID int, itmIDComp int);   
INSERT @t2 VALUES (3,10), (4,10);   
  
WITH vw AS  
 (  
    SELECT itmIDComp, itmID  
    FROM @t1  
  
    UNION ALL  
  
    SELECT itmIDComp, itmID  
    FROM @t2  
)   
,r AS  
 (  
    SELECT t.itmID AS itmIDComp  
           , NULL AS itmID  
           ,CAST(0 AS bigint) AS N  
           ,1 AS Lvl  
    FROM (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4) AS t (itmID)   
  
UNION ALL  
  
SELECT t.itmIDComp  
    , t.itmID  
    , ROW_NUMBER() OVER(PARTITION BY t.itmIDComp ORDER BY t.itmIDComp, t.itmID) AS N  
    , Lvl + 1  
FROM r   
    JOIN vw AS t ON t.itmID = r.itmIDComp  
)   
  
SELECT Lvl, N FROM r;  
```  
  
 Die folgenden Ergebnisse sind die erwarteten Ergebnisse für die Abfrage.  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    4  
2    3  
2    2  
2    1  
```  
  
 Die folgenden Ergebnisse sind die tatsächlichen Ergebnisse für die Abfrage.  
  
```  
Lvl  N  
1    0  
1    0  
1    0  
1    0  
2    1  
2    1  
2    1  
2    1  
```  
  
 `N` gibt 1 für jede Übergabe des rekursiven Teils des allgemeinen Tabellenausdrucks zurück, da nur die Teilmenge der Daten für diese Rekursionsebene an `ROWNUMBER` übergeben wird. Für jede Iteration des rekursiven Teils der Abfrage wird nur eine Zeile an `ROWNUMBER` übergeben.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="l-using-a-common-table-expression-within-a-ctas-statement"></a>L. Verwenden eines allgemeinen Tabellenausdrucks in einer CTAS-Anweisung  
 Das folgende Beispiel erstellt eine neue Tabelle mit der Gesamtanzahl der Kaufaufträge pro Jahr für jeden Vertriebsmitarbeiter [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].  
  
```  
-- Uses AdventureWorks  
  
CREATE TABLE SalesOrdersPerYear  
WITH  
(  
    DISTRIBUTION = HASH(SalesPersonID)  
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="m-using-a-common-table-expression-within-a-cetas-statement"></a>M. Verwenden eines allgemeinen Tabellenausdrucks in einer CETAS-Anweisung  
 Das folgende Beispiel erstellt eine neue externe Tabelle, die die Gesamtanzahl der Kaufaufträge pro Jahr für jeden Vertriebsmitarbeiter enthält [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].  
  
```  
-- Uses AdventureWorks  
  
CREATE EXTERNAL TABLE SalesOrdersPerYear  
WITH  
(  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:5000/files/Customer',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|' )   
)  
AS  
    -- Define the CTE expression name and column list.  
    WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)  
    AS  
    -- Define the CTE query.  
    (  
        SELECT SalesPersonID, SalesOrderID, YEAR(OrderDate) AS SalesYear  
        FROM Sales.SalesOrderHeader  
        WHERE SalesPersonID IS NOT NULL  
    )  
    -- Define the outer query referencing the CTE name.  
    SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, SalesYear  
    FROM Sales_CTE  
    GROUP BY SalesYear, SalesPersonID  
    ORDER BY SalesPersonID, SalesYear;  
GO  
```  
  
### <a name="n-using-multiple-comma-separated-ctes-in-a-statement"></a>N. Verwenden mehrere durch Trennzeichen voneinander getrennt allgemeine Tabellenausdrücke in einer Anweisung  
 Im folgende Beispiel wird veranschaulicht, einschließlich der zwei allgemeine Tabellenausdrücke in einer einzelnen Anweisung. Die allgemeine Tabellenausdrücke darf nicht sein (keine Rekursion) geschachtelt.  
  
```  
WITH   
 CountDate (TotalCount, TableName) AS  
    (  
     SELECT COUNT(datekey), 'DimDate' FROM DimDate  
    ) ,  
 CountCustomer (TotalAvg, TableName) AS  
    (  
     SELECT COUNT(CustomerKey), 'DimCustomer' FROM DimCustomer  
    )  
SELECT TableName, TotalCount FROM CountDate  
UNION ALL  
SELECT TableName, TotalAvg FROM CountCustomer;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Mit Ausnahme von und INTERSECT &#40; Transact-SQL &#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [INSERT &#40; Transact-SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
