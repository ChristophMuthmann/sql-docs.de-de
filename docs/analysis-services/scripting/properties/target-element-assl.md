---
title: Target-Element (ASSL) | Microsoft Docs
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
apiname: Target Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Target
helpviewer_keywords: Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1d4f0334fde6506dbb5630fc1dc47efe88a5d48a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="target-element-assl"></a>Target-Element (ASSL)
  Identifiziert das Ziel der [Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
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
|Übergeordnetes Element|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der erwartete Wert dieses Elements hängt vom Wert von der [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md) für das übergeordnete Element **Aktion**. In der folgenden Tabelle werden die erwarteten Werte für **Target** , basierend auf dem Wert für **TargetType**, beschrieben.  
  
|TargetType-Wert|Erwarteter Wert|  
|----------------------|--------------------|  
|*Cube*|Der Name eines Cubes.|  
|*Zellen*|Ein Teilcubeausdruck.|  
|*Festlegen*|Ein Mengenausdruck oder der Name einer benannten Menge.<br /><br /> Hinweis: Eine SELECT-Anweisung kann nicht verwendet werden.|  
|*HierarchyMembers-Hierarchie*|Der Name einer Hierarchie.|  
|*DimensionMembers-Dimension*|Der Name einer Dimension.|  
|*Ebene LevelMembers*|Der Name einer Ebene.|  
|*AttributeMembers-Attribut*|Der Name eines Attributs.|  
  
 Das Element, das das übergeordnete Element des entspricht **Ziel** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
