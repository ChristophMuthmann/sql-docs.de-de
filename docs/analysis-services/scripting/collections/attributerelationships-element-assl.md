---
title: AttributeRelationships-Element (ASSL) | Microsoft Docs
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
apiname: AttributeRelationships Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MemberProperties
helpviewer_keywords: AttributeRelationships element
ms.assetid: f2ff82f6-6a7f-481a-a1ef-014bef38face
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 37fd8d0c2520f4e3626b7a4261d888ed9ad8b21a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="attributerelationships-element-assl"></a>AttributeRelationships-Element (ASSL)
  Enthält die Auflistung der [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) Elemente für das Attribut.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <AttributeRelationships>  
      <AttributeRelationship>...</AttributeRelationship>  
   </AttributeRelationships>  
   ...  
</Attribute>  
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
|Übergeordnete Elemente|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) des Typs [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Untergeordnete Elemente|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.AttributeRelationshipCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
