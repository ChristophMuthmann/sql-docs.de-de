---
title: LOG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
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
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7918cb0d2832e88f3e4218b98c7f606f559f2e4e
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="log-transact-sql"></a>LOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den natürlichen Logarithmus des angegebenen **"float"** Ausdruck in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *float_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) des Typs **"float"** oder eines Typs, der implizit konvertiert werden können **"float"**.  
  
 *Basis*  
 Optionales ganzzahliges Argument, das die Basis des Logarithmus festlegt.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
## <a name="return-types"></a>Rückgabetypen  
 **float**  
  
## <a name="remarks"></a>Hinweise  
 Standardmäßig **LOG()** gibt den natürlichen Logarithmus zurück. Beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], Sie können die Basis des Logarithmus in einen anderen Wert ändern, indem Sie mit dem optionalen *Basis* Parameter.  
  
 Der natürliche Logarithmus ist der Logarithmus zur Basis **e**, wobei **e** entspricht eine Irrationale Konstante ungefähr 2,718281828 ist.  
  
 Der natürliche Logarithmus des Exponentialwerts einer Zahl ist die Zahl selbst: LOG (EXP (  *n*  )) =  *n* . Und der Exponentialwert des natürlichen Logarithmus einer Zahl ist die Zahl selbst: EXP (LOG (  *n*  )) =  *n* .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. Berechnen des Logarithmus für eine Zahl.  
 Das folgende Beispiel berechnet den `LOG` für den angegebenen **"float"** Ausdruck.  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. Berechnen des Logarithmus des Exponenten einer Zahl.  
 Das folgende Beispiel berechnet den `LOG`-Wert für den Exponenten einer Zahl.  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. Berechnen des Logarithmus für eine Zahl  
 Das folgende Beispiel berechnet den `LOG` für den angegebenen **"float"** Ausdruck.  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40; Transact-SQL &#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40; Transact-SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  


