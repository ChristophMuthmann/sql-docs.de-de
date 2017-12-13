---
title: CurrentTimeMember-Element (ASSL) | Microsoft Docs
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
apiname: CurrentTimeMember Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CurrentTimeMember
helpviewer_keywords: CurrentTimeMember element
ms.assetid: 2e73009c-9f2b-441c-bdf0-ca19b160da4f
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 76904b7d7973d75bbf7f74a9bf198862cdc65f71
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="currenttimemember-element-assl"></a>CurrentTimeMember-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert das aktuelle Element einer Dimension zugeordnet Uhrzeit einen [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Kpi>  
   ...  
   <CurrentTimeMember>...</CurrentTimeMember>  
   ...  
</AggregationDimension>  
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
 Der Wert dieses Elements ist eine MDX-Anweisung (Multidimensional Expressions), die zu einem einzigen Element in einer Zeitdimension ausgewertet wird, welche zum Abrufen des aktuellen Zeitraums beim Auswerten des Key Performance Indicator (KPI) dient.  
  
 Das Element, das das übergeordnete Element des entspricht **CurrentTimeMember** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
