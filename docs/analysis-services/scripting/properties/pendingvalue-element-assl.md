---
title: PendingValue-Element (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PendingValue Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PendingValue
helpviewer_keywords:
- PendingValue element
ms.assetid: 386b2ec6-3d83-42d2-b83a-83e375fbdcbd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: da8de30241236402174e576eb0c61be7174fbb23
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="pendingvalue-element-assl"></a>PendingValue-Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enthält den schreibgeschützten ausstehenden Wert des zugeordneten [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) -Elements.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ServerProperty>  
   ...  
   <PendingValue>...</PendingValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Jeder simpleType|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnetes Element|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Dieses Element enthält den Wert des der **ServerProperty** , der verwendet wird das nächste Mal von der aktuellen Instanz der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] gestartet wird. Dieser Wert wird in der Regel vom Speicherort des Werts der Servereigenschaft abgerufen: aus einer Initialisierungsdatei, der Windows-Registrierung [!INCLUDE[msCoName](../../../includes/msconame-md.md)] oder einem anderen Speichermechanismus.  
  
 Das Element, das das übergeordnete Element des entspricht **PendingValue** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Siehe auch  
 [ServerProperties-Element & #40; ASSL & #41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Datenbankeigenschaften & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
