---
title: RefreshRow-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 89452f34778b07f9e34b074beaf2b1e92f7be135
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="refreshrow-method-sqlserverresultset"></a>refreshRow-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die aktuelle Zeile mit dem aktuellen Wert aus der Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese RefreshRow-Methode wird von der RefreshRow-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode kann nicht aufgerufen werden, wenn sich der Cursor in der Einfügezeile befindet.  
  
 Mit dieser Methode kann der JDBC-Treiber von einer Anwendung explizit angewiesen werden, Zeilen aus der Datenbank erneut abzurufen. Eine Anwendung zum Aufrufen dieser Methode müssen möglicherweise bei der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] Inhalte zwischengespeichert oder vorab abgerufen werden, um den neuesten Wert einer Zeile aus der Datenbank abzurufen. Vom JDBC-Treiber werden möglicherweise mehrere Zeilen gleichzeitig aktualisiert, wenn die Abrufgröße den Wert "1" übersteigt.  
  
 Beim erneuten Abrufen von Werten werden die Transaktionsisolationsstufe und der Cursor berücksichtigt. Wenn diese Methode aufgerufen wird, nach dem Aufrufen einer Updater-Methode, jedoch vor dem Aufruf der [UpdateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) -Methode, die Updates zeilenupdates verloren. Häufiges Aufrufen dieser Methode kann sich negativ auf die Leistung auswirken.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

