---
title: SessionID-Element (XMLA) | Microsoft Docs
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
apiname: SessionID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#SessionID
- http://schemas.microsoft.com/analysisservices/2003/engine#SessionID
- microsoft.xml.analysis.sessionid
helpviewer_keywords: SessionID element
ms.assetid: 18220e00-76cf-48f6-9465-200465a0c553
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: afc320ef1cb6a913df7e4ecc6e65087de4cb0d5a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sessionid-element-xmla"></a>SessionID-Element (XMLA)
  Identifiziert eine aktive Sitzung, für das übergeordnete Element ausgeführt ["Abbrechen"](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Cancel>  
   ...  
   <SessionID>...</SessionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Abbrechen](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [CancelAssociated-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)   
 [ConnectionID-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SPID-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
