---
title: SetBytes-Methode (SQLServerPreparedStatement) | Microsoft Docs
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
- SQLServerPreparedStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 52e99ef9-b786-4a14-bfc5-4162e46aafbb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 909e36d5eb80b2642c7d68fff7d28c625045c283
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setbytes-method-sqlserverpreparedstatement"></a>SetBytes-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter auf das angegebene Bytearray fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setBytes(int n,  
                           byte[] x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *n*  
  
 Ein **Int** , der die Parameteranzahl angibt.  
  
 *x*  
  
 Ein Array von Bytes.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetBytes-Methode wird von der SetBytes-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

