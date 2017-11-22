---
title: GetMetaData-Methode (SQLServerPreparedStatement) | Microsoft Docs
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
apiname: SQLServerPreparedStatement.getMetaData
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 5ed49a53-ed61-4e95-ad67-45957aaabb6a
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4323ba40cc85e7f12a1dfcd7604959fe620a3456
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getmetadata-method-sqlserverpreparedstatement"></a>GetMetaData-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine [SQLServerResultSetMetaData-Klasse](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) Objekt, das Informationen zu den Spalten der enthält die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das beim zurückgegeben wird dies [ SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Objekt ausgeführt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final java.sql.ResultSetMetaData getMetaData()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein ResultSetMetaData-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetMetaData-Methode wird von der GetMetaData-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
