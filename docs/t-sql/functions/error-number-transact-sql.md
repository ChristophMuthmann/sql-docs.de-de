---
title: ERROR_NUMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_NUMBER_TSQL
- ERROR_NUMBER
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], numbers
- TRY...CATCH [SQL Server]
- ERROR_NUMBER function
- CATCH block
ms.assetid: 1de85fff-1ca2-4b31-841b-926e571cb150
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: cb65492a3be74474cd5afccdcaf0487d7cbd5167
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="errornumber-transact-sql"></a>ERROR_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Fehlernummer des Fehlers zurück, der die Ausführung des CATCH-Blockes eines TRY…CATCH-Konstruktes verursacht hat.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ERROR_NUMBER ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 Bei Aufruf in einem CATCH-Block wird die Fehlernummer der Fehlermeldung zurückgegeben, die die Ausführung des CATCH-Blockes verursacht hat.  
  
 Gibt NULL zurück, wenn die Funktion außerhalb des Bereichs eines CATCH-Blockes aufgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion kann an jeder beliebigen Position im Gültigkeitsbereich eines CATCH-Blockes aufgerufen werden.  
  
 ERROR_NUMBER gibt die Fehlermeldung unabhängig davon zurück, wie oft die Funktion ausgeführt wird oder wo innerhalb des Gültigkeitsbereiches des CATCH-Blockes sie ausgeführt wird. Dies steht im Gegensatz zur@ERROR, die nur die Fehlernummer zurückgibt, in der Anweisung unmittelbar auf das Projekt, das einen Fehler verursacht hat, oder die erste Anweisung eines catch-block.  
  
 In geschachtelten CATCH-Blöcken gibt ERROR_NUMBER die Fehlernummer zurück, die für den Gültigkeitsbereich des CATCH-Blockes, in dem auf die Funktion verwiesen wird, spezifisch ist. Beispielsweise könnte der CATCH-Block eines äußeren TRY...CATCH-Konstrukts ein geschachteltes TRY...CATCH-Konstrukt aufweisen. Innerhalb des geschachtelten CATCH-Blockes gibt ERROR_NUMBER die Nummer des Fehlers zurück, der den geschachtelten CATCH-Block aufgerufen hat. Falls ERROR_NUMBER im äußeren CATCH-Block ausgeführt wird, wird die Nummer des Fehlers zurückgegeben, der den CATCH-Block aufgerufen hat.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-errornumber-in-a-catch-block"></a>A. Verwenden von ERROR_NUMBER in einem CATCH-Block  
 Das folgende Codebeispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 generiert. Die Nummer des Fehlers wird zurückgegeben.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_NUMBER() AS ErrorNumber;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errornumber-in-a-catch-block-with-other-error-handling-tools"></a>B. Verwenden von ERROR_NUMBER in einem CATCH-Block mit anderen Fehlerbehandlungstools  
 Das folgende Codebeispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 generiert. Zusammen mit der Fehlernummer werden Informationen zum Fehler zurückgegeben.  
  
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
  
### <a name="c-using-errornumber-in-a-catch-block-with-other-error-handling-tools"></a>C. Verwenden von ERROR_NUMBER in einem CATCH-Block mit anderen Fehlerbehandlungstools  
 Das folgende Codebeispiel zeigt eine `SELECT`-Anweisung, die einen Fehler aufgrund einer Division durch 0 generiert. Zusammen mit der Fehlernummer werden Informationen zum Fehler zurückgegeben.  
  
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
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


