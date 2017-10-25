---
title: absolute-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c952c24cfab1a36715d98cf0aad6caad7212a601
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="absolute-method-sqlserverresultset"></a>absolute-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Verschiebt den Cursor in die vorhandene Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Zeile*  
  
 Ein **Int** , die angibt, dass der Nummer der Zeile zu verschieben. Kann positiv, negativ oder "0" sein.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn der Cursor an die angegebene Position verschoben wird. **"false"** vor der ersten Zeile oder hinter die letzte Zeile ist.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Dieser absolute-Methode wird von der absolute-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

