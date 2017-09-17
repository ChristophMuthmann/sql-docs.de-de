---
title: Start-Methode (SQLServerXAResource) | Microsoft Docs
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
- SQLServerXAResource.start
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 33c90213-92f7-416b-b2fa-67a1afe64e97
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9cd2cc2d720cc1324b60b685da4c61c3ff4985bb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="start-method-sqlserverxaresource"></a>start-Methode (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Startet die Arbeit für einen transaktionszweig, der im Xid Objekt angegeben ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void start(javax.transaction.xa.Xid xid,  
                  int flags)  
```  
  
#### <a name="parameters"></a>Parameter  
 *XID*  
  
 Ein Xid-Objekt.  
  
 *Flags*  
  
 Ein **Int** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Hinweise  
 Diese Start-Methode wird von der Start-Methode in der javax.transaction.xa.XAResource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Methoden](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource-Elemente](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource-Klasse](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
