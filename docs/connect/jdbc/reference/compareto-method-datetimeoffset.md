---
title: CompareTo-Methode (DateTimeOffset) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dfeede84cca769756d6408871924a384cd023edb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="compareto-method-datetimeoffset"></a>compareTo-Methode (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Vergleicht dieses **"DateTimeOffset"** Objekt in eine andere **"DateTimeOffset"** Objekt basierend auf der Uhrzeit nach GMT.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parameter  
 Ein ["DateTimeOffset"](../../../connect/jdbc/reference/datetimeoffset-class.md) Wert, der mit der aktuellen Instanz verglichen werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
 In der folgenden Tabelle wird der Rückgabewert für diese Methode beschrieben:  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|Beide **"DateTimeOffset"** -Objekte denselben Zeitpunkt darstellen.|  
|Negative Zahl|Dies **"DateTimeOffset"** Objekt stellt einen Punkt dar, zeitlich vor *andere*.|  
|Positive Zahl|Dies **"DateTimeOffset"** Objekt stellt einen Punkt dar, zeitlich nach *andere*.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn zwei **"DateTimeOffset"** Objekte gleichzeitig nach GMT haben, es gibt keine zusätzlichen Reihenfolge der Objekte basierend auf den Offset.  
  
## <a name="see-also"></a>Siehe auch  
 ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset-Elemente](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
