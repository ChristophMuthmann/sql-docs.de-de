---
title: AggregationDesignDimension-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AggregationDesignDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationDesignDimension
helpviewer_keywords: AggregationDesignDimension data type
ms.assetid: 06a0d418-014c-4f40-a63a-5cfeee3f6a41
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8145ea1ec5c7e6745a17d9182099222132e5192a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="aggregationdesigndimension-data-type-assl"></a>AggregationDesignDimension-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert einen Grunddatentyp, der die Beziehung zwischen einer Cubedimension darstellt und ein [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<AggregationDesignDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDesignDimension>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Attribute](../../../analysis-services/scripting/collections/attributes-element-assl.md), [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)|  
|Abgeleitete Elemente|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([Dimensionen](../../../analysis-services/scripting/collections/dimensions-element-assl.md) Auflistung von [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.AggregationDesignDimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [AggregationDesign-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)   
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
