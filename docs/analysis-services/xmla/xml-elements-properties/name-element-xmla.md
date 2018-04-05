---
title: Name-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Name Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 995792653603bd7ff5954a34755e7704544675b6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="name-element-xmla"></a>Name-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Enthält den Namen eines attributelements für das übergeordnete Element [Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) oder [Übersetzung](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgänger oder übergeordnetes Element|Cardinality|  
|------------------------|-----------------|  
|[Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1: Erforderliches Element, das nur einmal auftritt.|  
|[Übersetzung](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [Übersetzung](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|Untergeordnete Elemente|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Bei **Attribute** -Elementen enthält das **Name** -Element den Namen des Attributelements, das vom bzw. während des **Insert** - oder **Update** -Befehl(s) eingefügt oder aktualisiert wird.  
  
 Bei **Translation** -Elementen enthält das **Name** -Element die Beschriftung des Attributelements in der Sprache, die vom **Language** -Element des übergeordneten **Translation** -Objekts festgelegt wird. Wenn das **Name** -Element nicht festgelegt ist oder eine leere Zeichenfolge enthält, wird der Wert des **Name** -Elements für das **Attribute** -Element, das das **Translation** -Element enthält, verwendet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [INSERT-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Language-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [Update-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
