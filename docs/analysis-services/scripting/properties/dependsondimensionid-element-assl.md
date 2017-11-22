---
title: DependsOnDimensionID-Element (ASSL) | Microsoft Docs
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
apiname: DependsOnDimensionID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DependsOnDimensionID
helpviewer_keywords: DependsOnDimensionID element
ms.assetid: 66ec20dd-b475-4895-a92c-7ac0e7e1c675
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 642a9391256bc863bcecc9a6ab3a378d9a3fa7ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dependsondimensionid-element-assl"></a>DependsOnDimensionID-Element (ASSL)
  Enthält den Bezeichner (ID) einer anderen Dimension, von der die übergeordnete Dimension abhängt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Dimension>  
      ...  
   <DependsOnDimensionID>...</DependsOnDimensionID>  
   ...  
</Dimension>  
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
|Übergeordnete Elemente|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **DependsOnDimensionID** -Element wird von einer abhängigen Dimension verwendet, um die Dimension zu identifizieren, von der es abhängt.  
  
 Das Element, das das übergeordnete Element des entspricht **DependsOnDimensionID** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
