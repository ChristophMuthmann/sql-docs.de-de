---
title: GetObjectInstance-Methode (SQLServerDataSourceObjectFactory) | Microsoft Docs
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
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6140d267d0baff6334072fd7a55ce7b03e56312
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>getObjectInstance-Methode (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Instanz des angegebenen Datenquellenobjekts ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>Parameter  
 *ref*  
  
 Ein **Objekt** Wert.  
  
 *name*  
  
 Der Name des Objekts.  
  
 *C*  
  
 Der Kontext relativ zum angegebenen Namen.  
  
 *H*  
  
 Die Umgebung, die beim Erstellen des Objekts verwendet wird.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Objekt** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese GetObjectInstance-Methode wird von der GetObjectInstance-Methode in der javax.naming.spi.ObjectFactory-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Sqlserverdatasourceobjectfactory-Elemente](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory-Elemente](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory-Klasse](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
