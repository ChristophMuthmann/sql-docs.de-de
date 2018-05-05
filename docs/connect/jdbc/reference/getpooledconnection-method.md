---
title: GetPooledConnection-Methode () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aad6c325-3398-462c-aa6e-201dc89fa5ef
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7f70e710b03e0af9e91001da20afc97c3d839d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getpooledconnection-method-"></a>getPooledConnection-Methode ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt eine physische Datenbankverbindung her, die als Poolverbindung verwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.sql.PooledConnection getPooledConnection()  
```  
  
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
  
  
