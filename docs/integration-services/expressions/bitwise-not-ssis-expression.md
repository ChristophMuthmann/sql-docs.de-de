---
title: "~ (Bitweises NOT) (SSIS-Ausdruck) | Microsoft Docs"
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
  - "Bitweises NOT (~)"
  - "~ (Bitweises NOT)"
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# ~ (Bitweises NOT) (SSIS-Ausdruck)
  Führt eine bitweise Negation einer ganzen Zahl aus. Dieser Operator kann auf integer-Datentypen mit und ohne Vorzeichen angewendet werden.  
  
## Syntax  
  
```  
  
~integer_expression  
  
```  
  
## Argumente  
 *integer_expression*  
 Ein beliebiger gültiger Ausdruck eines integer-Datentyps. *integer*_*expression*ist eine ganze Zahl, die für die bitweise Operation in eine binäre Zahl transformiert wird. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Ergebnistypen  
 Gibt den Datentyp von *integer_expression* zurück.  
  
## Hinweise  
 InclusionThresholdSetting  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird eine bitweise ~ (NOT)-Operation für die Zahl 170 (0000 0000 1010 1010) ausgeführt. Diese Zahl ist eine ganze Zahl mit Vorzeichen.  
  
```  
  
~ 170  
```  
  
 Der Ausdruck wird zu -170 (1111111101010101) ausgewertet.  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  