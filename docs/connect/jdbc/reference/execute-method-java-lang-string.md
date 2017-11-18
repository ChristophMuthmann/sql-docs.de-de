---
title: Execute-Methode (java.lang.String) | Microsoft Docs
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
- SQLServerPreparedStatement.execute (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a871917e-d286-46c3-96cf-2e8e8b22111c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 219d4ff6ff793b244e30ca43582f4d194e7e6a5d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring"></a>execute-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Führt die angegebene SQL-Anweisung aus. Hierbei können mehrere Ergebnisse zurückgegeben werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parameter  
 *SQL*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** Wenn die Anweisung ein Resultset zurückgibt. **"false"** Wenn eine updatezählung oder kein Ergebnis zurückgegeben.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Execute-Methode wird von der Execute-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Diese Methode überschreibt die [ausführen](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) -Methode, die im gefunden wird die [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse.  
  
 Beim Aufrufen dieser Methode führt eine Ausnahme ausgelöst, da die SQL-Anweisung für die SQLServerPreparedStatement-Objekt angegeben wird, wenn das Objekt erstellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Execute-Methode &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

