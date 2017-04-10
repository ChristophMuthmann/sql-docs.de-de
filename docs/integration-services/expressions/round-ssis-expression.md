---
title: "ROUND (SSIS-Ausdruck) | Microsoft Docs"
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
  - "Rundungsausdrücke"
  - "ROUND-Funktion [SSIS]"
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# ROUND (SSIS-Ausdruck)
  Gibt einen numerischen Ausdruck zurück, der auf die angegebene Länge oder Genauigkeit gerundet wurde. Der length-Parameter muss zu einer ganzen Zahl ausgewertet werden.  
  
## Syntax  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## Argumente  
 *numeric_expression*  
 Ein Ausdruck eines gültigen numerischen Datentyps. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *length*  
 Ein ganzzahliger Ausdruck. Dies ist die Genauigkeit, auf die *numeric_expression* gerundet wird.  
  
## Ergebnistypen  
 Der Typ entspricht dem Typ von *numeric*_*expression*.  
  
## Hinweise  
 Das *length* -Argument muss zu einer positiven ganzen Zahl oder 0 (null) ausgewertet werden.  
  
 ROUND gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## Beispiele für Ausdrücke  
 Diese Beispiele runden numerische Literale auf eine Länge von drei. Als erstes Ergebnis wird 137.1570 zurückgegeben und als zweites Ergebnis 137.1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## Siehe auch  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  