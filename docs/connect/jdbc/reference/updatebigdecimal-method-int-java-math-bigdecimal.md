---
title: UpdateBigDecimal-Methode (Int, java.math.BigDecimal) | Microsoft Docs
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
- SQLServerResultSet.updateBigDecimal (int, java.math.BigDecimal)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e15de27-a490-45cd-a3a6-a49721f15a97
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b03e18f057f34bb03c91e05048f2b5ee88ad795e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatebigdecimal-method-int-javamathbigdecimal"></a>updateBigDecimal-Methode (int, java.math.BigDecimal)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Berücksichtigung des Spaltenindexes BigDecimal-Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBigDecimal(int index,  
                             java.math.BigDecimal x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Index*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *x*  
  
 Ein BigDecimal-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateBigDecimal-Methode wird von der UpdateBigDecimal-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBigDecimal-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
