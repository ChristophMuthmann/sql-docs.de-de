---
title: RequiresRestart-Element (ASSL) | Microsoft Docs
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
apiname: RequiresRestart Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RequiresRestart
helpviewer_keywords: RequiresRestart element
ms.assetid: 9e98f956-c41e-4e15-a7bd-e17c10ee6fc6
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 12998cda4f9ce55d99b427c0aca07b93f5ba82ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="requiresrestart-element-assl"></a>RequiresRestart-Element (ASSL)
  Enthält einen schreibgeschützten Wert, der zugeordnet einer [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) Element, das bestimmt, ob die Änderung des Werts der Servereigenschaft erfordert, dass die Instanz neu gestartet werden, damit die Änderung wirksam wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ServerProperty>  
   ...  
   <RequiresRestart>...</RequiresRestart>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das Element, das das übergeordnete Element des entspricht **RequiresRestart** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Siehe auch  
 [ServerProperties-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
