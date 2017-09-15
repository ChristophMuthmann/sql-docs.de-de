---
title: Next-Methode (SQLServerResultSet) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5fe62919bd765d83e2d3a38a9cdda33d88312e29
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="next-method-sqlserverresultset"></a>Next-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Versetzt den Cursor von seiner aktuellen Position aus um eine Zeile nach unten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn die neue parallelitätszeile gültig ist. **"false"** Wenn keine Zeilen mehr zur Bearbeitung vorhanden sind.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese next-Methode wird von der nächsten Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Ein Resultsetcursor wird anfänglich vor dieser Zeile positioniert. Der erste Aufruf der next-Methode wird die erste Zeile der aktuellen Zeile, beim zweiten Aufruf wird die zweite Zeile zur aktuellen Zeile, und so weiter.  
  
 Wenn ein Eingabedatenstrom geöffnet ist, für die aktuelle Zeile ist, wird es von ein Aufruf der next-Methode implizit geschlossen. Eine warnkette für die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt wird gelöscht, wenn eine neue Zeile gelesen wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
