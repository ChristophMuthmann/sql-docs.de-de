---
title: ERROR_PROCEDURE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_PROCEDURE_TSQL
- ERROR_PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_PROCEDURE function
- messages [SQL Server], trigger where occurred
- errors [SQL Server], stored procedure where occurred
- TRY...CATCH [SQL Server]
- CATCH block
- messages [SQL Server], stored procedure where occurred
- errors [SQL Server], trigger where occurred
ms.assetid: b81edbf0-856a-498f-ba87-48ff1426d980
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f0e40fe2d410037dd38dbb46613a9fb4c2622b0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="errorprocedure-transact-sql"></a>ERROR_PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Namen der gespeicherten Prozedur oder des Triggers zurück, an der bzw. an dem ein Fehler aufgetreten ist, durch den die Ausführung des CATCH-Blocks eines TRY…CATCH-Konstrukts verursacht wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ERROR_PROCEDURE ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar(128)**  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt beim Aufruf in einem CATCH-Block den Namen der gespeicherten Prozedur zurück, in der der Fehler aufgetreten ist.  
  
 Gibt NULL zurück, wenn der Fehler nicht in einer gespeicherten Prozedur bzw. nicht in einem Trigger aufgetreten ist.  
  
 Gibt NULL zurück, wenn die Funktion außerhalb des Bereichs eines CATCH-Blockes aufgerufen wird.  
  
## <a name="remarks"></a>Remarks  
 ERROR_PROCEDURE kann innerhalb des Bereichs eines CATCH-Blocks an beliebigen Stellen aufgerufen werden.  
  
 ERROR_PROCEDURE gibt den Namen der gespeicherten Prozedur bzw. des Triggers zurück, in der bzw. in dem der Fehler aufgetreten ist, unabhängig davon, wie oft die Funktion aufgerufen wurde bzw. wo sie innerhalb des Bereichs des CATCH-Blocks aufgerufen wurde. Dies steht im Gegensatz zu Funktionen wie @@ERROR, die die Fehlernummer in der Anweisung sofort (gefolgt von der Nummer, die den Fehler verursacht hat) oder in der ersten Anweisung des CATCH-Blocks zurückgeben.  
  
 In geschachtelten CATCH-Blöcken gibt ERROR_PROCEDURE den Namen der gespeicherten Prozedur oder des Triggers im Bereich des CATCH-Blocks zurück, in dem auf die gespeicherte Prozedur bzw. auf den Trigger verwiesen wird. Der CATCH-Block eines TRY…CATCH-Konstrukts kann beispielsweise ein geschachteltes TRY…CATCH-Konstrukt enthalten. Innerhalb des geschachtelten CATCH-Blocks gibt ERROR_PROCEDURE den Namen der gespeicherten Prozedur oder des Triggers zurück, in der bzw. in dem der Fehler aufgetreten ist, mit dem der geschachtelte CATCH-Block aufgerufen wurde. Wenn ERROR_PROCEDURE im äußeren CATCH-Block ausgeführt wird, gibt die Funktion den Namen der gespeicherten Prozedur oder des Triggers zurück, in der bzw. in dem der Fehler aufgetreten ist, mit dem dieser CATCH-Block aufgerufen wurde.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-errorprocedure-in-a-catch-block"></a>A. Verwenden von ERROR_PROCEDURE in einem CATCH-Block  
 Das folgende Codebeispiel zeigt eine gespeicherte Prozedur, in der ein Fehler aufgrund einer Division durch 0 generiert wird. `ERROR_PROCEDURE` gibt den Namen der gespeicherten Prozedur zurück, in der der Fehler aufgetreten ist.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>B. Verwenden von ERROR_PROCEDURE in einem CATCH-Block mit anderen Tools zur Fehlerbehandlung  
 Das folgende Codebeispiel zeigt eine gespeicherte Prozedur, in der ein Fehler aufgrund einer Division durch 0 generiert wird. Zusammen mit dem Namen der gespeicherten Prozedur, in der der Fehler aufgetreten ist, werden Informationen zurückgegeben, die sich auf den Fehler beziehen.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage,  
        ERROR_LINE() AS ErrorLine;  
        END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-using-errorprocedure-in-a-catch-block"></a>C. Verwenden von ERROR_PROCEDURE in einem CATCH-Block  
 Das folgende Codebeispiel zeigt eine gespeicherte Prozedur, in der ein Fehler aufgrund einer Division durch 0 generiert wird. `ERROR_PROCEDURE` gibt den Namen der gespeicherten Prozedur zurück, in der der Fehler aufgetreten ist.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>D. Verwenden von ERROR_PROCEDURE in einem CATCH-Block mit anderen Tools zur Fehlerbehandlung  
 Das folgende Codebeispiel zeigt eine gespeicherte Prozedur, in der ein Fehler aufgrund einer Division durch 0 generiert wird. Zusammen mit dem Namen der gespeicherten Prozedur, in der der Fehler aufgetreten ist, werden Informationen zurückgegeben, die sich auf den Fehler beziehen.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage;  
        END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

