---
title: SET IMPLICIT_TRANSACTIONS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IMPLICIT_TRANSACTIONS
- SET IMPLICIT_TRANSACTIONS
- IMPLICIT_TRANSACTIONS_TSQL
- SET_IMPLICIT_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- implicit transactions
- transactions [SQL Server], implicit
- connections [SQL Server], implicit transaction mode
- SET IMPLICIT_TRANSACTIONS statement
- IMPLICIT_TRANSACTIONS option
ms.assetid: a300ac43-e4c0-4329-8b79-a1a05e63370a
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89211c9b25ea2c488df71456cfbe6a5bc6c48eda
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-implicittransactions-transact-sql"></a>SET IMPLICIT_TRANSACTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Wird der BEGIN TRANSACTION-Modus auf *implizite*, für die Verbindung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET IMPLICIT_TRANSACTIONS { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn auf das System ist im *implizite* Transaktionsmodus. Das bedeutet, wenn @@TRANCOUNT = 0, eine der folgenden Transact-SQL-Anweisungen beginnt eine neue Transaktion. Dies entspricht einer unsichtbaren BEGIN TRANSACTION zuerst ausgeführt wird:  
  
||||  
|-|-|-|  
|ALTER TABLE|FETCH|REVOKE|  
|BEGIN TRANSACTION|GRANT|SELECT (siehe die Ausnahme unten).|  
|CREATE|INSERT|TRUNCATE TABLE|  
|DELETE|OPEN|UPDATE|  
|DROP|zugreifen.|zugreifen.|  
  
 Wenn wird OFF aller vorhergehenden T-SQL-Anweisungen durch eine unsichtbaren BEGIN TRANSACTION und einem unsichtbaren COMMIT TRANSACTION-Anweisung festgelegt. Bei OFF wir sprechen wird von der Transaktionsmodus *Autocommit*. Wenn Ihr T-SQL-Code sichtbar eine BEGIN TRANSACTION ausgegeben wird, sagen wir der Transaktionsmodus wird *explizite*.  
  
 Es gibt mehrere clarifying Punkt zu verstehen:  
  
-   Wenn Sie der Transaktionsmodus implizit ist, wird keine unsichtbaren BEGIN TRANSACTION ausgegeben If @@trancount > 0 bereits. Allerdings weiterhin alle expliziten BEGIN TRANSACTION-Anweisungen Inkrement @@TRANCOUNT.  
  
-   Wenn die INSERT-Anweisungen und nichts in die Arbeitseinheit abgeschlossen ist, müssen Sie COMMIT TRANSACTION-Anweisungen bis @ ausgeben@TRANCOUNT wieder auf 0 verringert wird. Oder Sie können eine ROLLBACK TRANSACTION ausgeben.  
  
-   Von SELECT-Anweisungen, die keine Daten aus einer Tabelle auswählen, werden keine impliziten Transaktionen gestartet. `SELECT GETDATE();` oder `SELECT 1, 'ABC';` erfordern beispielsweise keine Transaktionen.  
  
-   Implizite Transaktionen möglicherweise unerwartet ON aufgrund von ANSI-Standards. Weitere Informationen finden Sie [SET ANSI_DEFAULTS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-defaults-transact-sql.md).  
  
     IMPLICIT_TRANSACTIONS ON ist nicht beliebt. In den meisten Fällen, in denen IMPLICIT_TRANSACTIONS auf ON festgelegt ist, ist es, weil die Auswahl der SET ANSI_DEFAULTS ON vorgenommen wurde.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber automatisch IMPLICIT_TRANSACTIONS auf OFF festgelegt, wenn eine Verbindung herstellen. Für Verbindungen mit dem verwalteten SQLClient-Anbieter und für SOAP-Anforderungen, die über HTTP-Endpunkte empfangen, standardmäßig SET IMPLICIT_TRANSACTIONS auf OFF.  
  
 Um die aktuelle Einstellung für IMPLICIT_TRANSACTIONS anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @IMPLICIT_TRANSACTIONS VARCHAR(3) = 'OFF';  
