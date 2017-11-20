---
title: SQRT (SSIS-Ausdruck) | Microsoft Docs
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
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f5ae5e55d52ba0e4232d8e7a83d3aab2f70a6b56
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sqrt-ssis-expression"></a>SQRT (SSIS-Ausdruck)
  Gibt die Quadratwurzel eines numerischen Ausdrucks zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein numerischer Ausdruck mit einem beliebigen numerischen Datentyp. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_R8  
  
## <a name="remarks"></a>Hinweise  
 SQRT gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 SQRT schlägt fehl, wenn das Argument einen negativen Wert aufweist.  
  
 Das Argument wird in einen DT_R8-Datentyp umgewandelt, bevor die Quadratwurzel berechnet wird.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird die Quadratwurzel eines numerischen Literals zurückgegeben. Als Ergebnis wird 12 zurückgegeben.  
  
```  
SQRT(144)  
```  
  
 In diesem Beispiel wird die Quadratwurzel eines Ausdrucks zurückgegeben, die das Ergebnis der Subtraktion von Werten in den Spalten **Value1** und **Value2** ist.  
  
```  
SQRT(Value1 - Value2)  
```  
  
 In diesem Beispiel wird die Länge der dritten Seite eines rechtwinkligen Dreiecks zurückgegeben, indem die SQUARE-Funktion auf zwei Variablen angewendet und dann die Quadratwurzel der Summe berechnet wird. Falls **Side1** 3 und **Side2** 4 enthält, gibt die SQRT-Funktion 5 zurück.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  In Ausdrücken schließen Variablennamen stets das @-Präfix ein.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

