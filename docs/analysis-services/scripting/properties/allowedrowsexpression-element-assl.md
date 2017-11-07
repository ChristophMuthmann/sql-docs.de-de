---
title: AllowedRowsExpression-Element (ASSL) | Microsoft Docs
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cf9c12f586ff7ffab5f627f049748d1f44eb9428
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression-Element (ASSL)
  Enthält einen DAX-Ausdruck (Data Analysis Expression) des booleschen Typs, der den Inhalt des übergeordneten Elements definiert.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Für die **CellPermission** Element, das **Ausdruck** Element enthält einen logischen MDX-Ausdruck, der Zellen, die auf den angegebenen Rechte anwendbar identifiziert die [Zugriff](../../../analysis-services/scripting/properties/access-element-assl.md) Element von der **CellPermission** Element. Wenn der Wert eines **Expression** -Elements für ein **CellPermission** -Element leer ist, wird das **CellPermission** -Element ignoriert.  
  
 Beim Element **StandardAction** enthält das **Expression** -Element einen MDX-Ausdruck, der für die Inhalte der Aktion steht. Wenn der Wert eines **Expression** -Elements für ein **StandardAction** -Element leer ist, wird das **StandardAction** -Element ignoriert.  
  
 Die Elemente, die den übergeordneten Elementen im AMO-Objektmodell (Analysis Management Objects) entsprechen, sind <xref:Microsoft.AnalysisServices.CellPermission> und <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

