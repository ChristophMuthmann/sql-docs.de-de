---
title: PrepareStatement-Methode (java.lang.String, Int, Int) | Microsoft Docs
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
- SQLServerConnection.prepareStatement (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5bb96dbe-f673-41b5-911b-8f661cca071a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2ccee816190b9589e3bec02057efc32f7493abf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="preparestatement-method-javalangstring-int-int"></a>prepareStatement-Methode (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -Objekt, generiert [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte mit dem angegebenen Typ und der Parallelität.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sSql,  
                                                   int resultSetType,  
                                                   int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sSql*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
 *ResultSetType*  
  
 Ein **Int** , der den Typ des Resultsets angibt.  
  
 *resultSetConcurrency*  
  
 Ein **Int** , der das Resultset-Parallelitätstyp angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein PreparedStatement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese PrepareStatement-Methode wird von der PrepareStatement-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Methoden](../../../connect/jdbc/reference/sqlserverconnection-methods.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
