---
title: Commit-Methode (SQLServerConnection) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89d6620e4848d837cd98337f3d7faf67432da23f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="commit-method-sqlserverconnection"></a>Commit-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Macht alle Änderungen, die seit dem letzten Commit oder Rollback permanente vorgenommen wurden, und hebt sämtliche Datenbanksperren derzeit aufrecht erhalten werden von diesem [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Commit-Methode wird von der Commit-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die Methode sollte nur bei deaktiviertem Modus für automatische Commits verwendet werden.  
  
 Diese Methode ergibt einen Fehler und löst eine Ausnahme aus, wenn der Client mit einer manuellen Transaktion beginnt und von SQL Server aus irgendeinem Grund ein Rollback der manuellen Transaktion ausgeführt wird. Beispielsweise wird eine Ausnahme wird ausgelöst, wenn der Client eine gespeicherte Prozedur aufruft, die explizit ROLLBACK TRANSACTION aufruft, und der Client ruft dann die Commit-Methode. Wenn SQL Server einen Fehler mit einem Schweregrad (16 oder höher) ein Rollback auslöst initiiert der Client außerdem manuellen Transaktion; ein nachfolgender Aufruf von Commit-Methode wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
