---
title: QueryNotifications-Element (ASSL) | Microsoft Docs
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
apiname: QueryNotifications Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: QueryNotifications element
ms.assetid: 0e7e951f-c8b9-4492-bb01-e4b5d16edde6
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 47c6e735cb0485c488ba136c8a3afcc3d274529d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="querynotifications-element-assl"></a>QueryNotifications-Element (ASSL)
  Enthält die Auflistung der [QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md) Elemente, die Informationen zum Bereitstellen der [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) -Element zu Abfragen ausführen, um zu bestimmen, ob eine Datenquelle geändert wurde.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   ...  
   <QueryNotifications>  
      <QueryNotification>...</QueryNotification>  
...</QueryNotifications>  
   ...  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[ProactiveCachingQueryBinding](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|  
|Untergeordnete Elemente|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.QueryNotificationCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
