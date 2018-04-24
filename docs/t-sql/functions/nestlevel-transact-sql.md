---
title: '@@NESTLEVEL (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29c00b33b0d27b9f9446942dfb81430526ff4f85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40nestlevel-transact-sql"></a>&#x40;&#x40;NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Schachtelungsebene der aktuellen Ausführung einer gespeicherten Prozedur auf dem lokalen Server zurück (anfangs 0).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@NESTLEVEL  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 Jedes Mal, wenn eine gespeicherte Prozedur eine andere gespeicherte Prozedur aufruft oder durch Verweis auf eine Common Language Routine (CLR), einen Typ oder ein Aggregat verwalteten Code ausführt, wird die Schachtelungsebene erhöht. Wird der Höchstwert von 32 überschritten, so wird die Transaktion beendet.  
  
 Wenn @@NESTLEVEL innerhalb einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeichenfolge ausgeführt wird, entspricht der zurückgegebene Wert 1 + der aktuellen Schachtelungsebene. Wenn @@NESTLEVEL mithilfe von sp_executesql dynamisch ausgeführt wird, entspricht der zurückgegebene Wert 2 + der aktuellen Schachtelungsebene.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-nestlevel-in-a-procedure"></a>A. Verwenden von @@NESTLEVEL in einer Prozedur  
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
  
### <a name="b-calling-nestlevel"></a>B. Aufrufen von @@NESTLEVEL  
 Das folgende Beispiel zeigt die unterschiedlichen Werte, die von `SELECT`, `EXEC`und `sp_executesql` zurückgegeben werden, wenn jeweils `@@NESTLEVEL` aufgerufen wird.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
