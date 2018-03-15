---
title: LOWER (Transact-SQL) | Microsoft-Dokumentation
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
- LOWER
- LOWER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- characters [SQL Server], lowercase
- LOWER function
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
- converting uppercase to lowercase characters
ms.assetid: 1783352b-6852-4658-9d94-51963c59b9bf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: de6c63278089f6fd871fd826c6b64a2c8991f9e0
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="lower-transact-sql"></a>LOWER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen Zeichenausdruck zurück, dessen Zeichen von Großbuchstaben in Kleinbuchstaben umgewandelt wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
LOWER ( character_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) aus Zeichen- oder Binärdaten. *character_expression* kann eine Konstante, Variable oder Spalte sein. *character_expression* muss einen Datentyp aufweisen, der implizit nach **varchar** konvertiert werden kann. Verwenden Sie in allen anderen Fällen [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) zur expliziten Konvertierung von *character_expression*.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varchar** oder **nvarchar**  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel werden die `LOWER`- und die `UPPER`-Funktion sowie eine Schachtelung der `UPPER`-Funktion in der `LOWER`-Funktion verwendet, um die Produktnamen auszuwählen, deren Preis zwischen 11 $ und 20 $ liegt.  
  
```  
-- Uses AdventureWorks  
  
SELECT LOWER(SUBSTRING(EnglishProductName, 1, 20)) AS Lower,   
       UPPER(SUBSTRING(EnglishProductName, 1, 20)) AS Upper,   
       LOWER(UPPER(SUBSTRING(EnglishProductName, 1, 20))) As LowerUpper  
FROM dbo.DimProduct  
WHERE ListPrice between 11.00 and 20.00;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Lower                 Upper                  LowerUpper  
--------------------  ---------------------  --------------------  
minipump              MINIPUMP               minipump  
taillights – battery  TAILLIGHTS – BATTERY   taillights - battery
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [UPPER &#40;Transact-SQL&#41;](../../t-sql/functions/upper-transact-sql.md)  
  
  

