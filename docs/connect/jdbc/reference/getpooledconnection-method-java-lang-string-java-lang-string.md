---
title: GetPooledConnection-Methode (java.lang.String, java.lang.String) | Microsoft Docs
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
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c62f975b9d9176941906f3ab8b5e5d7d241d14ff
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getpooledconnection-method-javalangstring-javalangstring"></a>getPooledConnection-Methode (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt eine physische Datenbankverbindung her, die auf Grundlage des angegebenen Benutzernamens und Kennworts als Poolverbindung verwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.sql.PooledConnection getPooledConnection(java.lang.String user,  
                                                      java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Benutzer*  
  
 Ein **Zeichenfolge** , die den Benutzernamen enthält.  
  
 *passwword*  
  
 Ein **Zeichenfolge** , die das Kennwort enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese GetPooledConnection-Methode wird von der GetPooledConnection-Methode in der javax.sql.ConnectionPoolDataSource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource-Methoden](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource-Elemente](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource-Klasse](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

