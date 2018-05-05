---
title: ValueOf-Methode (java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e75ea9ae6b98041d2f79d2a8a0c515ed1b05b2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf-Methode (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine **"DateTimeOffset"** Objekt, einen Zeitpunkt in einem bestimmten Offset von GMT erhält ein java.sql.Timestamp-Wert und ein java.util.Calendar-Wert, der angibt, der des Offsets darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>Parameter  
 *timestamp*  
  
 Einjava.sql.Timestamp-Wert.  
  
 *Kalender*  
  
 Der Offsetwert.  Die Komponenten für Datum und Uhrzeit der *Kalender* wird entsprechend festgelegt werden die *Zeitstempel* Wert.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt ein "DateTimeOffset"-Objekt, die den Punkt in Ablaufzeitpunkt von der java.sql.Timestamp-Objekt, auf die Zeitzone für den angegebenen java.util.Calendar-Objekt darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode legt auch die java.util.Calendar-Objekt zu dem Punkt in Ablaufzeitpunkt vom java.sql.Timestamp-Objekt fest.  
  
## <a name="see-also"></a>Siehe auch  
 ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset-Elemente](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
