---
title: Event-Element (ASSL) | Microsoft Docs
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
- Event Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EVENT
helpviewer_keywords:
- Event element
ms.assetid: c7911bcd-e601-4a96-a6d8-20b7c7375ff2
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: af95382e32d013a079a5f808560797b3181a84f6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="event-element-assl"></a>Event-Element (ASSL)
  Definiert eine **Ereignis** als Teil der aufzuzeichnenden eine [Ablaufverfolgung](../../../analysis-services/scripting/objects/trace-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Events>  
   <Event>  
      <EventID>...</EventID>  
      <Columns>...</Columns>  
   </Event>  
</Events>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-n: Erforderliches Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Ereignisse](../../../analysis-services/scripting/collections/events-element-assl.md)|  
|Untergeordnete Elemente|[Spalten](../../../analysis-services/scripting/collections/columns-element-assl.md), [EventID](../../../analysis-services/scripting/properties/eventid-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.TraceEvent>.  
  
## <a name="see-also"></a>Siehe auch  
 [Trace-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

