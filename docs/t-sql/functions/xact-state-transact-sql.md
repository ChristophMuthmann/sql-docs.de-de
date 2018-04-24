---
title: XACT_STATE (Transact-SQL) | Microsoft-Dokumentation
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
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d4dfe8b32aed812d577b70f79c75596310a7829d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="xactstate-transact-sql"></a>XACT_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine Skalarfunktion, die den Status einer Benutzertransaktion einer zurzeit ausgeführten Anforderung meldet. XACT_STATE gibt an, ob für die Anforderung eine aktive Benutzertransaktion vorliegt und ob für die Transaktion ein Commit ausgeführt werden kann.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
XACT_STATE()  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **smallint**  
  
## <a name="remarks"></a>Remarks  
 XACT_STATE gibt folgende Werte zurück.  
  
|Rückgabewert|Bedeutung|  
|------------------|-------------|  
|1|Für die aktuelle Anforderung liegt eine aktive Benutzertransaktion vor. Die Anforderung kann beliebige Aktionen ausführen, z. B. können Daten geschrieben werden, und es kann ein Commit für die Transaktion ausgeführt werden.|  
|0|Für die aktuelle Anforderung liegt keine aktive Benutzertransaktion vor.|  
|-1|Für die aktuelle Anforderung liegt eine aktive Benutzertransaktion vor, allerdings ist ein Fehler aufgetreten, durch den die Transaktion als nicht commitfähig klassifiziert wurde. Die Anforderung kann für die Transaktion weder einen Commit noch ein Rollback zu einem Sicherungspunkt ausführen. Es ist lediglich möglich, ein vollständiges Rollback für die Transaktion anzufordern. Die Anforderung kann erst wieder Schreibvorgänge ausführen, wenn für die Transaktion ein Rollback ausgeführt wurde. Bis für die Transaktion ein Rollback ausgeführt wird, kann die Anforderung nur Lesevorgänge ausführen. Nachdem für die Transaktion ein Rollback ausgeführt worden ist, kann die Anforderung sowohl Lese- als auch Schreibvorgänge ausführen und eine neue Transaktion starten.<br /><br /> Wenn die Ausführung des äußersten Batchs abgeschlossen ist, führt die [!INCLUDE[ssDE](../../includes/ssde-md.md)] für alle aktiven nicht commitfähigen Transaktionen automatisch ein Rollback aus. Falls keine Fehlermeldung gesendet wurde, als die Transaktion in den nicht commitfähigen Status überging, wird bei Abschluss des Batches eine Fehlermeldung an die Clientanwendung gesendet. Durch diese Meldung wird angezeigt, dass eine nicht commitfähige Transaktion erkannt und ein Rollback für sie ausgeführt wurde.|  
  
 Sowohl über die XACT_STATE-Funktion als auch über die @@TRANCOUNT-Funktion kann ermittelt werden, ob für die aktuelle Anforderung eine aktive Benutzertransaktion vorliegt. Mit @@TRANCOUNT kann nicht bestimmt werden, ob die betreffende Transaktion als nicht commitfähig klassifiziert wurde. Mit XACT_STATE kann nicht bestimmt werden, ob geschachtelte Transaktionen vorhanden sind.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `XACT_STATE` im `CATCH`-Block eines `TRY…CATCH`-Konstrukts verwendet, um zu bestimmen, ob für eine Transaktion ein Commit- oder Rollback-Vorgang ausgeführt werden soll. Da `SET XACT_ABORT` auf den Wert `ON` festgelegt ist, wird die Transaktion wegen des aufgrund der Einschränkungsverletzung aufgetretenen Fehlers in einen nicht commitfähigen Zustand versetzt.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
