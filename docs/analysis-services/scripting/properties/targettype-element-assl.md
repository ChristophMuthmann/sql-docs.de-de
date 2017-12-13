---
title: TargetType-Element (ASSL) | Microsoft Docs
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
apiname: TargetType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TargetType
helpviewer_keywords: TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fc1978e4e7bd243f5921423f18e414ce83c0f4e8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="targettype-element-assl"></a>TargetType-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifiziert den Elementtyp des Elements identifiziert, der [Ziel](../../../analysis-services/scripting/properties/target-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Cube*|Das Ziel der Aktion ist ein Cube.|  
|*Zellen*|Das Ziel der Aktion ist ein Teilcube.|  
|*Festlegen*|Das Ziel der Aktion ist eine Menge.|  
|*Hierarchy*|Das Ziel der Aktion ist eine Hierarchie.|  
|*Level*|Das Ziel der Aktion ist eine Ebene.|  
|*DimensionMembers*|Das Ziel der Aktion sind die Elemente einer Dimension.|  
|*HierarchyMembers*|Das Ziel der Aktion sind die Elemente einer Hierarchie.|  
|*LevelMembers*|Das Ziel der Aktion sind die Elemente einer Ebene.|  
|*AttributeMembers*|Das Ziel der Aktion sind die Elemente eines Attributs.|  
  
 Die Enumeration, die den zulässigen Werten für entspricht **TargetType** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ActionTargetType>.  
  
 Das Element, das das übergeordnete Element des entspricht **TargetType** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
