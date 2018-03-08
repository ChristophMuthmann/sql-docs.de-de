---
title: LEFT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
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
- LEFT
- LEFT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- character strings [SQL Server], LEFT
- characters [SQL Server], leftmost
- LEFT function
- leftmost character of expression
ms.assetid: 44a8c71b-63d8-458b-8b5d-99d570067c3c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 822680e5939e628b17c15d08c3cb513ad9b348ed
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="left-transact-sql"></a>LEFT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den linken Teil einer Zeichenfolge mit der angegebenen Anzahl von Zeichen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichen- oder Binärdaten darstellen. *Character_expression* kann eine Konstante, Variable oder Spalte sein. *Character_expression* kann einen beliebigen Datentyp aufweisen, mit Ausnahme von **Text** oder **Ntext**, implizit zu konvertiert werden können **Varchar** oder  **Nvarchar**. Verwenden Sie andernfalls die [Umwandlung](../../t-sql/functions/cast-and-convert-transact-sql.md) Funktion explizit konvertieren *Character_expression*.  
  
 *integer_expression*  
 Eine positive ganze Zahl, die angibt, wie viele Zeichen von der *Character_expression* zurückgegeben werden. Wenn *Integer_expression* ist negativ ist, wird ein Fehler zurückgegeben. Wenn *Integer_expression* Typ **"bigint"** und enthält einen hohen Wert *Character_expression* muss einen Datentyp mit umfangreichen wie z. B. **varchar(max)**.  
  
 Die *Integer_expression* Parameter wird ein UTF-16-Ersatzzeichen als ein Zeichen gezählt.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt **Varchar** Wenn *Character_expression* ein nicht-Unicode-Zeichendatentyp ist.  
  
 Gibt **Nvarchar** Wenn *Character_expression* ein Unicode-Zeichendatentyp ist.  
  
## <a name="remarks"></a>Hinweise  
 Bei Verwendung von SC-Sortierungen der *Integer_expression* Parameter wird ein UTF-16-Ersatzpaar als ein Zeichen gezählt. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-left-with-a-column"></a>A. Verwenden von LEFT mit einer Spalte  
 Im folgenden Beispiel werden die fünf am weitesten links stehenden Zeichen jedes Produktnamens in der `Product`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>B. Verwenden von LEFT mit einer Zeichenfolge  
 Im folgenden Beispiel wird `LEFT` zur Rückgabe der beiden ersten Zeichen der Zeichenfolge `abcdefg` verwendet.  
  
```  
SELECT LEFT('abcdefg',2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab   
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>C. Verwenden von LEFT mit einer Spalte  
 Im folgenden Beispiel werden die ersten fünf Zeichen der Produktnamen zurückgegeben.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>D. Verwenden von LEFT mit einer Zeichenfolge  
 Im folgenden Beispiel wird `LEFT` zur Rückgabe der beiden ersten Zeichen der Zeichenfolge `abcdefg` verwendet.  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab  
```  
  
## <a name="see-also"></a>Siehe auch  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

