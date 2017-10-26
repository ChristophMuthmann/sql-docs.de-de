---
title: SetNull-Methode (Int, Int, java.lang.String) | Microsoft Docs
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
- SQLServerPreparedStatement.setNull (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43c74e06-2858-49ba-bae7-b88808e5fff4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f52604e2e94c1599ebbe9453789e502aea9e17f5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setnull-method-int-int-javalangstring"></a>setNull-Methode (int, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter unter Berücksichtigung des festzulegenden Parametertyps und -namens auf einen NULL-Wert fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setNull(int paramIndex,  
                          int sqlType,  
                          java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *paramIndex*  
  
 Ein **Int** , der die Parameteranzahl angibt.  
  
 *sqlType*  
  
 Ein JDBC-Typcode gemäß der Definition von "java.sql.Types".  
  
 *Typname*  
  
 Ein **Zeichenfolge** , die angibt, dass der vollqualifizierte Name des Parameters, der festgelegt wird.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetNull-Methode wird von der SetNull-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SetNull-Methode &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

