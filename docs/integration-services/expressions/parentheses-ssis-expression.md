---
title: () (Klammern) (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1dde4602208caf4bd12218903af8972ca01f7410
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
 Der Datentyp von *expression*. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Dieses Beispiel zeigt, wie die Rangfolge von Operatoren durch die Verwendung von Klammern geändert wird. Der erste Ausdruck wird zu 100 ausgewertet, der zweite zu 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
