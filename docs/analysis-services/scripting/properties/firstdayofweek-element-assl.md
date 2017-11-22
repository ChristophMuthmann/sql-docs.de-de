---
title: FirstDayOfWeek-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: FirstDayOfWeek Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: FirstDayOfWeek
helpviewer_keywords: FirstDayOfWeek element
ms.assetid: d3c92fa3-b293-43b5-806e-cd1c146a3a7c
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fb6949a52800150ec90e47e2c0bf4b2deaeed605
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="firstdayofweek-element-assl"></a>FirstDayOfWeek-Element (ASSL)
  Definiert den ersten Tag der Woche für eine [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<TimeBinding>  
   ...  
   <FirstDayOfWeek>...</FirstDayOfWeek>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Ganzzahl (zwischen 1 und 7, wobei 1 = Sonntag und 7 = Samstag).|  
|Standardwert|**1**|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das Element, das das übergeordnete Element des entspricht **"FirstDayOfWeek"** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
