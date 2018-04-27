---
title: () (Klammern) (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16412dc829f4a574a505928d6c4ff380dd8273d4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="-parentheses-ssis-expression"></a>() (Klammern) (SSIS-Ausdruck)
  Identifiziert die Auswertungsreihenfolge von Ausdrücken. Ausdrücke in Klammern haben die höchste Auswertungsrangfolge. Geschachtelte Ausdrücke, die in Klammern eingeschlossen sind, werden von innen nach außen ausgewertet.  
  
 Durch Klammern werden außerdem komplexe Ausdrücke verständlicher.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein gültiger Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 Der Datentyp von *expression*. Weitere Informationen finden Sie unter [Integration Services Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Dieses Beispiel zeigt, wie die Rangfolge von Operatoren durch die Verwendung von Klammern geändert wird. Der erste Ausdruck wird zu 100 ausgewertet, der zweite zu 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
