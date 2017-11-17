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
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 1868f902cf41eba9637138d7333ac908c72cb76e
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="difference-transact-sql"></a>Unterschied (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen Ganzzahlwert, der den Unterschied zwischen den SOUNDEX-Werten von zwei Zeichenausdrücken angibt.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein alphanumerischer [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichendaten. *Character_expression* kann eine Konstante, Variable oder Spalte sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>"Hinweise"  
 Die zurückgegebene ganze Zahl ist die Anzahl der Zeichen in den SOUNDEX-Werten, die identisch sind. Der Rückgabewert liegt zwischen 0 und 4:0 gibt an, schwache oder keiner Ähnlichkeit und 4 weist auf starke Ähnlichkeit oder identische Werte hin.  
  
 DIFFERENCE und SOUNDEX sind sortierungsabhängig.  
  
## <a name="examples"></a>Beispiele für  
 Im ersten Teil des folgenden Beispiels die `SOUNDEX` Werte von zwei sehr ähnlichen Zeichenfolgen verglichen werden. Bei einer Sortierung Latin1_General `DIFFERENCE` gibt einen Wert von `4`. Im zweiten Teil des folgenden Beispiels die `SOUNDEX` Werte von zwei sehr unterschiedliche Zeichenfolgen verglichen werden, und bei einer Sortierung Latin1_General `DIFFERENCE` gibt einen Wert von `0`.  
  
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
  
  


