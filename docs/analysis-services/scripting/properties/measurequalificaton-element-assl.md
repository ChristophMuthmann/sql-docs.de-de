---
title: MeasureQualificaton-Element (ASSL) | Microsoft Docs
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
- MeasureQualificaton Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MeasureQualification element
ms.assetid: 754a037c-f20b-4717-a6e8-12f495e8e3b4
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 01bb9fa9dab28eafbe0cd833028c7eef451d9c3f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="measurequalificaton-element-assl"></a>MeasureQualificaton-Element (ASSL)
  Bestimmt, ob ein Präfix auf Measures in der [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md).  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MeasureGroup>  
   ...  
   <MeasureQualification>...</MeasureQualification>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|*Keine*|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[MeasureGroup-Objekt](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Keine*|Kein Präfix wird für Measures innerhalb dieser Measuregruppe übernommen.|  
|*PrefixMeasureGroup*|Der eindeutige Name und die Beschriftung für jede Measure in dieser Measuregruppe erhalten als Präfix den Namen der Measuregruppe und ein einzelnes Leerzeichen.|  
  
## <a name="remarks"></a>Hinweise  
 Das Element, das das übergeordnete Element des entspricht **MeasureQualification** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Siehe auch  
 [Cube-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [MeasureGroup-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

