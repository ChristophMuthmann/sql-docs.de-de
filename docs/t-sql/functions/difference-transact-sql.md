---
title: Unterschied (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 373964f1d2c99935e012b257634ec97491971518
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen ganzzahligen Wert zurück, der den Unterschied zwischen den SOUNDEX-Werten von zwei Zeichenausdrücken angibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein alphanumerischer [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichendaten. *Character_expression* kann eine Konstante, Variable oder Spalte sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Die zurückgegebene ganze Zahl entspricht der Anzahl von gleichen Zeichen in den SOUNDEX-Werten. Der zurückgegebene Wert liegt im Bereich von 0 bis 4: 0 gibt an, dass keine oder nur eine geringe Ähnlichkeit besteht, 4 weist auf eine starke Ähnlichkeit oder identische Werte hin.  
  
 DIFFERENCE und SOUNDEX sind sortierungsabhängig.  
  
## <a name="examples"></a>Beispiele  
 Im ersten Teil des folgenden Beispiels werden die `SOUNDEX`-Werte von zwei sehr ähnlichen Zeichenfolgen verglichen. Bei einer Sortierung Latin1_General `DIFFERENCE` gibt einen Wert von `4`. Im zweiten Teil des folgenden Beispiels die `SOUNDEX` Werte von zwei sehr unterschiedliche Zeichenfolgen verglichen werden, und bei einer Sortierung Latin1_General `DIFFERENCE` gibt einen Wert von `0`.  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SOUNDEX &#40; Transact-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

