---
title: SET XACT_ABORT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/07/2016
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
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- XACT_ABORT_TSQL
- XACT_ABORT
- SET XACT_ABORT
- SET_XACT_ABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- XACT_ABORT option
- automatic transaction roll backs
- transactions [SQL Server], rolling back
- rolling back transactions, SET XACT_ABORT
- roll back transactions [SQL Server]
- SET XACT_ABORT statement
ms.assetid: cbcaa433-58f2-4dc3-a077-27273bef65b5
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3262e9dcbc40aeadf840181d9be5711858f08ec6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-xactabort-transact-sql"></a>SET XACT_ABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

    
> [!NOTE]  
>  Die **AUSLÖSEN** Anweisung berücksichtigt **Festlegen von XACT_ABORT RAISERROR** hingegen nicht. Neue Anwendungen sollten verwenden **AUSLÖSEN** anstelle von **RAISERROR**.  
  
 Gibt an, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die aktuelle Transaktion automatisch ein Rollback ausführt, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung einen Laufzeitfehler ausgibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET XACT_ABORT { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET XACT_ABORT ON   
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET XACT_ABORT auf ON festgelegt ist und eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung einen Laufzeitfehler auslöst, wird die gesamte Transaktion beendet, und es wird ein Rollback für sie ausgeführt.  
  
 Wenn SET XACT_ABORT auf OFF festgelegt ist, wird in einigen Fällen nur für die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, die den Fehler ausgelöst hat, ein Rollback ausgeführt, und die Transaktion wird fortgesetzt. Abhängig vom Schweregrad des Fehlers wird möglicherweise für die gesamte Transaktion ein Rollback ausgeführt, wenn SET XACT_ABORT auf OFF festgelegt ist. OFF ist die Standardeinstellung.  
  
 Kompilierungsfehler, wie z. B. Syntaxfehler, sind von SET XACT_ABORT nicht betroffen.  
  
 Es ist erforderlich, dass XACT_ABORT für Anweisungen zur Datenänderung in einer impliziten oder expliziten Transaktion für die meisten OLE DB-Anbieter, einschließlich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], auf ON festgelegt ist. Nur wenn der Anbieter geschachtelte Transaktionen unterstützt, ist diese Option nicht erforderlich.  
  
 Bei ANSI_WARNINGS=OFF werden Transaktionen aufgrund von Berechtigungsverletzungen abgebrochen.  
  
 Die Einstellung von SET XACT_ABORT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @XACT_ABORT VARCHAR(3) = 'OFF';  
IF ( (16384 & @@OPTIONS) = 16384 ) SET @XACT_ABORT = 'ON';  
SELECT @XACT_ABORT AS XACT_ABORT;  
  
```  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Codebeispiel wird eine Fremdschlüsselverletzung in einer Transaktion verursacht, die weitere [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen enthält. In der ersten Anweisungsgruppe wird der Fehler generiert; die anderen Anweisungen werden jedoch erfolgreich ausgeführt, und für die Transaktion wird erfolgreich ein Commit ausgeführt. Im zweiten Anweisungssatz ist `SET XACT_ABORT` auf `ON` festgelegt. Der Anweisungsfehler bewirkt daher, dass der Batch abgebrochen und für die Transaktion ein Rollback ausgeführt wird.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't2', N'U') IS NOT NULL  
    DROP TABLE t2;  
GO  
IF OBJECT_ID(N't1', N'U') IS NOT NULL  
    DROP TABLE t1;  
GO  
CREATE TABLE t1  
    (a INT NOT NULL PRIMARY KEY);  
CREATE TABLE t2  
    (a INT NOT NULL REFERENCES t1(a));  
GO  
INSERT INTO t1 VALUES (1);  
INSERT INTO t1 VALUES (3);  
INSERT INTO t1 VALUES (4);  
INSERT INTO t1 VALUES (6);  
GO  
SET XACT_ABORT OFF;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (1);  
INSERT INTO t2 VALUES (2); -- Foreign key error.  
INSERT INTO t2 VALUES (3);  
COMMIT TRANSACTION;  
GO  
SET XACT_ABORT ON;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (4);  
INSERT INTO t2 VALUES (5); -- Foreign key error.  
INSERT INTO t2 VALUES (6);  
COMMIT TRANSACTION;  
GO  
-- SELECT shows only keys 1 and 3 added.   
-- Key 2 insert failed and was rolled back, but  
-- XACT_ABORT was OFF and rest of transaction  
-- succeeded.  
-- Key 5 insert error with XACT_ABORT ON caused  
-- all of the second transaction to roll back.  
SELECT *  
    FROM t2;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [THROW &#40; Transact-SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

