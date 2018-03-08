---
title: RECHTS (Transact-SQL) | Microsoft Docs
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
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b6680078aff2e103655a94ec157371a0d09f79be
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den rechten Teil einer Zeichenfolge mit der angegebenen Anzahl von Zeichen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichen- oder Binärdaten darstellen. *Character_expression* kann eine Konstante, Variable oder Spalte sein. *Character_expression* kann einen beliebigen Datentyp aufweisen, mit Ausnahme von **Text** oder **Ntext**, implizit zu konvertiert werden können **Varchar** oder  **Nvarchar**. Verwenden Sie andernfalls die [Umwandlung](../../t-sql/functions/cast-and-convert-transact-sql.md) Funktion explizit konvertieren *Character_expression*.  
  
 *integer_expression*  
 Eine positive ganze Zahl, die angibt, wie viele Zeichen des *Character_expression* zurückgegeben werden. Wenn *Integer_expression* ist negativ ist, wird ein Fehler zurückgegeben. Wenn *Integer_expression* Typ **"bigint"** und enthält einen hohen Wert *Character_expression* muss einen Datentyp mit umfangreichen wie z. B. **varchar(max)**.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt **Varchar** Wenn *Character_expression* ein nicht-Unicode-Zeichendatentyp ist.  
  
 Gibt **Nvarchar** Wenn *Character_expression* ein Unicode-Zeichendatentyp ist.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Bei Verwendung von SC-Sortierungen zählt die RIGHT-Funktion ein UTF-16-Ersatzpaar als einzelnes Zeichen. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-right-with-a-column"></a>A: Verwenden von rechts mit einer Spalte  
 Im folgenden Beispiel werden die fünf am weitesten rechts stehenden Zeichen des Vornamens jeder Person in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. Verwenden von rechts mit einer Spalte  
 Das folgende Beispiel gibt die fünf äußersten rechten Zeichen von jeder letzte Name in der `DimEmployee` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>C. Verwenden von rechts mit einer Zeichenfolge  
 Im folgenden Beispiel wird `RIGHT` zurückzugebenden die beiden äußeren rechten Zeichen der Zeichenfolge `abcdefg`.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) RIGHT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>Siehe auch  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