IF ( (2 & @@OPTIONS) = 2 ) SET @IMPLICIT_TRANSACTIONS = 'ON';  
SELECT @IMPLICIT_TRANSACTIONS AS IMPLICIT_TRANSACTIONS;  
```  
  
## <a name="examples"></a>Beispiele  
 Die folgende Transact-SQL-Skript wird ein paar unterschiedliche Testfälle ausgeführt. Die Ausgabe von Text wird ebenfalls bereitgestellt, die zeigt, des detaillierten Verhaltens und von jedem Testfall muss führt.  
  
```tsql  
-- Transact-SQL.  
go  
-- Preparations.  
SET NOCOUNT ON;  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
WHILE (@@TranCount > 0) COMMIT TRANSACTION;  
go  
IF (OBJECT_ID(N'dbo.t1',N'U') IS NOT NULL) DROP TABLE dbo.t1;  
go  
CREATE table dbo.t1 (a int);  
go  
  
PRINT N'-------- [Test A] ---- OFF ----';  
PRINT N'[A.01] Now, SET IMPLICIT_TRANSACTIONS OFF.';  
PRINT N'[A.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
INSERT INTO dbo.t1 VALUES (11);  
INSERT INTO dbo.t1 VALUES (12);  
PRINT N'[A.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test B] ---- ON ----';  
PRINT N'[B.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[B.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
INSERT INTO dbo.t1 VALUES (21);  
INSERT INTO dbo.t1 VALUES (22);  
PRINT N'[B.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[B.04] @@TranCount, after COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test C] ---- ON, then BEGIN TRAN ----';  
PRINT N'[C.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[C.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
BEGIN TRANSACTION;  
INSERT INTO dbo.t1 VALUES (31);  
INSERT INTO dbo.t1 VALUES (32);  
PRINT N'[C.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[C.04] @@TranCount, after a COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
COMMIT TRANSACTION;  
PRINT N'[C.05] @@TranCount, after another COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test D] ---- ON, INSERT, BEGIN TRAN, INSERT ----';  
PRINT N'[D.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[D.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
INSERT INTO dbo.t1 VALUES (41);  
BEGIN TRANSACTION;  
INSERT INTO dbo.t1 VALUES (42);  
PRINT N'[D.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[D.04] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
COMMIT TRANSACTION;  
PRINT N'[D.05] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
-- Clean up.  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
WHILE (@@TranCount > 0) COMMIT TRANSACTION;  
go  
DROP TABLE dbo.t1;  
go  
```  
  
 Als Nächstes wird die Ausgabe von Text aus dem vorherigen Transact-SQL-Skript aus.  
  
```tsql  
-- Text output from Transact-SQL:  
  
-------- [Test A] ---- OFF ----  
[A.01] Now, SET IMPLICIT_TRANSACTIONS OFF.  
[A.02] @@TranCount, at start, == 0  
[A.03] @@TranCount, after INSERTs, == 0  
  
-------- [Test B] ---- ON ----  
[B.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[B.02] @@TranCount, at start, == 0  
[B.03] @@TranCount, after INSERTs, == 1  
[B.04] @@TranCount, after COMMIT, == 0  
  
-------- [Test C] ---- ON, then BEGIN TRAN ----  
[C.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[C.02] @@TranCount, at start, == 0  
[C.03] @@TranCount, after INSERTs, == 2  
[C.04] @@TranCount, after a COMMIT, == 1  
[C.05] @@TranCount, after another COMMIT, == 0  
  
-------- [Test D] ---- ON, INSERT, BEGIN TRAN, INSERT ----  
[D.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[D.02] @@TranCount, at start, == 0  
[D.03] @@TranCount, after INSERTs, == 2  
[D.04] @@TranCount, after INSERTs, == 1  
[D.05] @@TranCount, after INSERTs, == 0  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [Abrufen von Daten &#40; Transact-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPEN &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [TRUNCATE TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

