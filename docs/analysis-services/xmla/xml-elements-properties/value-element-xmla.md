---
title: Value-Element (XMLA) | Microsoft Docs
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
- Value Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: f87ca7f8-d9fe-4730-a706-5d50fcfe21df
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 18e6190fabc53df42e7ebd1d7284dfd3f987fbfe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="value-element-xmla"></a>Value-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Enthält den gewünschten Wert ein [Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) von hinzuzufügenden Elements ein [einfügen](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md) Befehl oder ein [Zelle](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) Element aktualisiert werden ein [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)Befehl.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Any|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Attribut](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [Zelle](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Bei **Attribute** -Elementen enthält das **Value** -Element den gewünschten Wert, den das Element nach der Übermittlung des **Insert** -Befehls enthalten soll. Weitere Informationen zum Einfügen von Elementen finden Sie unter [einfügen, aktualisieren und Löschen von Membern &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
 Bei **Cell** -Elementen enthält das **Value** -Element den gewünschten Wert, den die Zelle nach der Übermittlung des **UpdateCells** -Befehls enthalten soll. Der tatsächliche Wert, der in der Rückschreibetabelle für die Zelle gespeichert ist, ist die Differenz zwischen dem Originalwert der Zelle und dem gewünschten Wert der Zelle.  
  
 Der von diesem Element verwendete Datentyp sollte dem Datentyp der zu aktualisierenden Zelle entsprechen.  
  
 Weitere Informationen zum Aktualisieren von Zellen finden Sie unter [Aktualisieren von Zellen &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CellOrdinal-Element &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [INSERT-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
