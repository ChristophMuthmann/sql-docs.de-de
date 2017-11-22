---
title: "Zurückgeben von Daten von einer gespeicherten Prozedur | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 785491c26c65252756c49e7b405d10cdbece831c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="return-data-from-a-stored-procedure"></a>Zurückgeben von Daten von einer gespeicherten Prozedur
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Zurückgeben von Daten von einer gespeicherten Prozedur](https://msdn.microsoft.com/en-US/library/ms188655(SQL.120).aspx).

  Es gibt zwei Methoden, Resultsets oder Daten von einer Prozedur an ein aufrufendes Programm zurückzugeben: Ausgabeparameter und Rückgabecodes. Dieses Thema enthält Informationen zu beiden Ansätzen.  
  
## <a name="returning-data-using-an-output-parameter"></a>Zurückgeben von Daten mithilfe eines OUTPUT-Parameters  
 Wenn Sie in der Prozedurdefinition für einen Parameter das Schlüsselwort OUTPUT angeben, kann die Prozedur den aktuellen Wert des Parameters an das aufrufende Programm zurückgeben, wenn die Prozedur beendet wird. Um den Wert des Parameters in einer Variablen zu speichern, die in dem aufrufenden Programm verwendet werden kann, muss das aufrufende Programm beim Ausführen der Prozedur das Schlüsselwort OUTPUT verwenden. Weitere Informationen dazu, welche Datentypen als Ausgabeparameter verwendet werden können, finden Sie unter [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
### <a name="examples-of-output-parameter"></a>Beispiele für Ausgabeparameter  
 Das folgende Beispiel zeigt eine Prozedur mit einem Eingabe- und einem Ausgabeparameter. Der `@SalesPerson` -Parameter würde einen vom aufrufenden Programm angegebenen Eingabewert empfangen. Die SELECT-Anweisung verwendet den im Eingabeparameter übergebenen Wert, um den richtigen `SalesYTD` -Wert abzurufen. Die SELECT-Anweisung weist den Wert auch dem `@SalesYTD` -Ausgabeparameter zu, der den Wert an das aufrufende Programm zurückgibt, wenn die Prozedur beendet wird.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 Im folgenden Beispiel wird die im ersten Beispiel erstellte Prozedur aufgerufen und der Ausgabewert gespeichert, der von der aufgerufenen Prozedur in der `@SalesYTD` -Variablen, die eine lokale Variable des aufrufenden Programm ist, zurückgegeben wurde.  
  
```  
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 Eingabewerte können auch als Ausgabeparameter angegeben werden, wenn die Prozedur ausgeführt wird. Auf diese Weise kann die Prozedur einen Wert von dem aufrufenden Programm erhalten, diesen Wert ändern oder andere Operationen mit dem Wert ausführen und den neuen Wert anschließend an das aufrufende Programm zurückgeben. In dem zuvor aufgeführten Beispiel kann der `@SalesYTDBySalesPerson` -Variablen ein Wert zugewiesen werden, bevor das Programm die `Sales.uspGetEmployeeSalesYTD` -Prozedur aufruft. Das EXECUTE-Anweisung übergibt in diesem Fall den `@SalesYTDBySalesPerson` -Variablenwert an den OUTPUT-Parameter `@SalesYTD` . Im Prozedurtext kann der Wert zu Berechnungen verwendet werden, die einen neuen Wert generieren. Der neue Wert wird über den OUTPUT-Parameter aus der Prozedur heraus weitergereicht, wobei der Wert in der `@SalesYTDBySalesPerson` -Variablen aktualisiert wird, wenn die Prozedur beendet wird. Dies wird häufig als "Fähigkeit zur Verweisübergabe" bezeichnet.  
  
 Wenn beim Aufruf einer Prozedur OUTPUT für einen Parameter angegeben wird und dieser Parameter in der Prozedurdefinition nicht mithilfe von OUTPUT definiert worden ist, dann wird eine Fehlermeldung ausgegeben. Sie können eine Prozedur mit Ausgabeparameter ausführen, ohne OUTPUT beim Ausführen der Prozedur anzugeben. In diesem Fall wird kein Fehler zurückgegeben; der Ausgabewert kann jedoch nicht in dem aufrufenden Programm verwendet werden.  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>Verwenden des Cursor-Datentyps in OUTPUT-Parametern  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Prozeduren können den Datentyp **cursor** nur für OUTPUT-Parameter verwenden. Wenn der **cursor** -Datentyp für einen Parameter angegeben wird, müssen in der Prozedurdefinition sowohl das Schlüsselwort VARYING als auch das Schlüsselwort OUTPUT für diesen Parameter angegeben werden. Für einen Parameter kann nur das Schlüsselwort OUTPUT angegeben werden. Wenn allerdings das Schlüsselwort VARYING in der Parameterdeklaration angegeben worden ist, müssen der Datentyp **cursor** verwendet und zudem das Schlüsselwort OUTPUT angegeben werden.  
  
> [!NOTE]  
>  Der Datentyp **cursor** kann nicht durch Datenbank-APIs, wie z. B. OLE DB, ODBC, ADO und DB-Library, an Anwendungsvariablen gebunden werden. Da OUTPUT-Parameter gebunden werden müssen, bevor eine Anwendung eine Prozedur ausführen kann, können Prozeduren mit **cursor** -OUTPUT-Parametern nicht aus den Datenbank-APIs heraus aufgerufen werden. Diese Prozeduren können von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Batches, Prozeduren oder Triggern heraus aufgerufen werden, wenn die **cursor** -OUTPUT-Variable einer lokalen [!INCLUDE[tsql](../../includes/tsql-md.md)] - **cursor** -Variablen zugewiesen wird.  
  
### <a name="rules-for-cursor-output-parameters"></a>Regeln für Cursorausgabeparameter  
 Folgende Regeln gelten für Ausgabeparameter vom **cursor** -Datentyp, wenn die Prozedur ausgeführt wird:  
  
-   Bei einem Vorwärtscursor werden im Resultset des Cursors nur die Zeilen zurückgegeben, die sich am Ende der Ausführung der Prozedur an und hinter der Cursorposition befinden. Beispiel:  
  
    -   Ein nicht bildlauffähiger Cursor wird in einer Prozedur für ein Resultset namens RS geöffnet, das 100 Zeilen umfasst.  
  
    -   Die Prozedur ruft die ersten 5 Zeilen des Resultsets RS ab.  
  
    -   Die Prozedur gibt das Resultset an den Aufrufer zurück.  
  
    -   Das Resultset RS, das an den Aufrufer zurückgegeben wird, besteht aus den Zeilen 6 bis 100 von RS, und der Cursor im Aufrufer wird vor der ersten Zeile von RS positioniert.  
  
-   Wenn ein Vorwärtscursor beim Beenden der Prozedur vor der ersten Zeile positioniert ist, wird das gesamte Resultset an den aufrufenden Batch, die aufrufende Prozedur oder den aufrufenden Trigger zurückgegeben. Nach der Rückgabe wird der Cursor vor der ersten Zeile positioniert.  
  
-   Wenn ein Vorwärtscursor beim Beenden der Prozedur hinter dem Ende der letzten Zeile positioniert ist, wird ein leeres Resultset an den aufrufenden Batch, die aufrufende Prozedur oder den aufrufenden Trigger zurückgegeben.  
  
    > [!NOTE]  
    >  Ein leeres Resultset ist nicht das Gleiche wie ein NULL-Wert.  
  
-   Bei einem bildlauffähigen Cursor werden beim Beenden der Prozedur alle Zeilen im Resultset an den aufrufenden Batch, die aufrufende gespeicherte Prozedur oder den aufrufenden Trigger zurückgegeben. Nach der Rückgabe behält der Cursor die Position des letzten in der Prozedur ausgeführten Abrufs bei.  
  
-   Bei allen Cursortypen wird ein NULL-Wert an den aufrufenden Batch, die aufrufende Prozedur oder den aufrufenden Trigger zurückgegeben, wenn der Cursor geschlossen ist. Dies ist auch dann der Fall, wenn ein Cursor einem Parameter zugewiesen ist, dieser Cursor jedoch nie geöffnet wird.  
  
    > [!NOTE]  
    >  Der geschlossene Status ist nur zum Zeitpunkt der Rückgabe relevant. Beispielsweise ist es zulässig, einen Cursor während eines Teils der Prozedur zu schließen, ihn zu einem späteren Zeitpunkt in der Prozedur wieder zu öffnen und das Resultset dieses Cursors an den aufrufenden Batch, die aufrufende Prozedur oder den aufrufenden Trigger zurückzugeben.  
  
### <a name="examples-of-cursor-output-parameters"></a>Beispiele für Cursorausgabeparameter  
 Im folgenden Beispiel wird eine gespeicherte Prozedur mit einem Ausgabeparameter `@currency_cursor` vom Datentyp **cursor** erstellt. Die Prozedur wird anschließend in einem Batch aufgerufen.  
  
 Zuerst wird die Prozedur erstellt, die einen Cursor für die Currency-Tabelle deklariert und dann öffnet.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 Als Nächstes wird ein Batch ausgeführt, der eine lokale Cursorvariable deklariert, die Prozedur ausführt, um der lokalen Variablen den Cursor zuzuweisen, und dann die Zeilen aus dem Cursor abruft.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>Zurückgeben von Daten mithilfe eines Rückgabecodes  
 Eine Prozedur kann einen ganzzahligen Wert zurückgeben, der als Rückgabecode bezeichnet wird, um den Ausführungsstatus einer Prozedur anzuzeigen. Sie geben den Rückgabecode für eine Prozedur mithilfe der RETURN-Anweisung an. Wie schon die OUTPUT-Parameter müssen Sie auch den Rückgabecode in einer Variablen speichern, wenn die Prozedur ausgeführt wird, damit der Wert des Rückgabecodes in dem aufrufenden Programm verwendet werden kann. So wird z. B. in den folgenden Codezeilen die Zuweisungsvariable `@result` vom Datentyp **int** verwendet, um den Rückgabecode der Prozedur `my_proc`zu speichern:  
  
```  
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 Rückgabecodes werden häufig in Blöcken zur Ablaufsteuerung innerhalb von Prozeduren verwendet, um den Wert des Rückgabecodes für sämtliche Fehler festzulegen. Sie können die @@ERROR-Funktion nach einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung verwenden, um festzustellen, ob während der Ausführung der Anweisung ein Fehler aufgetreten ist.  
  
### <a name="examples-of-return-codes"></a>Beispiele für Rückgabecodes  
 Das folgende Beispiel zeigt die `usp_GetSalesYTD` -Prozedur mit Fehlerbehandlung, in der für verschiedene Fehler spezielle Rückgabecodewerte festgelegt sind. In der Tabelle werden die ganzzahligen Werte aufgeführt, die die Prozedur den einzelnen möglichen Fehlern zuweist, sowie die Bedeutung der einzelnen Werte.  
  
|Rückgabecodewert|Bedeutung|  
|-----------------------|-------------|  
|0|Erfolgreiche Ausführung|  
|1|Der erforderliche Parameterwert ist nicht angegeben.|  
|2|Der angegebene Parameterwert ist ungültig.|  
|3|Beim Abrufen der Vertriebswerte ist ein Fehler aufgetreten.|  
|4|Für diesen Vertriebsmitarbeiter wurde ein Vertriebswert von NULL gefunden.|  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 Im folgenden Beispiel wird ein Programm erstellt, das die von der `usp_GetSalesYTD` -Prozedur zurückgegebenen Rückgabecodes verarbeitet.  
  
```  
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'EERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [Cursor](../../relational-databases/cursors.md)   
 [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
