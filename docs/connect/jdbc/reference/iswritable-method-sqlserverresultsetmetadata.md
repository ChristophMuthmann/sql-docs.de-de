---
title: IsWritable-Methode (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.isWritable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 50846aa8-e4e5-4fc3-a638-0e5fa8b597be
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1b9ac44e7ddfe0cc09edc3cfa207780d1265aef4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="iswritable-method-sqlserverresultsetmetadata"></a>isWritable-Methode (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob ein Schreibvorgang in der angegebenen Spalte möglich ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean isWritable(int column)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Spalte*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** wenn Schreibvorgänge in der Spalte erfolgreich sein werden. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese IsWritable-Methode wird von der IsWritable-Methode in der java.sql.ResultSetMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSetMetaData-Methoden](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData-Elemente](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData-Klasse](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

