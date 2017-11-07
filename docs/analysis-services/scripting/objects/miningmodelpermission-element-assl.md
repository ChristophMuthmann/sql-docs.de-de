---
title: Miningmodelpermission-Element (ASSL) | Microsoft Docs
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
- MiningModelPermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningModelPermission
helpviewer_keywords:
- MiningModelPermission element
ms.assetid: 4bd2f7e7-ff0d-404e-96fb-7e2c4eeb91e9
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2cd366179355590dca84fb84f8a00e8dfc103a3f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="miningmodelpermission-element-assl"></a>MiningModelPermissions-Element (ASSL)
  Definiert die Berechtigungen der Elemente einer [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element besitzen, für ein einzelnes [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningModelPermissions>  
   <MiningModelPermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <AllowBrowsing>...</AllowBrowsing>  
   </MiningModelPermission>  
</MiningModelPermissions>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|[Berechtigung](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|  
|Untergeordnete Elemente|[AllowBrowsing](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md), [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], können Sie Drillthrough für Miningstrukturen aktivieren, durch Hinzufügen der **AllowDrillthrough** Berechtigung für die [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) Auflistung. Wenn **AllowDrillthrough** aktiviert ist, auf die Miningstruktur und das Miningmodell, jedes Mitglied einer Rolle mit [AllowDrillThrough-Element &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) Berechtigungen für das Modell können Datamining-Modell abzufragen und, die nicht im Modell enthalten waren, mithilfe der folgenden Syntax strukturspalten zurückgeben:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Daher sollten Sie zum Schutz sensibler oder persönlicher Informationen die **AllowDrillthrough** -Berechtigung für ein Miningmodell nur zulassen, wenn es unbedingt erforderlich ist. Weitere Informationen finden Sie unter [AllowDrillThrough-Element &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.MiningModelPermission>.  
  
## <a name="see-also"></a>Siehe auch  
 [Objekte &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

