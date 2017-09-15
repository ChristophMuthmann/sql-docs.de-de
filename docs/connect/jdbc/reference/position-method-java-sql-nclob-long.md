---
title: Position-Methode (java.sql.NClob, long) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0be71ad3437edf9febc776f83b26953593f294f7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="position-method-javasqlnclob-long"></a>position-Methode (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die Zeichenposition, an dem das angegebene **NClob** Objekt *Searchstr* wird angezeigt, in diesem **NClob** Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parameter  
 *searchstr*  
  
 Ein NClob-Objekt, nach dem gesucht werden soll.  
  
 *Starten*  
  
 Die Position, an der mit der Suche begonnen wird. Die erste Position ist "1".  
  
## <a name="return-value"></a>Rückgabewert  
 Die Position, an der sich die Teilzeichenfolge befindet, oder "-1", wenn sie nicht vorhanden ist. Die erste Position ist "1".  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Position-Methode wird von der Position-Methode in der java.sql.NClob-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Positionieren Sie die Methode &#40; SQLServerNClob &#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob-Methoden](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob-Elemente](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob-Klasse](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
