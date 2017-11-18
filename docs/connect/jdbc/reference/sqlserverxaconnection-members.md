---
title: SQLServerXAConnection-Elemente | Microsoft Docs
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
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0303bdf87283f2a7fba87b58991239f5d92a10d7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
 Keine.  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(Geerbt von [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) registriert den angegebenen Ereignislistener, damit dieser benachrichtigt wird, beim Auftreten eines Ereignisses für diese Verbindung-Objekt.|  
|[Schließen Sie](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(Geerbt von [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) schließt die physische Verbindung, die diese Verbindung-Objekt darstellt.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(Geerbt von [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) erstellt ein Objekthandle für die physische Verbindung, die diese Verbindung-Objekt darstellt.|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|Ruft eine [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Objekt, mit der Transaktions-Manager zum Verwalten der Beteiligung dieser verwenden [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) Objekt in einer verteilten Transaktion.|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(Geerbt von [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) entfernt den angegebenen Ereignislistener.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAConnection-Klasse](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  

