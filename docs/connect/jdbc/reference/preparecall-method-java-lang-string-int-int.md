---
title: PrepareCall-Methode (java.lang.String, Int, Int) | Microsoft Docs
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
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06e2dd2ed6da9d593a62f72d825c90abca256a88
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall-Methode (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Objekt, generiert [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte mit dem angegebenen Typ und der Parallelität.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameter  
 *SQL*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
 *resultSetType*  
  
 Ein **Int** , der den Typ des Resultsets angibt.  
  
 *resultSetConcurrency*  
  
 Ein **Int** , der das Resultset-Parallelitätstyp angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein CallableStatement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese PrepareCall-Methode wird von der PrepareCall-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [PrepareCall-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

