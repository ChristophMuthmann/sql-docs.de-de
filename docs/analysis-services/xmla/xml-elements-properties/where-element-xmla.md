---
title: Wobei-Element (XMLA) | Microsoft Docs
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
- Where Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords:
- Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b559e82af0840067e9448e83056a3f1e96937b39
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="where-element-xmla"></a>Where-Element (XMLA)
  Definiert eine Filterbedingung, die vom übergeordneten Befehl [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) oder [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
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
|Übergeordnete Elemente|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|Untergeordnete Elemente|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Bei **Drop** -Befehlen identifiziert das **Where** -Element zusammen mit dem [DeleteWithDescendants](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) -Element den Umfang der zu löschenden Attributelemente.  
  
 Bei **Update** -Befehlen identifiziert das **Where** -Element den Umfang der zu aktualisierenden Attributelemente. Mehrere Attributelemente können über eine Kombination aus Attributen, die in der **Attributes** -Auflistung des übergeordneten **Update** -Befehls und der **Attributes** -Auflistung des **Where** -Elements enthalten sind, aktualisiert werden.  
  
 Weitere Informationen zum Löschen und Aktualisieren von Attributelementen finden Sie unter [Einfügen, Aktualisieren und Löschen von Elementen &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
