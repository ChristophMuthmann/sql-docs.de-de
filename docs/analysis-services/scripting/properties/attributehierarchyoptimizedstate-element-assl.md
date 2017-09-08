---
title: AttributeHierarchyOptimizedState-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AttributeHierarchyOptimizedState Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeHierarchyOptimizedState
helpviewer_keywords:
- AttributeHierarchyOptimizedState element
ms.assetid: d87148c8-2011-45ae-94c3-851f48babc5f
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79b7f84f96c9921a0d1fafce4bc0c8604b5fd582
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="attributehierarchyoptimizedstate-element-assl"></a>AttributeHierarchyOptimizedState-Element (ASSL)
  Bestimmt die Optimierungsebene, die auf die Attributhierarchie angewendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute -->  
   ...  
   <AttributeHierarchyOptimizedState>...  
   </AttributeHierarchyOptimizedState>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*FullyOptimized*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*FullyOptimized*|Durch die Instanz werden Indizes zum Verbessern der Abfrageleistung für die Attributhierarchie erstellt.|  
|*NotOptimized*|Von der Instanz werden keine zusätzlichen Indizes erstellt.|  
  
 Die Enumeration, die den zulässigen Werten für die entsprechende **AttributeHierarchyOptimizedState** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.OptimizationType>. Die Elemente, die den übergeordneten Elementen von entsprechen **AttributeHierarchyOptimizedState** im AMO-Objektmodell sind <xref:Microsoft.AnalysisServices.CubeAttribute> und <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
