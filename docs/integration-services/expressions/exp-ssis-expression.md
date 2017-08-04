---
title: EXP (SSIS-Ausdruck) | Microsoft Docs
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
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ad14b1426435034ef5f4371cc8bb6904b536798
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="exp-ssis-expression"></a>EXP (SSIS-Ausdruck)
  Gibt den Exponenten für die Basis e eines numerischen Ausdrucks zurück. Die EXP-Funktion ergänzt die Aktion der LN-Funktion und wird auch als Antilogarithmus bezeichnet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_R8  
  
## <a name="remarks"></a>Hinweise  
 Der numerische Ausdruck wird in den DT_R8-Datentyp umgewandelt, bevor der Exponent berechnet wird. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Als Ergebnis wird immer eine positive Zahl zurückgegeben.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Diese Beispiele wenden die EXP-Funktion auf positive und negative Werte und auf Null an.  
  
```  
EXP(74)  
```  
  
 Gibt 1.373382979540176E+32 zurück.  
  
```  
EXP(-27)  
```  
  
 Gibt 1.879528816539083E-12 zurück.  
  
```  
EXP(0)  
```  
  
 Gibt 1 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Melden Sie sich &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
