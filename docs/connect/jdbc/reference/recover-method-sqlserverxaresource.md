---
title: recover-Methode (SQLServerXAResource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerXAResource.recover
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 73f341196b8dd86a098031afc8c556ceb7f26a2c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="recover-method-sqlserverxaresource"></a>recover-Methode (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Liste vorbereiteter Transaktionszweige von einem Ressourcen-Manager ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Flags*  
  
 Ein **Int** Wert, der einen der folgenden Werte annehmen kann: XAResource.TMSTARTRSCAN oder XAResource.TMENDRSCAN oder XAResource.TMNOFLAGS oder XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Xid-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode für die Wiederherstellung wird von der Methode "Wiederherstellen" in der javax.transaction.xa.XAResource-Schnittstelle angegeben.  
  
 Wenn der Parameter **Flag** ist kein XAResource.TMSTARTRSCAN oder XAResource.TMSTARTRSCAN | XAResource.TMENDRSCAN, muss eine Überprüfung der Wiederherstellung in Bearbeitung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Methoden](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource-Elemente](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource-Klasse](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
