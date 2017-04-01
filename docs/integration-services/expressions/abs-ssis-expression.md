---
title: "ABS (SSIS-Ausdruck) | Microsoft Docs"
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
  - "ABS-Funktion"
  - "Absoluter positiver Wert"
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# ABS (SSIS-Ausdruck)
  Gibt den absoluten, positiven Wert eines numerischen Ausdrucks zurück.  
  
## Syntax  
  
```  
  
ABS(numeric_expression)  
```  
  
## Argumente  
 *numeric_expression*  
 Ein numerischer Ausdruck mit oder ohne Vorzeichen.  
  
## Ergebnistypen  
 Der Datentyp des numerischen Ausdrucks, der an die Funktion übergeben wird.  
  
## Hinweise  
 ABS gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## Beispiele für Ausdrücke  
 In diesen Beispielen wird die ABS-Funktion auf eine positive und eine negative Zahl angewendet. In beiden Fällen wird 1.23 zurückgegeben.  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 In diesem Beispiel wird die ABS-Funktion auf einen Ausdruck angewendet, der Werte in den Variablen **HighTemperature** und **LowTempature**subtrahiert.  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  