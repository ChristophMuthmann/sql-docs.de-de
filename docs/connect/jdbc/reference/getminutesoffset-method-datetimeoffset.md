---
title: GetMinutesOffset-Methode (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ffaf44dae71da5c5f370c25dab87e4d799707dd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
  
  
