---
title: SetTransactionIsolation-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6a8fa4d3-5237-40f8-8a02-b40a3d7a1131
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b91e33388706cabe7436259193f9b2c0bb446b25
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="settransactionisolation-method-sqlserverconnection"></a>SetTransactionIsolation-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  So ändern Sie die Transaktionsisolationsstufe für dieses versucht [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) mit dem angegebenen Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setTransactionIsolation(int level)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Ebene*  
  
 Ein **Int** Wert, der einen der folgenden Isolationsstufen enthält:  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetTransactionIsolation-Methode wird von der SetTransactionIsolation-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Für Transaktionen wird kein Commit ausgeführt, wenn diese Methode während einer Transaktion aufgerufen wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

