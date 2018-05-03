---
title: Grundlegendes zur Java EE-Unterstützung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6d747e341fd931fd2ee41164c5d3632f7945592
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-java-ee-support"></a>Grundlegendes zur Java EE-Unterstützung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Den folgenden Abschnitten wird dokumentiert wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet Unterstützung für die Java-Plattform, Enterprise Edition (Java EE) und die optionalen JDBC 3.0-API-Funktionen. Die Quellcodebeispiele in diesem Hilfesystem stellen eine gute Referenz für erste Schritte mit diesen Funktionen dar.  
  
 Stellen Sie zunächst sicher, dass die Java-Umgebung (JDK, JRE) das Paket javax.sql einschließt. Dies ist ein erforderliches Paket für alle JDBC-Anwendungen, die die optionale API verwenden. JDK 1.5 und höhere Versionen umfassen dieses Paket bereits, sodass Sie es nicht separat installieren müssen.  
  
## <a name="driver-name"></a>Treibername  
 Der treiberklassenname lautet **com.microsoft.sqlserver.jdbc.SQLServerDriver**. 4.2 und 6.0, wird der Treiber für JDBC Driver 4.1 in der Datei "sqljdbc.jar", "sqljdbc4.jar", "sqljdbc41.jar" oder "sqljdbc42.jar" enthalten. Für den JDBC-Treiber 6.2 wird der Treiber im Mssql-Jdbc-6.2.1.jre7.jar oder Mssql-Jdbc-6.2.1.jre8.jar enthalten. Für JDBC Driver 6.4 wird der Treiber im Mssql-Jdbc-6.4.0.jre7.jar, Mssql-Jdbc-6.4.0.jre8.jar oder Mssql-Jdbc-6.4.0.jre9.jar enthalten.
  
 Der Name der Klasse wird verwendet, wenn Sie den Treiber mit der JDBC-DriverManager-Klasse laden. Er wird außerdem verwendet, wenn Sie den Klassennamen des Treibers in einer Treiberkonfiguration angeben müssen. Für das Konfigurieren einer Datenquelle in einem Java EE-Anwendungsserver kann es beispielsweise erforderlich sein, den Treiberklassennamen einzugeben.  
  
## <a name="data-sources"></a>Datenquellen  
 Der JDBC-Treiber unterstützt Java EE-/JDBC 3.0-Datenquellen. Der JDBC-Treiber [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) -Klasse wird implementiert von **com.microsoft.sqlserver.jdbc.SQLServerXADataSource**.  
  
### <a name="datasource-names"></a>DataSource-Namen  
 Sie können Datenbankverbindungen mithilfe von Datenquellen herstellen. Die mit dem JDBC-Treiber verfügbaren Datenquellen werden in der folgenden Tabelle beschrieben:  
  
|DataSource-Typ|Klassennamen und Beschreibung|  
|---------------|--------------------------|  
|DataSource|com.microsoft.sqlserver.jdbc.SQLServerDataSource <br/> <br/> Die Datenquelle ohne Pooling.|  
|ConnectionPoolDataSource|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource <br/> <br/> Die Datenquelle zum Konfigurieren von Verbindungspools für Java EE-Anwendungsserver. Wird normalerweise verwendet, wenn die Anwendung innerhalb eines Java EE-Anwendungsservers ausgeführt wird.|  
|XADataSource|com.microsoft.sqlserver.jdbc.SQLServerXADataSource <br/> <br/> Die Datenquelle zum Konfigurieren von Java EE-XA-Datenquellen. Wird normalerweise verwendet, wenn die Anwendung innerhalb eines Java EE-Anwendungsservers und eines XA-Transaktionsmanagers ausgeführt wird.|  
  
### <a name="data-source-properties"></a>Datenquelleneigenschaften  
 Alle Datenquellen unterstützen die Möglichkeit zum Festlegen und Abrufen aller Eigenschaften, die dem Eigenschaftenset des zugrunde liegenden Treibers zugeordnet sind.  
  
 Beispiele:  
  
 `setServerName("localhost");`  
  
 `setDatabaseName("AdventureWorks");`  
  
 Im Folgenden wird veranschaulicht, wie eine Anwendung mit einer Datenquelle eine Verbindung herstellt:  
  
```  
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 Weitere Informationen zu den Datenquelleneigenschaften finden Sie unter [Festlegen der Datenquelleneigenschaften](../../connect/jdbc/setting-the-data-source-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
