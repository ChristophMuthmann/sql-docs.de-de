---
title: CalculationProperties-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- CalculationProperties Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CalculationProperties
helpviewer_keywords:
- CalculationProperties element
ms.assetid: dccfe036-0b1b-4877-8bdd-4b128ccb55c9
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 22115f16242c685b1c32f7e15fb71849e55e8043
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calculationproperties-element-assl"></a>CalculationProperties-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält die Auflistung der [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) Elemente, die zu einer [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MdxScript>  
   ...  
   <CalculationProperties>  
      <CalculationProperty>...</CalculationProperty>  
   </CalculationProperties>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[MdxScript-Objekt](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
|Untergeordnete Elemente|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.CalculationPropertyCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
