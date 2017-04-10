---
title: "Festlegen des Cubekontexts in einer Abfrage (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Cubes [Analysis Services], MDX"
  - "MDX [Analysis Services], Cubekontext"
  - "SELECT-Anweisung [MDX]"
  - "Mehrdimensionale Ausdrücke [Analysis Services], Cubekontext"
  - "Abfragen [MDX], Cubekontext"
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# Festlegen des Cubekontexts in einer Abfrage (MDX)
  Jede MDX-Abfrage wird in einem bestimmten Cubekontext ausgeführt. Dieser Kontext definiert die Elemente, die durch die Ausdrücke in der Abfrage ausgewertet werden.  
  
 In der SELECT-Anweisung bestimmt die FROM-Klausel den Cubekontext. Bei diesem Kontext kann es sich um den gesamten Cube oder nur um einen Teilcube dieses Cubes handeln. Nachdem Sie den Cubekontext durch die FROM-Klausel angegeben haben, können Sie den Kontext mithilfe weiterer Funktionen erweitern oder einschränken.  
  
> [!NOTE]  
>  Mit den SCOPE- und CALCULATE-Anweisungen können Sie den Cubekontext auch innerhalb eines MDX-Skripts verwalten. Weitere Informationen finden Sie unter [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
## Syntax der FROM-Klausel  
 Die folgende Syntax beschreibt die FROM-Klausel:  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 In dieser Syntax beschreibt die `<SELECT subcube clause>` -Klausel den Cube oder Teilcube, auf dem die SELECT-Anweisung ausgeführt wird.  
  
 Ein einfaches Beispiel wäre eine FROM-Klausel, die auf dem gesamten Adventure Works-Beispielcube ausgeführt wird. Eine solche FROM-Klausel hätte das folgende Format:  
  
```  
FROM [Adventure Works]  
```  
  
 Weitere Informationen zur FROM-Klausel in der SELECT-Anweisung von MDX finden Sie unter [SELECT-Anweisung &#40;MDX&#41;](../Topic/SELECT%20Statement%20\(MDX\).md).  
  
## Genaueres Festlegen des Kontexts  
 Obwohl die FROM-Klausel den Cubekontext innerhalb eines einzelnen Cubes angibt, wird dadurch nicht ausgeschlossen, dass Sie Daten aus mehreren Cubes gleichzeitig verwenden.  
  
 Mit der MDX- [LookupCube](../../../mdx/lookupcube-mdx.md) -Funktion können Sie Daten aus Cubes außerhalb des Cubekontexts abrufen. Darüber hinaus stehen Funktionen wie die [Filter](../../../mdx/filter-mdx.md) -Funktion zur Verfügung, um den Kontext beim Auswerten der Abfrage vorübergehend einzuschränken.  
  
## Siehe auch  
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  