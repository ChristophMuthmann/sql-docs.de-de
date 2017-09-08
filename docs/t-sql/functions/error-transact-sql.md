---
title: '@@ERROR (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ERROR'
- '@@ERROR_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ERROR function'
- errors [SQL Server], Transact-SQL
- error numbers [SQL Server]
ms.assetid: c8b43477-b6c0-49bf-a608-394a0b6cc7a2
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ef3f7b2f0b051fd79dd59325af7900aefff95a9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40error-transact-sql"></a>& #x 40; & #x 40; Fehler (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Fehlernummer für die zuletzt ausgeführte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@ERROR  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 integer  
  
## <a name="remarks"></a>Hinweise  
 Gibt 0 zurück, wenn bei der vorherigen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung keine Fehler auftraten.  
  
 Gibt eine Fehlernummer zurück, wenn bei der vorherigen Anweisung ein Fehler auftrat. Wenn der Fehler einer der Fehler in der sys.messages-Katalogsicht, dann wurde@ERROR enthält den Wert aus der message_id-Spalte für diesen Fehler. Sie können den zugeordneten Text anzeigen ein @@ERROR Fehlernummer in sys.messages.  
  
 Da @@ERROR deaktiviert ist und nach jeder ausgeführten Anweisung zurücksetzen checken Sie es sofort nach der Anweisung, die überprüft wird, oder speichern Sie sie an eine lokale Variable, die später aktiviert werden kann.  
  
 Verwenden Sie das TRY...CATCH-Konstrukt zur Behandlung von Fehlern. Wiederholen Sie dann... CATCH erstellen auch unterstützt zusätzliche Systemfunktionen (ERROR_LINE, ERROR_MESSAGE, ERROR_PROCEDURE, ERROR_SEVERITY und ERROR_STATE), die mehr Fehlerinformationen als @ zurückgeben@ERROR. TRY...CATCH unterstützt darüber hinaus eine ERROR_NUMBER-Funktion, die nicht darauf beschränkt ist, die Fehlernummer in der Anweisung zurückzugeben, die unmittelbar auf die Anweisung folgt, die einen Fehler generiert hat. Weitere Informationen finden Sie unter [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-error-to-detect-a-specific-error"></a>A. Mit@ERROR zum Erkennen eines bestimmten Fehlers  
 Im folgenden Beispiel wird `@@ERROR` verwendet, um nach einer Verletzung einer CHECK-Einschränkung (Fehlernr. 547) in einer `UPDATE`-Anweisung zu suchen.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.EmployeePayHistory  
    SET PayFrequency = 4  
    WHERE BusinessEntityID = 1;  
IF @@ERROR = 547  
    PRINT N'A check constraint violation occurred.';  
GO  
```  
  
### <a name="b-using-error-to-conditionally-exit-a-procedure"></a>B. Mit@ERROR zur bedingten Beendigung eine Prozedur  
 Im folgenden Beispiel wird `IF...ELSE` Anweisungen zum Testen `@@ERROR` nach einer `INSERT` -Anweisung in einer gespeicherten Prozedur. Der Wert der `@@ERROR`-Variablen bestimmt den an das aufrufende Programm gesendeten Rückgabecode und gibt damit den Erfolg oder das Fehlschlagen der Prozedur an.  
  
```  
USE AdventureWorks2012;  
GO  
-- Drop the procedure if it already exists.  
IF OBJECT_ID(N'HumanResources.usp_DeleteCandidate', N'P') IS NOT NULL  
    DROP PROCEDURE HumanResources.usp_DeleteCandidate;  
GO  
-- Create the procedure.  
CREATE PROCEDURE HumanResources.usp_DeleteCandidate   
    (  
    @CandidateID INT  
    )  
AS  
-- Execute the DELETE statement.  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = @CandidateID;  
-- Test the error value.  
IF @@ERROR <> 0   
    BEGIN  
        -- Return 99 to the calling program to indicate failure.  
        PRINT N'An error occurred deleting the candidate information.';  
        RETURN 99;  
    END  
ELSE  
    BEGIN  
        -- Return 0 to the calling program to indicate success.  
        PRINT N'The job candidate has been deleted.';  
        RETURN 0;  
    END;  
GO  
```  
  
### <a name="c-using-error-with-rowcount"></a>C. Mit@ERROR mit @@ROWCOUNT  
 Im folgenden Beispiel wird `@@ERROR` mit `@@ROWCOUNT` verwendet, um den Vorgang einer `UPDATE`-Anweisung zu überprüfen. Der Wert von `@@ERROR` wird auf Fehler überprüft, und `@@ROWCOUNT` wird verwendet, um sicherzustellen, dass das Update erfolgreich auf eine Zeile in der Tabelle angewendet wurde.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Purchasing.usp_ChangePurchaseOrderHeader',N'P')IS NOT NULL  
    DROP PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader;  
GO  
CREATE PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader  
    (  
    @PurchaseOrderID INT  
    ,@BusinessEntityID INT  
   )  
AS  
-- Declare variables used in error checking.  
DECLARE @ErrorVar INT;  
DECLARE @RowCountVar INT;  
  
-- Execute the UPDATE statement.  
UPDATE PurchaseOrderHeader   
    SET BusinessEntityID = @BusinessEntityID   
    WHERE PurchaseOrderID = @PurchaseOrderID;  
  
-- Save the @@ERROR and @@ROWCOUNT values in local   
-- variables before they are cleared.  
SELECT @ErrorVar = @@ERROR  
    ,@RowCountVar = @@ROWCOUNT;  
  
-- Check for errors. If an invalid @BusinessEntityID was specified,  
-- the UPDATE statement returns a foreign key violation error #547.  
IF @ErrorVar <> 0  
    BEGIN  
        IF @ErrorVar = 547  
            BEGIN  
                PRINT N'ERROR: Invalid ID specified for new employee.';  
                 RETURN 1;  
            END  
        ELSE  
            BEGIN  
                PRINT N'ERROR: error '  
                    + RTRIM(CAST(@ErrorVar AS NVARCHAR(10)))  
                    + N' occurred.';  
                RETURN 2;  
            END  
    END  
  
-- Check the row count. @RowCountVar is set to 0   
-- if an invalid @PurchaseOrderID was specified.  
IF @RowCountVar = 0  
    BEGIN  
        PRINT 'Warning: The BusinessEntityID specified is not valid';  
        RETURN 1;  
    END  
ELSE  
    BEGIN  
        PRINT 'Purchase order updated with the new employee';  
        RETURN 0;  
    END;  
GO  
```  

  
## <a name="see-also"></a>Siehe auch  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40; Transact-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [Sys.Messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  


