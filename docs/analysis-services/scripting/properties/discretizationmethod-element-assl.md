---
title: DiscretizationMethod-Element (ASSL) | Microsoft Docs
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
apiname:
- DiscretizationMethod Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2bbf548ba16ccc81d1536c5c64a22e9c69d96d1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod-Element (ASSL)
  Definiert die zu verwendende Diskretisierungsmethode.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Keine*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert des **DiscretizationMethod** -Elements bestimmt, wie Werte für **DimensionAttribute** oder **ScalarMiningStructureColumn** diskretisiert oder in spezifischen Gruppen geordnet werden. Weitere Informationen über die Diskretisierung finden Sie unter [Diskretisierungsmethoden &#40; Data Mining &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*Automatic*|Entspricht der AUTOMATIC-Diskretisierungsmethode für Miningstrukturspalten.|  
|*EqualAreas*|Entspricht der EQUAL_AREAS-Diskretisierungsmethode für Miningstrukturspalten.|  
|*Cluster*|Entspricht der CLUSTERS-Diskretisierungsmethode für Miningstrukturspalten.|  
|*Schwellenwerte*|Entspricht der THRESHOLDS-Diskretisierungsmethode für Miningstrukturspalten.|  
|*EqualRanges*|Entspricht der EQUAL_RANGES-Diskretisierungsmethode für Miningstrukturspalten.|  
  
 Die Enumeration, die den zulässigen Werten für die entsprechende **DiscretizationMethod** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

