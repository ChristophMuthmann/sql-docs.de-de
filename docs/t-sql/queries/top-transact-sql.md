---
title: TOP (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql-non-specified
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
- TOP_TSQL
- TOP
dev_langs:
- TSQL
helpviewer_keywords:
- TOP clause
- first set of query result rows [SQL Server]
- TOP clause, about TOP clause
- queries [SQL Server], results
ms.assetid: da983c0a-06c5-4cf8-a6a4-7f9d66f34f2c
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 926de1152e7c1223441d9ac85da11246049e31ea
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="top-transact-sql"></a>TOP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Begrenzt die zurückgegebenen Zeilen in einem Abfrageresultset auf die in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] angegebene Anzahl bzw. den darin angegebenen diesbezüglichen Prozentwert. Wenn TOP in Verbindung mit der ORDER BY-Klausel verwendet wird, ist das Resultset auf die ersten *n* sortierten Zeilen beschränkt; andernfalls werden die ersten *n* Zeilen in zufälliger Reihenfolge zurückgegeben. Mit dieser Klausel können Sie die Anzahl der Zeilen angeben, die von einer SELECT-Anweisung zurückgegeben werden oder von einer INSERT-, UPDATE-, MERGE- oder DELETE-Anweisung betroffen sind.   
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[   
    TOP (expression) [PERCENT]  
    [ WITH TIES ]  
]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[   
    TOP ( expression )   
    [ WITH TIES ]  
]  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Der numerische Ausdruck, der angibt, dass eine Anzahl von Zeilen zurückgegeben wird. *expression* wird implizit in einen **float**-Wert konvertiert, wenn PERCENT angegeben ist. Andernfalls wird der Ausdruck in **bigint** konvertiert.  
  
 PERCENT  
 Gibt an, dass die Abfrage nur die ersten *expression* Prozent der Zeilen aus dem Resultset zurückgibt. Bruchwerte werden auf den nächsten ganzzahligen Wert aufgerundet.  
  
 WITH TIES  
 Wird verwendet, wenn Sie mindestens zwei Zeilen zurückgeben möchten, die zeitgleich den letzten Platz im beschränkten Resultset belegen. Muss mit der **ORDER BY**-Klausel verwendet werden. Durch **WITH TIES** werden möglicherweise mehr Zeilen zurückgegeben, als der Wert in *expression* angibt. Angenommen, *expression* ist auf den Wert 5 festgelegt, und zwei weitere Zeilen entsprechen den Werten der **ORDER BY**-Spalten in Zeile 5. In diesem Fall enthält das Resultset sieben Zeilen.  
  
 TOP...WITH TIES kann nur in SELECT-Anweisungen angegeben werden und nur dann, wenn eine ORDER BY-Klausel angegeben wurde. Die zurückgegebene Reihenfolge beim Binden von Datensätzen ist willkürlich. ORDER BY wirkt sich nicht auf diese Regel aus.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Verwenden Sie in einer SELECT-Anweisung immer eine ORDER BY-Klausel mit einer TOP-Klausel. Dies ist die einzige Möglichkeit, zuverlässig anzugeben, welche Zeilen von TOP betroffen sind.  
  
 Verwenden Sie OFFSET und FETCH in der ORDER BY-Klausel anstelle der TOP-Klausel, um eine Abfrageauslagerung zu implementieren. Eine Abfrageauslagerung (d. h. das Senden von Abschnitten oder "Seiten" von Daten an den Client) kann leichter mit OFFSET- und FETCH-Klauseln implementiert werden. Weitere Informationen finden Sie unter [ORDER BY-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
 Schränken Sie die Anzahl der zurückgegebenen Zeilen mithilfe von TOP (oder OFFSET und FETCH) anstelle von SET ROWCOUNT ein. Diese Methoden werden SET ROWCOUNT aus folgenden Gründen vorgezogen:  
  
-   Im Rahmen einer SELECT-Anweisung kann der Wert von *expression* in der TOP- oder der FETCH-Klausel vom Abfrageoptimierer während der Abfrageoptimierung berücksichtigt werden. Da SET ROWCOUNT außerhalb einer Anweisung verwendet wird, die eine Abfrage ausführt, kann ihr Wert nicht in einem Abfrageplan berücksichtigt werden.  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Aus Gründen der Abwärtskompatibilität sind die Klammern in SELECT-Anweisungen optional. Aus Gründen der Konsistenz wird jedoch empfohlen, TOP-Ausdrücke in SELECT-Anweisungen stets in Klammern einzuschließen, da diese in INSERT-, UPDATE-, MERGE- und DELETE-Anweisungen obligatorisch sind.  
  
## <a name="interoperability"></a>Interoperabilität  
 Der TOP-Ausdruck wirkt sich nicht auf Anweisungen aus, die möglicherweise wegen eines Triggers ausgeführt werden. Die Tabellen **inserted** und **deleted** in den Triggern geben nur die Zeilen zurück, die tatsächlich von den INSERT-, UPDATE- MERGE- oder DELETE-Anweisungen betroffen sind. Beispiel: Ein INSERT TRIGGER der aufgrund einer INSERT-Anweisung mit einer TOP-Klausel ausgelöst wird.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht das Aktualisieren von Zeilen über Sichten. Da die TOP-Klausel in der Sichtdefinition enthalten sein kann, können bestimmte Zeilen bei einem Update u. U. verschwinden, falls die Zeilen nicht länger die Anforderungen des TOP-Ausdrucks erfüllen.  
  
 Wenn dies in der MERGE-Anweisung angegeben ist, wird die TOP-Klausel angewendet, *nachdem* die gesamte Quelltabelle und die gesamte Zieltabelle verknüpft wurden und die verknüpften Zeilen, auf die keine INSERT-, UPDATE- oder DELETE-Aktion angewendet wird, entfernt wurden. Die TOP-Klausel verringert zudem die Anzahl der verknüpften Zeilen auf den angegebenen Wert, und die INSERT-, UPDATE- oder DELETE-Aktionen werden ungeordnet auf die verbliebenen verknüpften Zeilen angewendet. Dies bedeutet, dass für die Verteilung der Zeilen auf die in den WHEN-Klauseln definierten Aktionen keine bestimmte Reihenfolge gilt. Wenn beispielsweise TOP (10) angegeben wird, sind zehn Zeilen betroffen. Von diesen Zeilen können sieben aktualisiert und drei eingefügt werden, oder eine Zeile kann gelöscht, fünf können aktualisiert und vier eingefügt werden usw. Da die MERGE-Anweisung einen vollständigen Tabellenscan der Quell- und der Zieltabelle ausführt, kann die E/A-Leistung beeinträchtigt werden, wenn mit der TOP-Klausel eine große Tabelle durch Erstellen mehrerer Batches geändert wird. In diesem Szenario muss unbedingt sichergestellt werden, dass alle aufeinanderfolgenden Batches auf neue Zeilen ausgerichtet sind.  
  
 Geben Sie die TOP-Klausel in einer Abfrage mit einem UNION-, UNION ALL-, EXCEPT- oder INTERSECT-Operator mit Bedacht. Es ist denkbar, dass eine Abfrage geschrieben wird, die unerwartete Ergebnisse zurückgibt, weil die Reihenfolge der logischen Verarbeitung für die TOP-Klausel und die ORDER BY-Klausel nicht immer intuitiv ist, wenn diese Operatoren in einem SELECT-Vorgang verwendet werden. Beispiel: Für die folgende Tabelle und die darin enthaltenen Daten sollen das günstigste rote Auto sowie das günstigste blaue Auto zurückgeben werden. Dies sind der rote PKW und der blaue LKW.  
  
```sql  
CREATE TABLE dbo.Cars(Model varchar(15), Price money, Color varchar(10));  
INSERT dbo.Cars VALUES  
    ('sedan', 10000, 'red'), ('convertible', 15000, 'blue'),   
    ('coupe', 20000, 'red'), ('van', 8000, 'blue');  
```  
  
 Um diese Ergebnisse zu erreichen, können Sie die folgende Abfrage schreiben:  
  
```sql  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'red'  
UNION ALL  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'blue'  
ORDER BY Price ASC;  
GO    
```  
  
 Im Folgenden finden Sie das Resultset.  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 convertible   blue       15000.00
 ```  
  
 Die unerwarteten Ergebnisse werden zurückgegeben, da die logische Ausführung der TOP-Klausel der logischen Ausführung der ORDER BY-Klausel vorangeht, mit der die Ergebnisse des Operators (hier: UNION ALL) sortiert werden. Aus diesem Grund werden von der vorstehenden Abfrage ein beliebiges rotes und ein beliebiges blaues Auto zurückgegeben, und das Ergebnis dieser Union wird nach dem Preis sortiert. Im folgenden Beispiel wird veranschaulicht, wie eine Abfrage geschrieben wird, um das gewünschte Ergebnis zu erzielen.  
  
```sql  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'red'  
      ORDER BY Price ASC) AS a  
