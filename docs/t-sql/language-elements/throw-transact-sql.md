---
title: THROW (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- THROW_TSQL
- THROW
dev_langs:
- TSQL
helpviewer_keywords:
- THROW statement
ms.assetid: 43661b89-8f13-4480-ad53-70306cbb14c5
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e38c09d3ba90d57f56b5af98772b4c411524f31e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="throw-transact-sql"></a>THROW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Löst eine Ausnahme aus und übergibt die Ausführung an einem CATCH-Block eines TRY…CATCH-Konstrukts in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
THROW [ { error_number | @local_variable },  
        { message | @local_variable },  
        { state | @local_variable } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *error_number*  
 Eine Konstante oder Variable, die die Ausnahme darstellt. *error_number* ist vom Datentyp **int** und muss größer oder gleich 50.000 und kleiner oder gleich 2.147.483.647 sein.  
  
 *Nachricht*  
 Eine Zeichenfolge oder Variable, die die Ausnahme beschreibt. *message* entspricht **nvarchar(2048)**.  
  
 *state*  
 Ist eine Konstante oder Variable zwischen 0 und 255, die den Status angibt, der der Nachricht zugeordnet werden soll. *state* entspricht **tinyint**.  
  
## <a name="remarks"></a>Remarks  
 Auf die Anweisung vor der THROW-Anweisung muss als Anweisungsabschlusszeichen das Semikolon (;) folgen.  
  
 Wenn kein TRY…CATCH-Konstrukt verfügbar ist, wird der Anweisungsbatch beendet. Die Zeilennummer und die Prozedur, in der die Ausnahme ausgelöst wird, werden festgelegt. Der Schweregrad wird auf 16 festgelegt.  
  
 Wenn die THROW-Anweisung ohne Parameter angegeben wird, muss sie in einem CATCH-Block enthalten sein. Dies bewirkt, dass die abgefangene Ausnahme ausgelöst wird. Jeder in einer THROW-Anweisung auftretende Fehler führt dazu, dass der Anweisungsbatch beendet wird.  
  
 % ist ein reserviertes Zeichen im Nachrichtentext einer THROW-Anweisung und muss mit Escapezeichen versehen werden. Verwenden Sie ein weiteres Prozentzeichen, damit % als Teil des Nachrichtentextes zurückgegeben wird, z. B. "Der Anstieg überschreitet den ursprünglichen Wert um 15 %%."  
  
## <a name="differences-between-raiserror-and-throw"></a>Unterschiede zwischen RAISERROR und THROW  
 In der folgenden Tabelle werden Unterschiede zwischen der RAISERROR-Anweisung und der THROW-Anweisung aufgeführt.  
  
|RAISERROR-Anweisung|THROW-Anweisung|  
|-------------------------|---------------------|  
|Wenn eine *msg_id* an RAISERROR übergeben wird, muss die ID in „sys.messages“ definiert werden.|Der Parameter *error_number* muss nicht in „sys.messages“ definiert werden.|  
|Der Parameter *msg_str* kann **printf**-Formatierungen enthalten.|Der Parameter *message* akzeptiert keine **printf**-Formatierung.|  
|Der Parameter *severity* gibt den Schweregrad der Ausnahme an.|Es ist kein *severity*-Parameter vorhanden. Der Ausnahmeschweregrad ist immer auf 16 festgelegt.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-throw-to-raise-an-exception"></a>A. Verwenden von THROW zum Auslösen einer Ausnahme  
 Im folgenden Beispiel wird gezeigt, wie die `THROW`-Anweisung zum Auslösen einer Ausnahme verwendet wird.  
  
```sql  
THROW 51000, 'The record does not exist.', 1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 51000, Level 16, State 1, Line 1  
  
 The record does not exist.
 ```  
  
### <a name="b-using-throw-to-raise-an-exception-again"></a>B. Verwenden von THROW zum erneuten Auslösen einer Ausnahme  
 Im folgenden Beispiel wird gezeigt, wie die `THROW`-Anweisung verwendet wird, um die zuletzt ausgelöste Ausnahme erneut auszulösen.  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE dbo.TestRethrow  
(    ID INT PRIMARY KEY  
);  
BEGIN TRY  
    INSERT dbo.TestRethrow(ID) VALUES(1);  
--  Force error 2627, Violation of PRIMARY KEY constraint to be raised.  
    INSERT dbo.TestRethrow(ID) VALUES(1);  
END TRY  
BEGIN CATCH  
  
    PRINT 'In catch block.';  
    THROW;  
END CATCH;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 PRINT 'In catch block.';  
 Msg 2627, Level 14, State 1, Line 1  
 Violation of PRIMARY KEY constraint 'PK__TestReth__3214EC272E3BD7D3'. Cannot insert duplicate key in object 'dbo.TestRethrow'.  
 The statement has been terminated.
 ```  
  
### <a name="c-using-formatmessage-with-throw"></a>C. Verwenden von FORMATMESSAGE mit THROW  
 Im folgenden Beispiel wird gezeigt, wie die `FORMATMESSAGE`-Funktion mit `THROW` verwendet wird, um eine benutzerdefinierte Fehlermeldung auszulösen. Zunächst wird im Bespiel eine benutzerdefinierte Fehlermeldung mithilfe von `sp_addmessage` erstellt. Da die THROW-Anweisung im Unterschied zu RAISERROR keine Ersetzungsparameter im *message*-Parameter zulässt, werden die drei von der Fehlermeldung 60000 erwarteten Parameterwerte von der FORMATMESSAGE-Funktion übergeben.  
  
```sql  
EXEC sys.sp_addmessage  
     @msgnum   = 60000  
,@severity = 16  
,@msgtext  = N'This is a test message with one numeric parameter (%d), one string parameter (%s), and another string parameter (%s).'  
    ,@lang = 'us_english';   
GO  
  
DECLARE @msg NVARCHAR(2048) = FORMATMESSAGE(60000, 500, N'First string', N'second string');   
  
THROW 60000, @msg, 1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 60000, Level 16, State 1, Line 2  
 This is a test message with one numeric parameter (500), one string parameter (First string), and another string parameter (second string).
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)   
 [Database Engine Error Severities (Schweregrad von Datenbank-Engine-Fehlern)](../../relational-databases/errors-events/database-engine-error-severities.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [GOTO &#40;Transact-SQL&#41;](../../t-sql/language-elements/goto-transact-sql.md)   
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [XACT_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/xact-state-transact-sql.md)   
 [SET XACT_ABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-xact-abort-transact-sql.md)  
  
  

