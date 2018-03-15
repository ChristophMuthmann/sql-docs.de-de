---
title: REVERT (Transact-SQL) | Microsoft-Dokumentation
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
- REVERT_TSQL
- REVERT
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- context switching [SQL Server], reverting
- reverting execution context
- REVERT WITH COOKIE statement
- execution context [SQL Server]
- COOKIE clause
ms.assetid: 4688b17a-dfd1-4f03-8db4-273a401f879f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3350f92afbb6d6ed0278a9ae41ee25f5ed4096b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="revert-transact-sql"></a>REVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Wechselt den Ausführungskontext zurück zum Aufrufer der letzten EXECUTE AS-Anweisung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>Argumente  
 WITH COOKIE = @*varbinary_variable*  
 Gibt das Cookie an, das in einer entsprechenden eigenständigen [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)-Anweisung erstellt wurde. *@varbinary_variable* ist vom Datentyp **varbinary(100)**.  
  
## <a name="remarks"></a>Remarks  
 REVERT kann in einem Modul, wie einer gespeicherten Prozedur oder benutzerdefinierten Funktion, oder in einer eigenständigen Anweisung angegeben werden. Innerhalb eines Moduls kann REVERT nur auf EXECUTE AS-Anweisungen angewendet werden, die im Modul definiert sind. So gibt beispielsweise die folgende gespeicherte Prozedur eine `EXECUTE AS`-Anweisung aus, gefolgt von einer `REVERT`-Anweisung.  
  
```  
CREATE PROCEDURE dbo.usp_myproc   
  WITH EXECUTE AS CALLER  
AS   
    SELECT SUSER_NAME(), USER_NAME();  
    EXECUTE AS USER = 'guest';  
    SELECT SUSER_NAME(), USER_NAME();  
    REVERT;  
    SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
 Angenommen, in der Sitzung, in der die gespeicherte Prozedur ausgeführt wird, wird der Ausführungskontext der Sitzung explizit in `login1` geändert, wie im folgenden Beispiel veranschaulicht.  
  
```  
  -- Sets the execution context of the session to 'login1'.  
EXECUTE AS LOGIN = 'login1';  
GO  
EXECUTE dbo.usp_myproc;   
```  
  
 Die in `usp_myproc` definierte `REVERT`-Anweisung wechselt den im Modul festgelegten Ausführungskontext, wirkt sich jedoch nicht auf den außerhalb des Moduls festgelegten Ausführungskontext aus. Der Ausführungskontext für die Sitzung bleibt also auf `login1` festgelegt.  
  
 Als eigenständige Anweisung wird REVERT auf EXECUTE AS-Anweisungen angewendet, die in einem Batch oder einer Sitzung definiert sind. REVERT hat keinerlei Auswirkungen, wenn die entsprechende EXECUTE AS-Anweisung die WITH NO REVERT-Klausel enthält. In diesem Fall bleibt der Ausführungskontext so lange wirksam, bis die Sitzung gelöscht wird.  
  
## <a name="using-revert-with-cookie"></a>Verwenden von REVERT WITH COOKIE  
 Die zum Festlegen des Ausführungskontexts einer Sitzung verwendete EXECUTE AS-Anweisung kann die optionale Klausel WITH NO REVERT COOKIE = @*varbinary_variable* einschließen. Wird diese Anweisung ausgeführt, übergibt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] das Cookie an @*varbinary_variable*. Der von dieser Anweisung festgelegte Ausführungskontext kann nur auf einen vorherigen Kontext zurückgesetzt werden, wenn die aufrufende REVERT WITH COOKIE = @*varbinary_variable*-Anweisung den gleichen *@varbinary_variable*-Wert enthält.  
  
 Dieser Mechanismus eignet sich für eine Umgebung, in der Verbindungs-Pooling verwendet wird. Verbindungs-Pooling bezeichnet die Verwaltung einer Gruppe von Datenbankverbindungen für die Wiederverwendung durch Anwendungen durch mehrere Endbenutzer. Da der an *@varbinary_variable* übergebene Wert nur dem Aufrufer der EXECUTE AS-Anweisung (in diesem Fall die Anwendung) bekannt ist, kann der Aufrufer sicherstellen, dass der eingerichtete Ausführungskontext nicht von dem Endbenutzer geändert werden kann, der die Anwendung aufruft. Nach dem Wiederherstellen des Ausführungskontexts kann die Anwendung einen Kontextwechsel zu einem anderen Prinzipal durchführen.  
  
## <a name="permissions"></a>Berechtigungen  
 Es sind keine Berechtigungen erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>A. Verwenden von EXECUTE AS und REVERT zum Wechseln des Kontexts  
 Im folgenden Beispiel wird ein Kontextausführungsstapel mithilfe mehrere Prinzipale erstellt. Dann wird der Ausführungskontext mithilfe der REVERT-Anweisung zum vorherigen Aufrufer gewechselt. Die REVERT-Anweisung wird mehrfach ausgeführt und im Stapel nach oben verschoben, bis der Ausführungskontext beim ursprünglichen Aufrufer angelangt ist.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create two temporary principals.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
-- Give IMPERSONATE permissions on user2 to user1  
-- so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
-- Verify that the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
-- Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1, and login2.  
-- The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
-- Remove the temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. Verwenden der WITH COOKIE-Klausel  
 Im folgenden Beispiel wird der Ausführungskontext einer Sitzung auf einen angegebenen Benutzer festgelegt und die WITH NO REVERT COOKIE = @*varbinary_variable*-Klausel angegeben. In der `REVERT`-Anweisung muss der an die `@cookie`-Variable in der `EXECUTE AS`-Anweisung übergebene Wert angegeben sein, damit der Kontext erfolgreich auf den Aufrufer zurückgesetzt werden kann. Zur Ausführung dieses Beispiels müssen der `login1`-Anmeldename und der `user1`-Benutzer, die in Beispiel A erstellt wurden, vorhanden sein.  
  
```  
DECLARE @cookie varbinary(100);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie somewhere safe in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(100);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
  
