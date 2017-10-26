---
title: JDBC Driver-API-Referenz | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c19740d1247fa1fd7fe8036fa2aa557e01e74c82
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-api-reference"></a>API-Referenz für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] stellt eine API bereit, die verwendet werden kann, innerhalb von Java Programmiercode zum Herstellen einer Verbindung mit und interagieren mit einem [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank.  
  
> [!NOTE]  
>  Konzeptionelle Informationen zum Verwenden des JDBC-Treibers finden Sie unter [Überblick über die JDBC-Treiber](../../../connect/jdbc/overview-of-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Verwenden Sie Microsoft JDBC Driver 4.2 (oder höher) für JDBC 4.1 und 4.2 Compliance-Unterstützung für SQL Server. Die vorhergehenden Versionen Microsoft JDBC Driver 4.1 und 4.0 unterstützen die in JDBC 4.1 und 4.2 eingeführten neuen Methoden nicht.  
>   
>  API-Details zur JDBC 4.1-Kompatibilität werden in diesem Abschnitt nicht erörtert. Finden Sie unter [JDBC 4.1-Kompatibilität für JDBC Driver](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md).  
>   
>  API-Details zur JDBC 4.2-Kompatibilität werden in diesem Abschnitt nicht erörtert. Finden Sie unter [JDBC 4.2-Kompatibilität für JDBC Driver](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
>   
>  API-Details zur Massenkopierfunktion, beginnend mit Microsoft JDBC Driver 4.2 für SQL Server verfügbar sind in diesem Abschnitt nicht gefunden. Finden Sie unter [Verwenden von Massenkopieren mit dem JDBC-Treiber](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
>   
>  API-Details für Always Encrypted, beginnend mit Microsoft JDBC Driver 6.0 für SQL Server verfügbar werden nicht in diesem Abschnitt erörtert. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  API-Details zur Using Table-Valued-Parameter, beginnend mit Microsoft JDBC Driver 6.0 für SQL Server verfügbar sind in diesem Abschnitt nicht gefunden. Finden Sie unter [mit Tabellenwertparametern](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.0 und 4.2 unterstützen die Kompilierung mit JDK 5.0, 6.0, 7.0 und 8.0.  
>   
>  Microsoft JDBC Driver 4.1 unterstützt die Kompilierung mit JDK 5.0, 6.0 und 7.0.  
>   
>  Microsoft JDBC Driver 4.0 unterstützt die Kompilierung mit JDK 5.0 und 6.0.  
  
## <a name="interfaces"></a>Schnittstellen  
  
|Schnittstellenname|Description|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement-Schnittstelle](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|Mit dieser Klasse kann der gespeicherte Prozedurname angegeben werden, der mit Eingabe- und Ausgabeparametern aufgerufen wird.|  
|[ISQLServerConnection-Schnittstelle](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|Stellt eine JDBC-Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank.|  
|[SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|Stellt eine Liste mit spezifischen Eigenschaften zum Herstellen einer Verbindung mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank mithilfe einer [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|Stellt die grundlegende Implementierung der JDBC-Funktion für vorbereitete Anweisungen dar.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|Stellt ein JDBC-Resultset dar.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|Stellt die grundlegende Implementierung der JDBC-Anweisungsfunktion dar.|  
  
## <a name="classes"></a>Klassen  
  
|Klassenname|Description|  
|----------------|-----------------|  
|["DateTimeOffset"](../../../connect/jdbc/reference/datetimeoffset-class.md)|Stellt ein Objekt vom Typ "microsoft.sql.DateTimeOffset" dar.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|Stellt ein BLOB (Binary Large Object) dar.|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|Implementiert ISQLServerCallableStatement.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|Stellt ein CLOB (Character Large Binary Object) dar.|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|Implementiert ISQLServerConnectopn.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|Stellt die physischen Datenbankverbindungen für Verbindungspool-Manager dar.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|Stellt die Metadaten für die Datenbank dar.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|Stellt eine Liste mit spezifischen Eigenschaften zum Herstellen einer Verbindung mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank mithilfe einer [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|Stellt ein Objektfactory zum Materialisieren von Datenquellen aus der JNDI (Java Naming and Directory Interface) dar.|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|Stellt den JDBC-Treiber dar. Diese Klasse enthält Methoden zum Herstellen einer Verbindung mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Datenbank und zum Abrufen von Informationen zum JDBC-Treiber.|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|Stell die fehlerhafte oder unvollständige Ausführung einer SQL-Anweisung dar.|  
|[SQLServerNClob-Klasse](../../../connect/jdbc/reference/sqlservernclob-class.md)|Stellt ein CLOB (Character Large Binary Object) mit nationalem Zeichensatz dar.|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|Stellt die Metadaten für die Parameter vorbereiteter Anweisungen dar.|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|Stellt eine physische Datenbankverbindung in einem Verbindungspool dar.|  
|[Sqlserverpreparedstatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|Implementiert ISQLServerPreparedStatement.|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|Stellt eine Ressource für lokalisierte Fehlerzeichenfolgen dar. Diese Klasse dient nur zur internen Verwendung.|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|Implementiert ISQLServerResultSet.|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|Stellt die Metadaten der Spalten innerhalb eines Resultsets dar.|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|Stellt den Prüfpunkt dar, bis zu dem ein Transaktionsrollback durchgeführt werden kann.|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|Implementiert ISQLServerStatement.|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|Stellt JDBC-Verbindungen dar, die an verteilten Transaktionen (XA-Transaktionen) beteiligt sein können.|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|Stellt eine Factory für [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) Objekte, die intern verwendet wird.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|Stellt einen XAResource für den XA-verteilter Verwaltung Transaktionen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

