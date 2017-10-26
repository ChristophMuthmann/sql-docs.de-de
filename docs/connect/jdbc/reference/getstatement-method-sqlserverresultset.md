---
title: GetStatement-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dea981b-b4fd-4f8d-954f-e686124627e2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 129fcea59f7ff9555203fe7ced9b51fabade1d83
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getstatement-method-sqlserverresultset"></a>GetStatement-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das Dies erzeugt [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Statement getStatement()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein SQLServerStatement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetStatement-Methode wird von der GetStatement-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Wenn das Resultset auf andere Weise, wie z. B. von generiert wurde eine [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Methode, diese Methode gibt null zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

