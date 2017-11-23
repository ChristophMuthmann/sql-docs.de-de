---
title: Sp_executesql (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_executesql
- sp_executesql_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_executesql
- dynamic SQL
ms.assetid: a8d68d72-0f4d-4ecb-ae86-1235b962f646
caps.latest.revision: "64"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b6dec48efa27a14443e69158ed9e9fffb55eba29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spexecutesql-transact-sql"></a>sp_executesql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Führt eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder einen -Batch aus, die bzw. der mehrfach wiederverwendet werden kann oder dynamisch erstellt wurde. Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder der -Batch können eingebettete Parameter enthalten.  
  
> [!IMPORTANT]  
>  Durch zur Laufzeit kompilierte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen können Anwendungen böswilligen Angriffen ausgesetzt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_executesql [ @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [ OUT | OUTPUT ][ ,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @stmt=] *Anweisung*  
 Ist eine Unicode-Zeichenfolge, enthält eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung oder eines Batches. @stmteine Unicode-Konstante oder eine Unicode-Variable muss sein. Komplexere Unicodeausdrücke, wie z. B. die Verkettung von zwei Zeichenfolgen mit dem +-Operator, sind nicht zulässig. Zeichenkonstanten sind nicht zulässig. Wenn eine Unicode-Konstante angegeben wird, muss er mit vorangestellt ein **N**. Beispielsweise die Unicode-Konstante **N 'Sp_who'** gültig ist, aber die Zeichenkonstante **'Sp_who'** nicht. Die Länge der Zeichenfolge wird nur durch den verfügbaren Arbeitsspeicher des Datenbankservers begrenzt. Auf 64-Bit-Servern, die Größe der Zeichenfolge ist auf 2 GB sind, die maximale Größe des beschränkt **nvarchar(max)**.  
  
> [!NOTE]  
>  @stmtkann Parameter aufweisen, z. B. das gleiche Format wie ein Variablenname enthalten:`N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Für jeden Parameter in @stmt ist ein entsprechender Eintrag in der @params-Parameterdefinitionsliste und in der Parameterwerteliste erforderlich.  
  
 [ @params=] N'@*Parameter_name**Data_type* [,... *n* ] '  
 Eine Zeichenfolge, die die Definitionen aller Parameter enthält, die in @stmt eingebettet wurden. Die Zeichenfolge muss eine Unicode-Konstante oder eine Unicode-Variable sein. Jede Parameterdefinition besteht aus einem Parameternamen und einem Datentyp. *n*ist ein Platzhalter, der zusätzliche Parameterdefinitionen. Jeder Parameter im angegebenen @stmtmust definiert werden, @params. Wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung bzw. ein solcher Batch in @stmt keine Parameter enthält, ist @params nicht erforderlich. Der Standardwert für diesen Parameter ist NULL.  
  
 [ @param1=] '*value1*"  
 Der Wert für den ersten Parameter, der in der Parameterzeichenfolge definiert ist. Bei diesem Wert kann es sich um eine Unicode-Konstante oder eine Unicode-Variable handeln. Für jeden Parameter in @stmt muss ein Parameterwert angegeben werden. Die Werte sind nicht erforderlich, wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder der -Batch in @stmt keine Parameter aufweist.  
  
 [ OUT | OUTPUT ]  
 Gibt an, dass es sich bei dem Parameter um einen Ausgabeparameter handelt. **Text**, **Ntext**, und **Image** Parameter können als OUTPUT-Parameter verwendet werden, es sei denn, die Prozedur eine Prozedur der common Language Runtime (CLR) ist. Ein Ausgabeparameter, der das Schlüsselwort OUTPUT verwendet, kann ein Cursorplatzhalter sein, es sei denn, bei der Prozedur handelt es sich um eine CLR-Prozedur (Common Language Runtime).  
  
 *n*  
 Ein Platzhalter für die Werte zusätzlicher Parameter. Werte können nur Konstanten oder Variablen sein. Werte können keine komplexeren Ausdrücke sein, wie z. B. Funktionen oder Ausdrücke, die mithilfe von Operatoren erstellt werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder ungleich 0 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt die Resultsets von allen SQL-Anweisungen der SQL-Zeichenfolge zurück.  
  
## <a name="remarks"></a>Hinweise  
 Sp_executesql-Parameter müssen in der Reihenfolge eingegeben werden, wie im Abschnitt "Syntax" weiter oben in diesem Thema beschrieben. Wenn die Parameter nicht in der vorgegebenen Reihenfolge eingegeben werden, wird eine Fehlermeldung ausgegeben.  
  
 sp_executesql verhält sich hinsichtlich Batches, Namensbereichen und Datenbankkontext wie EXECUTE. Die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung oder einen Batch im Sp_executesql @stmt Parameter wird nicht kompiliert werden, bis die Sp_executesql-Anweisung ausgeführt wird. Der Inhalt von @stmt wird dann kompiliert und als Ausführungsplan ausgeführt, der separat vom Ausführungsplan des Batches ist, der sp_executesql aufgerufen hat. Der sp_executesql-Batch kann nicht auf Variablen verweisen, die in dem Batch deklariert werden, der sp_executesql aufruft. Lokale Cursor oder Variablen im sp_executesql-Batch sind für den Batch, der sp_executesql aufruft, nicht sichtbar. Änderungen am Datenbankkontext sind nur bis zum Ende der sp_executesql-Anweisung vorhanden.  
  
 sp_executesql kann anstelle von gespeicherten Prozeduren verwendet werden, um eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung mehrere Male auszuführen, wenn sich nur die Parameterwerte in der Anweisung ändern. Da die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung selbst unverändert bleibt und nur die Parameterwerte geändert werden, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer wahrscheinlich den Ausführungsplan wiederverwenden, der für die erste Ausführung erstellt wird.  
  
> [!NOTE]  
>  Verwenden Sie zur Verbesserung der Leistung vollqualifizierte Objektnamen in der Anweisungszeichenfolge.  
  
 sp_executesql unterstützt das von der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeichenfolge getrennte Festlegen von Parameterwerten, wie dem folgenden Beispiel zu entnehmen ist.  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
  
/* Build the SQL string one time.*/  
SET @SQLString =  
     N'SELECT BusinessEntityID, NationalIDNumber, JobTitle, LoginID  
       FROM AdventureWorks2012.HumanResources.Employee   
       WHERE BusinessEntityID = @BusinessEntityID';  
SET @ParmDefinition = N'@BusinessEntityID tinyint';  
/* Execute the string with the first parameter value. */  
SET @IntVariable = 197;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
/* Execute the same string with the second parameter value. */  
SET @IntVariable = 109;  
EXECUTE sp_executesql @SQLString, @ParmDefinition,  
                      @BusinessEntityID = @IntVariable;  
```  
  
 Die Verwendung von Ausgabeparametern mit sp_executesql ist ebenfalls möglich. Im folgenden Beispiel wird eine Berufsbezeichnung aus der `AdventureWorks2012.HumanResources.Employee`-Tabelle abgerufen und im Ausgabeparameter `@max_title` zurückgegeben.  
  
```  
DECLARE @IntVariable int;  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @max_title varchar(30);  
  
SET @IntVariable = 197;  
SET @SQLString = N'SELECT @max_titleOUT = max(JobTitle)   
   FROM AdventureWorks2012.HumanResources.Employee  
   WHERE BusinessEntityID = @level';  
SET @ParmDefinition = N'@level tinyint, @max_titleOUT varchar(30) OUTPUT';  
  
EXECUTE sp_executesql @SQLString, @ParmDefinition, @level = @IntVariable, @max_titleOUT=@max_title OUTPUT;  
SELECT @max_title;  
```  
  
 Die Möglichkeit, Parameter in sp_executesql zu ersetzen, bietet die folgenden Vorteile gegenüber der Verwendung der EXECUTE-Anweisung, um eine Zeichenfolge auszuführen:  
  
-   Da sich der tatsächliche Text der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung in der sp_executesql-Zeichenfolge für die verschiedenen Ausführungen nicht ändert, findet der Abfrageoptimierer wahrscheinlich für die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung bei der zweiten Ausführung die Übereinstimmung mit dem Ausführungsplan, der für die erste Ausführung generiert wurde. Deshalb muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die zweite Anweisung nicht kompilieren.  
  
-   Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeichenfolge wird nur einmal erstellt.  
  
-   Der integer-Parameter wird im systemeigenen Format angegeben. Die Konvertierung in Unicode ist nicht erforderlich.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-executing-a-simple-select-statement"></a>A. Ausführen einer einfachen SELECT-Anweisung  
 In diesem Beispiel wird eine einfache `SELECT`-Anweisung erstellt und ausgeführt, die den eingebetteten Parameter `@level` enthält.  
  
```  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
          WHERE BusinessEntityID = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
### <a name="b-executing-a-dynamically-built-string"></a>B. Ausführen einer dynamisch erstellten Zeichenfolge  
 In folgenden Beispiel wird veranschaulicht, wie mithilfe von `sp_executesql` eine dynamisch erstellte Zeichenfolge ausgeführt wird. Mit der gespeicherten Prozedur im Beispiel werden Daten in mehrere Tabellen eingefügt, die zum Partitionieren der Jahresverkaufszahlen verwendet werden. Für jeden Monat des Jahres ist eine Tabelle mit dem folgenden Format vorhanden:  
  
```  
CREATE TABLE May1998Sales  
    (OrderID int PRIMARY KEY,  
    CustomerID int NOT NULL,  
    OrderDate  datetime NULL  
        CHECK (DATEPART(yy, OrderDate) = 1998),  
    OrderMonth int  
        CHECK (OrderMonth = 5),  
    DeliveryDate datetime  NULL,  
        CHECK (DATEPART(mm, OrderDate) = OrderMonth)  
    )  
```  
  
 Die gespeicherte Prozedur in diesem Beispiel erstellt eine `INSERT`-Anweisung dynamisch und führt sie aus, um neue Aufträge in die entsprechende Tabelle einzufügen. Im Beispiel wird das Bestelldatum verwendet, um den Namen der Tabelle zu erstellen, die die Daten enthalten soll. Anschließend wird dieser Name in eine `INSERT`-Anweisung integriert.  
  
> [!NOTE]  
>  Dies ist ein einfaches Beispiel für sp_executesql. Das Beispiel enthält keine Fehlerprüfung und keine Überprüfung etwaiger Geschäftsregeln, wie z. B. um sicherzustellen, dass Bestellnummern in den Tabellen nicht doppelt vorhanden sind.  
  
```  
CREATE PROCEDURE InsertSales @PrmOrderID INT, @PrmCustomerID INT,  
                 @PrmOrderDate DATETIME, @PrmDeliveryDate DATETIME  
AS  
DECLARE @InsertString NVARCHAR(500)  
DECLARE @OrderMonth INT  
  
-- Build the INSERT statement.  
SET @InsertString = 'INSERT INTO ' +  
       /* Build the name of the table. */  
       SUBSTRING( DATENAME(mm, @PrmOrderDate), 1, 3) +  
       CAST(DATEPART(yy, @PrmOrderDate) AS CHAR(4) ) +  
       'Sales' +  
       /* Build a VALUES clause. */  
       ' VALUES (@InsOrderID, @InsCustID, @InsOrdDate,' +  
       ' @InsOrdMonth, @InsDelDate)'  
  
/* Set the value to use for the order month because  
   functions are not allowed in the sp_executesql parameter  
   list. */  
SET @OrderMonth = DATEPART(mm, @PrmOrderDate)  
  
EXEC sp_executesql @InsertString,  
     N'@InsOrderID INT, @InsCustID INT, @InsOrdDate DATETIME,  
       @InsOrdMonth INT, @InsDelDate DATETIME',  
     @PrmOrderID, @PrmCustomerID, @PrmOrderDate,  
     @OrderMonth, @PrmDeliveryDate  
  
GO  
```  
  
 Das Verwenden von sp_executesql in dieser Prozedur ist effizienter als das Verwenden von EXECUTE zum Ausführen einer Zeichenfolge. Beim Verwenden von sp_executesql werden nur 12 Versionen der INSERT-Zeichenfolge generiert, nämlich eine Version für jede Monatstabelle. Mit EXECUTE ist jede INSERT-Zeichenfolge eindeutig, weil die Parameterwerte unterschiedlich sind. Obwohl beide Methoden die gleiche Anzahl von Batches generieren, ist es wegen der Ähnlichkeit der von sp_executesql generierten INSERT-Zeichenfolgen wahrscheinlicher, dass der Abfrageoptimierer die Ausführungspläne wiederverwendet.  
  
### <a name="c-using-the-output-parameter"></a>C. Verwenden des OUTPUT-Parameters  
 Im folgenden Beispiel wird ein `OUTPUT` Parameter zum Speichern von generierten Resultset die `SELECT` -Anweisung in der `@SQLString` Parameter. Zwei `SELECT` Anweisungen werden dann ausgeführt, die den Wert des verwenden die `OUTPUT` Parameter.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SQLString nvarchar(500);  
DECLARE @ParmDefinition nvarchar(500);  
DECLARE @SalesOrderNumber nvarchar(25);  
DECLARE @IntVariable int;  
SET @SQLString = N'SELECT @SalesOrderOUT = MAX(SalesOrderNumber)  
    FROM Sales.SalesOrderHeader  
    WHERE CustomerID = @CustomerID';  
SET @ParmDefinition = N'@CustomerID int,  
    @SalesOrderOUT nvarchar(25) OUTPUT';  
SET @IntVariable = 22276;  
EXECUTE sp_executesql  
    @SQLString  
    ,@ParmDefinition  
    ,@CustomerID = @IntVariable  
    ,@SalesOrderOUT = @SalesOrderNumber OUTPUT;  
-- This SELECT statement returns the value of the OUTPUT parameter.  
SELECT @SalesOrderNumber;  
-- This SELECT statement uses the value of the OUTPUT parameter in  
-- the WHERE clause.  
SELECT OrderDate, TotalDue  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderNumber = @SalesOrderNumber;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-executing-a-simple-select-statement"></a>D. Ausführen einer einfachen SELECT-Anweisung  
 In diesem Beispiel wird eine einfache `SELECT`-Anweisung erstellt und ausgeführt, die den eingebetteten Parameter `@level` enthält.  
  
```  
-- Uses AdventureWorks  
  
EXECUTE sp_executesql   
          N'SELECT * FROM AdventureWorksPDW2012.dbo.DimEmployee   
          WHERE EmployeeKey = @level',  
          N'@level tinyint',  
          @level = 109;  
```  
  
 Weitere Beispiele finden Sie unter [Sp_executesql (Transact-SQL)](http://msdn.microsoft.com/library/ms188001.aspx).  
  
## <a name="see-also"></a>Siehe auch  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
