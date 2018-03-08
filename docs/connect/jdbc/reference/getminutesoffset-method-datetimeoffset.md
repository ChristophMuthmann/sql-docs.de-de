---
title: GetMinutesOffset-Methode (DateTimeOffset) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9adb82758a3833da60e22c55b61274a255f0a5cc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset-Methode (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt den Offset in Minuten von GMT dieses "DateTimeOffset"-Objekts an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Das Offset in Minuten.  
  
## <a name="remarks"></a>Hinweise  
 Für eine "DateTimeOffset"-Objekts darstellt 8. März 2010 11:35:48-0800, GetMinutesOffset gibt den Wert 480 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset-Elemente](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
