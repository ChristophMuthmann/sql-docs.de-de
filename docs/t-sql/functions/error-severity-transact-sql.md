---
title: ERROR_SEVERITY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_SEVERITY_TSQL
- ERROR_SEVERITY
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], severity
- messages [SQL Server], severity
- TRY...CATCH [SQL Server]
- CATCH block
- ERROR_SEVERITY function
ms.assetid: 50228f2f-6949-4d2e-8e43-fad11bf973ab
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11cbfa6cc0ca35e5bb5e3358bf9d9dc2dfcfb644
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="errorseverity-transact-sql"></a>ERROR_SEVERITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Schweregrad des Fehlers zurück, der die Ausführung des CATCH-Blockes eines TRY…CATCH-Konstrukts bewirkt hat.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ERROR_SEVERITY ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 Bei einem Aufruf in einem CATCH-Block wird der Schweregrad der Fehlermeldung zurückgegeben, die die Ausführung des CATCH-Blockes bewirkt hat.  
  
 Gibt NULL zurück, wenn die Funktion außerhalb des Bereichs eines CATCH-Blockes aufgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
 ERROR_SEVERITY kann von einer beliebigen Stelle innerhalb des Bereichs eines CATCH-Blockes aufgerufen werden.  
  
 ERROR_SEVERITY gibt den Fehlerschweregrad unabhängig von der Anzahl der Ausführungen oder von der Stelle der Ausführung innerhalb des Bereichs des CATCH-Blockes zurück. Dies steht im Gegensatz zu Funktionen, wie etwa @@ERROR, das nur die Anzahl der Fehler zurückgibt, in der Anweisung unmittelbar auf das Projekt, das einen Fehler verursacht hat, oder klicken Sie in der ersten Anweisung eines CATCH-Blockes.  
  
 In geschachtelten CATCH-Blöcken gibt ERROR_SEVERITY den für den Bereich des CATCH-Blockes spezifischen Fehlerschweregrad zurück, auf den im Block verwiesen wird. Beispielsweise könnte der CATCH-Block eines äußeren TRY...CATCH-Konstrukts ein geschachteltes TRY...CATCH-Konstrukt aufweisen. Innerhalb des geschachtelten CATCH-Blockes gibt ERROR_SEVERITY den Schweregrad des Fehlers zurück, der den geschachtelten CATCH-Block aufgerufen hat. Wird ERROR_SEVERITY im äußeren CATCH-Block ausgeführt, wird der Schweregrad des Fehlers zurückgegeben, der den CATCH-Block aufgerufen hat.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-errorseverity-in-a-catch-block"></a>A. Verwenden von ERROR_SEVERITY in einem CATCH-Block  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Der Schweregrad des Fehlers wird zurückgegeben.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>B. Verwenden von ERROR_SEVERITY in einem CATCH-Block mit anderen Tools zur Fehlerbehandlung  
 Das folgende Beispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch Null generiert. Abgesehen von Schweregrad werden Informationen im Zusammenhang mit dem Fehler zurückgegeben.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorseverity-in-a-catch-block"></a>C. Verwenden von ERROR_SEVERITY in einem CATCH-Block  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Der Schweregrad des Fehlers wird zurückgegeben.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_SEVERITY() AS ErrorSeverity;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorseverity-in-a-catch-block-with-other-error-handling-tools"></a>D. Verwenden von ERROR_SEVERITY in einem CATCH-Block mit anderen Tools zur Fehlerbehandlung  
 Das folgende Beispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch Null generiert. Abgesehen von Schweregrad werden Informationen im Zusammenhang mit dem Fehler zurückgegeben.  
  
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
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


