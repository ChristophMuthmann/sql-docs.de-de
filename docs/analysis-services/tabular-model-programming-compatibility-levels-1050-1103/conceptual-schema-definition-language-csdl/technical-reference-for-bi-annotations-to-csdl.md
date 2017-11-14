---
title: "Technische Referenz für BI-Anmerkungen zu CSDL | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0cf821eb8c5db3410901f3d72826e0c2c8b8a274
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>Technische Referenz für BI-Anmerkungen zu CSDL
  Dieser Abschnitt listet die Elemente, Attribute und Eigenschaften in CSDL auf, die verwendet werden, um darzustellen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tabellarische Modelle. Einige Elemente sind neu; andere wurden mit Anmerkungen versehen oder zur Unterstützung von Business Intelligence-Modellen erweitert.  
  
 Eine Übersicht über tabellarische Modelle und wie die Entitäten, Beziehungen und Formeln in CSDL dargestellt werden, finden Sie unter [CSDL-Anmerkungen für Business Intelligence &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="extended-csdl-elements-complex-types"></a>Erweiterte CSDL-Elemente: Komplexe Typen  
 Die folgenden CSDL-Elemente wurden hinzugefügt oder erweitert, um tabellarische und mehrdimensionale Business Intelligence-Modelle zu unterstützen.  
  
-   [AssociationSet-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)  
  
-   [BaseProperty-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)  
  
-   [DefaultDetails-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md)  
  
-   [DisplayKey-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md)  
  
-   [EntityContainer-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)  
  
-   [EntitySet-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
-   [EntityType-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)  
  
-   [Hierarchy-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md)  
  
-   [KPI-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
-   [KpiGoal-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpigoal-element-csdlbi.md)  
  
-   [KpiStatus-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpistatus-element-csdlbi.md)  
  
-   [Level-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/level-element-csdlbi.md)  
  
-   [Measure-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/measure-element-csdlbi.md)  
  
-   [Member-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/member-element-csdlbi.md)  
  
-   [MemberRef-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md)  
  
-   [NavigationProperty-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/navigationproperty-element-csdlbi.md)  
  
-   [Property-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)  
  
-   [PropertyRef-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>Einfacher Typ und Untertypen  
 Die folgende Tabelle enthält einige einfache Typen sowie einige untergeordnete komplexe Typen, die in den Definitionen der oben aufgeführten komplexen Typen enthalten sind. Die Dokumentation für die in der linken Spalte aufgeführten einfachen Typen oder Untertypen wird bei den übergeordneten Elementen in der rechten Spalte bereitgestellt.  
  
|Einfacher Typ|Aus dem Thema|  
|-----------------|--------------------|  
|Ausrichtung|[BaseProperty-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
|CompareOptions|[EntityContainer-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)|  
|Inhalt|[EntityType-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Member-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Property-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|DirectQueryMode|[EntityContainer-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Property-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|MemberRefs|[MemberRef-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md)|  
|PropertyRefs|[PropertyRef-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)|  
|SortDirection|[BaseProperty-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
|Status|[AssociationSet-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
|Stability|[Property-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|SortDirection|[BaseProperty-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [CSDLBI-Konzepte](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  

