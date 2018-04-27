---
title: '&amp;&amp; (Logisches AND) (SSIS-Ausdruck) | Microsoft-Dokumentation'
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
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcb0af893f7ae19ba4283c03fc90b5768df4d97c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (Logisches AND) (SSIS-Ausdruck)
  Führt eine logische AND-Operation aus. Der Ausdruck wird zu TRUE ausgewertet, falls alle Bedingungen TRUE sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>Argumente  
 *boolean_expression1, boolean_expression2*  
 Ein gültiger Ausdruck, der zu TRUE, FALSE oder NULL ausgewertet wird.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 In der folgenden Tabelle wird das Ergebnis des &&-Operators dargestellt.  
  
|Ergebnis|expression|expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel werden die Spalten **StandardCost** und **ListPrice** verwendet. In diesem Beispiel wird zu TRUE ausgewertet, falls der Wert der **StandardCost** -Spalte kleiner als 300 und falls die **ListPrice** -Spalte größer als 500 ist.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 In diesem Beispiel werden die Variablen **SPrice** und **LPrice** anstelle von Literalen verwendet.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [& &#40;Bitweises AND&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
