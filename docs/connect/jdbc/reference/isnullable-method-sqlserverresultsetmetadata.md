---
title: IsNullable-Methode (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.isNullable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c0fce3fe-5b16-4f60-9b0e-e9b30a90525e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e9db7f5fcc66d52b5942e2e30d0288745d6ae17
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="isnullable-method-sqlserverresultsetmetadata"></a>isNullable-Methode (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die NULL-Zulässigkeit von Werten in der angegebenen Spalte an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int isNullable(int column)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Spalte*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn die Spalte null zulässig ist. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese IsNullable-Methode wird von der IsNullable-Methode in der java.sql.ResultSetMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSetMetaData-Methoden](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData-Elemente](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData-Klasse](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

