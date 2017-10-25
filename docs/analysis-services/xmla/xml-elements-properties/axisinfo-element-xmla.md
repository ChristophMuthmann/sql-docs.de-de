---
title: AxisInfo-Element (XMLA) | Microsoft Docs
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
- AxisInfo Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AxisInfo
- microsoft.xml.analysis.axisinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#AxisInfo
helpviewer_keywords:
- AxisInfo element
ms.assetid: 060741db-b2ec-4174-9277-58d996440a88
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa8b5554573ebb3f34212fd7ba48b6583fb926af
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="axisinfo-element-xmla"></a>AxisInfo-Element (XMLA)
  Stellt die Metadaten einer einzelnen Achse dar, die im [AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md) -Element enthalten sind.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<AxesInfo>  
   ...  
   <AxisInfo name="string">  
      <HierarchyInfo>...</HierarchyInfo>  
   </AxisInfo>  
   ...  
</AxesInfo>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-n: Erforderliches Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md)|  
|Untergeordnete Elemente|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Description|  
|---------------|-----------------|  
|Name|Erforderliches **String** -Attribut. Der Name der Achse.|  
  
## <a name="remarks"></a>Hinweise  
 In einem **root** -Element, das das **MDDataSet** -Objekt verwendet, enthält ein **AxisInfo** -Element eine Auflistung von **HierarchyInfo** -Elementen, die in Kombination mit dem Wert des **name** -Attributs eine Definition einer einzelnen Achse darstellt, die im multidimensionalen Datensatz zurückgegeben wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

