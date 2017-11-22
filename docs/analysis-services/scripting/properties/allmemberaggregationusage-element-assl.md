---
title: AllMemberAggregationUsage-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: AllMemberAggregationUsage Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllMemberAggregationUsage
helpviewer_keywords: AllMemberAggregationUsage element
ms.assetid: 264fe9d8-8e9a-4642-8cee-7c2804126926
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd04b33e9150cc2bceb7e744e858a3f72b5759e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="allmemberaggregationusage-element-assl"></a>AllMemberAggregationUsage-Element (ASSL)
  Steuerelemente wie der Aggregations-Designer in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Aggregationen entwirft.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CubeDimension>  
   ...  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Standardwert*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Full*|Jede Aggregation für den Cube muss das Alle-Element enthalten.|  
|*Keine*|Keine Aggregation für den Cube darf das Alle-Element enthalten.|  
|*Nicht eingeschränkt*|Keine Einschränkungen für den Aggregations-Designer.|  
|*Standardwert*|Identisch mit *Unrestricted*.|  
  
## <a name="remarks"></a>Hinweise  
 Das Element, das das übergeordnete Element des entspricht **AllMemberAggregationUsage** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Cube-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
