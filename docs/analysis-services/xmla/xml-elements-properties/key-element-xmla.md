---
title: Key-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Key Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Key
- urn:schemas-microsoft-com:xml-analysis#Key
- microsoft.xml.analysis.key
helpviewer_keywords: Key element
ms.assetid: 09d3cd48-49f7-4b58-b8bb-ca75b81bb02f
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2e6c77841fa78b1ad2c866abc5c3aea5af50ef27
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="key-element-xmla"></a>Key-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Enthält einen Elementschlüsselwert für ein Attributelement.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Any|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Schlüssel](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der von diesem Element verwendete Datentyp sollte dem Datentyp der jeweiligen Schlüsselspalte für das angegebene Attribut entsprechen. Wenn **Key** -Elemente nicht für ein übergeordnetes **Attribute** -Element angegeben sind, werden das **AttributeName** und das **Name** -Element, die im übergeordneten **Attribute** -Element angegeben sind, zur Identifizierung des zu modifizierenden Attributelements verwendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [AttributeName-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [Drop-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [INSERT-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [Update-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Wobei-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
