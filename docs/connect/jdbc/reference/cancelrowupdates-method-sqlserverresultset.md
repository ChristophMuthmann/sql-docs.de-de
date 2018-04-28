---
title: CancelRowUpdates-Methode (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 23253bf357797540e014996c555ac9d1172093e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>CancelRowUpdates-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Bricht die Aktualisierungen an der aktuellen Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese CancelRowUpdates-Methode wird von der CancelRowUpdates-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode kann aufgerufen werden, nach dem Aufruf einer Aktualisierungsmethode und vor dem Aufruf der [UpdateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) Methode, um die Updates ein Rollback auszuführen, die an einer Zeile vorgenommen wurden. Wenn keine Updates vorgenommen wurden, oder UpdateRow bereits aufgerufen wurde, hat diese Methode keine Auswirkung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
