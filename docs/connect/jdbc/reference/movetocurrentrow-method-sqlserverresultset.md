---
title: MoveToCurrentRow-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.moveToCurrentRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9a7c754c-2d72-4207-b3bd-2afc6047fb3d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8548c196214955e03a04a9a318a30701b0b26f1e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="movetocurrentrow-method-sqlserverresultset"></a>MoveToCurrentRow-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Versetzt den Cursor an die gespeicherte Cursorposition (üblicherweise die aktuelle Zeile).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void moveToCurrentRow()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese MoveToCurrentRow-Methode wird von der MoveToCurrentRow-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Die Methode zeigt keine Auswirkungen, wenn der Cursor sich nicht in der Einfügezeile befindet.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

