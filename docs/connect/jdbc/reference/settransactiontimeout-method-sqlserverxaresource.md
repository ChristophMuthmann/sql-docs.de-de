---
title: SetTransactionTimeout-Methode (SQLServerXAResource) | Microsoft Docs
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
- SQLServerXAResource.setTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38bf4a1a-6ad3-437c-b9ed-8792ab6dde7e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d2bcc25cfb09d40df95029f0c9d36e38e9658725
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>setTransactionTimeout-Methode (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt die aktuelle Transaktion Timeout-Wert für diesen [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Sekunden*  
  
 Ein **Int** Wert.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn das Timeout festgelegt wurde. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetTransactionTimeout-Methode wird von der SetTransactionTimeout-Methode in der javax.transaction.xa.XAResource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Methoden](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource-Elemente](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource-Klasse](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  

