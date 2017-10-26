---
title: ValueOf-Methode (java.sql.Timestamp, Int) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5bd8228a590f165b9df5df8dcc76798dea81e43
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
  

