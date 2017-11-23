---
title: Grundlegendes zu MDX-Abfragen (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statements [MDX]
- Multidimensional Expressions [Analysis Services], statements
- Multidimensional Expressions [Analysis Services], queries
- MDX [Analysis Services], statements
- MDX queries [Analysis Services]
- MDX [Analysis Services], queries
- queries [MDX]
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 280033210c597c611ce1af8ff98c4ea94e1852f5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-query-fundamentals-analysis-services"></a>Grundlegendes zu MDX-Abfragen (Analysis Services)
  MDX (Multidimensional Expressions) ermöglicht Ihnen das Abfragen von mehrdimensionalen Objekten (z. B. Cubes) sowie das Zurückgeben von mehrdimensionalen Cellsets, die die Daten des jeweiligen Cubes enthalten. Dieses Thema und die zugehörigen Unterthemen bieten eine Übersicht über MDX-Abfragen.  
  
 In den folgenden Themen werden MDX-Abfragen und die von ihnen erstellten Cellsets beschrieben und detailliertere Informationen zur grundlegenden MDX-Syntax bereitgestellt.  
  
> [!NOTE]  
>  Weitere Informationen zu Leistungsproblemen im Zusammenhang mit MDX-Abfragen und -Berechnungen finden Sie im Abschnitt "Writing Efficient MDX" unter [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(in Englisch).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Die grundlegende MDX-Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)|Stellt grundlegende Syntaxinformationen für die MDX-SELECT-Anweisung bereit.|  
|[Beschränken die Abfrage mit Abfrage- und Slicer-Achse &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)|Beschreibt, was Abfrage- und Slicerachsen sind und wie diese angegeben werden.|  
|[Festlegen des Cubekontexts in einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|Beschreibt den Zweck, den die FROM-Klausel in einer MDX-SELECT-Anweisung hat.|  
|[Erstellen von benannten Mengen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)|Beschreibt den Zweck benannter Mengen in MDX sowie die erforderlichen Techniken, um sie zu erstellen und in MDX-Abfragen zu verwenden.|  
|[Erstellen von berechneten Elementen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)|Stellt Informationen zu berechneten Elementen in MDX bereit, einschließlich der Techniken, um sie zu erstellen und in MDX-Ausdrücken zu verwenden.|  
|[Erstellen von Zellenberechnungen in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)|Erläutert den Prozess des Erstellens und Verwendens berechneter Zellen.|  
|[Erstellen und Verwenden von Eigenschaftswerten &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)|Erläutert das Erstellen und Verwenden der Eigenschaften von Dimensionen, Ebenen, Elementen und Zellen.|  
|[Bearbeiten von Daten &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)|Beschreibt die Grundlagen für das Bearbeiten von Daten mit Drillthrough sowie Rollup und beschreibt Durchlaufreihenfolge und Lösungsreihenfolge in MDX.|  
|[Ändern von Daten &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)|Beschreibt, wie Rückschreiben verwendet wird, um mehrdimensionale Daten temporär oder dauerhaft zu ändern.|  
|[Verwenden von Variablen und Parametern &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|Beschreibt, wie Variablen und Parameter in MDX-Abfragen verwendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Multidimensional Expressions &#40;MDX&#41; – Referenz](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
