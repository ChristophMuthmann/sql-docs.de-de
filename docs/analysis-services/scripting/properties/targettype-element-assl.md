---
title: TargetType-Element (ASSL) | Microsoft Docs
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
- TargetType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49c2fd13925130bfb76730708775f6bb0d5e79ca
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="targettype-element-assl"></a>TargetType-Element (ASSL)
  Identifiziert den Elementtyp des Elements identifiziert, der [Ziel](../../../analysis-services/scripting/properties/target-element-assl.md) Element.  
  
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
  
  
