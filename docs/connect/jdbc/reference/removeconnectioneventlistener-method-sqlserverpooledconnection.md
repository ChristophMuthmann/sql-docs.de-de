---
title: RemoveConnectionEventListener-Methode (SQLServerPooledConnection) | Microsoft Docs
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
- SQLServerPooledConnection.removeConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 46902e89-f512-40af-a2d9-a896f03d1200
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2547e45f5fd02f81d0cb2e285d58ce6e4f8fa26c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="removeconnectioneventlistener-method-sqlserverpooledconnection"></a>removeConnectionEventListener-Methode (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Entfernt den vorhandenen Ereignislistener.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void removeConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Listener*  
  
 Ein ConnectionEventListener-Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Diese RemoveConnectionEventListener-Methode wird von der RemoveConnectionEventListener-Methode in der javax.sql.PooledConnection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPooledConnection-Methoden](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection-Elemente](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection-Klasse](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
