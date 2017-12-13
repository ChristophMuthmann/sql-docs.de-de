---
title: DimensionPermission-Element (ASSL) | Microsoft Docs
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
apiname: DimensionPermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DimensionPermission
helpviewer_keywords: DimensionPermission element
ms.assetid: e06efbda-64fd-4dca-a2b5-c8ffbf21512c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a3a38dfd173d886d299211ee45dd20ea486c0ce1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="dimensionpermission-element-assl"></a>DimensionPermission-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Definiert die Berechtigungen, die zu einem bestimmten gehören [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) -Element für eine spezifische Datenbank- oder Cubedimension.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionPermissions>  
   <DimensionPermission xsi:type="DimensionPermission">...</DimensionPermission> <!-- ancestor: Dimension -->  
   <!-- or -->  
   <DimensionPermission xsi:type="CubeDimensionPermission">...</DimensionPermission> <!-- ancestor: CubePermission -->  
</DimensionPermissions>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Im folgenden sind die gültigen übergeordneten (oder einen Vorgänger): Datentyp Paare:<br /><br /> [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md):[DimensionPermission](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md)<br /><br /> [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md):<br />                        [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das einmal oder mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Die entsprechenden Elemente im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.DimensionPermission> und <xref:Microsoft.AnalysisServices.CubeDimensionPermission>.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
