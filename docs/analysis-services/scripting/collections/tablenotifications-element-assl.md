---
title: TableNotifications-Element (ASSL) | Microsoft Docs
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
apiname: TableNotifications Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: TableNotifications element
ms.assetid: 4cecdfea-0d4d-4bd6-bbb3-4d0d2284c665
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2421bf88e811264c60fcf181ebe75474563a0963
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tablenotifications-element-assl"></a>TableNotifications-Element (ASSL)
  Enthält die Auflistung der [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md) Elemente, die Anmeldeinformationen für die [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) Element zu Tabellen oder Sichten in einer Datenquelle, die geändert wurden.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <TableNotifications>  
      <TableNotification>...</TableNotification>  
...</TableNotifications>  
</ProactiveCachingTablesBinding>  
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
|Übergeordnete Elemente|[ProactiveCachingTablesBinding](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)|  
|Untergeordnete Elemente|[TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.TableNotificationCollection>.  
  
## <a name="see-also"></a>Siehe auch  
 [ProactiveCachingBinding-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)   
 [ProactiveCachingObjectNotificationBinding-Datentyp &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)   
 [Schemaauflistungen &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
