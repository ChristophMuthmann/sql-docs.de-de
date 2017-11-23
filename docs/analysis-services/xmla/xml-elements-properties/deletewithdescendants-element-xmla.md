---
title: DeleteWithDescendants-Element (XMLA) | Microsoft Docs
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
apiname: DeleteWithDescendants Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DeleteWithDescendants
- microsoft.xml.analysis.deletewithdescendants
- urn:schemas-microsoft-com:xml-analysis#DeleteWithDescendants
helpviewer_keywords: DeleteWithDescendants element
ms.assetid: adfc9437-aaa7-4364-bcdb-128fcc9a410d
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7420b12875dd521186741726b084fc99131fa5cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="deletewithdescendants-element-xmla"></a>DeleteWithDescendants-Element (XMLA)
  Gibt an, ob auch die Nachfolger der Attributelemente auch vom übergeordneten [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) -Befehl gelöscht werden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Drop>  
   ...  
   <DeleteWithDescendants>...</DeleteWithDescendants>  
   ...  
</Drop>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|False|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Löschen](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **DeleteWithDescendants** -Element bestimmt, ob der **Drop** -Befehl die vom [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) -Element identifizierten Attribute löschen sollte und ob die Nachfolger dieser Attributelemente ebenfalls gelöscht werden sollen.  
  
> [!NOTE]  
>  Dieses Element gilt nur für Attributelemente in Über-/Unterordnungshierarchien.  
  
 Weitere Informationen zum Löschen und Aktualisieren von Attributelementen finden Sie unter [Einfügen, Aktualisieren und Löschen von Elementen &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