UNION ALL  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'blue'  
      ORDER BY Price ASC) AS b;  
GO    
```  
  
 Durch die Verwendung von TOP und ORDER BY in einem untergeordneten SELECT-Vorgang stellen Sie sicher, dass die Ergebnisse der ORDER BY-Klausel auf die TOP-Klausel angewendet werden und damit nicht das Ergebnis des UNION-Vorgangs sortiert wird.  
  
 Im Folgenden finden Sie das Resultset.  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 van           blue        8000.00
 ```  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Wenn TOP mit INSERT, UPDATE, MERGE oder DELETE verwendet wird, werden die Zeilen, auf die verwiesen wird, nicht auf bestimmte Weise angeordnet, und die ORDER BY-Klausel kann in diesen Anweisungen nicht direkt angegeben werden. Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge einzufügen, zu löschen oder zu bearbeiten, müssen Sie sie zusammen mit einer ORDER BY-Klausel in einer untergeordneten SELECT-Anweisung verwenden. Weitere Informationen finden Sie im Abschnitt "Beispiele" in diesem Thema.  
  
 TOP kann nicht in UPDATE- und DELETE-Anweisungen für partitionierte Sichten verwendet werden.  
  
 TOP kann nicht mit OFFSET und FETCH im gleichen Abfrageausdruck (im gleichen Abfragebereich) kombiniert werden. Weitere Informationen finden Sie unter [ORDER BY-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Grundlegende Syntax](#BasicSyntax)|TOP • PERCENT|  
|[Einschließen von gleichwertigen Werten](#tie)|WITH TIES|  
|[Beschränken der von DELETE, INSERT oder UPDATE betroffenen Zeilen](#DML)|DELETE • INSERT • UPDATE|  
  
###  <a name="BasicSyntax"></a> Grundlegende Syntax  
 Anhand von Beispielen in diesem Abschnitt wird die grundlegende Funktion der ORDER BY-Klausel mithilfe der mindestens erforderlichen Syntax veranschaulicht.  
  
#### <a name="a-using-top-with-a-constant-value"></a>A. Verwenden von TOP mit einem konstanten Wert  
 In den folgenden Beispielen wird die Anzahl der Mitarbeiter, die in einem Abfrageresultset zurückgegeben werden, mit einem konstanten Wert angegeben. Im ersten Beispiel werden die ersten 10 nicht definierten Zeilen zurückgegeben, da keine ORDER BY-Klausel verwendet wird. Im zweiten Beispiel wird eine ORDER BY-Klausel verwendet, um die ersten 10 Mitarbeiter zurückzugeben, die kürzlich eingestellt wurden.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Select the first 10 random employees.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee;  
GO  
-- Select the first 10 employees hired most recently.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO  
```  
  
#### <a name="b-using-top-with-a-variable"></a>B. Verwenden von TOP mit einer Variablen  
 Im folgenden Beispiel wird die Anzahl der Mitarbeiter, die im Abfrageresultset zurückgegeben werden, mit einer Variablen angegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @p AS int = 10;  
SELECT TOP(@p)JobTitle, HireDate, VacationHours  
FROM HumanResources.Employee  
ORDER BY VacationHours DESC;  
GO  
```  
  
#### <a name="c-specifying-a-percentage"></a>C. Angeben eines Prozentsatzes  
 Im folgenden Beispiel wird die Anzahl der Mitarbeiter, die im Abfrageresultset zurückgegeben werden, mit PERCENT angegeben. Die Tabelle `HumanResources.Employee` enthält 290 Mitarbeiter. Da 5 Prozent von 290 ein Dezimalstellenwert ist, wird der Wert auf die nächste ganze Zahl aufgerundet.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(5)PERCENT JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
GO    
```  
  
###  <a name="tie"></a> Einschließen von gleichwertigen Werten  
  
#### <a name="a-using-with-ties-to-include-rows-that-match-the-values-in-the-last-row"></a>A. Einschließen von Zeilen mit identischen Werten wie vorangehende Zeilen mit WITH TIES  
 Im folgenden Beispiel werden die obersten `10` Prozent aller Mitarbeiter mit dem höchsten Gehalt abgerufen und in absteigender Reihenfolge nach der Höhe des Gehalts zurückgegeben. Durch Angeben von `WITH TIES` wird sichergestellt, dass alle Mitarbeiter mit einem Gehalt, das dem niedrigsten zurückgegebenen Gehalt (letzte Zeile) entspricht, ebenfalls im Resultset enthalten sind, auch wenn dadurch `10` Prozent der Mitarbeiter überschritten werden.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP(10)WITH TIES  
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate  
FROM Person.Person AS pp   
    INNER JOIN HumanResources.Employee AS e  
        ON pp.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeePayHistory AS r  
        ON r.BusinessEntityID = e.BusinessEntityID  
ORDER BY Rate DESC;  
GO    
```  
  
###  <a name="DML"></a> Beschränken der von DELETE, INSERT oder UPDATE betroffenen Zeilen  
  
#### <a name="a-using-top-to-limit-the-number-of-rows-deleted"></a>A. Verwenden von TOP, um die Anzahl der zu löschenden Zeilen einzuschränken  
 Wenn eine TOP (*n*)-Klausel wird zusammen mit DELETE verwendet, der Löschvorgang wird ausgeführt, auf eine nicht definierte Auswahl von *n* Zeilen. D. h. die DELETE-Anweisung wählt eine beliebige (*n*) Anzahl der Zeilen, die in der WHERE-Klausel definierten Kriterien erfüllen. Im folgenden Beispiel löscht `20` Zeilen mit Fälligkeitsdaten vor dem 1. Juli 2002 aus der `PurchaseOrderDetail`-Tabelle.  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge zu löschen, müssen Sie sie zusammen mit ORDER BY in einer untergeordneten SELECT-Anweisung verwenden. Die folgende Abfrage löscht die zehn Zeilen der `PurchaseOrderDetail` -Tabelle mit den frühesten Fälligkeitsdaten. Die in der untergeordneten SELECT-Anweisung angegebene Spalte (`PurchaseOrderID`) ist der Primärschlüssel der Tabelle, um sicherzustellen, dass nur 10 Zeilen gelöscht werden. Wird in der untergeordneten SELECT-Anweisung eine Nichtschlüsselspalte verwendet, werden möglicherweise mehr als 10 Zeilen gelöscht, wenn die angegebene Spalte doppelte Werte enthält.  
  
```sql  
USE AdventureWorks2012;  
GO  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
#### <a name="b-using-top-to-limit-the-number-of-rows-inserted"></a>B. Einschränken der Anzahl eingefügter Zeilen mit TOP  
 Im folgenden Beispiel wird die `EmployeeSales`-Tabelle erstellt, und der Name und die Verkaufszahlen des laufenden Jahres für die ersten 5 Mitarbeiter aus der `HumanResources.Employee`-Tabelle werden eingefügt. Die INSERT-Anweisung wählt beliebige 5 Zeilen aus, die von der `SELECT`-Anweisung zurückgegeben werden, die die in der WHERE-Klausel definierten Kriterien erfüllen.  Mit der OUTPUT-Klausel werden die Zeilen angezeigt, die in die `EmployeeSales`-Tabelle eingefügt werden. Beachten Sie, dass die ersten 5 Mitarbeiter in der SELECT-Anweisung nicht mit der ORDER BY-Klausel ermittelt werden.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
 Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge einzufügen, müssen Sie sie zusammen mit einer ORDER BY-Klausel in einer untergeordneten SELECT-Anweisung verwenden, wie im folgenden Beispiel veranschaulicht. Mit der OUTPUT-Klausel werden die Zeilen angezeigt, die in die `EmployeeSales`-Tabelle eingefügt werden. Beachten Sie, dass die ersten 5 Mitarbeiter jetzt anhand der Ergebnisse der ORDER BY-Klausel und nicht anhand nicht definierter Zeilen eingefügt werden.  
  
```sql  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
GO    
```  
  
#### <a name="c-using-top-to-limit-the-number-of-rows-updated"></a>C. Einschränken der Anzahl aktualisierter Zeilen mit TOP  
 Im folgenden Beispiel wird die TOP-Klausel zur Aktualisierung von Zeilen in einer Tabelle verwendet. Wenn eine TOP (*n*)-Klausel mit UPDATE verwendet wird, wird der Updatevorgang auf eine nicht definierte Anzahl von Zeilen durchgeführt. D. h. die UPDATE-Anweisung wählt eine beliebige (*n*) Anzahl der Zeilen, die in der WHERE-Klausel definierten Kriterien erfüllen. Im folgenden Beispiel werden 10 Kunden von einem Vertriebsmitarbeiter zu einem anderen zugewiesen.  
  
```sql  
USE AdventureWorks2012;  
UPDATE TOP (10) Sales.Store  
SET SalesPersonID = 276  
WHERE SalesPersonID = 275;  
GO  
```  
  
 Wenn TOP verwendet werden muss, um Updates in einer sinnvollen Abfolge anzuwenden, muss in einer untergeordneten SELECT-Anweisung TOP gemeinsam mit ORDER BY verwendet werden. Mit dem nachfolgenden Beispiel werden die Urlaubsstunden der 10 Mitarbeiter mit dem frühesten Einstellungsdatum aktualisiert.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel werden die obersten 31 Zeilen zurückgegeben, die den Abfragekriterien entsprechen. Die **ORDER BY**-Klausel wird verwendet, um sicherzustellen, dass es sich bei den 31 zurückgegebenen Zeilen um die ersten 31 Zeilen (basierend auf einer alphabetischen Sortierung der `LastName`-Spalte) handelt.  
  
 Verwenden Sie **TOP**, ohne WITH TIES anzugeben.  
  
```sql  
SELECT TOP (31) FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 Ergebnis: 31 Zeilen werden zurückgegeben.  
  
 Verwenden Sie TOP mit Angabe von WITH TIES.  
  
```sql  
SELECT TOP (31) WITH TIES FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 Ergebnis: 33 Zeilen werden zurückgegeben, da drei Mitarbeiter namens „Brown“ in der 31. Zeile vorhanden sind.  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40; Transact-SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [ORDER BY-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
 
