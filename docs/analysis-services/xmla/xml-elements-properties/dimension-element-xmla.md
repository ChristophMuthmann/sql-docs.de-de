---
title: Dimension-Element (XMLA) | Microsoft Docs
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
- Dimension Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Dimension
- urn:schemas-microsoft-com:xml-analysis#Dimension
- microsoft.xml.analysis.dimension
helpviewer_keywords:
- Dimension element
ms.assetid: 85093468-e971-4b8e-9ee4-7b264ad01711
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eb5f7e0e5c8cb8032074396d43a24efb0429bfe4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dimension-element-xmla"></a>Dimension-Element (XMLA)
  Identifiziert die Cubedimension, die durch das übergeordnete Element dargestellten [Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Object>  
   ...  
   <Dimension>...</Dimension>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **Dimension** -Element ist ein Objektbezeichner, der den Namen der Cubedimension enthält, der vom **Object** -Element dargestellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Database-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)   
 [Dimension-Element (XMLA)](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
