---
title: '! (Logisches NOT) (SSIS-Ausdruck) | Microsoft-Dokumentation'
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
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8c6c84a9efe60ffc7d9ebda818ddeabf833d05a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="-logical-not-ssis-expression"></a>! (Logisches NOT) (SSIS-Ausdruck)
  Negiert einen booleschen Operanden.  
  
> [!NOTE]  
>  Der !-Operator kann nicht zusammen mit anderen Operatoren verwendet werden. Beispielsweise können nicht den !-Operator und den >-Operator zum !>-Operator zusammenfassen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>Argumente  
 *boolean_expression*  
 Ein gültiger Ausdruck, der zu einem booleschen Wert ausgewertet wird. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_BOOL  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle wird das Ergebnis des Operation.  
  
|Ursprünglicher boolescher Ausdruck|Nach dem Anwenden des !- Operator|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird zu FALSE ausgewertet, falls der Wert in der **Color** -Spalte "red" ist.  
  
```  
!(Color == "red")  
```  
  
 In diesem Beispiel wird zu TRUE ausgewertet, falls der Wert der **MonthNumber** -Variablen mit der ganzen Zahl identisch ist, die den aktuellen Monat darstellt. Weitere Informationen finden Sie unter [MONTH &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/month-ssis-expression.md) und [GETDATE &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
