---
title: IsSigned-Methode (SQLServerResultSetMetaData) | Microsoft Docs
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
apiname: SQLServerResultSetMetaData.isSigned
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 1d16672f-1515-4255-8b20-e7911c999f60
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 015cdf33b8dcf02c9e9d214ff6a6f1acd12e99ba
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="issigned-method-sqlserverresultsetmetadata"></a>isSigned-Methode (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob es sich bei den Werten in der angegebenen Spalte um Zahlen mit Vorzeichen handelt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean isSigned(int column)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Spalte*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn die Spalte signierte Nummern enthält. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese IsSigned-Methode wird von der IsSigned-Methode in der java.sql.ResultSetMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSetMetaData-Methoden](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData-Elemente](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData-Klasse](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
