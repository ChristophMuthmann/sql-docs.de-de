---
title: UND (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- TRUE
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f21efc0360c992c3a88706a13f84f35d7026b101
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Kombiniert zwei boolesche Ausdrücke und gibt **"true"** Wenn beide Ausdrücke sind **"true"**. Wenn in einer Anweisung mehrere logische Operatoren verwendet wird die **AND** Operatoren werden zuerst ausgewertet. Sie können die Auswertungsreihenfolge ändern, indem Sie Klammern verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>Argumente  
 *boolean_expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , die einen booleschen Wert zurückgibt: **"true"**, **"false"**, oder **unbekannte**.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 Gibt TRUE zurück, wenn beide Ausdrücke TRUE sind.  
  
## <a name="remarks"></a>Hinweise  
 Das folgende Diagramm zeigt die Ergebnisse des Vergleichs von TRUE- und FALSE-Werten mit dem AND-Operator.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**"TRUE"**|TRUE|FALSE|UNKNOWN|  
|**"FALSE"**|FALSE|FALSE|FALSE|  
|**UNBEKANNT**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-and-operator"></a>A. Verwenden des AND-Operators  
 Im folgenden Beispiel werden Informationen zu Mitarbeitern, die sowohl den Titel `Marketing Assistant` führen als auch mehr als `41` Resturlaubsstunden haben, ausgewählt.  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. Verwenden des AND-Operators in einer IF-Anweisung  
 In den folgenden Beispielen wird gezeigt, wie AND in einer IF-Anweisung verwendet wird. In der ersten Anweisung ist sowohl `1 = 1` als auch `2 = 2` zutreffend. Das Ergebnis lautet deshalb TRUE. Im zweiten Beispiel trifft das Argument `2 = 17` nicht zu. Das Ergebnis lautet daher FALSE.  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

