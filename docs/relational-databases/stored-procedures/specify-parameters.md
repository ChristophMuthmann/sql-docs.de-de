---
title: Angeben von Parameter | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 24527c0b1e2bfcbcdf7d3a8ceb62f0f0cf140625
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="specify-parameters"></a>Angeben von Parametern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Aufrufende Programme sind in der Lage, durch die Angabe von Prozedurparametern Werte in den Textkörper der Prozedur zu übergeben. Jene Werte können während der Prozedurausführung zu einer Vielzahl von Zwecken verwendet werden. Prozedurparameter können auch Werte an das aufrufende Programm zurückgeben, wenn der Parameter als OUTPUT-Parameter markiert wird.  
  
 Eine Prozedur kann über maximal 2100 Parameter verfügen, denen jeweils ein Name, eine Datentyp und eine Richtung zugewiesen wird. Optional können Parametern Standardwerte zugewiesen werden.  
  
 Der folgende Abschnitt enthält Informationen zur Übergabe von Werten in Parameter und zur Verwendung der verschiedenen Parameterattribute in einem Prozeduraufruf.  
  
## <a name="passing-values-into-parameters"></a>Übergeben von Werte in Parameter  
 Die mit einem Prozeduraufruf angegebenen Parameterwerte müssen Konstanten oder Variablen sein. Ein Funktionsname kann nicht als Parameterwert verwendet werden. Variablen können benutzerdefiniert oder Systemvariablen (z.B. @@spid) sein.  
  
 Die folgenden Beispiele zeigen, wie Parameterwerte an die Prozedur `uspGetWhereUsedProductID`übergeben werden. Sie zeigen, wie Parameter als Konstanten und Variablen übergeben werden, sowie die Verwendung einer Variablen, um den Wert einer Funktion zu übergeben.  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>Angeben von Parameternamen  
 Wenn eine Prozedur erstellt und ein Parameternamen deklariert wird, muss ein Parametername gewählt werden, der mit einem einzelnen @-Zeichen beginnt und im Bereich der Prozedur eindeutig ist.  
  
 Durch das explizite Benennen der Parameter und Zuweisen der entsprechenden Werte zu jedem Parameter in einem Prozeduraufruf ist es möglich, dass die Parameter in beliebiger Reihenfolge angegeben werden. Wenn z. B. die gespeicherte Prozedur **my_proc** drei Parameter mit den Namen **@first**, **@second**und **@third**erwartet, können die Werte, die an die gespeicherte Prozedur übergeben werden, wie den Parameternamen, wie folgt zugewiesen werden: `EXECUTE my_proc @second = 2, @first = 1, @third = 3;`  
  
> [!NOTE]  
>  Wenn ein Parameterwert im Format **@parameter =***Wert* angegeben wird, dann müssen auch alle nachfolgenden Parameter auf diese Weise angegeben werden. Wenn die Parameterwerte nicht im Format **@parameter =***Wert* übergeben werden, dann müssen die Werte in derselben Reihenfolge (von links nach rechts) angegeben werden, in der die Parameter in der CREATE PROCEDURE-Anweisung aufgeführt sind.  
  
> [!WARNING]  
>  Jeder Parameter, der im Format **@parameter =***Wert* übergeben wird, aber geschrieben ist, bewirkt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler generiert und die Prozedurausführung beendet.  
  
## <a name="specifying-parameter-data-types"></a>Angeben von Parameterdatentypen  
 Parameter müssen mit einem Datentyp definiert werden, wann sie in einer CREATE PROCEDURE-Anweisung deklariert werden. Durch den Datentyp eines Parameters werden der Typ und der Wertebereich festgelegt, die beim Aufruf der Prozedur für den Parameter akzeptiert werden. Wenn Sie z. B. einen Parameter mit dem **tinyint** -Datentyp definieren, werden nur numerische Werte im Bereich von 0 bis 255 als Werte für diesen Parameter akzeptiert. Wenn eine Prozedur mit einem Wert ausgeführt wird, der nicht mit dem Datentyp kompatibel ist, wird ein Fehler zurückgegeben.  
  
## <a name="specifying-parameter-default-values"></a>Angeben von Standardwerten für Parameter  
 Ein Parameter, für den in der Parameterdeklaration ein Standardwert angeben wird, wird als optional betrachtet. Es ist nicht notwendig, in einem Prozeduraufruf einen Wert für einen optionalen Parameter bereitzustellen.  
  
 Der Standardwert eines Parameters wird verwendet, wenn:  
  
