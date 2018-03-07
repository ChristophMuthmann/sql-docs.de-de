---
title: SET ROWCOUNT (Transact-SQL) | Microsoft Docs
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
- SET_ROWCOUNT_TSQL
- ROWCOUNT_TSQL
- SET ROWCOUNT
- ROWCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- row return limitations [SQL Server]
- SET ROWCOUNT statement
- number of rows affected by statement
- ROWCOUNT option
- counting rows
- stopping queries
- limiting rows returned
- queries [SQL Server], stopping
ms.assetid: c6966fb7-6421-47ef-98f3-82351f2f6bdc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1e27fcb521763eb38d7aec4a89d8a9e13d7e520f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="set-rowcount-transact-sql"></a>SET ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bewirkt, dass die Verarbeitung der Abfrage durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet wird, sobald die angegebene Anzahl von Zeilen zurückgegeben wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET ROWCOUNT { number | @number_var }   
```  
  
## <a name="arguments"></a>Argumente  
 *Anzahl* | @*Number_var*  
 Die Zahl (eine ganze Zahl), die festlegt, wie viele Zeilen verarbeitet werden sollen, bevor die angegebene Abfrage beendet wird.  
  
## <a name="remarks"></a>Hinweise  
  
> [!IMPORTANT]  
>  Die Verwendung von SET ROWCOUNT wird in einer zukünftigen Version von SQL Server keine Auswirkungen auf die Anweisungen DELETE, INSERT und UPDATE haben. Vermeiden Sie beim Entwickeln neuer Anwendungen das Verwenden von SET ROWCOUNT zusammen mit DELETE-, INSERT- und UPDATE-Anweisungen, und planen Sie die Änderung von Anwendungen, in denen dies zurzeit verwendet wird. Die Verwendung der TOP-Syntax ergibt ein ähnliches Verhalten. Weitere Informationen finden Sie unter [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 Um diese Option zu deaktivieren (sodass alle Zeilen zurückgegeben werden), geben Sie SET ROWCOUNT 0 an.  
  
 Das Festlegen der Option ROWCOUNT veranlasst, dass die meisten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen die Verarbeitung beenden, wenn die angegebene Anzahl von Zeilen bearbeitet wurde. Dies gilt auch für Trigger. Die Option ROWCOUNT wirkt sich nicht auf dynamische Cursor aus, begrenzt jedoch das Rowset von Keyset- und INSENSITIVE-Cursorn. Diese Option sollte mit Vorsicht eingesetzt werden.  
  
 SET ROWCOUNT überschreibt das TOP-Schlüsselwort der SELECT-Anweisung, wenn die Zeilenanzahl der kleinere Wert ist.  
  
 Die Einstellung von SET ROWCOUNT wird zur Laufzeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 SET ROWCOUNT beendet die Verarbeitung nach der angegebenen Anzahl von Zeilen. Beachten Sie im folgenden Beispiel, dass über 500 Zeilen mit dem Kriterium `Quantity` kleiner als `300` übereinstimmen. Wenn SET ROWCOUNT angewendet wurde, werden jedoch nicht alle Zeilen zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT count(*) AS Count  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Count 
 ----------- 
 537 
 
 (1 row(s) affected)
 ```  
  
 Legen Sie jetzt `ROWCOUNT` auf `4` fest, und geben Sie alle Zeilen zurück, um zu zeigen, dass nur 4 Zeilen zurückgegeben werden.  
  
```  
SET ROWCOUNT 4;  
SELECT *  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
  
(4 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 SET ROWCOUNT beendet die Verarbeitung nach der angegebenen Anzahl von Zeilen. Im folgenden Beispiel beachten Sie, dass mehr als 20 Zeilen mit dem Kriterium `AccountType = 'Assets'`. Wenn SET ROWCOUNT angewendet wurde, werden jedoch nicht alle Zeilen zurückgegeben.  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 5;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
 Um alle Zeilen zurückzugeben, ZEILENANZAHL auf 0 festgelegt.  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 0;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

