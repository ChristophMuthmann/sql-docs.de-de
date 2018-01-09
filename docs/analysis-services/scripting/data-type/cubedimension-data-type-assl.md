---
title: CubeDimension-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CubeDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeDimension
helpviewer_keywords: CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 222126f9cef7e778cc9271796e7147a36389424b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="cubedimension-data-type-assl"></a>CubeDimension-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert einen Grunddatentyp, der die Beziehung zwischen einer Dimension und einem Cube darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Basisdatentypen|InclusionThresholdSetting|  
|Abgeleitete Datentypen|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|InclusionThresholdSetting|  
|Untergeordnete Elemente|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md), [Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Attribute](../../../analysis-services/scripting/collections/attributes-element-assl.md), [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md), [Hierarchien](../../../analysis-services/scripting/collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md), [Namen](../../../analysis-services/scripting/properties/name-element-assl.md), [sichtbar](../../../analysis-services/scripting/properties/visible-element-assl.md), [Übersetzungen](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Abgeleitete Elemente|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([Dimensionen](../../../analysis-services/scripting/collections/dimensions-element-assl.md) Auflistung von [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Es gibt eine **CubeDimension** für jede Dimensionsbeziehung auf einem **Cube**. Die **CubeDimension** umfasst alle **MeasureGroups** des Cubes.  
  
 Ein **CubeDimension** umfasst eine [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md) , wenn die Dimension etwas bestimmtes über die Hierarchie treffen kann, darunter Deaktivieren der Hierarchie (, wodurch der Auswahl Hierarchien gelten für eine bestimmte Dimensionsverwendung), oder die Hierarchie unsichtbar zu machen.  
  
 Auf ähnliche Weise eine **CubeDimension** umfasst eine [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md) nur, wenn die Dimension bestimmte Aussagen über das Attribut treffen. (Es kann nicht ausgewählt werden, für welche Attribute eine bestimmte Dimensionsverwendung gilt, jedoch können Attribute ausgeblendet werden.)  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
