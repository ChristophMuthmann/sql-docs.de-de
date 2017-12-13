---
title: Expression-Element (ASSL) | Microsoft Docs
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
apiname: Expression Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Expression
helpviewer_keywords: Expression element
ms.assetid: a9491b21-5279-4531-b6a5-9e8022060dd8
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 169567bda91aeb759fcf77e54726422992e6a032
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="expression-element-assl"></a>Expression-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Enthält einen Multidimensional Expressions (MDX)-Ausdruck, der den Inhalt des übergeordneten Elements definiert.  
  
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
  
  
