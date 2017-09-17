---
title: GetMaxRows-Methode (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d9f64d60a08727f239ca3eee4354fc094e06107a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getmaxrows-method-sqlserverstatement"></a>GetMaxRows-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die maximale Anzahl der Zeilen ab, die eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das von diesem erzeugt wird [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt enthalten kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , die die maximale Anzahl von Zeilen, oder 0 gibt an, wenn kein Limit vorhanden ist.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetMaxRows-Methode wird von der GetMaxRows-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Diese GetMaxRows-Methode gibt immer 0 für dynamische, scrollfähige Cursor zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
