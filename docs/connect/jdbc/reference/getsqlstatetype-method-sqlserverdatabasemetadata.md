---
title: GetSQLStateType-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
apiname: SQLServerDatabaseMetaData.getSQLStateType
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dce25152f13c146261da11f03f4d26ba6a134bf1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
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
  
  
