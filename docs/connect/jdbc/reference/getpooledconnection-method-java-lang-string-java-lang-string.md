---
title: GetPooledConnection-Methode (java.lang.String, java.lang.String) | Microsoft Docs
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
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60c232f9ec1d31cf935dbbf2f093c8b488bfb4d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
 *user*  
  
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
  
  
