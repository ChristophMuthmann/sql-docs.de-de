---
title: ROUND (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROUND_TSQL
- ROUND
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: cba8b5a9b62a21fc810ff9bb5fcd3d0c6429f9f5
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen numerischen Wert zurück, der auf die angegebene Länge oder Genauigkeit gerundet wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ROUND (numeric_expression , length )  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme der **Bit** -Datentyp.  
  
 *length*  
 Ist die Genauigkeit, auf die *Numeric_expression* gerundet werden soll. *Länge* muss ein Ausdruck vom Typ **"tinyint"**, **"smallint"**, oder **Int**. Wenn *Länge* ist eine positive Zahl *numerischer_ausdruck* wird gerundet, um die Anzahl der Dezimalstellen gemäß *Länge*. Wenn *Länge* ist eine negative Zahl *numerischer_ausdruck* gerundet ist und auf der linken Seite des Dezimaltrennzeichens gemäß *Länge*.  
  
 *Funktion*  
 Die Art der auszuführenden Operation. *Funktion* muss **"tinyint"**, **"smallint"**, oder **Int**. Wenn *Funktion* fehlt oder hat den Wert 0 (Standard), *Numeric_expression* wird gerundet. Wenn ein anderer Wert als 0 angegeben wird, *Numeric_expression* abgeschnitten wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt die folgenden Datentypen zurück.  
  
|Ausdrucksergebnis|Rückgabetyp|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**Decimal** und **numerischen** Kategorie (p, s)|**Decimal (p, s)**|  
|**Money** und **Smallmoney** Kategorie|**money**|  
|**"float"** und **echte** Kategorie|**float**|  
  
## <a name="remarks"></a>Hinweise  
 ROUND gibt immer einen Wert zurück. Wenn *Länge* ist negativ und größer als die Anzahl der Ziffern vor dem Dezimaltrennzeichen, ROUND gibt 0 zurück.  
  
|Beispiel|Ergebnis|  
|-------------|------------|  
|ROUND (748.58 STANDARDMÄSSIG, -4)|0|  
  
 GERUNDET zurück *numerischer_ausdruck*, unabhängig vom Datentyp, wenn *Länge* ist eine negative Zahl.  
  
|Beispiele|Ergebnis|  
|--------------|------------|  
|ROUND (748.58 STANDARDMÄSSIG, -1)|750.00|  
|ROUND (748.58 STANDARDMÄSSIG,-2)|700.00|  
|ROUND(748.58, -3)|Verursacht einen arithmetischen Überlauffehler, da 748.58 standardmäßig zu decimal(5,2) wird und eine Rückgabe von 1000.00 nicht möglich ist.|  
|Um bis auf 4 Stellen aufzurunden, ändern Sie den Datentyp für die Eingabe. Beispiel:<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-round-and-estimates"></a>A. Verwenden von ROUND und Schätzwerten  
 Im folgenden Beispiel werden zwei Ausdrücke gezeigt, die veranschaulichen, dass mit `ROUND` die letzte Ziffer immer ein Näherungswert ist.  
  
```  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. Verwenden von ROUND und gerundeten Näherungswerten  
 Das folgende Beispiel zeigt das Runden und die Näherungsberechnung von Werten.  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ----------
123.45    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. Verwenden von ROUND zum Kürzen  
 Das folgende Beispiel verwendet zwei `SELECT`-Anweisungen, um den Unterschied zwischen dem Runden und dem Kürzen zu verdeutlichen. Die erste Anweisung rundet das Ergebnis. Die zweite Anweisung kürzt das Ergebnis.  
  
```  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-round-and-estimates"></a>D. Verwenden von ROUND und Schätzwerten  
 Im folgenden Beispiel werden zwei Ausdrücke gezeigt, die veranschaulichen, dass mit `ROUND` die letzte Ziffer immer ein Näherungswert ist.  
  
```  
SELECT ROUND(123.994999, 3), ROUND(123.995444, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ---------
123.995000    123.995444
```
  
## <a name="see-also"></a>Siehe auch  
 [CEILING &#40; Transact-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40; Transact-SQL &#41;](../../t-sql/functions/floor-transact-sql.md)   
 [Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


