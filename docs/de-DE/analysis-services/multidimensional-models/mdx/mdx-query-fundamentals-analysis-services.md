---
title: Grundlegendes zu MDX-Abfragen (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b4d1309a411688e79f9f44e58dba65add8434611
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-query-fundamentals-analysis-services"></a>Grundlegendes zu MDX-Abfragen (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX (Multidimensional Expressions) ermöglicht Ihnen das Abfragen von mehrdimensionalen Objekten (z. B. Cubes) sowie das Zurückgeben von mehrdimensionalen Cellsets, die die Daten des jeweiligen Cubes enthalten. Dieses Thema und die zugehörigen Unterthemen bieten eine Übersicht über MDX-Abfragen.  
  
 In den folgenden Themen werden MDX-Abfragen und die von ihnen erstellten Cellsets beschrieben und detailliertere Informationen zur grundlegenden MDX-Syntax bereitgestellt.  
  
> [!NOTE]  
>  Weitere Informationen zu Leistungsproblemen im Zusammenhang mit MDX-Abfragen und -Berechnungen finden Sie im Abschnitt "Writing Efficient MDX" unter [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(in Englisch).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Grundlegende MDX-Abfrage & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)|Stellt grundlegende Syntaxinformationen für die MDX-SELECT-Anweisung bereit.|  
|[Einschränken der Abfrage mit Abfrage- und Slicer-Achse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)|Beschreibt, was Abfrage- und Slicerachsen sind und wie diese angegeben werden.|  
|[Des Cubekontexts in einer Abfrage & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|Beschreibt den Zweck, den die FROM-Klausel in einer MDX-SELECT-Anweisung hat.|  
|[Erstellen von benannten Mengen in MDX & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)|Beschreibt den Zweck benannter Mengen in MDX sowie die erforderlichen Techniken, um sie zu erstellen und in MDX-Abfragen zu verwenden.|  
|[Erstellen von berechneten Elementen in MDX & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)|Stellt Informationen zu berechneten Elementen in MDX bereit, einschließlich der Techniken, um sie zu erstellen und in MDX-Ausdrücken zu verwenden.|  
|[Erstellen von Zellenberechnungen in MDX & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)|Erläutert den Prozess des Erstellens und Verwendens berechneter Zellen.|  
|[Erstellen und Verwenden von Eigenschaftswerten & #40; MDX & #41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)|Erläutert das Erstellen und Verwenden der Eigenschaften von Dimensionen, Ebenen, Elementen und Zellen.|  
|[Bearbeiten von Daten & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)|Beschreibt die Grundlagen für das Bearbeiten von Daten mit Drillthrough sowie Rollup und beschreibt Durchlaufreihenfolge und Lösungsreihenfolge in MDX.|  
|[Ändern von Daten & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)|Beschreibt, wie Rückschreiben verwendet wird, um mehrdimensionale Daten temporär oder dauerhaft zu ändern.|  
|[Verwenden von Variablen und Parametern & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|Beschreibt, wie Variablen und Parameter in MDX-Abfragen verwendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionale Ausdrücke & #40; MDX & #41; Referenz](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
