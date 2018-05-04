---
title: GetConcurrency-Methode (SQLServerResultSet) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38a9bf912c0a967a29c8a6ff3543418d1c29b957
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getconcurrency-method-sqlserverresultset"></a>GetConcurrency-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Parallelitätsmodus dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , die angibt, dass der Parallelitätstyp, die der folgenden Werte sind möglich:  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetConcurrency-Methode wird von der GetConcurrency-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Die verwendete Parallelität richtet sich nach der [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das Resultset erstellt.  
  
 Diese Methode kann zur Bestimmung der eigentlichen Parallelität verwendet werden. Wurde von der Anwendung "CONCUR_READ_ONLY" oder "CONCUR_UPDATABLE" ausgewählt, werden diese Elemente zurückgegeben. Wurde von der Anwendung die Standardparallelität verwendet, wird "CONCUR_READ_ONLY" zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
