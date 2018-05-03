---
title: MeasureGroupDimension-Datentyp (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MeasureGroupDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fc9affe514e806e53d131308105efd1f470062d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="measuregroupdimension-data-type-assl"></a>MeasureGroupDimension-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert einen abstrakten Grunddatentyp, der die Beziehung zwischen einer Dimension und einer Measuregruppe darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|[DataMiningMeasureGroupDimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md), [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md), [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|Abgeleitete Elemente|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md) , Auflistung von [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Jede **MeasureGroupDimension** ist ein Verweis auf eine der Dimensionen auf dem Cube. Sie definieren, welche Cubedimension für die Measuregruppe gilt.  
  
 Der Attributsatz, der geliefert wird, bestimmt die Granularität (Umfang), indem die Measures in der Measuregruppe bekannt sind. Measures, die für Produktverkäufe stehen, sind beispielsweise in der Verkäufe-Measuregruppe enthalten. Informationen über diese Measures werden auf monatlicher und nicht auf wöchentlicher oder täglicher Basis in der zugrunde liegenden Datenquelle gespeichert. In diesem Fall würde nur das Attribut Monat in der **MeasureGroupDimension** aufgeführt werden, die die Beziehung zwischen einer Zeit-Dimension und der Verkäufe-Measuregruppe beschreibt. In seltenen Fällen könnte die Granularität in Hinsicht auf einen Satz von Attributen definiert werden. Wenn man beispielsweise den Attributsatz {Tag, Woche, Monat, Jahr} nimmt, in dem Tag Woche und Monat impliziert, aber Woche nicht Monat impliziert, könnten die in der Vorhersagen-Measuregruppe enthaltenen Measures nach Monat und Woche, nicht aber nach Tag bekannt sein.  
  
 Wenn kein Attribut geliefert wird, ist es so, als ob nur das Schlüsselattribut für die Dimension geliefert wäre (das die niedrigste Granularitätsstufe definiert). Jede Partition einer Measuregruppe muss die gleiche Granularität haben. Der Attributsatz, der aufgelistet wird, sollte in Bezug auf die Beziehungen zwischen Attributen nicht redundant sein. Wenn Monat beispielsweise Jahr impliziert, wird die Granularität als Monat, nicht als Monat  und Jahr definiert.  
  
 Eine **MeasureGroupDimension** muss nur dann eine Hierarchie enthalten, wenn sie darüber etwas Bestimmtes angeben kann. (Es gibt keine Möglichkeit, auszuwählen, welche Hierarchien für eine bestimmte Measuregruppe gelten). Genauso muss sie nur dann ein [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md) enthalten, wenn sie darüber etwas Bestimmtes angeben kann.  
  
 Jede Hierarchie muss eine Teilmenge der in der [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)enthaltenen Hierarchien sein. Die Ebenen können nicht ausgewählt werden, auch wenn einige Ebenen abhängig von der Granularität der Measuregruppe automatisch deaktiviert werden könnten.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.MeasureGroupDimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
