---
title: ExecuteBatch-Methode (SQLServerPreparedStatement) | Microsoft Docs
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
apiname: SQLServerPreparedStatement.executeBatch
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a459eef327f162e362cf5f86fbba1c2a726e78af
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>executeBatch-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Übermittelt einen Befehlsbatch zur Ausführung an die Datenbank. Werden alle Befehle erfolgreich ausgeführt, wird ein Array mit Updatezählungen zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Array aus int-Elementen, das die Updatezählungen enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Hinweise  
 Diese ExecuteBatch-Methode wird von der ExecuteBatch-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 ist kompatibel mit der JDBC 4.0-Empfehlung, dass ein Aufruf der CallableStatement.executeBatch-Methode (geerbt von PreparedStatement) eine BatchUpdateException ausgelöst wird, wenn die gespeicherte Prozedur OUT oder INOUT akzeptiert. Parameter oder gibt etwas anderes als eine updatezählung.  
  
 Diese Methode überschreibt [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
