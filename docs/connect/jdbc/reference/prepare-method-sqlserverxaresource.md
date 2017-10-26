---
title: Prepare-Methode (SQLServerXAResource) | Microsoft Docs
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
- SQLServerXAResource.prepare
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f800c966-3fae-41b3-963a-464988f80da3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82f95895d2467f1cc24bf927d2193ef6719256e3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="prepare-method-sqlserverxaresource"></a>prepare-Methode (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fordert an, dass der Ressourcen-Manager für einen Commit der Transaktion der Transaktion, durch das angegebene Objekt der Xid vorzubereiten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int prepare(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>Parameter  
 *XID*  
  
 Ein Xid-Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Hinweise  
 Diese Prepare-Methode wird von der Prepare-Methode in der javax.transaction.xa.XAResource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Methoden](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource-Elemente](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource-Klasse](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  

