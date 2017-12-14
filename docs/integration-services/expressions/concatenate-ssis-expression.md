---
title: + (Verketten) (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
caps.latest.revision: "37"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 58486c56db62bf033cc5c700d5ba0798b4df26d2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="-concatenate-ssis-expression"></a>+ (Verketten) (SSIS-Ausdruck)
  Verkettet zwei Ausdrücke zu einem einzelnen Ausdruck.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *expression1, expression2*  
 Ein gültiger Ausdruck vom Datentyp DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT oder DT_IMAGE.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
 Für den Ausdruck können die Datentypen DT_STR und/oder DT_WSTR verwendet werden.  
  
 Die Verkettung der Datentypen DT_STR und DT_WSTR gibt ein Ergebnis vom DT_WSTR-Datentyp zurück. Die Länge der Zeichenfolge ist die Summe der Längen der ursprünglichen Zeichenfolgen, ausgedrückt in Zeichen.  
  
 Nur Daten mit den Zeichenfolgen-Datentypen DT_STR und DT_WSTR oder den BLOB-Datentypen (Binary Large Object Block) DT_TEXT, DT_NTEXT und DT_IMAGE können verkettet werden. Andere Datentypen müssen vor der Verkettung explizit in einen dieser Datentypen konvertiert werden. Weitere Informationen zu zulässigen Datentypumwandlungen finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Beide Ausdrücke müssen vom gleichen Datentyp sein, oder es muss möglich sein, einen Ausdruck implizit in den Datentyp des anderen Ausdrucks zu konvertieren. Wenn z. B. die Zeichenfolge "Order date is " und die **OrderDate** -Spalte verkettet werden, werden die Werte in **OrderDate** implizit in einen Zeichenfolgen-Datentyp konvertiert. Um zwei numerische Werte zu verketten, müssen beide numerischen Werte explizit in einen Zeichenfolgen-Datentyp umgewandelt werden.  
  
 In einer Verkettung kann nur ein BLOB-Datentyp verwendet werden: DT_TEXT, DT_NTEXT oder DT_IMAGE.  
  
 Wenn eines der Elemente NULL ist, ist das Ergebnis NULL.  
  
 Zeichenfolgenliterale müssen in Anführungszeichen eingeschlossen werden.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel werden die Werte in den Spalten **FirstName** und **LastName** verkettet und ein Leerzeichen dazwischen eingefügt.  
  
```  
FirstName + ' ' + LastName  
```  
  
 In diesem Beispiel werden die Variablen **ZIPCode** und **ZIPCode+4**verkettet. Beide Variablen weisen einen Zeichenfolgen-Datentyp auf. **ZIPCode+4** muss in eckige Klammern eingeschlossen werden, weil der Variablenname das Zeichen + enthält.  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
