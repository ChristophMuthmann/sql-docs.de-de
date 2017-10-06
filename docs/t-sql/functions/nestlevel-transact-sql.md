---
title: '@@NESTLEVEL (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@NESTLEVEL'
- '@@NESTLEVEL_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@NESTLEVEL function'
- nesting stored procedures
- stored procedure nesting levels [SQL Server]
ms.assetid: 8c0b2134-8616-44f6-addc-6583c432fb62
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: d02995ee7093d311cbdc6f4b69430a8bc66a618c
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40nestlevel-transact-sql"></a>& #x 40; & #x 40; NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Schachtelungsebene der aktuellen Ausführung einer gespeicherten Prozedur auf dem lokalen Server zurück (anfangs 0).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@NESTLEVEL  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Jedes Mal, wenn eine gespeicherte Prozedur eine andere gespeicherte Prozedur aufruft oder durch Verweis auf eine Common Language Routine (CLR), einen Typ oder ein Aggregat verwalteten Code ausführt, wird die Schachtelungsebene erhöht. Wird der Höchstwert von 32 überschritten, so wird die Transaktion beendet.  
  
 Wenn @@NESTLEVEL ausgeführt wird, innerhalb einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Zeichenfolge, der zurückgegebene Wert ist 1 + der aktuellen Schachtelungsebene. Wenn @@NESTLEVEL ausgeführt wird dynamisch mithilfe von Sp_executesql ist der zurückgegebene Wert 2 + der aktuellen Schachtelungsebene.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-nestlevel-in-a-procedure"></a>A. Mit@NESTLEVEL in einer Prozedur  
 Dieses Beispiel erstellt zwei Prozeduren: Eine, die eine andere Prozedur aufruft, und eine, die die `@@NESTLEVEL` -Einstellung beider Prozeduren anzeigt.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'usp_OuterProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_OuterProc;  
GO  
IF OBJECT_ID (N'usp_InnerProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_InnerProc;  
GO  
CREATE PROCEDURE usp_InnerProc AS   
    SELECT @@NESTLEVEL AS 'Inner Level';  
GO  
CREATE PROCEDURE usp_OuterProc AS   
    SELECT @@NESTLEVEL AS 'Outer Level';  
    EXEC usp_InnerProc;  
GO  
EXECUTE usp_OuterProc;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Outer Level  
-----------  
1  
  
Inner Level  
-----------  
2
```  
  
### <a name="b-calling-nestlevel"></a>B. Aufrufen@NESTLEVEL  
 Das folgende Beispiel zeigt die unterschiedlichen Werte, die von `SELECT`, `EXEC`und `sp`_`executesql` zurückgegeben werden, wenn beide jeweils `@@NESTLEVEL`aufrufen.  
  
```  
CREATE PROC usp_NestLevelValues AS  
    SELECT @@NESTLEVEL AS 'Current Nest Level';  
EXEC ('SELECT @@NESTLEVEL AS OneGreater');   
EXEC sp_executesql N'SELECT @@NESTLEVEL as TwoGreater' ;  
GO  
EXEC usp_NestLevelValues;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Current Nest Level  
------------------  
1  
  
(1 row(s) affected)  
  
OneGreater  
-----------  
2  
  
(1 row(s) affected)  
  
TwoGreater  
-----------  
3  
  
(1 row(s) affected)
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

