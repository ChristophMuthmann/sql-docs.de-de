---
title: Finalize-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6762b75f40e3b1fdc0a309c67dea461b1dada974
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="finalize-method-sqlserverresultset"></a>Finalize-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Schließt dies explizit [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Hinweise  
 Schließt das Resultset, wenn dies nicht durch die Anwendung geschieht. Diese Methode entspricht der JDBC-Spezifikation. Da die Java Virtual Machine (JVM) keine Garantie dafür bietet, wann ein Finalizer ausgeführt werden kann, können Anwendungen, von denen ihre Resultsets nicht explizit geschlossen werden, einen Deadlock für eine andere Anweisung auslösen, von der die gleiche Verbindung verwendet wird und die für eine gemeinsame Serverressource (z. B. Zeilensperren) blockiert wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

