---
title: InsertRow-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9297b57b1ad4ded2611fadb1034a61046e3a4d25
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="insertrow-method-sqlserverresultset"></a>InsertRow-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fügt den Inhalt der Einfügezeile diesem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt bzw. aus einer Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese InsertRow-Methode wird von der InsertRow-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Beim Aufruf dieser Methode muss sich der Cursor in der Einfügezeile befinden. Nach dem Aufruf dieser Methode verbleibt der Cursor in der Einfügezeile, und das Resultset im Einfügemodus.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

