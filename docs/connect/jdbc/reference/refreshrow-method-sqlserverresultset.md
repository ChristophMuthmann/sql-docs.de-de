---
title: RefreshRow-Methode (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50d89d95b5aecdd3ae430b278d83ab2222cde7d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
