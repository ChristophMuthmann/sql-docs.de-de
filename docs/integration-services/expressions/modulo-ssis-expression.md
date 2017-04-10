---
title: "(Modulo) (SSIS-Ausdr&#252;cke) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "% (Modulooperator)"
  - "Rest eines Divisionsvorgangs"
  - "Modulooperator (%)"
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# (Modulo) (SSIS-Ausdr&#252;cke)
  Stellt den ganzzahligen Rest einer Division des ersten numerischen Ausdrucks durch den zweiten bereit.  
  
## Syntax  
  
```  
  
dividend % divisor  
  
```  
  
## Argumente  
 *dividend*  
 Der zu dividierende numerische Ausdruck. *dividend* kann ein beliebiger numerischer Ausdruck sein. Weitere Informationen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *divisor*  
 Der numerische Ausdruck, durch den der Dividend geteilt werden soll. *divisor* kann ein beliebiger numerischer Ausdruck außer Null sein.  
  
## Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Hinweise  
 Beide Ausdrücke müssen zu ganzzahligen Datentypen mit oder ohne Vorzeichen ausgewertet werden.  
  
 Wenn einer der Operanden NULL ist, ist das Ergebnis NULL.  
  
 Modulo Null ist nicht zulässig.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird der Teilungsrest von zwei numerischen Literalen berechnet. Das Ergebnis ist 3.  
  
```  
42 % 13  
```  
  
 In diesem Beispiel wird der Teilungsrest von der **SalesQuota** -Spalte und einem numerischen Literal berechnet.  
  
```  
SalesQuota % 12  
```  
  
 In diesem Beispiel wird der Teilungsrest von den beiden numerischen Variablen **Sales$** und **Month**berechnet. Die **Sales$** -Variable muss in eckige Klammern eingeschlossen werden, weil der Name das $-Zeichen enthält. Weitere Informationen finden Sie unter [Bezeichner &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
@[Sales$] % @Month  
```  
  
 In diesem Beispiel wird mithilfe des Modulo-Operators ermittelt, ob der Wert der **Value** -Variablen gerade oder ungerade ist, und mit dem Bedingungsoperator wird eine Zeichenfolge zur Beschreibung des Ergebnisses zurückgegeben. Weitere Informationen finden Sie unter [? : &#40;Bedingt, SSIS-Ausdruck&#41;](../../integration-services/expressions/conditional-ssis-expression.md).  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  