---
title: LEFT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e197c6ea66af3cc5f2ba83200a61c29ce6d6eca2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) aus Zeichen- oder Binärdaten. *character_expression* kann eine Konstante, Variable oder Spalte sein. *character_expression* kann von einem beliebigen Datentyp sein, ausschließlich **text** oder **ntext**, der implizit in **varchar** oder **nvarchar** konvertiert werden kann. Verwenden Sie in allen anderen Fällen die [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md)-Funktion zur expliziten Konvertierung von *character_expression*.  
  
 *integer_expression*  
 Ein positiver Integer, der angibt, wie viele Zeichen von *character_expression* zurückgegeben werden. Wenn *integer_expression* negativ ist, wird ein Fehler zurückgegeben. Wenn *integer_expression* vom Typ **bigint** ist und einen hohen Wert hat, muss *character_expression* von einem umfangreicheren Datentyp wie z.B. **varchar(max)** sein.  
  
 Für den *integer_expression*-Parameter wird ein UTF-16-Ersatzzeichen als ein Zeichen gezählt.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt **varchar** zurück, wenn es sich bei *character_expression* um einen Zeichendatentyp handelt, der Unicode nicht unterstützt.  
  
 Gibt **nvarchar** zurück, wenn es sich bei *character_expression* um einen Zeichendatentyp handelt, der Unicode nicht unterstützt.  
  
## <a name="remarks"></a>Remarks  
 Bei Verwendung von SC-Sortierungen zählt der *integer_expression*-Parameter ein UTF-16-Ersatzpaar als ein Zeichen. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

