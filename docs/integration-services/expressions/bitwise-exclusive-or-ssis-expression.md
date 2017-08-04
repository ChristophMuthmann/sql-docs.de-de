---
title: ^ (Bitweises exklusives OR) (SSIS-Ausdruck) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4c0a93affde5af98cdeb24fd04bb00d9ac72af7
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^ (Bitweises exklusives OR) (SSIS-Ausdruck)
  Führt eine bitweise exklusive OR-Operation mit zwei ganzzahligen Werten aus. Jedes Bit des ersten Operanden wird mit dem entsprechenden Bit des zweiten Operanden verglichen. Wenn ein Bit 0 und das andere 1 ist, wird das entsprechende Ergebnisbit auf 1 festgelegt. Wenn beide Bits 0 oder 1 sind, wird das entsprechende Ergebnisbit auf 0 festgelegt.  
  
 Beide Bedingungen müssen als Datentyp eine ganze Zahl mit Vorzeichen oder aber eine ganze Zahl ohne Vorzeichen aufweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *integer_expression1, integer_expression2*  
 Ein gültiger Ausdruck eines integer-Datentyps mit oder ohne Vorzeichen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine der Bedingungen NULL ist, lautet das Ergebnis des Ausdrucks NULL.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird eine bitweise exklusive OR-Operation mit den Variablen **NumberA** und **NumberB**ausgeführt. **NumberA** enthält 3 (00000011) und **NumberB** enthält 7 (00000111).  
  
```  
@NumberA ^ @NumberB  
```  
  
 Der Ausdruck wird zu 4 (00000100) ausgewertet.  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 In diesem Beispiel wird eine bitweise exklusive OR-Operation mit den Spalten **ReorderPoint** und **SafetyStockLevel** ausgeführt.  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 Falls **ReorderPoint** gleich 10 und **SafetyStockLevel** gleich 8 ist, wird der Ausdruck zu 2 (00000010) ausgewertet.  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 In diesem Beispiel wird eine bitweise exklusive OR-Operation mit zwei ganzen Zahlen ausgeführt.  
  
```  
3 ^ 5   
```  
  
 Der Ausdruck wird zu 6 (00000110) ausgewertet.  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## <a name="see-also"></a>Siehe auch  
 [&#124; &#124; &#40; Logisches OR &#41; &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [&#124; &#40; Bitweises inklusives OR &#41; &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [Operatorrangfolge und Assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
