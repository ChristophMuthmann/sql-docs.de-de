---
title: GetArray-Methode (java.lang.String) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getArray java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a98d159b-1fae-482a-9465-5411ce60f901
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3be182943c5ea6e145b203bbb1bb839c70e61d74
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getarray-method-javalangstring-sqlserverresultset"></a>GetArray-Methode (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltennamens in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als ein Arrayobjekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Array getArray(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *colName*  
  
 Ein **Zeichenfolge** , die den Namen der Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Arrayobjekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetArray-Methode wird von der GetArray-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetArray-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

