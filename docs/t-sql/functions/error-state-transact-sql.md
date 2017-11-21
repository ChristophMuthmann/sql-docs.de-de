---
title: ERROR_STATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 2d5448d8dbd738177acbcd407448d7a10d835a23
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="errorstate-transact-sql"></a>ERROR_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt die Statusnummer des Fehlers, der den CATCH-Block einer try wurde... CATCH-Konstrukts ausgeführt werden.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ERROR_STATE ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 Wenn in einem CatchBlock aufgerufen wird, gibt die Statusnummer der Fehlermeldung, die die CATCH-Block ausgeführt werden wurde zurück.  
  
 Gibt NULL zurück, wenn außerhalb des Bereichs eines CATCH-Blockes aufgerufen.  
  
## <a name="remarks"></a>"Hinweise"  
 Einige Fehlermeldungen ausgelöst werden können, an mehreren Punkten im Code für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Beispielsweise kann Fehler "1105 aufgrund" verschiedener Bedingungen ausgelöst werden. Jeder Bedingung, die den Fehler auslöst, wird einen eindeutiger Statuscode zugewiesen.  
  
 Wenn Datenbanken von bekannten Problemen, wie z. B. Anzeigen der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base, können Sie mithilfe der Statusnummer bestimmen, ob das aufgezeichnete Problem mit dem aufgetretenen Fehler möglicherweise aufgetretenen. Hatten z. B. wenn ein Knowledge Base-Artikel wird Fehler 1105 mit dem Status 2 erläutert und die Sie empfangene Fehlermeldung 1105 den Status 3 hatte, der Fehler wahrscheinlich eine andere als die im Artikel gemeldete Ursache.  
  
 Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Supporttechniker können auch den Statuscode von einem Fehler finden Sie den Speicherort in den Quellcode, in denen dieser Fehler ausgelöst wird, noch weitere Ideen zur Problemdiagnose bereit kann.  
  
 ERROR_STATE kann überall innerhalb des Bereichs eines CATCH-Blockes aufgerufen werden.  
  
 ERROR_STATE gibt den Status "Fehler" unabhängig davon, wie oft die ausgeführt wird, oder, in denen es innerhalb des Bereichs des CATCH-Blockes. Dies steht im Gegensatz zu Funktionen, wie etwa @@ERROR, das nur die Anzahl der Fehler zurückgibt, in der Anweisung unmittelbar auf das Projekt, das einen Fehler verursacht hat, oder klicken Sie in der ersten Anweisung eines CATCH-Blockes.  
  
 In geschachtelten CATCH-Blöcken gibt ERROR_STATE den Fehler Status für den Bereich des CATCH-block in dem darauf verwiesen wird. Beispielsweise der CATCH-Block eine äußere try... TRY…catch-Konstrukt möglicherweise einen geschachtelten TRY... CATCH-Konstrukt. Innerhalb des geschachtelten CATCH-Blockes gibt ERROR_STATE den Status des Fehlers, der den geschachtelten CATCH-Block aufgerufen hat. Wenn ERROR_STATE im äußeren CATCH-Block ausgeführt wird, gibt den Status des Fehlers, der diesen CATCH-Block aufgerufen hat zurück.  
  
## <a name="examples"></a>Beispiele für  
  
### <a name="a-using-errorstate-in-a-catch-block"></a>EIN. Verwenden von ERROR_STATE in einem CATCH-block  
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
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Zusammen mit den Status "Fehler" werden Informationen im Zusammenhang mit dem Fehler zurückgegeben.  
  
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
  
### <a name="c-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>C. Verwenden von ERROR_STATE in einem CATCH-Block mit anderen Fehlerbehandlungstools  
 Das folgende Beispiel zeigt eine `SELECT` -Anweisung, die Fehler aufgrund einer Division durch 0 generiert. Zusammen mit den Status "Fehler" werden Informationen im Zusammenhang mit dem Fehler zurückgegeben.  
  
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
 [Sys.Messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [WIEDERHOLEN SIE DEN... CATCH &#40; Transact-SQL &#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40; Transact-SQL &#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40; Transact-SQL &#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40; Transact-SQL &#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40; Transact-SQL &#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40; Transact-SQL &#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


