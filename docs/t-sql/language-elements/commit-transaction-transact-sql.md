---
title: COMMIT TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 815d114944cfa233777fce1ba01c4639cc7417b3
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Markiert das Ende einer erfolgreichen impliziten oder expliziten Transaktion. @ IF@TRANCOUNT beträgt 1, COMMIT TRANSACTION macht alle datenänderungen seit dem Start der Transaktion einen dauerhaften Bestandteil der Datenbank durch die Transaktion und dekrementiert @ belegten Ressourcen freigegeben@TRANCOUNT auf 0. @ IF@TRANCOUNT ist größer als 1, COMMIT TRANSACTION dekrementiert @@TRANCOUNT nur von 1 und die Transaktion bleibt aktiv.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>Argumente  
 *transaction_name*  
 **GILT für:** SQL Server- und Azure SQL-Datenbank
 
 Wird vom [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ignoriert. *Transaction_name* gibt einen Transaktionsnamen an, die von einer vorherigen BEGIN TRANSACTION zugewiesen. *Transaction_name*muss den Regeln für Bezeichner entsprechen, jedoch 32 Zeichen nicht überschreiten. *Transaction_name* kann die Übersichtlichkeit Übersichtlichkeit verbessern Programmierern angezeigt wird, welcher geschachtelten BEGIN TRANSACTION, COMMIT TRANSACTION zugeordnet ist.  
  
 *@tran_name_variable*  
 **GILT für:** SQL Server- und Azure SQL-Datenbank  
 
Ist der Name einer benutzerdefinierten Variablen, die einen gültigen Transaktionsnamen enthält. Die Variable muss mit einem Char, Varchar, Nchar oder Nvarchar-Datentyp deklariert werden. Werden mehr als 32 Zeichen an die Variable übergeben, werden nur die ersten 32 Zeichen verwendet, die restlichen Zeichen werden abgeschnitten.  
  
 DELAYED_DURABILITY  
 **GILT für:** SQL Server- und Azure SQL-Datenbank   

 Eine Option, die erfordert, dass für diese Transaktion ein Commit mit verzögerter Dauerhaftigkeit ausgeführt wird. Die Anforderung wird ignoriert, wenn die Datenbank mit `DELAYED_DURABILITY = DISABLED` oder `DELAYED_DURABILITY = FORCED` geändert wurde. Finden Sie im Thema [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md) für Weitere Informationen.  
  
## <a name="remarks"></a>Hinweise  
 Es liegt in der Verantwortung des [!INCLUDE[tsql](../../includes/tsql-md.md)]-Programmierers, COMMIT TRANSACTION nur zu einem Zeitpunkt auszugeben, zu dem alle Daten, auf die die Transaktion verweist, logisch richtig sind.  
  
 War die Transaktion, für die ein Commit ausgeführt wird, eine verteilte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion, wird MS DTC von COMMIT TRANSACTION veranlasst, mithilfe eines Zweiphasencommit-Protokolls für alle an der Transaktion beteiligten Server ein Commit auszuführen. Erstreckt sich eine lokale Transaktion über mehrere Datenbanken in derselben Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s, verwendet die Instanz einen internen Zweiphasencommit, um für alle an der Transaktion beteiligten Datenbanken einen Commit auszuführen.  
  
 Bei der Verwendung in geschachtelten Transaktionen werden durch Commits der inneren Transaktionen keine Ressourcen freigegeben oder Änderungen dauerhaft gespeichert. Die Datenänderungen werden nur dann dauerhaft und Ressourcen nur dann freigegeben, wenn für die äußere Transaktion ein Commit ausgeführt wird. Jeder COMMIT TRANSACTION ausgegeben, wenn @@TRANCOUNT ist größer als 1 einfach dekrementiert @@TRANCOUNT um 1. Wenn @@TRANCOUNT wird schließlich den Wert 0 erreicht, die gesamte äußere Transaktion wird ein Commit ausgeführt wurde. Da *Transaction_name* ignoriert wird die [!INCLUDE[ssDE](../../includes/ssde-md.md)], Ausgeben einer COMMIT TRANSACTION verweisen auf den Namen einer äußeren Transaktion, wenn ausstehende innere Transaktionen nur dekrementiert @@TRANCOUNT um 1.  
  
 Ausgeben einer COMMIT TRANSACTION Wenn @@TRANCOUNT ist 0, führt zu einem Fehler; Es besteht keine entsprechende BEGIN TRANSACTION.  
  
 Nach der Ausgabe einer COMMIT TRANSACTION-Anweisung kann kein Rollback für eine Transaktion ausgeführt werden, da die Datenänderungen zu einem dauerhaften Bestandteil der Datenbank geworden sind.  
  
 Die Transaktionsanzahl in einer Anweisung wird vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] nur erhöht, wenn die Transaktionsanzahl beim Start der Anweisung 0 (null) lautet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-committing-a-transaction"></a>A. Ausführen eines Commits für eine Transaktion  
**GILT für:** SQLServer, Azure SQL-Datenbank, Azure SQL Datawarehouse und Parallel Datawarehouse   

Im folgenden Beispiel wird ein Stellenbewerber gelöscht. AdventureWorks verwendet. 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. Ausführen eines Commits für eine geschachtelte Transaktion  
**GILT für:** SQL Server- und Azure SQL-Datenbank    

Im folgenden Beispiel werden eine Tabelle erstellt und drei Ebenen von geschachtelten Transaktionen generiert, und anschließend wird für die geschachtelte Transaktion ein Commit ausgeführt. Obwohl jede `COMMIT TRANSACTION` Anweisung verfügt über eine *Transaction_name* Parameter, besteht keine Beziehung zwischen der `COMMIT TRANSACTION` und `BEGIN TRANSACTION` Anweisungen. Die *Transaction_name* Parameter sind lediglich Hilfen zur und helfen dem Programmierer, stellen Sie sicher, dass die richtige Anzahl von Commits codiert sind, verringern `@@TRANCOUNT` auf 0 und somit die äußere Transaktion ein commit. 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
