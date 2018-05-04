---
title: Next-Methode (SQLServerResultSet) | Microsoft Docs
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
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d3a94b1ba58b88fdf2552980e70b9b0bfb135ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
