---
title: UpdateTimestamp-Methode (Int, java.sql.Timestamp) | Microsoft Docs
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
- SQLServerResultSet.updateTimestamp (int, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db83d9d7-137b-4a28-a2ca-d4782e0a256e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f73e665c3c9d5b072f8505e3fe7e7386cd188713
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatetimestamp-method-int-javasqltimestamp"></a>updateTimestamp-Methode (int, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte unter Berücksichtigung des Spaltenindexes mit einem Zeitstempelwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateTimestamp(int index,  
                            java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Index*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *x*  
  
 Ein Zeitstempelwert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateTimestamp-Methode wird von der UpdateTimestamp-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateTimestamp-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

