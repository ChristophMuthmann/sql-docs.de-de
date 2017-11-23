---
title: Aggregation-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Aggregation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Aggregation
helpviewer_keywords: Aggregation element
ms.assetid: f37af388-b2b3-4234-a1d6-936ee9b7f2ae
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8831a4563c3ca52c425eb64f9c6c4c9e6023e2b8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="aggregation-element-assl"></a>Aggregation-Element (ASSL)
  Definiert eine einzelne Aggregation für ein [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Aggregations>  
      <Aggregation>  
      <ID>...</ID>  
      <Name>...</Name>  
      <Dimensions>...</Dimensions>  
            <Annotations>...</Annotations>  
      <Description>...</Description>  
   </Aggregation>  
</Aggregations>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Aggregationen](../../../analysis-services/scripting/collections/aggregations-element-assl.md)|  
|Untergeordnete Elemente|[Anmerkungen](../../../analysis-services/scripting/collections/annotations-element-assl.md), [Beschreibung](../../../analysis-services/scripting/properties/description-element-assl.md), [Dimensionen](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Aggregation>.  
  
## <a name="see-also"></a>Siehe auch  
 [Partition-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)   
 [AggregationDesign-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)   
 [MeasureGroup-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
