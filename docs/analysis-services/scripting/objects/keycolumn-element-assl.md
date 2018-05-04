---
title: KeyColumn-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- KeyColumn Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- KeyColumn
helpviewer_keywords:
- KeyColumn element
ms.assetid: 7b03eeb3-d478-4c38-822e-8cdfcc485039
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 20122b7c8cd12e00d4f89cadba3fd96416756a16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="keycolumn-element-assl"></a>KeyColumn-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält die Definition einer Spalte, die der Schlüssel oder Teil eines Schlüssels für ein Attribut ist.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Standardwert|Keine|  
|Kardinalität|1-n: Erforderliches Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen zu den **DataItem** Typ, einschließlich einer Tabelle von Analysis Services Scripting Language (ASSL)-Objekten und Eigenschaften der **DataItem** finden Sie unter [DataItem-Datentyp & #40; ASSL & #41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Die Elemente, die den übergeordneten Elementen von entsprechen den **KeyColumns** Auflistung im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>, und <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Siehe auch  
 [AggregationInstanceAttribute-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)   
 [AggregationInstanceCubeDimension-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)   
 [DimensionAttribute-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [MeasureGroupAttribute-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)   
 [ScalarMiningStructureColumn-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)   
 [Objekte & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
