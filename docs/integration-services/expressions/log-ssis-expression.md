---
title: LOG (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8dd39c7271c1258b67aec056c89d9cbfa5891c23
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="log-ssis-expression"></a>LOG (SSIS-Ausdruck)
  Gibt den Logarithmus eines numerischen Ausdrucks zur Basis 10 zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck, der ungleich 0 oder nicht negativ ist.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 Der *numerische Ausdruck* wird in den DT_R8-Datentyp umgewandelt, bevor der Logarithmus berechnet wird. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Falls *numeric_expression* zu 0 (null) oder einem negativen Wert ausgewertet wird, wird als Ergebnis NULL zurückgegeben.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein numerisches Literal verwendet. Die Funktion gibt den Wert 1.988291341907488 zurück.  
  
```  
LOG(97.34)  
```  
  
 In diesem Beispiel wird die **Length**-Spalte verwendet. Falls der Spaltenwert 101.24 ist, gibt die Funktion 2.005352136486217 zurück.  
  
```  
LOG(Length)   
```  
  
 In diesem Beispiel wird die **Length**-Variable verwendet. Die Variable muss einen numerischen Datentyp aufweisen, oder der Ausdruck muss eine explizite Umwandlung in einen numerischen [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Datentyp einschließen. Falls **Length** gleich 234.567 ist, gibt die Funktion 2.370266913465859 zurück.  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [EXP &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/ln-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
