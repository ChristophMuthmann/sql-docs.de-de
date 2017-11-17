---
title: += (Verketten) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c557bcc1d3c2f314ce57e93701b11833f5a6fc6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="string-concatenation---equal-transact-sql"></a>Verketten von Zeichenfolgen – gleich (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Verkettet zwei Zeichenfolgen und legt die Zeichenfolge auf das Ergebnis des Vorgangs fest. Angenommen, eine Variable @x ist gleich 'Adventure', klicken Sie dann @x += 'Works' nimmt den ursprünglichen Wert des @x'Works' der Zeichenfolge hinzugefügt, und setzt @x auf diesen neuen Wert 'AdventureWorks'.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Zeichendatentyps.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt den Datentyp zurück, der für die Variable definiert wird.  
  
## <a name="remarks"></a>Hinweise  
 Legen Sie @v1 += 'Ausdruck' entspricht SET @v1 = @v1 + ('Ausdruck'). Legen Sie außerdem @v1 = @v2 + @v3 + @v4 entspricht dem Satz @v1 = (@v2 + @v3) + @v4.  
  
 Der Operator += kann nicht ohne eine Variable verwendet werden. So verursacht z. B. der folgende Code einen Fehler:  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>Beispiele  
### <a name="a-concatenation-using--operator"></a>A. Verkettung mit:: Operator +=-Operator
 Im folgenden Beispiel wird mithilfe des `+=`-Operators verkettet.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. Reihenfolge der Auswertung beim Verketten von mithilfe von:: Operator +=-Operator
Im folgenden Beispiel werden mehrere Zeichenfolgen zu einer langen Zeichenfolge verkettet und versucht dann, um die Länge der endgültigen Zeichenfolge zu berechnen. Dieses Beispiel zeigt die Reihenfolge und Abschneiden-Auswertungsregeln dar, bei der Verwendung des Operators für Verkettungen. 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>Siehe auch  
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+= &#40; Hinzufügen von EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40; Verketten von Zeichenfolgen &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  

