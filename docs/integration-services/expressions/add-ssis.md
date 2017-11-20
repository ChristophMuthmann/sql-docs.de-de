---
title: "+ (Hinzufügen) (SSIS) | Microsoft Docs"
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
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04596cf4762f2473da1555f4ce5f9cd210678986
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="-add-ssis"></a>+ (Addieren) (SSIS)
  Addiert zwei numerische Ausdrücke.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression1, numeric_ expression2*  
 Jeder gültige Ausdruck mit einem numerischen Datentyp.  
  
## <a name="result-types"></a>Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn einer der Operanden NULL ist, ist das Ergebnis NULL.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel werden numerische Literale addiert.  
  
```  
5 + 6.09 + 7.0  
```  
  
 In diesem Beispiel werden Werte in den Spalten **VacationHours** und **SickLeaveHours** addiert.  
  
```  
VacationHours + SickLeaveHours  
```  
  
 In diesem Beispiel wird ein berechneter Wert zur **StandardCost** -Spalte addiert. Die **Profit%** -Variable muss in eckige Klammern eingeschlossen werden, weil der Name das Zeichen % enthält. Weitere Informationen finden Sie unter [Bezeichner &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatorrangfolge und Assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

