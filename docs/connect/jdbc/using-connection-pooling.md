---
title: Verbindungspooling | Microsoft Docs
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
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af73ee2a721ccd8da4a77b7d294460cf1d4da75b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-connection-pooling"></a>Verwenden von Verbindungspools
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet Unterstützung für Java-Plattform, Enterprise Edition (Java EE) Verbindungspooling. Der JDBC-Treiber implementiert die erforderlichen JDBC 3.0-Schnittstellen, damit der Treiber Verbindungspoolimplementierungen von Middlewareherstellern nutzen kann. Der JDBC-Treiber ist JDBC 3.0-kompatibel. Middleware wie Java EE-Anwendungsserver bieten häufig kompatible Verbindungspoolfunktionen. Der JDBC-Treiber nutzt in diesen Umgebungen Verbindungspools.  
  
> [!NOTE]  
>  Obwohl der JDBC-Treiber Java EE-Verbindungspools unterstützt, stellt er keine eigene Poolimplementierung bereit. Der Treiber benötigt Java-Anwendungsserver eines Drittanbieters zum Verwalten der Verbindungen.  
  
## <a name="remarks"></a>Hinweise  
 Für die Verbindungspoolimplementierung stehen die folgenden Klassen zur Verfügung.  
  
|Klasse|Implementiert|Description|  
|-----------|----------------|-----------------|  
|com.Microsoft.SqlServer.JDBC. SQLServerXADataSource|javax.sql.ConnectionPoolDataSource und javax.sql.XADataSource|Wir empfehlen die Verwendung der [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) Klasse für alle Java EE-Serverfunktionen benötigt, da sie alle JDBC 3.0-poolfunktionen und XA-Schnittstellen implementiert.|  
|com.Microsoft.SqlServer.JDBC. SQLServerConnectionPoolDataSource|javax.sql.ConnectionPoolDataSource|Bei dieser Klasse handelt es sich um ein Verbindungsfactory, das es dem Java EE-Anwendungsserver ermöglicht, den Verbindungspool mit physischen Verbindungen zu füllen. Wenn die Konfiguration des Java EE-Herstellers eine Klasse, die javax.sql.ConnectionPoolDataSource implementiert erfordert, geben Sie den Klassennamen als [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md). Im Allgemeinen sollten Sie verwenden die [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) Klasse stattdessen, da er sowohl poolfunktionen implementiert und XA-Schnittstellen und in weitere Java EE-Serverkonfigurationen überprüft wurde.|  
  
 Der JDBC-Anwendungscode sollte die Verbindungen immer explizit schließen, damit die Pools optimal genutzt werden können. Wenn die Anwendung eine Verbindung explizit schließt, kann die Poolimplementierung die Verbindung sofort wiederverwenden kann. Wenn die Verbindung nicht geschlossen wird, kann sie von anderen Anwendungen nicht wiederverwendet werden. Anwendungen können die `finally` Konstrukt, um sicherzustellen, dass poolverbindungen geschlossen werden, auch wenn eine Ausnahme auftritt.  
  
> [!NOTE]  
>  Der JDBC-Treiber ruft zurzeit nicht die gespeicherte Prozedur "sp_reset_connection" auf, wenn die Verbindung an den Pool zurückgegeben wird. Der Treiber geht stattdessen davon aus, dass die Java-Anwendungsserver der Drittanbieter die Verbindungen wieder in den ursprünglichen Status zurück versetzen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden von SQL Server mit dem JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
