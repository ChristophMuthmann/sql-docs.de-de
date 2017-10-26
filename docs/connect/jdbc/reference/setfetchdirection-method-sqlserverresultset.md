---
title: SetFetchDirection-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dd6ab9a94acf883ed27cdd79fee886b6c54ca596
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setfetchdirection-method-sqlserverresultset"></a>setFetchDirection-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt Aufschluss über die Richtung, in dem die Zeilen in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt verarbeitet werden.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt durch die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Bei Verwendung dieser Methode wird die Einstellung vom JDBC-Treiber zwar gespeichert, sie wird jedoch derzeit nicht genutzt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Richtung*  
  
 Ein **Int** , der angibt, dass der vorgeschlagenen abrufrichtung. Folgende Werte sind möglich:  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetFetchDirection-Methode wird von der SetFetchDirection-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Der Anfangswert dieser Methode richtet sich nach der [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das dieses SQLServerResultSet-Objekt erstellt wurde. Die Abrufrichtung kann jedoch jederzeit geändert werden.  
  
> [!NOTE]  
>  Handelt es sich beim Cursortyp um einen Vorwärtscursor, hat die Verwendung dieser Methode keine Auswirkungen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

