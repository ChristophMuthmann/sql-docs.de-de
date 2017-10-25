---
title: TrendGraphic-Element (ASSL) | Microsoft Docs
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
- TrendGraphic Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TrendGraphic
helpviewer_keywords:
- TrendGraphic element
ms.assetid: 7448fd80-3072-4d85-b3a0-6606d1d20885
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c209d484e004deddd1c9ba2e169511c07658e13d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="trendgraphic-element-assl"></a>TrendGraphic-Element (ASSL)
  Enthält die empfohlene grafische Darstellung des Trends des der [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Kpi>  
   ...  
   <TrendGraphic>...</TrendGraphic>  
   ...  
</Kpi>  
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
|Übergeordnetes Element|[KPI](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Standardpfeil*|Standardpfeil|  
|*Statuspfeil - aufsteigend*|Statuspfeil|  
|*Statuspfeil - absteigend*|Umgekehrter Statuspfeil|  
|*Smileysymbol*|Gesicht|  
  
 Das Element, das das übergeordnete Element des entspricht **TrendGraphic** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

