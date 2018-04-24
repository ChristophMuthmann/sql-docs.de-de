---
title: '@@ERROR (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 08/29/2017
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 616c8570026e3c57259ea6bad091fdbbae93bb75
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40error-transact-sql"></a>&#x40;&#x40;ERROR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Fehlernummer für die zuletzt ausgeführte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@ERROR  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 integer  
  
## <a name="remarks"></a>Remarks  
 Gibt 0 zurück, wenn bei der vorherigen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung keine Fehler auftraten.  
  
 Gibt eine Fehlernummer zurück, wenn bei der vorherigen Anweisung ein Fehler auftrat. Wenn es sich bei dem Fehler um einen der Fehler in der sys.messages-Katalogsicht handelt, enthält @@ERROR den Wert der sys.messages.message_id-Spalte dieses Fehlers. Sie können den zu einer @@ERROR-Fehlernummer gehörenden Text in sys.messages anzeigen.  
  
 Da @@ERROR nach jeder ausgeführten Anweisung gelöscht und zurückgesetzt wird, sollten Sie den Fehler sofort nach der Überprüfung der Anweisung überprüfen oder ihn in einer lokalen Variablen speichern, die zu einem späteren Zeitpunkt überprüft werden kann.  
  
 Verwenden Sie das TRY...CATCH-Konstrukt zur Behandlung von Fehlern. Das TRY...CATCH-Konstrukt unterstützt auch zusätzliche Systemfunktionen (ERROR_LINE, ERROR_MESSAGE, ERROR_PROCEDURE, ERROR_SEVERITY und ERROR_STATE), die mehr Fehlerinformationen als @@ERROR zurückgeben. TRY...CATCH unterstützt darüber hinaus eine ERROR_NUMBER-Funktion, die nicht darauf beschränkt ist, die Fehlernummer in der Anweisung zurückzugeben, die unmittelbar auf die Anweisung folgt, die einen Fehler generiert hat. Weitere Informationen finden Sie unter [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-error-to-detect-a-specific-error"></a>A. Verwenden von @@ERROR zum Erkennen eines bestimmten Fehlers  
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
  
### <a name="b-using-error-to-conditionally-exit-a-procedure"></a>B. Verwenden von @@ERROR zur bedingten Beendigung einer Prozedur  
 In den folgenden Beispielen werden `IF...ELSE`-Anweisungen verwendet, um `@@ERROR` nach einer `DELETE`-Anweisung in einer gespeicherten Prozedur zu testen. Der Wert der `@@ERROR`-Variablen bestimmt den an das aufrufende Programm gesendeten Rückgabecode und gibt damit den Erfolg oder das Fehlschlagen der Prozedur an.  
  
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
  
### <a name="c-using-error-with-rowcount"></a>C. Verwenden von @@ERROR mit @@ROWCOUNT  
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

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  

