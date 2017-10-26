---
title: CODEPOINT (SSIS-Ausdruck) | Microsoft Docs
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
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: af56c3de2d4e285960b9e6631084b20440396eb3
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="codepoint-ssis-expression"></a>CODEPOINT (SSIS-Ausdruck)
  Gibt das Unicode-Codeelement des äußeren linken Zeichens eines Zeichenausdrucks zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein Zeichenausdruck, dessen äußeres linkes Zeichen ausgewertet wird.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_UI2  
  
## <a name="remarks"></a>Hinweise  
 *character_expression* muss den Datentyp „DT_WSTR“ aufweisen.  
  
 CODEPOINT gibt ein NULL-Ergebnis zurück, wenn *character_expression* NULL oder eine leere Zeichenfolge ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Als Ergebnis wird 77 zurückgegeben, das Unicode-Codeelement für M.  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 In diesem Beispiel wird eine Variable verwendet. Falls **Name** Touring Front Wheel ist, wird als Ergebnis 84 zurückgegeben, das Unicode-Codeelement für T.  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

