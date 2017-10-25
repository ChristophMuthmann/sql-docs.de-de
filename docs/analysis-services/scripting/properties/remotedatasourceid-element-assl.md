---
title: RemoteDatasourceID-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RemoteDatasourceID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RemoteDatasourceID
helpviewer_keywords:
- RemoteDatasourceID element
ms.assetid: 2eaf0b9c-8c2d-4dc6-9bad-1db70a4b04b1
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eade7b321c47c5add6a5302f5c015ed6484c2b5f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="remotedatasourceid-element-assl"></a>RemoteDatasourceID-Element (ASSL)
  Gibt den Bezeichner (ID) der OLAP-Datenquelle, die auf der Instanz von verweist [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , die die Remotepartition gespeichert.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Partition>  
      ...  
   <RemoteDatasourceID>...</RemoteDatasourceID>  
   ...  
</Partition>  
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
|Übergeordnetes Element|[Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Wenn **RemoteDatasourceID** NULL ist, dann ist die Partition lokal.  
  
 Das Element, das das übergeordnete Element des entspricht **RemoteDatasourceID** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

