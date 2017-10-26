---
title: GetXAResource-Methode (SQLServerXAConnection) | Microsoft Docs
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
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 78999ece74ad80f7d4ce107484d225cc1ab6f4f6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource-Methode (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Objekt, mit der Transaktions-Manager verwendet wird, um dieses Problem [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) objektspezifischen Teilnahme an einer verteilten Transaktion.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein XAResource-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese GetXAResource-Methode wird von der GetXAResource-Methode in der javax.sql.XAConnection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAConnection-Methoden](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection-Elemente](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection-Klasse](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  

