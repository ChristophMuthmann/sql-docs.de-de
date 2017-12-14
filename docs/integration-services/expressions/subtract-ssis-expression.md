---
title: '- (Subtrahieren) (SSIS-Ausdruck) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5a677e5a997f1b6d4bb440a60afdfbd65f25d3e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="--subtract-ssis-expression"></a>- (Subtrahieren) (SSIS-Ausdruck)
  Subtrahiert den zweiten numerischen Ausdruck vom ersten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
numeric_expression1 – numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression1, numeric_expression2*  
 Jeder gültige Ausdruck mit einem numerischen Datentyp. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Hinweise  
 Schließen Sie den unären Minusausdruck in Klammern ein, um sicherzustellen, dass der Ausdruck in der richtigen Reihenfolge ausgewertet wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn einer der Operanden NULL ist, ist das Ergebnis NULL.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel werden numerische Literale subtrahiert.  
  
```  
5 - 6.09  
```  
  
 In diesem Beispiel wird der Wert in der **StandardCost** -Spalte vom Wert in der **ListPrice** -Spalte subtrahiert.  
  
```  
ListPrice - StandardCost  
```  
  
 In diesem Beispiel wird ein berechneter Wert von der **ListPrice** -Spalte subtrahiert. Die **Discount%** -Variable muss in eckige Klammern eingeschlossen werden, weil der Name das Zeichen % enthält. Weitere Informationen finden Sie unter [Bezeichner &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
