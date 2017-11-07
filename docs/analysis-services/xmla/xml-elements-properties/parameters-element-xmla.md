---
title: Parameters-Element (XMLA) | Microsoft Docs
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
- Parameters Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 27bf966c1a1fb44c547a74f38cc3cddd6399793c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="parameters-element-xmla"></a>Parameters-Element (XMLA)
  Enthält eine Auflistung von [Parameter](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md) Elementen, die verwendet werden, indem die [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.  
  
 **Namespace:**`urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
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
|Übergeordnete Elemente|[Ausführen](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|Untergeordnete Elemente|[Parameter](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Einige XMLA-Befehle (XML for Analysis) wie der [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) -Befehl können weitere Informationen erfordern. Die **Parameter** Element bietet einen Mechanismus zum Bereitstellen zusätzlicher Informationen, einschließlich segmentierter Informationen, XMLA-Befehl.  
  
 Wenn der XMLA-Befehl nicht verwendet die **Parameter** Element, das Element kann ausgelassen werden, beim Aufrufen der **Execute** Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

