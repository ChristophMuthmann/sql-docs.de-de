---
title: RowUpdated-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f9b34859431b995ddfe6788b6eb08d6d9ed9d74
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rowupdated-method-sqlserverresultset"></a>RowUpdated-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob die aktuelle Zeile aktualisiert wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn die Zeile sichtbar vom Besitzer oder einem anderen Benutzer aktualisiert wurde, und Updates ermittelt werden. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese RowUpdated-Methode wird von der RowUpdated-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Der zurückgegebene Wert ist davon abhängig, ob vom Resultset Updates ermittelt werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]aktualisierte Zeilen für jeden Cursortyp wird nicht erkannt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

