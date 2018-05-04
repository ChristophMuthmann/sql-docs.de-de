---
title: IsBeforeFirst-Methode (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 672b60c1e131dd579b33947b9ff351f4ef939aa1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>IsBeforeFirst-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob der Cursor befindet sich vor der ersten Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn der Cursor vor der ersten Zeile befindet. **"false"** , wenn der Cursor an einer beliebigen anderen Position befindet oder wenn das Resultset keine Zeilen enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese IsBeforeFirst-Methode wird von der IsBeforeFirst-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Wird diese Methode mit dynamischen Cursors verwendet, einschließlich schreibgeschützten Vorwärtscursors und die selectMethod-Verbindungseigenschaft auf "cursor" festgelegt, wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
