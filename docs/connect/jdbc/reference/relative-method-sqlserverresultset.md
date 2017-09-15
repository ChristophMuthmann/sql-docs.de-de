---
title: relative-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36db05ec89818195c4b710591f1d0db71e091fe0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="relative-method-sqlserverresultset"></a>relative-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Verschiebt dem Cursor der angegebenen Anzahl von Zeilen, relativ zur aktuellen Zeile entweder in einer positiven oder negativen Richtung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>Parameter  
 *nRows*  
  
 Ein **Int** , der die Anzahl der zu verschiebenden Zeilen angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn der Cursor in einer Zeile befindet. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese relative-Methode wird von der relativen-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Wenn versucht wird, den Cursor über die erste oder letzte Zeile im Resultset hinaus zu verschieben, wird er vor oder hinter der ersten bzw. letzten Reihe positioniert. Aufrufen von `relative(0)` gültig ist, ändert jedoch nicht der Cursorposition eingefügt.  
  
 Aufrufen der Methode `relative(1)` entspricht dem Aufruf der [Weiter](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) Methode. Aufrufen der Methode `relative(-1)` entspricht dem Aufruf der [vorherigen](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
