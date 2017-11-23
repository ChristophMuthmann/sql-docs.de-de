---
title: SAVE TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SAVE
- SAVE_TSQL
- SAVE_TRANSACTION_TSQL
- SAVE TRANSACTION
dev_langs: TSQL
helpviewer_keywords:
- rolling back transactions, SAVE TRANSACTION
- SAVE TRANSACTION statement
- transactions [SQL Server], rolling back
- marking transactions [SQL Server]
- savepoints [SQL Server]
- marked transactions [SQL Server], SAVE TRANSACTION statement
- duplicate savepoints
ms.assetid: b953c3f1-f96d-42f1-95a2-30e314292b35
caps.latest.revision: "53"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a3a252fced11410718d1bcdbc82d9bb199585745
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="save-transaction-transact-sql"></a>SAVE TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Legt einen Sicherungspunkt in einer Transaktion fest.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
.|  
 ## <a name="syntax"></a>Syntax  
  
```  
  
SAVE { TRAN | TRANSACTION } { savepoint_name | @savepoint_variable }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *savepoint_name*  
 Dies ist der Name, der dem Sicherungspunkt zugewiesen ist. Sicherungspunktnamen müssen den Regeln für Bezeichner entsprechen, sind jedoch auf 32 Zeichen begrenzt. *Transaction_name* wird immer Groß-/ Kleinschreibung, auch wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist nicht in der Groß-/Kleinschreibung beachtet.  
  
 @*savepoint_variable*  
 Ist der Name einer benutzerdefinierten Variablen, die einen gültigen Sicherungspunktnamen enthält. Die Variable muss deklariert werden, mit einem **Char**, **Varchar**, **Nchar**, oder **Nvarchar** -Datentyp. Es können mehr als 32 Zeichen an die Variable übergeben werden, jedoch werden nur die ersten 32 Zeichen verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Ein Benutzer kann einen Sicherungspunkt oder Marker innerhalb einer Transaktion festlegen. Der Sicherungspunkt definiert die Position, zu der eine Transaktion zurückkehren kann, wenn ein Teil der Transaktion bedingt abgebrochen wird. Falls für eine Transaktion ein Rollback bis zu einem Sicherungspunkt ausgeführt wird, muss dieser abgeschlossen werden, bei Bedarf mit mehreren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen und einer COMMIT TRANSACTION-Anweisung, oder ganz abgebrochen werden,  indem ein Rollback der Transaktion zurück zum Anfang ausgeführt wird. Verwenden Sie zum Abbrechen der gesamten Transaktion, die Syntax ROLLBACK TRANSACTION *Transaction_name*. Alle Anweisungen oder Prozeduren der Transaktion werden rückgängig gemacht.  
  
 Doppelte Sicherungspunktnamen sind in einer Transaktion zulässig. Eine ROLLBACK TRANSACTION-Anweisung, die den Sicherungspunktnamen angibt, führt jedoch nur ein Rollback der Transaktion bis zur letzten SAVE TRANSACTION-Anweisung mit diesem Namen aus.  
  
 SAVE TRANSACTION wird nicht in verteilten Transaktionen unterstützt, die explizit mit BEGIN DISTRIBUTED TRANSACTION gestartet wurden oder aus einer lokalen Transaktion stammen.  
  
> [!IMPORTANT]  
>  Mit einer ROLLBACK TRANSACTION-Anweisung, in der savepoint_name angegeben ist, werden alle Sperren freigegeben, die außerhalb des Sicherungspunkts aktiviert werden, mit Ausnahme von Ausweitungen und Konvertierungen. Diese Sperren werden nicht aufgehoben, und sie werden nicht in ihren vorherigen Sperrmodus zurückkonvertiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Verwenden eines Sicherungspunkts für eine Transaktion zur Ausführung eines Rollbacks nur der Änderungen veranschaulicht, die von einer gespeicherten Prozedur vorgenommen werden, wenn eine aktive Transaktion vor der Ausführung der gespeicherten Prozedur gestartet wird.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
           WHERE name = N'SaveTranExample')  
    DROP PROCEDURE SaveTranExample;  
GO  
CREATE PROCEDURE SaveTranExample  
    @InputCandidateID INT  
AS  
    -- Detect whether the procedure was called  
    -- from an active transaction and save  
    -- that for later use.  
    -- In the procedure, @TranCounter = 0  
    -- means there was no active transaction  
    -- and the procedure started one.  
    -- @TranCounter > 0 means an active  
    -- transaction was started before the   
    -- procedure was called.  
    DECLARE @TranCounter INT;  
    SET @TranCounter = @@TRANCOUNT;  
    IF @TranCounter > 0  
        -- Procedure called when there is  
        -- an active transaction.  
        -- Create a savepoint to be able  
        -- to roll back only the work done  
        -- in the procedure if there is an  
        -- error.  
        SAVE TRANSACTION ProcedureSave;  
    ELSE  
        -- Procedure must start its own  
        -- transaction.  
        BEGIN TRANSACTION;  
    -- Modify database.  
    BEGIN TRY  
        DELETE HumanResources.JobCandidate  
            WHERE JobCandidateID = @InputCandidateID;  
        -- Get here if no errors; must commit  
        -- any transaction started in the  
        -- procedure, but not commit a transaction  
        -- started before the transaction was called.  
        IF @TranCounter = 0  
            -- @TranCounter = 0 means no transaction was  
            -- started before the procedure was called.  
            -- The procedure must commit the transaction  
            -- it started.  
            COMMIT TRANSACTION;  
    END TRY  
    BEGIN CATCH  
        -- An error occurred; must determine  
        -- which type of rollback will roll  
        -- back only the work done in the  
        -- procedure.  
        IF @TranCounter = 0  
            -- Transaction started in procedure.  
            -- Roll back complete transaction.  
            ROLLBACK TRANSACTION;  
        ELSE  
            -- Transaction started before procedure  
            -- called, do not roll back modifications  
            -- made before the procedure was called.  
            IF XACT_STATE() <> -1  
                -- If the transaction is still valid, just  
                -- roll back to the savepoint set at the  
                -- start of the stored procedure.  
                ROLLBACK TRANSACTION ProcedureSave;  
                -- If the transaction is uncommitable, a  
                -- rollback to the savepoint is not allowed  
                -- because the savepoint rollback writes to  
                -- the log. Just return to the caller, which  
                -- should roll back the outer transaction.  
  
        -- After the appropriate rollback, echo error  
        -- information to the caller.  
        DECLARE @ErrorMessage NVARCHAR(4000);  
        DECLARE @ErrorSeverity INT;  
        DECLARE @ErrorState INT;  
  
        SELECT @ErrorMessage = ERROR_MESSAGE();  
        SELECT @ErrorSeverity = ERROR_SEVERITY();  
        SELECT @ErrorState = ERROR_STATE();  
  
        RAISERROR (@ErrorMessage, -- Message text.  
                   @ErrorSeverity, -- Severity.  
                   @ErrorState -- State.  
                   );  
    END CATCH  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [XACT_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/xact-state-transact-sql.md)  
  
  
