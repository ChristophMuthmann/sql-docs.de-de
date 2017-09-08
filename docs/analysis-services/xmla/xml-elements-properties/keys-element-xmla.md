---
title: Keys-Element (XMLA) | Microsoft Docs
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
- Keys Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Keys
- http://schemas.microsoft.com/analysisservices/2003/engine#Keys
- microsoft.xml.analysis.keys
helpviewer_keywords:
- Keys element
ms.assetid: 67291791-0032-412a-9a4f-74f68533e83d
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b5c60bd6a10a32d886fa342e63c946e9be83ce24
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="keys-element-xmla"></a>Keys-Element (XMLA)
  Enthält eine Auflistung von [Schlüssel](../../../analysis-services/xmla/xml-elements-properties/key-element-xmla.md) Elemente verwendet, um die Elementschlüssel der Attributelemente vom übergeordneten Element dargestellt zu identifizieren [Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Attribute>  
   ...  
   <Keys>  
      <Key>...</Key>  
   </Keys>  
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
|Untergeordnete Elemente|[Key](../../../analysis-services/xmla/xml-elements-properties/key-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Drop-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [INSERT-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
