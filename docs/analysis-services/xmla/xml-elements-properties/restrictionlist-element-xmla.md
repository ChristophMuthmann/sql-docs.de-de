---
title: RestrictionList-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
apiname:
- RestrictionList Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df82fa9bb12094ae01535977f10f26622cbac6b2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="restrictionlist-element-xmla"></a>RestrictionList-Element (XMLA)
  Enthält eine Sammlung von Einschränkungsspalten und Werten, die von der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) -Methode verwendet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
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
|Übergeordnete Elemente|[Einschränkungen](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|Untergeordnete Elemente|Einschränkungsspalten und Werte (siehe Hinweise).|  
  
## <a name="remarks"></a>Hinweise  
 Das **RestrictionList** -Element enthält eine Auflistung von Einschränkungsspalten, in denen die von der **Discover** -Methode zurückgegebenen Daten gefiltert werden können. Jede Einschränkungsspalte im **RestrictionList** -Element wird durch ein separates XML-Element definiert. Beim Wert der Einschränkungsspalte handelt es sich um die Daten, die im XML-Element enthalten sind. Der Name der Einschränkungsspalte entspricht dem Namen des XML-Elements.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

