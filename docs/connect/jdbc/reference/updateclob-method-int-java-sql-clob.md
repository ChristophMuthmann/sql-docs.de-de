---
title: UpdateClob-Methode (Int, java.sql.Clob) | Microsoft Docs
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
- SQLServerResultSet.updateClob (int, java.sql.Clob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2a5e9cb-2631-4f6e-a90c-4bee58e2f7b8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 312a1007daf8298998f667d2832d0c5ccbd91710
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updateclob-method-int-javasqlclob"></a>updateClob-Methode (int, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte unter Berücksichtigung des Spaltenindex mit einem java.sql.Clob-Wert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateClob(int columnIndex,  
                       java.sql.Clob clobValue)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *clobValue*  
  
 Ein Clob-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateClob-Methode wird von der UpdateClob-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateClob-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

