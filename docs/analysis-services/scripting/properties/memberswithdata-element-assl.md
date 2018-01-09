---
title: MembersWithData-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MembersWithData Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MembersWithData
helpviewer_keywords: MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6021c376319135614c6938ee522acf0151c72989
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="memberswithdata-element-assl"></a>MembersWithData-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Bestimmt, ob Datenelemente für nichtblatt-Datenelemente im übergeordneten Attribut angezeigt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*NonLeafDataVisible*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Hinweise  
 Den Wert des der **MembersWithData** Element wird nur von übergeordneten Attributen verwendet (also der Wert der die [Verwendung](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) Element des der **DimensionAttribute** übergeordnetes Element wird festgelegt, um *übergeordneten*) zu bestimmen, ob Datenelemente für nichtblatt-Datenelemente im übergeordneten Attribut angezeigt. Weitere Informationen zu Datenelementen finden Sie unter [Attribute in über- und untergeordneten Hierarchien](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|value|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|Nichtblattdaten werden ausgeblendet.|  
|*NonLeafDataVisible*|Nichtblattdaten sind sichtbar.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **MembersWithData** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MembersWithData>.  
  
## <a name="see-also"></a>Siehe auch  
 [MembersWithDataCaption-Element &#40; ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)   
 [DimensionAttribute-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
