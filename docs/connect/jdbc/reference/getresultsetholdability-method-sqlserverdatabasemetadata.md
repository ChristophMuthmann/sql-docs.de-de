---
title: GetResultSetHoldability-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData,getResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0bd6283-83ab-4a0a-b825-ec4cdccf03e1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 55939de8fdf5a48441ae67fc4e85b77b164ac725
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getresultsetholdability-method-sqlserverdatabasemetadata"></a>getResultSetHoldability-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die Standardhaltbarkeit von Resultsets für diese Datenbank ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getResultSetHoldability()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , der die standardhaltbarkeit angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetResultSetHoldability-Methode wird von der GetResultSetHoldability-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank dieser Methoden gibt 1 zurück, entspricht der Hold_cursors_over_commit-Konstanten.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

