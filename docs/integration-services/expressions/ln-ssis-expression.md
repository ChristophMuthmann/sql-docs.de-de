---
title: LN (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f13cbf798c6063ea9bd0400ebab8491acc502beb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="ln-ssis-expression"></a>LN (SSIS-Ausdruck)
  Gibt den natürlichen Logarithmus eines numerischen Ausdrucks zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger, nicht negativer numerischer Ausdruck ungleich NULL.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 Der numerische Ausdruck wird in den DT_R8-Datentyp umgewandelt, bevor der Logarithmus berechnet wird. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Falls *numeric_expression* zu 0 (null) oder einem negativen Wert ausgewertet wird, wird als Ergebnis NULL zurückgegeben.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein numerisches Literal verwendet. Die Funktion gibt den Wert 3,737766961828337 zurück.  
  
```  
LN(42)  
```  
  
 In diesem Beispiel wird die **Length**-Spalte verwendet. Falls der Spaltenwert 53.99 ist, gibt die Funktion 3.9887988442302 zurück.  
  
```  
LN(Length)   
```  
  
 In diesem Beispiel wird die **Length**-Variable verwendet. Die Variable muss einen numerischen Datentyp aufweisen, oder der Ausdruck muss eine explizite Umwandlung in einen numerischen Datentyp einschließen. Falls **Length** gleich 234,567 ist, gibt die Funktion 5,45774126708797 zurück.  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LOG &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
