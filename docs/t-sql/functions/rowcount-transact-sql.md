---
title: '@@ROWCOUNT (Transact-SQL) | Microsoft Docs'
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
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411dc7eb628ddff52eb2f9426488e05860c9d279
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40rowcount-transact-sql"></a>& #x 40; & #x 40; ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Anzahl der Zeilen zurück, auf die sich die letzte Anweisung ausgewirkt hat. Wenn die Anzahl der Zeilen mehr als 2 Milliarden ist, verwenden Sie [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen können legen Sie den Wert im @@ROWCOUNT auf folgende Weise:  
  
-   Set @@ROWCOUNT auf die Anzahl der Zeilen betroffen sind bzw. davon zu lesen. Zeilen werden möglicherweise an den Client gesendet.  
  
-   Beibehalten@ROWCOUNT aus der vorherigen anweisungsausführung.  
  
-   Zurücksetzen@ROWCOUNT auf 0 jedoch keinen Wert an den Client zurück.  
  
 Anweisungen, die eine einfache Zuweisung, legen Sie immer die @@ROWCOUNT den Wert 1. Es werden keine Zeilen an den Client gesendet. Beispiele für diese Anweisungen: SET @*Local_variable*, RETURN, READTEXT und Select ohne abfrageanweisungen wie SELECT GETDATE() oder SELECT **"***Generic Text* **'**.  
  
 Anweisungen, die eine Zuweisung in einer Abfrage vornehmen oder RETURN in einer Abfrage der @@ROWCOUNT Wert, der die Anzahl der Zeilen von betroffenen oder gelesenen die Abfrage z. B.: Wählen Sie*Local_variable* = c1 FROM t1.  
  
 Data Manipulation Language (DML) Anweisungen legen die @@ROWCOUNT -Wert an die Anzahl der Zeilen, die von der Abfrage betroffen sind, und gibt diesen Wert an den Client zurück. Die DML-Anweisungen senden möglicherweise keine Zeilen an den Client.  
  
 DECLARE CURSOR und FETCH legen Sie den @@ROWCOUNT den Wert 1.  
  
 EXECUTE-Anweisungen behalten die vorherige @@ROWCOUNT.  
  
 Anweisungen wie z. B. verwenden, legen Sie \<Option >, DEALLOCATE CURSOR, CLOSE CURSOR, BEGIN TRANSACTION oder COMMIT TRANSACTION der ROWCOUNT-Wert auf 0 zurückgesetzt.  
  
 Systemintern kompilierte gespeicherte Prozeduren erhalten die vorherigen @@ROWCOUNT. [!INCLUDE[tsql](../../includes/tsql-md.md)]Legen Sie die Anweisungen in systemintern kompilierten gespeicherten Prozeduren nicht@ROWCOUNT. Weitere Informationen finden Sie unter [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel führt eine `UPDATE`-Anweisung aus und erkennt mithilfe von `@@ROWCOUNT`, ob Zeilen geändert wurden.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SET ROWCOUNT &#40; Transact-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  

