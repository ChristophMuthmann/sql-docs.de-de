---
title: CubePermission-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CubePermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubePermission
helpviewer_keywords: CubePermission element
ms.assetid: b144b623-ff20-4ead-91ad-4c718f3b140b
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cc020c7976f795d0d734323eab3892398167b3c5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="cubepermission-element-assl"></a>CubePermission-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert die Berechtigungen der Elemente eines bestimmten [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element in einer bestimmten [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CubePermissions>  
   <CubePermission>  
      <!-- The following elements extend Permission -->  
      <ReadSourceData>...</ReadSourceData>  
            <DimensionPermissions>...</DimensionPermissions>  
            <CellPermissions>...</CellPermissions>  
   </CubePermission>  
</CubePermissions>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|[Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-n: Optionales Element, das einmal oder mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[CubePermissions](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)|  
|Untergeordnete Elemente|[CellPermissions](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md), [DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md), [ReadSourceData](../../../analysis-services/scripting/properties/readsourcedata-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.CubePermission>.  
  
## <a name="see-also"></a>Siehe auch  
 [Cube-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
