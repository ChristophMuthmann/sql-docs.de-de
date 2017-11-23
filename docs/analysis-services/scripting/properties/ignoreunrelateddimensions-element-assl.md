---
title: IgnoreUnrelatedDimensions-Element (ASSL) | Microsoft Docs
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
apiname: IgnoreUnrelatedDimensions Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: IgnoreUnrelatedDimensions
helpviewer_keywords: IgnoreUnrelatedDimensions element
ms.assetid: c7d7a1cd-a8e0-4ae7-9464-a1d2a55a86ab
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 920bc28033619bc546f84351d53ab76720fda6db
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="ignoreunrelateddimensions-element-assl"></a>IgnoreUnrelatedDimensions-Element (ASSL)
  Bestimmt, ob nicht verknüpfte Dimensionen auf ihre höchste Ebene gezwungen werden, wenn Elemente von Dimensionen, die nicht mit der Measuregruppe verknüpft sind, in eine Abfrage eingeschlossen werden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MeasureGroup>  
   ...  
   <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|Wahr|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Wenn **IgnoreUnrelatedDimensions** **true**ist, werden nicht verknüpfte Dimensionen auf ihre höchste Ebene gezwungen; wenn der Wert **false**ist, werden die Dimensionen nicht auf ihre oberste Ebene gezwungen. Diese Eigenschaft ist ähnlich, die MDX (Multidimensional Expressions) [ValidMeasure](../../../mdx/validmeasure-mdx.md) Funktion.  
  
 Das Element, das das übergeordnete Element des entspricht **IgnoreUnrelatedDimensions** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
