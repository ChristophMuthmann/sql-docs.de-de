---
title: "CEILING (SSIS-Ausdruck) | Microsoft Docs"
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
  - "Kleinste ganze Zahl größer oder gleich einem Ausdruck"
  - "CEILING-Funktion [SSIS]"
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# CEILING (SSIS-Ausdruck)
  Gibt die kleinste ganze Zahl zurück, die größer oder gleich einem numerischen Ausdruck ist.  
  
## Syntax  
  
```  
  
CEILING(numeric_expression)  
```  
  
## Argumente  
 *numeric_expression*  
 Ein gültiger numerischer Ausdruck.  
  
## Ergebnistypen  
 Der Datentyp des numerischen Ausdrucks, der an die Funktion übergeben wird.  
  
## Hinweise  
 CEILING gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## Beispiele für Ausdrücke  
 In diesen Beispielen wird die CEILING-Funktion auf positive und negative Werte und auf Null angewendet.  
  
```  
CEILING(123.74)  
```  
  
 Gibt 124,00 zurück.  
  
```  
CEILING(-124.27)  
```  
  
 Gibt -124.00 zurück.  
  
```  
CEILING(0.00)  
```  
  
 Gibt 0.00 zurück.  
  
## Siehe auch  
 [FLOOR &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  