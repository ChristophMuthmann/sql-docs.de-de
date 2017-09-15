---
title: GetObjectInstance-Methode (SQLServerDataSourceObjectFactory) | Microsoft Docs
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
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d560f49aeb499c304028b3f2b317b2cb790faaa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
 *c*  
  
 Der Kontext relativ zum angegebenen Namen.  
  
 *h*  
  
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
  
  
