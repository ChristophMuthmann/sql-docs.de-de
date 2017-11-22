---
title: SPID-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
apiname: SPID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#SPID
- microsoft.xml.analysis.spid
- urn:schemas-microsoft-com:xml-analysis#SPID
helpviewer_keywords: SPID element
ms.assetid: c4a54dcb-a0cd-4255-9e0f-a34eb990854f
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4feb6748cacd70b31470c0496ead5c7dacec6dd1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spid-element-xmla"></a>SPID-Element (XMLA)
  Identifiziert einen aktiven Serverprozessbezeichner (SPID), für das übergeordnete Element ausgeführt ["Abbrechen"](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Cancel>  
   ...  
   <SPID>...</SPID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Integer|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Abbrechen](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die **SPID** Element darstellt, die Serverprozess-ID (SPID) für eine bestimmte Sitzung auf einer Instanz von verwendet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [CancelAssociated-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)   
 [ConnectionID-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SessionID-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
