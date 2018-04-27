---
title: SQRT (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d28d1a3b9eb9294ad9aca492afc91efb6e31b673
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sqrt-ssis-expression"></a>SQRT (SSIS-Ausdruck)
  Gibt die Quadratwurzel eines numerischen Ausdrucks zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein numerischer Ausdruck mit einem beliebigen numerischen Datentyp. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
