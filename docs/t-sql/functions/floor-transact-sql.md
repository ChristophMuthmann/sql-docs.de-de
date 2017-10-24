---
title: FLOOR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FLOOR_TSQL
- FLOOR
dev_langs:
- TSQL
helpviewer_keywords:
- integers [SQL Server]
- largest integers
- FLOOR function [Transact-SQL]
ms.assetid: 4f26c784-9240-491f-b854-754be3fccae4
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 765cdfb78d13dfa2054571812a051250b19d9d8e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="floor-transact-sql"></a>FLOOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt die größte ganze Zahl zurück, die kleiner oder gleich dem angegebenen numerischen Ausdruck ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
FLOOR ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ist ein Ausdruck, der Kategorie der genauen numerischen oder ungefähren numerischen Daten, mit Ausnahme der **Bit** -Datentyp.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt denselben Typ wie *Numerischer Ausdruck*zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Verwendung von positiven und negativen numerischen Werten sowie von Währungsangaben mit der `FLOOR`-Funktion gezeigt.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 Das Ergebnis ist der ganzzahlige Teil des berechneten Werts den gleichen Datentyp wie *Numeric_expression*.  
  
```  
---------      ---------     -----------  
123            -124          123.0000     
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel zeigt die positiven numerischen, negativen numerischen und Werte mit den `FLOOR` Funktion.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 Das Ergebnis ist der ganzzahlige Teil des berechneten Werts den gleichen Datentyp wie *Numeric_expression*.  
  
 ```
 -----   ---------    -----------  
  
 123     -124         123
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


