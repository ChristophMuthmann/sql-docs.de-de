---
title: ~ (Bitweises NOT) (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 12fc51c1923e918a3b63813f20ff58d205915195
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="-bitwise-not-ssis-expression"></a>~ (Bitweises NOT) (SSIS-Ausdruck)
  Führt eine bitweise Negation einer ganzen Zahl aus. Dieser Operator kann auf integer-Datentypen mit und ohne Vorzeichen angewendet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>Argumente  
 *integer_expression*  
 Ein beliebiger gültiger Ausdruck eines integer-Datentyps. *integer*_*expression* ist eine ganze Zahl, die für die bitweise Operation in eine binäre Zahl transformiert wird. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt den Datentyp von *integer_expression*zurück.  
  
## <a name="remarks"></a>Remarks  
 InclusionThresholdSetting  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird eine bitweise ~ (NOT)-Operation für die Zahl 170 (0000 0000 1010 1010) ausgeführt. Diese Zahl ist eine ganze Zahl mit Vorzeichen.  
  
```  
  
~ 170  
```  
  
 Der Ausdruck wird zu -170 (1111111101010101) ausgewertet.  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
