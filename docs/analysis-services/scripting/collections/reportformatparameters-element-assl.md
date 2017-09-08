---
title: ReportFormatParameters-Element (ASSL) | Microsoft Docs
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
- ReportFormatParameters Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReportFormatParameters
helpviewer_keywords:
- ReportFormatParameters element
ms.assetid: f2e677bf-7b6b-4ce4-b0ec-75a4999306c9
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3039f088a38a46501f86868fbede780294301f2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="reportformatparameters-element-assl"></a>ReportFormatParameters-Element (ASSL)
  Enthält die Auflistung der [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md) -Elemente für ein [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md) -Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action xsi:type="ReportAction">  
   ...  
   <ReportFormatParameters>  
      <ReportFormatParameter>...</ReportFormatParameter>  
   </ReportFormatParameters>  
   ...  
</Action>  
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
|Übergeordnete Elemente|[Action](../../../analysis-services/scripting/objects/action-element-assl.md) des Typs [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)|  
|Untergeordnete Elemente|[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das Element, das das übergeordnete Element des entspricht **ReportFormatParameters** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
