---
title: Update-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: Update Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Update
- microsoft.xml.analysis.update
- http://schemas.microsoft.com/analysisservices/2003/engine#Update
helpviewer_keywords: Update command [XMLA]
ms.assetid: 324dcc16-865d-4d0a-b393-2b06c18ac807
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 27c1f3b97b33be50db274d47ef83c3fce1086d0f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="update-element-xmla"></a>Update-Element (XMLA)
  Aktualisiert Attributelemente in einer Dimension.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <Update>  
      <Object>...</Object>  
      <MoveWithDescendants>...</MoveWithDescendants>  
      <Attributes>...</Attributes>  
      <Where>...</Where>  
   </Update>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md), [MoveWithDescendants](../../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md), [Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md), [, in denen](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Der **Update** -Befehl verschiebt Attributelemente innerhalb einer Dimension mit aktiviertem Schreibzugriff.  
  
 Weitere Informationen zum Aktualisieren von Elementen finden Sie unter [einfügen, aktualisieren und Löschen von Elementen &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Drop-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [INSERT-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
