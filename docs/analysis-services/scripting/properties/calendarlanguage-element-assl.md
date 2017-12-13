---
title: CalendarLanguage-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CalendarLanguage Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CalendarLanguage
helpviewer_keywords: CalendarLanguage element
ms.assetid: e43a0f48-a583-418b-a0a4-d73a40035573
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f373a1f9ca778e7d209ca317dcf8625813a24938
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="calendarlanguage-element-assl"></a>CalendarLanguage-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert die für verwendete Kalendersprache der [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<TimeBinding>  
   ...  
   <CalendarLanguage>...</CalendarLanguage>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Integer|  
|Standardwert|**1033**|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Dies ist die Sprache, in der Dimensionselementnamen erstellt werden. Die Sprache von Beschriftungen sollte mit ganzzahlig-basierten LCID-Codes definiert werden. Zum Beispiel stellt den Standardwert die English-US LCID dar.  
  
 Das Element, das das übergeordnete Element des entspricht **CalendarLanguage** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
