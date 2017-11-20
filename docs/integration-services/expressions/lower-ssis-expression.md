---
title: LOWER (SSIS-Ausdruck) | Microsoft Docs
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
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d8887035d26ba829dae2153e4e9261836ada70d
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="lower-ssis-expression"></a>LOWER (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck zurück, nachdem Großbuchstaben in Kleinbuchstaben konvertiert wurden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein Zeichenausdruck zum Konvertieren in Kleinbuchstaben.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
 LOWER kann nur mit dem DT_WSTR-Datentyp verwendet werden. Ein *character_expression* -Argument, das ein Zeichenfolgenliteral oder eine Datenspalte mit dem DT_STR-Datentyp ist, wird implizit in den DT_WSTR-Datentyp umgewandelt, bevor LOWER ausgeführt wird. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md) und [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LOWER gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral in Kleinbuchstaben konvertiert. Als Ergebnis wird "new york" zurückgegeben.  
  
```  
LOWER("New York")  
```  
  
 In diesem Beispiel werden alle Zeichen in der **Color** -Eingabespalte in Kleinbuchstaben konvertiert, außer dem ersten Zeichen. Wenn Color gleich YELLOW ist, wird als Ergebnis "Yellow" zurückgegeben. Weitere Informationen finden Sie unter [SUBSTRING &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 In diesem Beispiel wird der Wert in der **CityName** -Variablen in Kleinbuchstaben konvertiert.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Obere &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

