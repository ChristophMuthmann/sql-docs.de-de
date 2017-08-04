---
title: '|| (Logisches OR) (SSIS-Ausdruck) | Microsoft Docs'
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
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c369d66dbfdfefa0249ef0e479266bf17cf8f7d6
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="-logical-or-ssis-expression"></a>|| (Logisches OR) (SSIS-Ausdruck)
  Führt eine logische OR-Operation aus. Der Ausdruck wird zu TRUE ausgewertet, falls mindestens eine Bedingung TRUE ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>Argumente  
 *boolean_expression1, boolean_expression2*  
 Ein gültiger Ausdruck, der zu TRUE, FALSE oder NULL ausgewertet wird.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_BOOL  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle wird das Ergebnis des ||-Operators dargestellt.  
  
|Ergebnis|expression|expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## <a name="ssis-expression-examples"></a>Beispiele für SSIS-Ausdrücke  
 In diesem Beispiel werden die Spalten **StandardCost** und **ListPrice** verwendet. In diesem Beispiel wird zu TRUE ausgewertet, falls der Wert der **StandardCost** -Spalte kleiner als 300 oder falls die **ListPrice** -Spalte größer als 500 ist.  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 In diesem Beispiel werden die Variablen **SPrice** und **LPrice** anstelle numerischer Literale verwendet.  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Siehe auch  
 [&#124; &#40; Bitweises inklusives OR &#41; &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [^ &#40; Bitweises exklusives OR &#41; &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Operatorrangfolge und Assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
