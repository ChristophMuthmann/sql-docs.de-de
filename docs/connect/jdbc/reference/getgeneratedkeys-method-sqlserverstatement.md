---
title: GetGeneratedKeys-Methode (SQLServerStatement) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getGeneratedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3325950-0e81-4ae8-aa0c-e1f6d371adcd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 224930c0a364158033e0e30ccfe855f8b71579aa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getgeneratedkeys-method-sqlserverstatement"></a>getGeneratedKeys-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft sämtliche automatisch generierte Schlüssel, die aufgrund der Ausführung dieser erstellt werden [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final java.sql.ResultSet getGeneratedKeys()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein ResultSet-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetGeneratedKeys-Methode wird von der GetGeneratedKeys-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Weitere Informationen zur Verwendung dieser Methode finden Sie unter [mithilfe von automatisch generierten Schlüssel](../../../connect/jdbc/using-auto-generated-keys.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

