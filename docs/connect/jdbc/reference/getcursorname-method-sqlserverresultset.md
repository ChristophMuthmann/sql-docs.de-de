---
title: GetCursorName-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5b3af67-423a-4551-a4c6-a4bc076bd504
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56da8245700f7e4d93ad0dcd3503d1b214df61a1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getcursorname-method-sqlserverresultset"></a>getCursorName-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Namen der SQL-Cursor, die von diesem dient [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt durch die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Bei Aufruf wird eine Ausnahme ausgelöst.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getCursorName()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , enthält der Name des Cursors.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetCursorName-Methode wird von der GetCursorName-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

