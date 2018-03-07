---
title: ERROR_LINE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 83783fdaa950777ae0a8002182abc273e32c2ca0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="errorline-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Zeilennummer der Zeile zurück, in der der Fehler aufgetreten ist, der die Ausführung des CATCH-Blockes eines TRY…CATCH-Konstrukts bewirkt hat.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 Aufruf in einem CATCH-Block:  
  
-   Gibt die Zeilennummer der Zeile zurück, in der der Fehler aufgetreten ist.  
  
-   Gibt die Zeilennummer in einer Routine zurück, wenn der Fehler in einer gespeicherten Prozedur oder einem Trigger aufgetreten ist.  
  
 Gibt NULL zurück, wenn die Funktion außerhalb des Bereichs eines CATCH-Blockes aufgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion kann an jeder beliebigen Position im Gültigkeitsbereich eines CATCH-Blockes aufgerufen werden.  
  
 ERROR_LINE gibt die Zeilennummer der Zeile zurück, in der der Fehler aufgetreten ist, unabhängig von der Aufrufhäufigkeit bzw. der Stelle innerhalb des Bereichs des CATCH-Blockes, an dem ERROR_LINE aufgerufen wurde. Dies steht im Gegensatz zu Funktionen, z. B.@ERROR, die eine Fehlernummer zurück, in der Anweisung unmittelbar folgt, die einen Fehler verursacht hat, oder in der ersten Anweisung eines CATCH-Blockes.  
  
 In geschachtelten CATCH-Blöcken gibt ERROR_LINE die für den Bereich des CATCH-Blockes spezifische Fehlerzeilennummer zurück, auf die im Block verwiesen wird. So könnte beispielsweise der CATCH-Block eines TRY…CATCH-Konstrukts ein geschachteltes TRY…CATCH-Konstrukt enthalten. Innerhalb des geschachtelten CATCH-Blocks gibt ERROR_LINE die Zeilennummer des Fehlers zurück, der den geschachtelten CATCH-Block aufgerufen hat. Wird ERROR_LINE im äußeren CATCH-Block ausgeführt, wird die Zeilennummer des Fehlers zurückgegeben, der den CATCH-Block aufgerufen hat.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-errorline-in-a-catch-block"></a>A. Verwenden von ERROR_LINE in einem CATCH-Block  
 Das folgende Codebeispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 generiert. Es wird die Zeilennummer der Zeile zurückgegeben, in der der Fehler aufgetreten ist.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>B. Verwenden von ERROR_LINE in einem CATCH-Block mit einer gespeicherten Prozedur  
 Das folgende Codebeispiel zeigt eine gespeicherte Prozedur, die einen Fehler aufgrund einer Division durch Null generiert. `ERROR_LINE` gibt die Zeilennummer in der gespeicherten Prozedur zurück, in der der Fehler aufgetreten ist.  
  
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
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>C. Verwenden von ERROR_LINE in einem CATCH-Block mit anderen Tools zur Fehlerbehandlung  
 Das folgende Codebeispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 generiert. Abgesehen von der Zeilennummer der Zeile, in der der Fehler aufgetreten ist, werden Informationen im Zusammenhang mit dem Fehler zurückgegeben.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
