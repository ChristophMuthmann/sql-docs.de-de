---
title: Translations-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Translations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.translations
- urn:schemas-microsoft-com:xml-analysis#Translations
- http://schemas.microsoft.com/analysisservices/2003/engine#Translations
helpviewer_keywords:
- Translations element
ms.assetid: 86fd2119-9bea-4306-829e-cc439da05566
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d327f43d6b193f0add12166009d0008a2c0af202
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="translations-element-xmla"></a>Translations-Element (XMLA)
  Enthält eine Auflistung von [Translation](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) -Elementen, die verwendet werden, um die Elementschlüssel der Attributelemente zu identifizieren, die vom übergeordneten [Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) -Element dargestellt werden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Attribute>  
   ...  
   <Translations>  
      <Translation>...</Translation>  
   </Translations>  
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
|Übergeordnete Elemente|[Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|Untergeordnete Elemente|[Übersetzung](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [INSERT-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

