---
title: DIFFERENCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
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
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 359260c8c0b227cd756650be5ad1b2f9738d6852
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 Ein alphanumerischer [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der Zeichendaten. *character_expression* kann eine Konstante, Variable oder Spalte sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 Die zurückgegebene ganze Zahl entspricht der Anzahl von gleichen Zeichen in den SOUNDEX-Werten. Der zurückgegebene Wert liegt im Bereich von 0 bis 4: 0 gibt an, dass keine oder nur eine geringe Ähnlichkeit besteht, 4 weist auf eine starke Ähnlichkeit oder identische Werte hin.  
  
 DIFFERENCE und SOUNDEX sind sortierungsabhängig.  
  
## <a name="examples"></a>Beispiele  
 Im ersten Teil des folgenden Beispiels werden die `SOUNDEX`-Werte von zwei sehr ähnlichen Zeichenfolgen verglichen. Für eine Latin1_General-Sortierung gibt `DIFFERENCE` einen Wert von `4` zurück. Im zweiten Teil des folgenden Beispiels werden die `SOUNDEX`-Werte von zwei sehr unterschiedlichen Zeichenfolgen verglichen, wobei `DIFFERENCE` für eine Latin1_General-Sortierung den Wert `0` zurückgibt.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

