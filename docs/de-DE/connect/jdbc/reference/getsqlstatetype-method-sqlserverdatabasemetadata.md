---
title: GetSQLStateType-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aa0243e8b990783bfca96b769d4011cc6611f7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob "SQLSTATE" (zurückgegeben von der SQLException.getSQLState-Methode) den Wert "X/Open" (jetzt "Open Group"), "SQL CLI", "SQL99" (JDBC 3.0) oder "SQL:2003" (JDBC 4.0) besitzt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , die gibt den Typ des SQLSTATE, die der folgenden Werte sind möglich:  
  
-   Für Java-Laufzeitumgebung Version 5.0: Wenn die **XopenStates** Connection-Eigenschaft wird festgelegt, um **"true"**, DatabaseMetaData.sqlStateXOpen Methodenrückgabe. Andernfalls DatabaseMetaData.sqlStateSQL99.  
  
-   Für Java-Laufzeitumgebung Version 6.0: Wenn die **XopenStates** Connection-Eigenschaft wird festgelegt, um **"true"**, DatabaseMetaData.sqlStateXOpen Methodenrückgabe. Andernfalls DatabaseMetaData.sqlStateSQL.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetSQLStateType-Methode wird von der GetSQLStateType-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
