---
title: Target-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Target Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4673735780942f161ccb09438c035087a898f41e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="target-element-assl"></a>Target-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
