---
title: EXP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- EXP_TSQL
- EXP
dev_langs:
- TSQL
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 5a9b8c52-6fb6-4e33-8b02-a878785b2f51
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c50757291a8f1fc3d58d8a9a131c4a24aa79a008
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="exp-transact-sql"></a>EXP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Exponentialwert des angegebenen **"float"** Ausdruck.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
EXP ( float_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *float_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) des Typs **"float"** oder eines Typs, der implizit konvertiert werden können **"float"**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **float**  
  
## <a name="remarks"></a>Hinweise  
 Die Konstante **e** (2,718281...), ist die Basis des natürlichen Logarithmus.  
  
 Der Exponent einer Zahl ist die Konstante **e** potenziert mit der Zahl. Beispielsweise EXP(1,0) = e^1,0 = 2,71828182845905 und EXP(10) = e^10 = 22026,4657948067.  
  
 Der Exponentialwert des natürlichen Logarithmus einer Zahl ist die Zahl selbst: EXP (LOG (*n*)) =  *n* . Und der natürliche Logarithmus des Exponentialwerts einer Zahl ist die Zahl selbst: LOG (EXP (*n*)) =  *n* .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-finding-the-exponent-of-a-number"></a>A. Suchen des Exponenten einer Zahl  
 Im folgenden Beispiel wird eine Variable deklariert und der exponentielle Wert der angegebenen Variablen (`10`) mit einer Textbeschreibung zurückgegeben.  
  
```  
DECLARE @var float  
SET @var = 10  
SELECT 'The EXP of the variable is: ' + CONVERT(varchar,EXP(@var))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------------------------------  
The EXP of the variable is: 22026.5  
(1 row(s) affected)  
```  
  
### <a name="b-finding-exponentials-and-natural-logarithms"></a>B. Suchen von Exponentialgrößen und natürlichen Logarithmen  
 Im folgenden Beispiel werden der exponentielle Wert des natürlichen Logarithmus von `20` sowie der natürliche Logarithmus des exponentiellen Werts von `20` zurückgegeben. Bei diesen Funktionen handelt es sich um Umkehrfunktionen anderer Funktionen. Deshalb ist der Rückgabewert in beiden Fällen `20`.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------- ----------------------  
20                     20  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-finding-the-exponent-of-a-number"></a>C. Suchen des Exponenten einer Zahl  
 Das folgende Beispiel gibt den Exponentialwert des angegebenen Werts zurück (`10`).  
  
```  
SELECT EXP(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------  
22026.4657948067  
```  
  
### <a name="d-finding-exponential-values-and-natural-logarithms"></a>D. Suchen exponentieller Werte und natürlicher Logarithmen  
 Im folgenden Beispiel werden der exponentielle Wert des natürlichen Logarithmus von `20` sowie der natürliche Logarithmus des exponentiellen Werts von `20` zurückgegeben. Bei diesen Funktionen handelt es sich um Umkehrfunktionen anderer Funktionen. Deshalb ist der Rückgabewert in beiden Fällen `20`.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------- -----------------  
20                  20  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [Melden Sie sich &#40; Transact-SQL &#41;](../../t-sql/functions/log-transact-sql.md)   
 [LOG10 &#40; Transact-SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  


