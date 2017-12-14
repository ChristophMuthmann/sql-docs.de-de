---
title: Erstellen von benutzerdefinierten Funktionen (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: udf
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: b90ec3cc6932d9487dd339041fc1f580f63a8db6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-user-defined-functions-database-engine"></a>Erstellen von benutzerdefinierten Funktionen (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie eine benutzerdefinierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktion (User-defined Function, UDF) mit [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellt wird.  

  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Mit benutzerdefinierten Funktionen können keine Aktionen ausgeführt werden, die den Status einer Datenbank ändern.  
  
-   Benutzerdefinierte Funktion dürfen keine OUTPUT INTO-Klausel enthalten, deren Ziel eine Tabelle ist.  
  
-   Von benutzerdefinierten Funktionen können nicht mehrere Resultsets zurückgegeben werden. Falls mehrere Resultsets zurückgegeben werden müssen, verwenden Sie eine gespeicherte Prozedur.  
  
-   Die Fehlerbehandlung ist in einer benutzerdefinierten Funktion eingeschränkt. TRY…CATCH, @ERROR oder RAISERROR wird von UDFs nicht unterstützt.  
  
-   Von benutzerdefinierten Funktionen kann zwar keine gespeicherte Prozedur, aber eine erweiterte gespeicherte Prozedur aufgerufen werden.  
  
-   Von benutzerdefinierten Funktionen können kein dynamisches SQL bzw. keine temporären Tabellen verwendet werden. Tabellenvariablen sind zulässig.  
  
-   SET-Anweisungen sind in einer benutzerdefinierten Funktionen nicht zulässig.  
  
-   Die FOR XML-Klausel ist nicht zulässig.  
  
-   Benutzerdefinierte Funktionen können geschachtelt werden. Dies bedeutet, dass eine benutzerdefinierte Funktion eine andere aufrufen kann. Die Schachtelungsebene wird um eins erhöht, wenn die aufgerufene Funktion mit der Ausführung beginnt, und wird wieder um eins erniedrigt, wenn die aufgerufene Funktion die Ausführung beendet. Benutzerdefinierte Funktionen unterstützen bis zu 32 geschachtelte Ebenen. Ein Überschreiten der maximalen Schachtelungsebenen verursacht das Fehlschlagen der gesamten Funktionsaufrufskette. Alle Verweise auf verwalteten Code von einer benutzerdefinierten Transact-SQL-Funktion aus gelten hinsichtlich des Maximums von 32 Schachtelungsebenen als eine Ebene. Methoden, die aus verwaltetem Code aufgerufen werden, werden nicht mitgezählt.  
  
-   Die folgenden Service Broker-Anweisungen **können nicht** in die Definition einer benutzerdefinierten Transact-SQL-Funktion eingeschlossen werden:  
  
    -   BEGIN DIALOG CONVERSATION  
  
    -   END CONVERSATION  
  
    -   GET CONVERSATION GROUP  
  
    -   MOVE CONVERSATION  
  
    -   RECEIVE  
  
    -   SEND  
  
###  <a name="Security"></a> Berechtigungen 

Erfordert die CREATE FUNCTION-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Funktion erstellt wird. Wenn die Funktion einen benutzerdefinierten Typ angibt, wird die EXECUTE-Berechtigung für den Typ benötigt.  
  
##  <a name="Scalar"></a> Skalarfunktionen  
 Im folgenden Beispiel wird eine Skalarfunktion mit mehreren Anweisungen in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank erstellt. Die Funktion nimmt einen Eingabewert ( `ProductID`) an und gibt einen einzelnen Datenwert zurück, der die aggregierte Menge des Lagerbestands für das angegebene Produkt darstellt.  
  
```t-sql  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END; 
```  
  
 Im folgenden Beispiel wird die `ufnGetInventoryStock` -Funktion verwendet, um den aktuellen Lagerbestand für Produkte mit einer `ProductModelID` zwischen 75 und 80 zurückzugeben.  
  
```t-sql  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
##  <a name="TVF"></a> Tabellenwertfunktionen  
 Im folgenden Beispiel wird eine Inline-Tabellenwertfunktion in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank erstellt. Die Funktion nimmt einen Eingabeparameter (eine Kunden-ID (Geschäfts-ID)) an und gibt die Spalten `ProductID`, `Name`sowie das Aggregat der bisherigen Verkaufseinnahmen dieses Jahres als `YTD Total` für jedes Produkt zurück, das an das Geschäft verkauft wurde.  
  
```t-sql  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
```  
  
 Das folgende Beispiel ruft die Funktion auf und gibt die Kunden-ID 602 an.  
  
```t-sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
 Im folgenden Beispiel wird eine Tabellenwertfunktion in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank erstellt. Die Funktion nimmt einen einzelnen Eingabeparameter ( `EmployeeID` ) an und gibt eine Liste aller Mitarbeiter zurück, die dem angegebenen Mitarbeiter direkt oder indirekt unterstellt sind. Die Funktion wird dann unter Angabe der Mitarbeiternummer 109 aufgerufen.  
  
```t-sql  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
```  
  
## <a name="more-examples"></a>Weitere Beispiele  
 - [Benutzerdefinierte Funktionen](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 - [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) 
 - [ALTER FUNCTION (Transact SQL)](../../tools/sql-server-profiler/start-sql-server-profiler.md) 
 - [DROP FUNCTION (Transact SQL)](../../tools/sql-server-profiler/start-sql-server-profiler.md)
 - [DROP PARTITION FUNCTION (Transact-SQL)](https://msdn.microsoft.com/library/ms187759(SQL.130).aspx)
 - Weitere Beispiele in der [Community](https://www.bing.com/search?q=user%20defined%20function%20%22sql%20server%202016%22%20examples&qs=n&form=QBRE&pq=user%20defined%20function%20%22sql%20server%202016%22%20examples&sc=0-48&sp=-1&sk=&cvid=C3AD337125A840AD9EEFA3AAC36A3712)
  
