---
title: '&amp; (Bitweises AND) (SSIS-Ausdruck) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10d05b3fcf9187125bbac9a1f64acaf0ab748d79
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp; (Bitweises AND) (SSIS-Ausdruck)
  Führt eine bitweise AND-Operation mit zwei ganzzahligen Werten aus. Jedes Bit des ersten Operanden wird mit dem entsprechenden Bit des zweiten Operanden verglichen. Wenn beide Bits 1 sind, wird das entsprechende Ergebnisbit auf 1 festgelegt. Andernfalls wird das entsprechende Ergebnisbit auf 0 festgelegt.  
  
 Beide Bedingungen müssen als Datentyp eine ganze Zahl mit Vorzeichen oder aber eine ganze Zahl ohne Vorzeichen aufweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *integer_expression1, integer_expression2*  
 Ein gültiger Ausdruck eines integer-Datentyps mit oder ohne Vorzeichen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Wenn eine der Bedingungen NULL ist, lautet das Ergebnis des Ausdrucks NULL.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird eine bitweise AND-Operation mit den Spalten **NumberA** und **NumberB**ausgeführt. **NumberA** enthält 3 (0000011) und die Spalte **NumberB** enthält 7 (00000111).  
  
```  
NumberA & NumberB  
```  
  
 Der Ausdruck wird zu 3 (00000011) ausgewertet.  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 In diesem Beispiel wird eine bitweise AND-Operation mit den Spalten **ReorderPoint** und **SafetyStockLevel** ausgeführt.  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 Falls **ReorderPoint** gleich 10 und **SafetyStockLevel** gleich 8 ist, wird der Ausdruck zu 8 (00001000) ausgewertet.  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 In diesem Beispiel wird eine bitweise AND-Operation mit zwei ganzen Zahlen ausgeführt.  
  
```  
3 & 5   
```  
  
 Der Ausdruck wird zu 1 (00000001) ausgewertet.  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [&& &#40;Logisches AND&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
