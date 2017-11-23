---
title: Wobei-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Where Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords: Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5cff731a9673f8f811895f6dcc2b1a65c77f5716
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
  
  
