---
title: Action-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Action Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6dc68139ddfbce5151cb3750aaca1ffd54d37041
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="action-data-type-assl"></a>Action-Datentyp (ASSL)
  Definiert einen abstrakten Grunddatentyp, der eine Aktion in einem [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element oder eine [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Caption>...</Caption>  
      <CaptionIsMdx>...</CaptionIsMdx>  
      <Translations>...</Translations>  
   <TargetType>...</TargetType>  
   <Target>...</Target>  
   <Condition>...</Condition>  
   <Type>...</Type>  
   <Invocation>...</Invocation>  
   <Application>...</Application>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
</Action>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Aktionen](../../../analysis-services/scripting/collections/actions-element-assl.md)|  
|Untergeordnete Elemente|[Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Anwendung](../../../analysis-services/scripting/properties/application-element-assl.md), [Beschriftung](../../../analysis-services/scripting/properties/caption-element-assl.md), [CaptionIsMdx](../../../analysis-services/scripting/properties/captionismdx-element-assl.md), [Bedingung](../../../analysis-services/scripting/properties/condition-element-assl.md), [Beschreibung ](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Aufruf](../../../analysis-services/scripting/properties/invocation-element-assl.md), [Namen](../../../analysis-services/scripting/properties/name-element-assl.md), [Ziel](../../../analysis-services/scripting/properties/target-element-assl.md), [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md), [Übersetzungen](../../../analysis-services/scripting/collections/translations-element-assl.md), [Typ](../../../analysis-services/scripting/properties/type-element-action-assl.md)|  
|Abgeleitete Elemente|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen zu Aktionstypen finden Sie unter [Aktionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Siehe auch  
 [Cube-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Perspective-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)   
 [PerspectiveAction-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)   
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
