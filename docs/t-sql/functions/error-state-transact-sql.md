---
title: ERROR_STATE (Transact-SQL) | Microsoft Docs
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
- ERROR_STATE_TSQL
- ERROR_STATE
dev_langs:
- TSQL
helpviewer_keywords:
- messages [SQL Server], state
- ERROR_STATE function
- errors [SQL Server], state
- TRY...CATCH [SQL Server]
- CATCH block
- states [SQL Server], error numbers
ms.assetid: 6059af00-83fe-409f-ab7c-daad111bc671
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98b5a1ecfbfd9efd84f8a5cc55454aaaec6f8423
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="errorstate-transact-sql"></a>ERROR_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt die Statusnummer des Fehlers zurück, der bewirkt hat, dass der CATCH-Block eines TRY…CATCH-Konstrukts ausgeführt wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
ERROR_STATE ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 Wenn diese Funktion in einem CATCH-Block aufgerufen wird, wird die Statusnummer der Fehlermeldung zurückgegeben, die bewirkt hat, dass der CATCH-Block ausgeführt wurde.  
  
 Gibt NULL zurück, wenn die Funktion außerhalb des Bereichs eines CATCH-Blockes aufgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
 Einige Fehlermeldungen ausgelöst werden können, an mehreren Punkten im Code für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. So kann z. B. der Fehler "1105" aufgrund verschiedener Bedingungen ausgelöst werden. Jeder Bedingung, die den Fehler auslöst, wird ein eindeutiger Statuscode zugewiesen.  
  
 Beim Anzeigen von Datenbanken mit bekannten Problemen, wie z. B. der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base, können Sie mithilfe der Statusnummer ermitteln, ob das aufgezeichnete Problem mit dem aufgetretenen Fehler übereinstimmt. Wenn z. B. ein Knowledge Base-Artikel den Fehler 1105 mit dem Status 2 erläutert und die von Ihnen empfangene Fehlermeldung 1105 den Status 3 aufweist, ist der Fehler wahrscheinlich auf eine andere als die im Artikel gemeldete Ursache zurückzuführen.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Software Service kann ebenfalls mithilfe des Fehlerzustandscodes die Stelle im Quellcode finden, an der dieser Fehler ausgelöst wird. Dies kann Anregungen für die Diagnose des Problems bereitstellen.  
  
 ERROR_STATE kann überall innerhalb des Bereichs eines CATCH-Blockes aufgerufen werden.  
  
 ERROR_STATE gibt den Fehlerzustand zurück. Dabei spielt es keine Rolle, wie oft die Funktion ausgeführt wird oder wo sie innerhalb des Bereichs des CATCH-Blockes ausgeführt wird. Dies steht im Gegensatz zu Funktionen, wie etwa @@ERROR, das nur die Anzahl der Fehler zurückgibt, in der Anweisung unmittelbar auf das Projekt, das einen Fehler verursacht hat, oder klicken Sie in der ersten Anweisung eines CATCH-Blockes.  
  
 In geschachtelten CATCH-Blöcken gibt ERROR_STATE den Fehlerzustand für den Bereich des CATCH-Blockes zurück, in dem auf die Funktion verwiesen wird. Beispielsweise könnte der CATCH-Block eines äußeren TRY...CATCH-Konstrukts ein geschachteltes TRY...CATCH-Konstrukt aufweisen. Innerhalb des geschachtelten CATCH-Blockes gibt ERROR_STATE den Status des Fehlers zurück, der den geschachtelten CATCH-Block aufgerufen hat. Wenn ERROR_STATE im äußeren CATCH-Block ausgeführt wird, wird der Status des Fehlers zurückgegeben, der diesen CATCH-Block aufgerufen hat.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-errorstate-in-a-catch-block"></a>A. Verwenden von ERROR_STATE in einem CATCH-Block  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Der Status des Fehlers wird zurückgegeben.  
  
```  
BEGIN TRY  
    -- Generate a divide by zero error  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_STATE() AS ErrorState;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>B. Verwenden von ERROR_STATE in einem CATCH-Block mit anderen Fehlerbehandlungstools  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Zusammen mit dem Fehlerzustand werden Informationen zu dem Fehler zurückgegeben.  
  
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
  
### <a name="c-using-errorstate-in-a-catch-block"></a>C. Verwenden von ERROR_STATE in einem CATCH-Block  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Der Status des Fehlers wird zurückgegeben.  
  
```  
BEGIN TRY  
    -- Generate a divide by zero error  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_STATE() AS ErrorState;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>D. Verwenden von ERROR_STATE in einem CATCH-Block mit anderen Fehlerbehandlungstools  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Zusammen mit dem Fehlerzustand werden Informationen zu dem Fehler zurückgegeben.  
  
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
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


