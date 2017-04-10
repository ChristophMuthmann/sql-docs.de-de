---
title: "(Division) (SSIS-Ausdruck) | Microsoft Docs"
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
  - "/ (Division)"
  - "Operator für Division (/)"
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# (Division) (SSIS-Ausdruck)
  Dividiert den ersten numerischen Ausdruck durch den zweiten numerischen Ausdruck.  
  
## Syntax  
  
```  
  
dividend / divisor  
  
```  
  
## Argumente  
 *Dividend*  
 Der zu dividierende numerische Ausdruck. *dividend* kann ein beliebiger numerischer Ausdruck sein. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *divisor*  
 Der numerische Ausdruck, durch den der Dividend geteilt werden soll. *divisor* kann ein beliebiger numerischer Ausdruck außer Null sein.  
  
## Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Hinweise  
 Wenn einer der Operanden NULL ist, ist das Ergebnis NULL.  
  
 Division durch Null ist nicht zulässig. Je nachdem, wie der *divisor* -Teilausdruck ausgewertet wird, wird einer der folgenden Fehler gemeldet:  
  
-   Falls der zu Null ausgewertete *divisor* -Teilausdruck eine Konstante ist, wird der Fehler zur Entwurfszeit angezeigt, und der Ausdruck kann deshalb nicht überprüft werden.  
  
-   Falls der zu Null ausgewertete *divisor*-Teilausdruck Variablen, aber keine Eingabespalten enthält, wird für die zugehörige Komponente bei der Überprüfung vor der Ausführung (die vor der Ausführung des Pakets erfolgt) ein Fehler gemeldet.  
  
-   Falls der zu 0 (null) ausgewertete *divisor* -Teilausdruck Eingabespalten enthält, wird der Fehler zur Laufzeit gemeldet und gemäß den Fehlerflussregeln der Datenflusskomponente behandelt.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel werden zwei numerische Literale dividiert.  
  
```  
25 / 5  
```  
  
 In diesem Beispiel werden Werte in der **ListPrice** -Spalte durch die Werte in der **StandardCost** -Spalte dividiert.  
  
```  
ListPrice / StandardCost  
```  
  
## Siehe auch  
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  