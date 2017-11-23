---
title: Filter-Element (Ablaufverfolgung) (ASSL) | Microsoft Docs
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
apiname: Filter Element (Trace)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: filter
helpviewer_keywords: Filter element
ms.assetid: 411a598e-3bb1-487b-9f37-cce4b57a67b4
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c9782c112a6c46f6a6203ad186e792d68f55fcb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="filter-element-trace-assl"></a>Filter-Element (Ablaufverfolgung) (ASSL)
  Enthält ein XML-Dokument-Fragment, beschreibt die [Ablaufverfolgung](../../../analysis-services/scripting/objects/trace-element-assl.md) Filter.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Trace>  
   ...  
   <Filter>...</Filter>  
   ...  
</Trace>  
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
|Übergeordnetes Element|[Trace](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das Element, das das übergeordnete Element des entspricht **Filter** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [Traces-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)  
  
  