-   Für den Parameter im Prozeduraufruf kein Wert angegeben wird.  
  
-   Das DEFAULT-Schlüsselwort im Prozeduraufruf als Wert für den Parameter angegeben wird.  
  
> [!NOTE]  
>  Wenn es sich bei dem Standardwert um eine Zeichenfolge handelt, die eingebettete Leerzeichen oder Satzzeichen enthält oder mit einer Zahl beginnt (z. B. 6xxx), muss der Wert in einfache, gerade Anführungszeichen eingeschlossen werden.  
  
 Wenn kein entsprechender Wert als Standardwert für den Parameter angegeben werden kann, geben Sie NULL als Standardwert an. Es empfiehlt sich, die Prozedur eine benutzerdefinierte Meldung zurückgeben zu lassen, wenn sie ohne Wertangabe für den Parameter ausgeführt wird.  
  
 Im folgenden Beispiel wird die gespeicherte Prozedur `uspGetSalesYTD` mit einem Eingabeparameter ( `@SalesPerson`) ausgeführt. NULL wird als Standardwert für den Parameter zugewiesen und in Fehlerbehandlungsanweisungen zum Zurückgeben einer benutzerdefinierten Fehlermeldung verwendet, wenn die Prozedur ohne einen Wert für den Parameter `@SalesPerson` ausgeführt wird.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 Im folgenden Beispiel wird die Prozedur ausgeführt. Die erste Anweisung führt die Prozedur ohne Angabe eines Eingabewerts aus. Dies bewirkt, dass die Fehlerbehandlungsanweisungen in der Prozedur die benutzerdefinierte Fehlermeldung zurückgeben. Die zweite Anweisung stellt einen Eingabewert zur Verfügung und gibt das erwartete Resultset zurück.  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.uspGetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.uspGetSalesYTD N'Blythe';  
GO  
```  
  
 Sie können Parameter auslassen, für die Standardwerte angegeben wurden; dies ist jedoch nur durch Abschneiden der Parameterliste möglich. Wenn eine Prozedur z. B. über fünf Parameter verfügt, können sowohl der vierte als auch der fünfte Parameter weggelassen werden. Der vierte Parameter kann jedoch nicht weggelassen werden, solange der fünfte Parameter angegeben wird, es sei denn, die Parameter werden im Format **@parameter =***Wert* angegeben.  
  
## <a name="specifying-parameter-direction"></a>Angeben der Parameterrichtung  
 Die Parameterrichtung ist entweder Eingabe, d. h. ein Wert wird in den Textkörper der Prozedur übergeben, oder Ausgabe, d. h. die Prozedur gibt einen Wert an das aufrufende Programm zurück. Standardmäßig wird ein Eingabeparameter verwendet.  
  
 Um einen Ausgabeparameter anzugeben müssen Sie das OUTPUT-Schlüsselwort in der Definition des Parameters in der CREATE PROCEDURE-Anweisung angeben. Die Prozedur gibt den aktuellen Wert des Ausgabeparameters an das aufrufende Programm zurück, wenn die Prozedur beendet wird. Um den Wert des Parameters in einer Variablen zu speichern, die in dem aufrufenden Programm verwendet werden kann, muss das aufrufende Programm beim Ausführen der Prozedur ebenfalls das Schlüsselwort OUTPUT verwenden.  
  
 Im nachfolgenden Beispiel wird die `Production.usp_GetList`-Prozedur erstellt, von der eine Liste der Produkte zurückgegeben wird, deren Preis einen angegebenen Betrag nicht übersteigt. In dem Beispiel wird die Verwendung mehrerer SELECT-Anweisungen und mehrerer OUTPUT-Parameter dargestellt. OUTPUT-Parameter ermöglichen einer externen Prozedur, einem Batch oder mehreren [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen während dem Ausführen der Prozedur den Zugriff auf einen Satz von Werten.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 Führen Sie `usp_GetList` aus, um eine Liste der [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] -Produkte (Bikes) zurückzugeben, die weniger als 700 $ kosten. Die OUTPUT-Parameter **@cost** und **@compareprices** werden mit einer Ablaufsteuerungssprache verwendet, um eine Meldung an das Fenster **Meldungen** zurückzugeben.  
  
> [!NOTE]  
>  Die OUTPUT-Variable muss sowohl beim Erstellen der Prozedur als auch beim Verwenden der Variable definiert werden. Parametername und Variablenname brauchen nicht übereinzustimmen. Jedoch müssen der Datentyp und die Position des Parameters übereinstimmen, es sei denn, es wird **@listprice=** *variable* verwendet.  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  
