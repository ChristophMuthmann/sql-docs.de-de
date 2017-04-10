---
title: "Grundlegendes zu MDX-Abfragen (Analysis Services) | Microsoft Docs"
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
  - "Anweisungen [MDX]"
  - "Mehrdimensionale Ausdrücke [Analysis Services], Anweisungen"
  - "Mehrdimensionale Ausdrücke [Analysis Services], Abfragen"
  - "MDX [Analysis Services], Anweisungen"
  - "MDX-Abfragen [Analysis Services]"
  - "MDX [Analysis Services], Abfragen"
  - "Abfragen [MDX]"
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 30
---
# Grundlegendes zu MDX-Abfragen (Analysis Services)
  MDX (Multidimensional Expressions) ermöglicht Ihnen das Abfragen von mehrdimensionalen Objekten (z. B. Cubes) sowie das Zurückgeben von mehrdimensionalen Cellsets, die die Daten des jeweiligen Cubes enthalten. Dieses Thema und die zugehörigen Unterthemen bieten eine Übersicht über MDX-Abfragen.  
  
 In den folgenden Themen werden MDX-Abfragen und die von ihnen erstellten Cellsets beschrieben und detailliertere Informationen zur grundlegenden MDX-Syntax bereitgestellt.  
  
> [!NOTE]  
>  Weitere Informationen zu Leistungsproblemen im Zusammenhang mit MDX-Abfragen und -Berechnungen finden Sie im Abschnitt "Writing Efficient MDX" unter [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(in Englisch).  
  
## In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Die grundlegende MDX-Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-query-mdx.md)|Stellt grundlegende Syntaxinformationen für die MDX-SELECT-Anweisung bereit.|  
|[Einschränken der Abfrage mit Abfrage- und Slicerachsen &#40;MDX&#41;](../Topic/Restricting%20the%20Query%20with%20Query%20and%20Slicer%20Axes%20\(MDX\).md)|Beschreibt, was Abfrage- und Slicerachsen sind und wie diese angegeben werden.|  
|[Festlegen des Cubekontexts in einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|Beschreibt den Zweck, den die FROM-Klausel in einer MDX-SELECT-Anweisung hat.|  
|[Erstellen von benannten Mengen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md)|Beschreibt den Zweck benannter Mengen in MDX sowie die erforderlichen Techniken, um sie zu erstellen und in MDX-Abfragen zu verwenden.|  
|[Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md)|Stellt Informationen zu berechneten Elementen in MDX bereit, einschließlich der Techniken, um sie zu erstellen und in MDX-Ausdrücken zu verwenden.|  
|[Erstellen von Zellenberechnungen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-cell-calculations-in-mdx-mdx.md)|Erläutert den Prozess des Erstellens und Verwendens berechneter Zellen.|  
|[Erstellen und Verwenden von Eigenschaftswerten &#40;MDX&#41;](../Topic/Creating%20and%20Using%20Property%20Values%20\(MDX\).md)|Erläutert das Erstellen und Verwenden der Eigenschaften von Dimensionen, Ebenen, Elementen und Zellen.|  
|[Bearbeiten von Daten &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/manipulating-data-mdx.md)|Beschreibt die Grundlagen für das Bearbeiten von Daten mit Drillthrough sowie Rollup und beschreibt Durchlaufreihenfolge und Lösungsreihenfolge in MDX.|  
|[Ändern von Daten &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/modifying-data-mdx.md)|Beschreibt, wie Rückschreiben verwendet wird, um mehrdimensionale Daten temporär oder dauerhaft zu ändern.|  
|[Verwenden von Variablen und Parametern &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|Beschreibt, wie Variablen und Parameter in MDX-Abfragen verwendet werden.|  
  
## Siehe auch  
 [Multidimensional Expressions &#40;MDX&#41; – Referenz](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  