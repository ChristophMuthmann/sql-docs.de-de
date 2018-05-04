---
title: AddConnectionEventListener-Methode (SQLServerPooledConnection) | Microsoft Docs
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
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6482521780045b1d5f0482731c1b6f8e2f5f3571
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>addConnectionEventListener-Methode (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registriert den angegebenen Ereignislistener, damit dieser benachrichtigt wird, beim Auftreten eines Ereignisses für dieses [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Listener*  
  
 Ein ConnectionEventListener-Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Diese AddConnectionEventListener-Methode wird von der AddConnectionEventListener-Methode in der javax.sql.PooledConnection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPooledConnection-Methoden](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection-Elemente](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection-Klasse](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
