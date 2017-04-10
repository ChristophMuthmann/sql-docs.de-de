---
title: "- (Negation) (SSIS-Ausdruck) | Microsoft Docs"
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
  - "- (Negativ)"
  - "Negativ-Operator (-)"
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# - (Negation) (SSIS-Ausdruck)
  Negiert einen numerischen Ausdruck.  
  
## Syntax  
  
```  
  
-numeric_expression  
  
```  
  
## Argumente  
 *numeric_expression*  
 Jeder gültige Ausdruck mit einem numerischen Datentyp. Nur numerische Datentypen mit Vorzeichen werden unterstützt. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Ergebnistypen  
 Gibt den Datentyp von *numeric_expression* zurück.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird der Wert der **Counter** -Variablen negiert und das numerische Literal 50 hinzugefügt.  
  
```  
-@Counter + 50  
```  
  
## Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  