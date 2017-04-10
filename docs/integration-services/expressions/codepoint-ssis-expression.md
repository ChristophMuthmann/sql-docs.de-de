---
title: "CODEPOINT (SSIS-Ausdruck) | Microsoft Docs"
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
  - "CODEPOINT-Funktion"
  - "Äußeres linkes Zeichen eines Ausdrucks"
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# CODEPOINT (SSIS-Ausdruck)
  Gibt das Unicode-Codeelement des äußeren linken Zeichens eines Zeichenausdrucks zurück.  
  
## Syntax  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## Argumente  
 *character_expression*  
 Ein Zeichenausdruck, dessen äußeres linkes Zeichen ausgewertet wird.  
  
## Ergebnistypen  
 DT_UI2  
  
## Hinweise  
 *character_expression* muss den Datentyp „DT_WSTR“ aufweisen.  
  
 CODEPOINT gibt ein NULL-Ergebnis zurück, wenn *character_expression* NULL oder eine leere Zeichenfolge ist.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Als Ergebnis wird 77 zurückgegeben, das Unicode-Codeelement für M.  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 In diesem Beispiel wird eine Variable verwendet. Falls **Name** Touring Front Wheel ist, wird als Ergebnis 84 zurückgegeben, das Unicode-Codeelement für T.  
  
```  
CODEPOINT(@Name)  
```  
  
## Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  