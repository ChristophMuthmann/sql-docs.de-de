---
title: SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURSOR_CLOSE_ON_COMMIT
- SET CURSOR_CLOSE_ON_COMMIT
- CURSOR_CLOSE_ON_COMMIT_TSQL
- SET_CURSOR_CLOSE_ON_COMMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CURSOR_CLOSE_ON_COMMIT option
- transactions [SQL Server], cursors
- closing cursors
- cursors [SQL Server], closing
- SET CURSOR_CLOSE_ON_COMMIT statement
ms.assetid: 7b976154-98ce-4a06-bbae-7e59c34211f7
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de736d329175fe44c8bf837a2a6ef0ca966666ee
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-cursorcloseoncommit-transact-sql"></a>SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Steuert das Verhalten der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung COMMIT TRANSACTION. Der Standardwert für diese Einstellung ist OFF. Dies bedeutet, dass der Server Cursor nicht schließt, wenn Sie ein Commit für eine Transaktion ausführen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET CURSOR_CLOSE_ON_COMMIT auf ON festgelegt ist, schließt diese Einstellung alle offenen Cursor bei Ausführung des Commits oder Rollbacks in Übereinstimmung mit ISO. Wenn SET CURSOR_CLOSE_ON_COMMIT auf OFF festgelegt ist, wird der Cursor nicht geschlossen, wenn ein Commit für eine Transaktion ausgeführt wird.  
  
> [!NOTE]  
>  Wenn SET CURSOR_CLOSE_ON_COMMIT auf ON festgelegt ist, werden geöffnete Cursor bei Ausführung des Rollbacks nicht geschlossen, wenn das Rollback von einer SAVE TRANSACTION-Anweisung auf savepoint_name angewendet wird.  
  
 Wenn SET CURSOR_CLOSE_ON_COMMIT auf OFF festgelegt ist, schließt eine ROLLBACK-Anweisung nur geöffnete asynchrone Cursor ein, die nicht vollständig aufgefüllt sind. STATIC- oder INSENSITIVE-Cursor, die geöffnet wurden, nachdem Änderungen vorgenommen wurden, spiegeln den Datenstatus nicht mehr wider, wenn für die Änderungen ein Rollback ausgeführt wird.  
  
 SET CURSOR_CLOSE_ON_COMMIT steuert das gleiche Verhalten wie die Datenbankoption CURSOR_CLOSE_ON_COMMIT. Wenn CURSOR_CLOSE_ON_COMMIT auf ON oder OFF festgelegt ist, wird diese Einstellung für die Verbindung verwendet. Wenn SET CURSOR_CLOSE_ON_COMMIT nicht angegeben wurde, den Wert in der **Is_cursor_close_on_commit_on** Spalte in der **sys.databases** Katalogsicht gilt.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber sowohl CURSOR_CLOSE_ON_COMMIT auf OFF festgelegt, wenn sie eine Verbindung herstellen. Die DB-Library legt den Wert von CURSOR_CLOSE_ON_COMMIT nicht automatisch fest.  
  
 Ist SET ANSI_DEFAULTS auf ON festgelegt, so ist SET CURSOR_CLOSE_ON_COMMIT aktiviert.  
  
 Die Einstellung von SET CURSOR_CLOSE_ON_COMMIT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @CURSOR_CLOSE VARCHAR(3) = 'OFF';  
IF ( (4 & @@OPTIONS) = 4 ) SET @CURSOR_CLOSE = 'ON';  
SELECT @CURSOR_CLOSE AS CURSOR_CLOSE_ON_COMMIT;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Cursor in einer Transaktion definiert. Anschließend wird versucht, den Cursor zu verwenden, nachdem ein Commit für die Transaktion ausgeführt wurde.  
  
```  
-- SET CURSOR_CLOSE_ON_COMMIT  
-------------------------------------------------------------------------------  
SET NOCOUNT ON;  
  
CREATE TABLE t1 (a INT);  
GO   
  
INSERT INTO t1   
VALUES (1), (2);  
GO  
  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT ON';  
GO  
SET CURSOR_CLOSE_ON_COMMIT ON;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT OFF';  
GO  
SET CURSOR_CLOSE_ON_COMMIT OFF;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
DROP TABLE t1;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [Schließen &#40; Transact-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  

