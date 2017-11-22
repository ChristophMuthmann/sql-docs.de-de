---
title: WIEDERHOLEN SIE DEN... CATCH (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BEGIN_TRY_TSQL
- BEGIN_CATCH_TSQL
- TRY
- BEGIN TRY
- TRY_TSQL
- BEGIN CATCH
dev_langs: TSQL
helpviewer_keywords:
- BEGIN CATCH statement
- uncommittable transactions
- errors [SQL Server], TRY...CATCH
- TRY block [SQL Server]
- XACT_STATE function
- TRY...CATCH [SQL Server]
- BEGIN TRY statement
- CATCH block
ms.assetid: 248df62a-7334-4bca-8262-235a28f4b07f
caps.latest.revision: "79"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6bf90e58d4956877786dd0d247653e8a99480c67
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="trycatch-transact-sql"></a>TRY...CATCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Implementiert die Fehlerbehandlung für [!INCLUDE[tsql](../../includes/tsql-md.md)], die Ähnlichkeiten mit der Ausnahmebehandlung in den Sprachen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++ hat. Eine Gruppe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen kann in einen TRY-Block eingeschlossen werden. Wenn innerhalb des TRY-Blocks ein Fehler auftritt, wird die Steuerung an eine andere Gruppe von Anweisungen innerhalb eines CATCH-Blocks übergeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
BEGIN TRY  
     { sql_statement | statement_block }  
END TRY  
BEGIN CATCH  
     [ { sql_statement | statement_block } ]  
END CATCH  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *sql_statement*  
 Eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung.  
  
 *statement_block*  
 Eine beliebige Gruppe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem Batch oder in einem BEGIN…END-Block.  
  
## <a name="remarks"></a>Hinweise  
 Ein TRY…CATCH-Konstrukt fängt alle Ausführungsfehler ab, deren Schweregrad größer als 10 ist und durch die die Datenbankverbindung nicht geschlossen wird.  
  
 Auf einen TRY-Block muss direkt ein dazugehöriger CATCH-Block folgen. Werden andere Anweisungen zwischen die END TRY- und BEGIN CATCH-Anweisungen eingeschlossen, wird dadurch ein Syntaxfehler generiert.  
  
 Ein TRY…CATCH-Konstrukt darf sich nicht über mehrere Batches erstrecken. Ein TRY…CATCH-Konstrukt darf sich nicht über mehrere Blöcke von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen erstrecken. So darf sich ein TRY…CATCH-Konstrukt beispielsweise nicht über zwei BEGIN…END-Blöcke von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen und nicht über ein IF…ELSE-Konstrukt erstrecken.  
  
 Ist der Code in einem TRY-Block fehlerfrei, wird nach Abschluss der letzten Anweisung im TRY-Block die Steuerung an die Anweisung übergeben, die direkt auf die dazugehörige END CATCH-Anweisung folgt. Enthält der in einen TRY-Block eingeschlossene Code einen Fehler, wird die Steuerung an die erste Anweisung im dazugehörigen CATCH-Block übergeben. Ist die END CATCH-Anweisung die letzte Anweisung in einer gespeicherten Prozedur oder in einem Trigger, wird die Steuerung wieder an die Anweisung zurückgegeben, die die gespeicherte Prozedur aufgerufen bzw. den Trigger ausgelöst hat.  
  
 Wenn die Ausführung des Codes im CATCH-Block abgeschlossen ist, wird die Steuerung an die Anweisung übergeben, die direkt auf die END CATCH-Anweisung folgt. Fehler, die von einem CATCH-Block aufgefangen werden, werden nicht an die aufrufende Anwendung zurückgegeben. Falls Fehlerinformationen an die Anwendung zurückgegeben werden sollen, müssen im Code im CATCH-Block bestimmte Mechanismen dafür verwendet werden, z. B. SELECT-Resultsets oder die RAISERROR-Anweisung und die PRINT-Anweisung.  
  
 TRY…CATCH-Konstrukte können geschachtelt werden. Entweder ein TRY-Block oder ein CATCH-Block kann geschachtelte TRY…CATCH-Konstrukte enthalten. So kann beispielsweise ein CATCH-Block ein eingebettetes TRY…CATCH-Konstrukt enthalten, das Fehler behandelt, die vom CATCH-Code festgestellt werden.  
  
 Fehler, die in einem CATCH-Block festgestellt werden, werden wie alle anderen Fehler behandelt. Wenn der CATCH-Block ein geschachteltes TRY…CATCH-Konstrukt enthält, wird bei jedem Fehler im geschachtelten TRY-Block die Steuerung an den geschachtelten CATCH-Block übergeben. Ist kein geschachteltes TRY…CATCH-Konstrukt vorhanden, wird der Fehler an den Aufrufer zurückgegeben.  
  
 TRY…CATCH-Konstrukte können nicht behandelte Fehler aus gespeicherten Prozeduren oder Triggern auffangen, die mit dem Code im TRY-Block ausgeführt werden. Alternativ dazu können die gespeicherten Prozeduren oder Trigger eigene TRY…CATCH-Konstrukte enthalten, die vom Code generierte Fehler behandeln. Wenn beispielsweise ein TRY-Block eine gespeicherte Prozedur ausführt und in dieser ein Fehler auftritt, dann gibt es folgende Möglichkeiten für die Behandlung des Fehlers:  
  
-   Wenn die gespeicherte Prozedur kein eigenes TRY…CATCH-Konstrukt enthält, übergibt der Fehler die Steuerung an den CATCH-Block, der mit dem TRY-Block verknüpft ist, der die EXECUTE-Anweisung enthält.  
  
-   Wenn die gespeicherte Prozedur ein TRY…CATCH-Konstrukt enthält, übergibt der Fehler die Steuerung an den CATCH-Block in der gespeicherten Prozedur. Wenn die Ausführung des Codes im CATCH-Block abgeschlossen ist, wird die Steuerung an die Anweisung zurückgegeben, die direkt auf die EXECUTE-Anweisung folgt, von der die gespeicherte Prozedur aufgerufen wurde.  
  
 GOTO-Anweisungen können nicht verwendet werden, um einen TRY- oder CATCH-Block einzugeben. GOTO-Anweisungen können verwendet werden, um innerhalb eines TRY- oder CATCH-Blocks zu einer Marke zu springen oder um einen TRY- oder CATCH-Block zu verlassen.  
  
 Das TRY…CATCH-Konstrukt kann nicht in einer benutzerdefinierten Funktion verwendet werden.  
  
## <a name="retrieving-error-information"></a>Abrufen von Fehlerinformationen  
 Im Bereich eines CATCH-Blocks können folgende Systemfunktionen verwendet werden, um Informationen zu dem Fehler abzurufen, der zur Ausführung des CATCH-Blocks geführt hat:  
  
-   [ERROR_NUMBER()](../../t-sql/functions/error-number-transact-sql.md) gibt die Anzahl der Fehler zurück.  
  
-   [ERROR_SEVERITY()](../../t-sql/functions/error-severity-transact-sql.md) gibt den Schweregrad zurück.  
  
-   [ERROR_STATE()](../../t-sql/functions/error-state-transact-sql.md) gibt die fehlerzustandsnummer zurück.  
  
-   [ERROR_PROCEDURE()](../../t-sql/functions/error-procedure-transact-sql.md) gibt den Namen der gespeicherten Prozedur oder des Triggers zurück, in dem der Fehler aufgetreten ist.  
  
-   [ERROR_LINE()](../../t-sql/functions/error-line-transact-sql.md) gibt die Nummer der Zeile in der Routine, die den Fehler verursacht hat.  
  
-   [ERROR_MESSAGE()](../../t-sql/functions/error-message-transact-sql.md) gibt den vollständigen Text der Fehlermeldung. Der Text umfasst die Werte, die für alle ersetzbaren Parameter angegeben werden, wie z. B. Längen, Objektnamen oder Zeitangaben.  
  
 Diese Funktionen geben NULL zurück, wenn sie außerhalb des Bereichs eines CATCH-Blocks aufgerufen werden. Fehlerinformationen können mithilfe dieser Funktionen an beliebiger Stelle im Bereich des CATCH-Blocks abgerufen werden. Das folgende Skript zeigt beispielsweise eine gespeicherte Prozedur, die Fehlerbehandlungsfunktionen umfasst. Im `CATCH`-Block eines `TRY…CATCH`-Konstrukts wird die gespeicherte Prozedur aufgerufen, und Informationen zum Fehler werden zurückgegeben.  
  
```t-sql  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_GetErrorInfo', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_GetErrorInfo;  
GO  
  
-- Create procedure to retrieve error information.  
CREATE PROCEDURE usp_GetErrorInfo  
AS  
SELECT  
    ERROR_NUMBER() AS ErrorNumber  
    ,ERROR_SEVERITY() AS ErrorSeverity  
    ,ERROR_STATE() AS ErrorState  
    ,ERROR_PROCEDURE() AS ErrorProcedure  
    ,ERROR_LINE() AS ErrorLine  
    ,ERROR_MESSAGE() AS ErrorMessage;  
GO  
  
BEGIN TRY  
    -- Generate divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    -- Execute error retrieval routine.  
    EXECUTE usp_GetErrorInfo;  
END CATCH;   
```  
  
 Der Fehler\_ \* Funktionen funktionieren auch in einem `CATCH` -Block ein [systemintern kompilierte gespeicherte Prozedur](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="errors-unaffected-by-a-trycatch-construct"></a>Fehler, auf die sich ein TRY…CATCH-Konstrukt nicht auswirkt  
 TRY…CATCH-Konstrukte fangen folgende Bedingungen nicht auf:  
  
-   Warnungen oder Informationsmeldungen mit einem Schweregrad von 10 oder niedriger.  
  
-   Fehler mit einem Schweregrad von 20 oder höher, die dazu führen, dass die Verarbeitung des [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Tasks für die Sitzung beendet wird. Wenn ein Fehler mit einem Schweregrad von 20 oder höher auftritt und die Datenbankverbindung nicht unterbrochen wird, wird der Fehler durch TRY…CATCH behandelt.  
  
-   Warnungen, z. B. Clientunterbrechungsanforderungen oder unterbrochene Clientverbindungen.  
  
-   Wenn die Sitzung von einem Systemadministrator mit der KILL-Anweisung beendet wird.  
  
 Die folgenden Fehlertypen werden von einem CATCH-Block nicht behandelt, wenn sie auf der gleichen Ausführungsebene wie das TRY…CATCH-Konstrukt auftreten:  
  
-   Kompilierungsfehler, z. B. Syntaxfehler, die die Ausführung eines Batches verhindern.  
  
-   Fehler, die bei der Neukompilierung auf Anweisungsebene auftreten, beispielsweise Fehler bei der Objektnamensauflösung, die aufgrund einer verzögerten Namensauflösung nach der Kompilierung auftreten.  
  
 Diese Fehler werden auf die Ebene zurückgegeben, auf der der Batch, die gespeicherte Prozedur oder der Trigger ausgeführt wurden.  
  
 Tritt ein Fehler bei der Kompilierung oder Neukompilierung auf Anweisungsebene auf einer niedrigeren Ausführungsebene (z. B. bei Ausführung von sp_executesql oder einer benutzerdefinierten gespeicherten Prozedur) innerhalb des TRY-Blocks auf, befindet sich der Fehler auf einer niedrigeren Ebene als das TRY…CATCH-Konstrukt und wird vom dazugehörigen CATCH-Block behandelt.  
  
 Das folgende Beispiel zeigt, wie ein Fehler bei der Objektnamensauflösung, der von einer `SELECT`-Anweisung generiert wurde, nicht vom `TRY…CATCH`-Konstrukt erfasst wurde. Er wird jedoch vom `CATCH`-Block erfasst, wenn dieselbe `SELECT`-Anweisung innerhalb einer gespeicherten Prozedur ausgeführt wird.  
  
```t-sql  
BEGIN TRY  
    -- Table does not exist; object name resolution  
    -- error not caught.  
    SELECT * FROM NonexistentTable;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
       ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH  
```  
  
 Der Fehler wird nicht erfasst, und die Steuerung wird vom `TRY…CATCH`-Konstrukt an die nächsthöhere Ebene weitergegeben.  
  
 Das Ausführen der `SELECT`-Anweisung innerhalb einer gespeicherten Prozedur führt dazu, dass der Fehler auf einer Ebene unter dem `TRY`-Block auftritt. Der Fehler wird vom `TRY…CATCH`-Konstrukt behandelt.  
  
```t-sql  
-- Verify that the stored procedure does not exist.  
IF OBJECT_ID ( N'usp_ExampleProc', N'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that will cause an   
-- object resolution error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT * FROM NonexistentTable;  
GO  
  
BEGIN TRY  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
```  
  
## <a name="uncommittable-transactions-and-xactstate"></a>Nicht commitfähige Transaktionen und XACT_STATE  
 Wenn ein Fehler, der in einem TRY-Block generiert wurde, dazu führt, dass der Status der aktuellen Transaktion ungültig wird, dann wird die Transaktion als nicht commitfähige Transaktion klassifiziert. Ein Fehler, der außerhalb eines TRY-Blocks normalerweise zur Beendigung einer Transaktion führt, hat bei Auftreten innerhalb eines TRY-Blocks zur Folge, dass eine Transaktion zu einer nicht commitfähigen Transaktion wird. Eine nicht commitfähige Transaktion kann nur Leseoperationen oder ROLLBACK TRANSACTION durchführen. Die Transaktion kann keine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen ausführen, die eine Schreiboperation oder COMMIT TRANSACTION generieren. Die XACT_STATE-Funktion gibt den Wert -1 zurück, wenn eine Transaktion als nicht commitfähige Transaktion klassifiziert wurde. Nach Abschluss einer Batchausführung wird für alle aktiven nicht commitfähigen Transaktionen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] ein Rollback ausgeführt. Falls keine Fehlermeldung gesendet wurde, als die Transaktion in den nicht commitfähigen Status überging, wird bei Abschluss des Batches eine Fehlermeldung an die Clientanwendung gesendet. Auf diese Weise wird angezeigt, dass eine nicht commitfähige Transaktion erkannt und ein Rollback für sie ausgeführt wurde.  
  
 Weitere Informationen zu nicht commitfähigen Transaktionen und zur XACT_STATE-Funktion finden Sie unter [XACT_STATE &#40; Transact-SQL &#41; ](../../t-sql/functions/xact-state-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-trycatch"></a>A. Verwenden von TRY…CATCH  
 Das folgende Beispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 (null) generiert. Der Fehler führt dazu, dass die Ausführung zum dazugehörigen `CATCH`-Block wechselt.  
  
```t-sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-trycatch-in-a-transaction"></a>B. Verwenden von TRY…CATCH in einer Transaktion  
 Das folgende Beispiel zeigt die Funktionsweise eines `TRY…CATCH`-Blocks innerhalb einer Transaktion. Die Anweisung innerhalb des `TRY`-Blocks generiert einen Fehler aufgrund einer Einschränkungsverletzung.  
  
```t-sql  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Generate a constraint violation error.  
    DELETE FROM Production.Product  
    WHERE ProductID = 980;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
### <a name="c-using-trycatch-with-xactstate"></a>C. Verwenden von TRY…CATCH mit XACT_STATE  
 Das folgende Beispiel zeigt, wie das `TRY…CATCH`-Konstrukt zur Behandlung von Fehlern verwendet wird, die innerhalb einer Transaktion auftreten. Über die `XACT_STATE`-Funktion wird bestimmt, ob für die Transaktion ein Commit oder ein Rollback ausgeführt werden soll. In diesem Beispiel hat `SET XACT_ABORT` den Wert `ON`. Dies bewirkt, dass die Transaktion nach dem Fehler aufgrund einer Einschränkungsverletzung nicht commitfähig ist.  
  
```t-sql  
-- Check to see whether this stored procedure exists.  
IF OBJECT_ID (N'usp_GetErrorInfo', N'P') IS NOT NULL  
    DROP PROCEDURE usp_GetErrorInfo;  
GO  
  
-- Create procedure to retrieve error information.  
CREATE PROCEDURE usp_GetErrorInfo  
AS  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_LINE () AS ErrorLine  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
GO  
  
-- SET XACT_ABORT ON will cause the transaction to be uncommittable  
-- when the constraint violation occurs.   
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the DELETE statement succeeds, commit the transaction.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Execute error retrieval routine.  
    EXECUTE usp_GetErrorInfo;  
  
    -- Test XACT_STATE:  
        -- If 1, the transaction is committable.  
        -- If -1, the transaction is uncommittable and should   
        --     be rolled back.  
        -- XACT_STATE = 0 means that there is no transaction and  
        --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT  
            N'The transaction is in an uncommittable state.' +  
            'Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is committable.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT  
            N'The transaction is committable.' +  
            'Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-trycatch"></a>D. Verwenden von TRY…CATCH  
 Das folgende Beispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 (null) generiert. Der Fehler führt dazu, dass die Ausführung zum dazugehörigen `CATCH`-Block wechselt.  
  
```t-sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [THROW &#40; Transact-SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Datenbankmodulfehlern](../../relational-databases/errors-events/database-engine-error-severities.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [GOTO &#40; Transact-SQL &#41;](../../t-sql/language-elements/goto-transact-sql.md)   
 [GESTARTET... END &#40; Transact-SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [XACT_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/xact-state-transact-sql.md)   
 [SET XACT_ABORT &#40; Transact-SQL &#41;](../../t-sql/statements/set-xact-abort-transact-sql.md)  
  
  

