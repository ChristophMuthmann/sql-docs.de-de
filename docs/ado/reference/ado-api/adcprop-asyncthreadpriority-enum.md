---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf0f8e2f68eccceecbbe7fe3b2c17039b55d2887
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Für eine RDS [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt, gibt die Ausführungspriorität des asynchronen Threads, die Daten abruft.  
  
 Verwenden Sie diese Konstanten mit der **Recordset** "**Background Thread Priorität**" dynamische Eigenschaft, die im Index ADO, OLE DB-dynamische Eigenschaft verwiesen wird und die dokumentiert, die der [ Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) Dokumentation.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Legt die Priorität zwischen normalen und höchsten fest.|  
|**adPriorityBelowNormal**|2|Legt die Priorität zwischen dem niedrigsten und "normal" fest.|  
|**adPriorityHighest**|5|Legt die Priorität auf die höchstmögliche fest.|  
|**AdPriorityLowest**|1|Legt die Priorität auf den niedrigsten fest.|  
|**adPriorityNormal**|3|Legt die Priorität auf Normal fest.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|

