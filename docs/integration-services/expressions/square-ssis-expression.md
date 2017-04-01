---
title: "SQUARE (SSIS-Ausdruck) | Microsoft Docs"
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
  - "SQUARE"
  - "Quadratwerte"
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# SQUARE (SSIS-Ausdruck)
  Gibt das Quadrat eines numerischen Ausdrucks zurück.  
  
## Syntax  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## Argumente  
 *numeric_expression*  
 Ein numerischer Ausdruck mit einem beliebigen numerischen Datentyp. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Ergebnistypen  
 DT_R8  
  
## Hinweise  
 SQUARE gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
 Das Argument wird in einen DT_R8-Datentyp umgewandelt, bevor das Quadrat berechnet wird.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird das Quadrat von 12 zurückgegeben. Als Ergebnis wird 144 zurückgegeben.  
  
```  
SQUARE(12)  
```  
  
 In diesem Beispiel wird das Quadrat des Ergebnisses aus der Subtraktion von Werten in zwei Spalten zurückgegeben. Falls **Value1** 12 und **Value2** 4 enthält, gibt die SQUARE-Funktion 64 zurück.  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 In diesem Beispiel wird die Länge der dritten Seite eines rechtwinkligen Dreiecks zurückgegeben, indem die SQUARE-Funktion auf zwei Variablen angewendet und dann die Quadratwurzel der Summe berechnet wird. Falls **Side1** 3 und **Side2** 4 enthält, gibt die SQRT-Funktion 5 zurück.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  In Ausdrücken schließen Variablennamen stets das @-Präfix ein.  
  
## Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  