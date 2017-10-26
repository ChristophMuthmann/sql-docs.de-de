---
title: RowInserted-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 885d101c9f19cd416fa85155be74aabd72bdefff
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rowinserted-method-sqlserverresultset"></a>RowInserted-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob in der aktuellen Zeile eine Einfügung vorgenommen wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn eine Zeile eine Einfügung wurde und einfügungen erkannt werden. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese RowUpdated-Methode wird von der RowUpdated-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Der zurückgegebene Wert hängt davon ab, ob dies [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt sichtbare einfügungen erkennen kann.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]eingefügte Zeilen für jeden Cursortyp wird nicht erkannt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

