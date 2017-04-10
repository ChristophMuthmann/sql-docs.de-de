---
title: "REVERSE (SSIS-Ausdruck) | Microsoft Docs"
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
  - "REVERSE-Funktion"
  - "Umgekehrte Zeichenausdrücke"
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# REVERSE (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck in umgekehrter Reihenfolge zurück.  
  
## Syntax  
  
```  
  
REVERSE(character_expression)  
```  
  
## Argumente  
 *character_expression*  
 Der Zeichenausdruck, dessen Reihenfolge umgekehrt werden soll.  
  
## Ergebnistypen  
 DT_WSTR  
  
## Hinweise  
 Das *character_expression*-Argument muss den Datentyp „DT_WSTR“ aufweisen.  
  
 REVERSE gibt ein NULL-Ergebnis zurück, wenn *character_expression* NULL ist.  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird ein Zeichenfolgenliteral verwendet. Als Ergebnis wird "ekiB niatnuoM" zurückgegeben.  
  
```  
REVERSE("Mountain Bike")  
```  
  
 In diesem Beispiel wird eine Variable verwendet. Falls **Name** Touring Bike enthält, wird als Ergebnis "ekiB gniruoT" zurückgegeben.  
  
```  
REVERSE(@Name)  
```  
  
## Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  