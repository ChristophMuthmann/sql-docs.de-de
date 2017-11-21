---
title: '@@TRANCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TRANCOUNT_TSQL'
- '@@TRANCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TRANCOUNT function'
- number of active transactions
- connections [SQL Server], active transactions
- active transactions
ms.assetid: b2638410-e410-4bd0-9b54-90096182b2b6
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19713aeb9058e83f97500075a1024c6c715628e9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40trancount-transact-sql"></a>& #x 40; & #x 40; TRANCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Anzahl von BEGIN TRANSACTION-Anweisungen zurück, die auf der aktuellen Verbindung aufgetreten sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@TRANCOUNT  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 Die BEGIN TRANSACTION-Anweisung erhöht @@@TRANCOUNT um 1. Setzt ROLLBACK TRANSACTION @@TRANCOUNT auf 0; lediglich ROLLBACK TRANSACTION *Savepoint_name*, wirkt sich nicht@TRANCOUNT. COMMIT TRANSACTION oder COMMIT WORK @ Dekrementieren@TRANCOUNT um 1.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-showing-the-effects-of-the-begin-and-commit-statements"></a>A. Veranschaulichen der Auswirkungen der Anweisungen BEGIN und COMMIT  
 Im folgenden Beispiel wird die Wirkung von geschachtelten `BEGIN`- und `COMMIT`-Anweisungen auf die `@@TRANCOUNT`-Variable gezeigt.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The COMMIT statement will decrement the transaction count by 1.  
    COMMIT  
    PRINT @@TRANCOUNT  
COMMIT  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--1  
--0  
```  
  
### <a name="b-showing-the-effects-of-the-begin-and-rollback-statements"></a>B. Veranschaulichen der Auswirkungen der Anweisungen BEGIN und ROLLBACK  
 Im folgenden Beispiel wird die Wirkung von geschachtelten `BEGIN TRAN`- und `ROLLBACK`-Anweisungen auf die `@@TRANCOUNT`-Variable gezeigt.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The ROLLBACK statement will clear the @@TRANCOUNT variable  
--  to 0 because all active transactions will be rolled back.  
ROLLBACK  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--0  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

