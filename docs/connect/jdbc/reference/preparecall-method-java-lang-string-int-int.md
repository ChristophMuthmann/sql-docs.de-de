---
title: PrepareCall-Methode (java.lang.String, Int, Int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b3eb39174f6164d76c4e60eada168987871abc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
 *sql*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
 *ResultSetType*  
  
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
 [PrepareCall-Methode &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
