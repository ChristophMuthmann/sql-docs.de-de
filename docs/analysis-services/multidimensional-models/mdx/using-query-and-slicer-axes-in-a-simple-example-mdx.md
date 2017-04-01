---
title: "Verwenden von Abfrage- und Slicerachsen in einem einfachen Beispiel (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
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
  - "Slicerachse"
  - "Abfrageachse [MDX]"
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Verwenden von Abfrage- und Slicerachsen in einem einfachen Beispiel (MDX)
  Anhand des einfachen Beispiels, das in diesem Thema vorgestellt wird, werden die Grundlagen zum Angeben und Verwenden von Abfrage- und Slicerachsen erläutert.  
  
## Der Cube  
 Ein Cube namens TestCube hat zwei einfache Dimensionen mit den Namen Route und Time. Jede Dimension hat nur eine Benutzerhierarchie, die den Namen Route bzw. Time hat. Da die Measures des Cubes Teil der Measures-Dimension sind, hat dieser Cube insgesamt drei Dimensionen.  
  
## Die Abfrage  
 Die Abfrage muss eine Matrix bereitstellen, in der das Packages-Measure über Routen und Zeiten hinweg verglichen werden kann.  
  
 Im folgenden MDX-Abfragebeispiel sind die Hierarchien Route und Time die Abfrageachsen, und die Measures-Dimension ist die Slicerachse. Die [Members](../../../mdx/members-set-mdx.md) -Funktion zeigt an, dass MDX die Elemente der Hierarchie oder der Ebene zum Erstellen einer Menge verwendet. Wird die **Members** -Funktion verwendet, ist es nicht erforderlich, dass Sie in der jeweiligen MDX-Abfrage explizit jedes Element einer bestimmten Hierarchie oder Ebene angeben.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## Das Ergebnis  
 Das Ergebnis ist ein Raster, das die Werte enthält, die das Packages-Measure in jedem Schnittpunkt der Achsendimensionen COLUMNS und ROWS hat. Die folgende Tabelle zeigt, wie dieses Raster aussehen würde:  
  
||air|sea|  
|-|---------|---------|  
|Erstes Quartal|60|50|  
|Zweites Quartal|45|45|  
  
## Siehe auch  
 [Angeben des Inhalts einer Abfrageachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-query-axis-mdx.md)   
 [Angeben des Inhalts einer Slicerachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-slicer-axis-mdx.md)  
  
  