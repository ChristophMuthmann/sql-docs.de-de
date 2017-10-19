---
title: COT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COT_TSQL
- COT
dev_langs:
- TSQL
helpviewer_keywords:
- COT function
- cotangent
ms.assetid: c87a9dac-e398-4125-80c3-7df3c2ce6b63
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 080b20e15242342e9662b5b4c459a9e8160822ab
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="cot-transact-sql"></a>COT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine mathematische Funktion, die den trigonometrischen Kotangens des angegebenen Winkels im Bogenmaß im angegebenen zurückgibt **"float"** Ausdruck.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
COT ( float_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*float_expression*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md)des Typs **"float"** oder eines Typs, der implizit konvertiert werden können **"float"**.
  
## <a name="return-types"></a>Rückgabetypen
**float**
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird der Kotangens des angegebenen Winkels zurückgegeben.
  
```sql
DECLARE @angle float;  
SET @angle = 124.1332;  
SELECT 'The COT of the angle is: ' + CONVERT(varchar,COT(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COT of the angle is: -0.040312                
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


