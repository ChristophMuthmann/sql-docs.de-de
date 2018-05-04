---
title: AggregationAttribute-Datentyp (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- AggregationAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationAttribute
helpviewer_keywords:
- AggregationAttribute data type
ms.assetid: 636827c7-938d-4b7d-9827-46da3bc60d9a
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 09295db73608fa040960a709271f1c72816848b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationattribute-data-type-assl"></a>AggregationAttribute-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert den Grunddatentyp, der die Zuordnung zwischen einem [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) -Element und einem Attribut darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<AggregationAttribute>  
   <AttributeID>...</AttributeID>  
      <Annotations>...</Annotations>  
</AggregationAttribute>  
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
|Untergeordnete Elemente|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|Abgeleitete Elemente|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) -Auflistung von [AggregationDimension](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Die entsprechende Klasse im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.AggregationAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Aggregation-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [Analysis Services Scripting Language-XML-Datentypen & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
