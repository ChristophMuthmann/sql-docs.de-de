---
title: Cube Zellen (Analysis Services – mehrdimensionale Daten) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 077e0631a6b2557525a436d3fd4448ccda23b82d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Cubezellen (Analysis Services – Mehrdimensionale Daten)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein Cube besteht aus Zellen, die nach Measuregruppen und nach Dimensionen organisiert werden. Eine Zelle stellt den eindeutigen logischen Schnittpunkt in einem Cube eines Elements aus jeder Dimension des Cubes dar. Der im folgenden Diagramm beschriebene Cube enthält beispielsweise eine Measuregruppe mit zwei Measures, die nach den drei Dimensionen Source, Route und Time organisiert sind.  
  
 ![Cubediagramm mit einer einzelnen Zelle](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro5.gif "Cubediagramm mit einer einzelnen Zelle")  
  
 Die schattierte Zelle in diesem Diagramm ist der Schnittpunkt der folgenden Elemente:  
  
-   Das air-Element der Route-Dimension.  
  
-   Das Africa-Element der Source-Dimension.  
  
-   Das 4th quarter-Element der Time-Dimension.  
  
-   Das Packages-Measure.  
  
## <a name="leaf-and-nonleaf-cells"></a>Blatt- und Nichtblattzellen  
 Der Wert für eine Zelle in einem Cube kann auf eine der folgenden Arten abgerufen werden. Im vorherigen Beispiel der Wert in der Zelle kann abgerufen werden, direkt aus der Faktentabelle des Cubes sein, da alle Member, die zum Identifizieren dieser Zelle verwendet werden *Blattelemente*. Ein Blattelement weist in der Hierarchie keine untergeordneten Elemente auf und verweist normalerweise auf einen einzelnen Datensatz in einer Dimensionstabelle. Diese Art der Zelle wird als bezeichnet eine *Blattzelle*.  
  
 Allerdings eine Zelle kann auch ermittelt werden mithilfe von *Blattelemente*. Ein Nichtblattelement ist ein Element, das mindestens ein untergeordnetes Element aufweist. In diesem Fall wird der Wert der Zelle normalerweise aus der Aggregation der mit dem Nichtblattelement verknüpften untergeordneten Elemente abgeleitet. Der Schnittpunkt der folgenden Elemente und Dimensionen bezieht sich z. B. auf eine Zelle, deren Wert durch Aggregation angegeben wird:  
  
-   Das air-Element der Route-Dimension.  
  
-   Das Africa-Element der Source-Dimension.  
  
-   Das 2nd half-Element der Time-Dimension.  
  
-   Das Packages-Element.  
  
 Das 2nd half-Element der Time-Dimension ist ein Nichtblattelement. Daher müssen alle mit ihm verbundenen Elemente aggregierte Werte sein, wie im folgenden Diagramm dargestellt.  
  
 ![3. und 4. Quartal Zellen für 2nd half-Element](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro6.gif "3. und 4. Quartal Zellen für 2nd half-Element")  
  
 Wenn es sich beispielsweise bei den Aggregationen für das 3rd quarter- und 4th quarter-Element um Summen handelt, dann ist der Wert der angegebenen Zelle 400, die Summe aller Blattzellen, die im vorherigen Diagramm schattiert sind. Da der Wert der Zelle aus der Aggregation anderer Zellen abgeleitet wird, gilt die angegebene Zelle einer *nichtblattzelle*.  
  
 Die Zellenwerte, die für Elemente, die benutzerdefinierte Rollups und Elementgruppen verwenden, sowie für benutzerdefinierte Elemente abgeleitet werden, werden ähnlich behandelt. Zellwerte, die für berechnete Elemente abgeleitet werden, basieren jedoch vollständig auf dem MDX-Ausdruck (Multidimensional Expressions), der zum Definieren des berechneten Elements verwendet wird. Möglicherweise sind in einigen Fällen keine tatsächlichen Zellendaten betroffen. Weitere Informationen finden Sie unter [benutzerdefinierte Rollupoperatoren in über-und untergeordneten Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md), [Definieren von benutzerdefinierten Elementformeln](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md), und [Berechnungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
## <a name="empty-cells"></a>Leere Zellen  
 Nicht jede Zelle in einem Cube muss einen Wert enthalten. Es können Schnittpunkte in einem Cube enthalten sein, die keine Daten enthalten. Diese Schnittpunkte, die als leere Zellen bezeichnet werden, treten in Cubes häufig auf, da nicht jeder Schnittpunkt eines Dimensionsattributs mit einem Measure innerhalb eines Cubes einen entsprechenden Datensatz in einer Faktentabelle enthält. Das Verhältnis zwischen leeren Zellen in einem Cube auf die Gesamtzahl der Zellen in einem Cube wird häufig als bezeichnet den *geringe Datendichte* eines Cubes.  
  
 Die in dem folgenden Diagramm abgebildete Cubestruktur ähnelt z. B. anderen Beispielen in diesem Thema. In diesem Beispiel sind jedoch keine Luftfrachtlieferungen nach Afrika im dritten Quartal oder nach Australien im vierten Quartal vorhanden. In der Faktentabelle sind keine Daten enthalten, die die Schnittpunkte dieser Dimensionen und Measures unterstützen können, sodass die Zellen an diesen Schnittpunkten leer sind.  
  
 ![Cubediagramm mit leere Zellen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro7.gif "Cubediagramm mit leere Zellen")  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], eine leere Zelle ist eine Zelle, die besonderen Qualitäten. Da leere Zellen die Ergebnisse von Crossjoins, Zählungen usw. verfälschen können, ermöglichen viele MDX-Funktionen das Ignorieren dieser leeren Zellen bei der Berechnung. Weitere Informationen finden Sie unter [mehrdimensionale Ausdrücke &#40;MDX&#41; Verweis](../../mdx/multidimensional-expressions-mdx-reference.md), und [Schlüsselkonzepte in MDX &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>Sicherheit  
 Der Zugriff auf Zellendaten wird in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf Rollenebene verwaltet und kann mithilfe von MDX-Ausdrücken genau gesteuert werden. Weitere Informationen finden Sie unter [Erteilen von benutzerdefiniertem Zugriff auf Dimensionsdaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md), und [Erteilen von benutzerdefiniertem Zugriff auf Zellendaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Cube Speicher &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [Aggregationen und Aggregationsentwürfe](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
