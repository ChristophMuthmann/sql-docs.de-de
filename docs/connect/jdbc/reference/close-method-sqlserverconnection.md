---
title: Close-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0f26585-bdf7-4737-b434-8c7e115c8e94
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9f7dc84edb37bde6242be79830198ab565547e0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="close-method-sqlserverconnection"></a>Close-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dies frei [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objektspezifischen Datenbank- und JDBC-Ressourcen sofort gewartet, sondern deren automatische Freigabe sein.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Close-Methode wird von der close-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Aufrufen der close-Methode in der Mitte einer Transaktion wird die Transaktion ein Rollback ausgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
