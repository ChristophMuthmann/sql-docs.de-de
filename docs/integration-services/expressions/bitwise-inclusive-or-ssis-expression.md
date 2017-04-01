---
title: "| (Bitweises inklusives OR) (SSIS-Ausdruck) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "| (bitweises inklusives OR)"
  - "Bitweises inklusives OR (|)"
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# | (Bitweises inklusives OR) (SSIS-Ausdruck)
  Führt eine bitweise OR-Operation mit zwei ganzzahligen Werten aus. Jedes Bit des ersten Operanden wird mit dem entsprechenden Bit des zweiten Operanden verglichen. Wenn eines der Bits 1 ist, wird das entsprechende Ergebnisbit auf 1 festgelegt. Andernfalls wird das entsprechende Ergebnisbit auf 0 (null) festgelegt.  
  
 Beide Bedingungen müssen als Datentyp eine ganze Zahl mit Vorzeichen oder aber eine ganze Zahl ohne Vorzeichen aufweisen.  
  
## Syntax  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## Argumente  
 *integer_expression1, integer_expression2*  
 Ein gültiger Ausdruck eines integer-Datentyps mit oder ohne Vorzeichen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Hinweise  
 Wenn eine der Bedingungen NULL ist, lautet das Ergebnis des Ausdrucks NULL.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird eine bitweise inklusive OR-Operation mit den Variablen **NumberA** und **NumberB**ausgeführt. **NumberA** enthält 3 (00000011) und **NumberB** enthält 9 (00001001).  
  
```  
@NumberA | @NumberB  
```  
  
 Der Ausdruck wird zu 11 (00001011) ausgewertet.  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 In diesem Beispiel wird eine bitweise inklusive OR-Operation mit den Spalten **ReorderPoint** und **SafetyStockLevel** ausgeführt.  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 Falls **ReorderPoint** gleich 10 und **SafetyStockLevel** gleich 8 ist, wird der Ausdruck zu 10 (00001010) ausgewertet.  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 In diesem Beispiel wird eine bitweise inklusive OR-Operation mit zwei ganzen Zahlen ausgeführt.  
  
```  
3 | 5   
```  
  
 Der Ausdruck wird zu 7 (00000111) ausgewertet.  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## Siehe auch  
 [&#124;&#124; &#40;Logisches OR&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40;Bitweises exklusives OR&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  