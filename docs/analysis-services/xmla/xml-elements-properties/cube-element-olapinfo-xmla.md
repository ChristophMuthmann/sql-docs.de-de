---
title: Cube-Element (OlapInfo) (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Cube Element (OlapInfo)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords: Cube element
ms.assetid: c2b6fe41-6ad4-4181-98a9-3a2517f0b7cc
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7be9f0e7dbcdddc853debf2536d97ac9de0c25ce
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="cube-element-olapinfo-xmla"></a>Cube-Element (OlapInfo) (XMLA)
  Enthält Informationen über einen Cube für das übergeordnete [CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md) -Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CubeInfo>  
   <Cube>  
      <CubeName>...</CubeName>  
      <LastDataUpdate>...</LastDataUpdate>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
   </Cube>  
   ...  
</CubeInfo>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md)|  
|Untergeordnete Elemente|[CubeName](../../../analysis-services/xmla/xml-elements-properties/cubename-element-xmla.md), [LastDataUpdate](../../../analysis-services/xmla/xml-elements-properties/lastdataupdate-element-xmla.md), [LastSchemaUpdate](../../../analysis-services/xmla/xml-elements-properties/lastschemaupdate-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
