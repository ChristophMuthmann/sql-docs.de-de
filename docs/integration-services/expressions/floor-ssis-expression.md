---
title: "FLOOR (SSIS-Ausdruck) | Microsoft Docs"
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
  - "Größte ganze Zahl kleiner oder gleich dem Ausdruck"
  - "FLOOR-Funktion [SSIS]"
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# FLOOR (SSIS-Ausdruck)
  Gibt die größte ganze Zahl zurück, die kleiner oder gleich einem numerischen Ausdruck ist.  
  
## Syntax  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck.  
  
## Ergebnistypen  
 Der numerische Datentyp des expression-Arguments. Das Ergebnis ist der ganzzahlige Teil des berechneten Werts mit dem gleichen Datentyp wie *numeric_expression*.  
  
## Hinweise  
 FLOOR gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## Beispiele für Ausdrücke  
 In diesen Beispielen wird die FLOOR-Funktion auf positive und negative Werte und auf Null angewendet.  
  
```  
FLOOR(123.45)  
```  
  
 Gibt 123.00 zurück.  
  
```  
FLOOR(-123.45)  
```  
  
 Gibt -124.00 zurück.  
  
```  
FLOOR(0.00)  
```  
  
 Gibt 0.00 zurück.  
  
## Siehe auch  
 [CEILING &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  