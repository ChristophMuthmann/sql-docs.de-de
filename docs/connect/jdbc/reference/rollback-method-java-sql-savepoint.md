---
title: Rollback-Methode (java.sql.Savepoint) | Microsoft Docs
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
- SQLServerConnection.rollback (java.sql.Savepoint)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d5dbd9ef-194f-4130-bfcc-7901a4fa8ded
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b774454bdd981decb1a2f40be43550b2bdd3272
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rollback-method-javasqlsavepoint"></a>rollback-Methode (java.sql.Savepoint)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Macht alle Änderungen, die nach der angegebenen [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) Objekt festgelegt wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void rollback(java.sql.Savepoint s)  
```  
  
#### <a name="parameters"></a>Parameter  
 *s*  
  
 Das Rollback zum Sicherungspunkt-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese RollBack-Methode wird von der RollBack-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die Methode sollte nur bei deaktiviertem Modus für automatische Commits verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Rollback-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

