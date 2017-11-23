---
title: ValueOf-Methode (java.sql.Timestamp, Int) | Microsoft Docs
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
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c79a5f486377bc86264377a898a9f908bbc7153
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf-Methode (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine **"DateTimeOffset"** Objekt, einen Zeitpunkt in einem bestimmten Offset von GMT erhält ein java.sql.Timestamp-Wert und einen Wert, der angibt, der des Offsets in Minuten darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parameter  
 *timestamp*  
  
 Einjava.sql.Timestamp-Wert.  
  
 *minutesOffset*  
  
 Das Offset in Minuten.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt ein "DateTimeOffset"-Objekt, das den Zeitpunkt gegebenen Zeitpunkt vom java.sql.Timestamp-Objekt am angegebenen Offset in Minuten von GMT darstellt.  
  
## <a name="see-also"></a>Siehe auch  
 ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset-Elemente](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
