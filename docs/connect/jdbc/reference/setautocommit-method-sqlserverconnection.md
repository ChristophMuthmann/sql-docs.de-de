---
title: SetAutoCommit-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7bf6842881256a5de4da2805b2c07c5f64fbeff4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="setautocommit-method-sqlserverconnection"></a>SetAutoCommit-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Autocommit-Modus für diese [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt, das dem angegebenen Status.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>Parameter  
 *value*  
  
 **"true"** Autocommit-Modus für die Verbindung aktivieren **"false"** zu deaktivieren.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetAutoCommit-Methode wird von der SetAutoCommit-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Ist für eine Verbindung der Modus für automatische Commits aktiviert, werden alle SQL-Anweisungen als einzelne Transaktionen ausgeführt, und die Commits der SQL-Anweisungen werden als einzelne Transaktionen ausgeführt. Andernfalls die SQL-Anweisungen in Transaktionen, die durch einen Aufruf von entweder beendet werden gruppiert die [Commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) Methode oder die [Rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) Methode. Der Modus für automatische Commits ist für neue Verbindungen standardmäßig aktiviert.  
  
 Der Commit wird ausgeführt, wenn die Anweisung abgeschlossen wird oder die nächste Ausführung durchgeführt wird, je nachdem, welches Ereignis zuerst eintritt. Im Fall von Anweisungen, die Zurückgeben einer [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, die Anweisung abgeschlossen wird, wenn die letzte Zeile des Resultsets abgerufen wurde, oder wenn das Resultset geschlossen wurde. In erweiterten Fällen kann eine einzelne Anweisung zusätzlich zu den Ausgabeparameterwerten mehrere Ergebnisse zurückgeben. In diesen Fällen wird der Commit ausgeführt, nachdem alle Ergebnisse und Ausgabeparameterwerte abgerufen wurden.  
  
 Wenn der Autocommit-Modus ist **"false"**, der JDBC-Treiber eine neue Transaktion nach jedem Commit implizit gestartet.  
  
> [!NOTE]  
>  Wenn diese Methode während einer Transaktion aufgerufen wird, wird ein Commit der Transaktion ausgeführt.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
