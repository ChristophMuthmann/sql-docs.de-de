---
title: SQLServerXADataSource-Elemente | Microsoft Docs
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
ms.assetid: 04178645-915f-4569-8907-d45e299bbe7d
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee5a0ea6a351a5f0bce49ff3fccd26d636048f2d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverxadatasource-members"></a>SQLServerXADataSource-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
  
|Name|Description|  
|----------|-----------------|  
|[((SQLServerXADataSource)](../../../connect/jdbc/reference/sqlserverxadatasource-constructor.md)|Initialisiert eine neue Instanz der dem [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) Klasse.|  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
 Keine.  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Wert der **ApplicationIntent** Connection-Eigenschaft.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Anwendungsnamen zurück.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) versucht, eine Verbindung mit der Datenquelle herzustellen, die diese DataSource-Objekt darstellt.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Datenbanknamen zurück.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Namen des Failoverservers, der verwendet wird, in einer Datenbank-Spiegelungskonfiguration.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanzname.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt eine **booleschen** -Wert, der angibt, ob die LastUpdateCount-Eigenschaft aktiviert ist.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt eine **Int** Wert, der die Anzahl von Millisekunden angibt, die die Datenbank bis zum Melden eines Sperrtimeouts gewartet wird.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt die Anzahl der Sekunden an, die dieses Datenquellenobjekt gewartet wird, bei dem Versuch, eine Verbindung herzustellen.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt einen zeichenausgabedatenstrom für alle protokollierungs- und Ablaufverfolgungsmeldungen verwendet werden.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Ruft den Wert des der **MultiSubnetFailover** Connection-Eigenschaft.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|(Geerbt von [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)) stellt eine physische datenbankverbindung her, die als poolverbindung verwendet werden können.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt die aktuelle Portnummer, die verwendet wird, für die Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverxadatasource.md)|Gibt einen Verweis auf diese [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) Objekt.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Standardcursortyp, der für alle Resultsets verwendet wird, die mithilfe dieser DataSource-Objekt erstellt werden.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt eine **booleschen** Wert, der angibt senden **Zeichenfolge** Parameter an den Server im Unicode-Format aktiviert ist.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Namen des Computers, der ausgeführt wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt die URL, die für die Verbindung mit der Datenquelle verwendet wird.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Benutzernamen zurück, der verwendet wird, mit der Datenquelle hergestellt.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt den Namen des Clients Computernamen, die für die Verbindung mit der Datenquelle verwendet wird.|  
|[getXAConnection](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)|Stellt eine physische Datenbankverbindung her, die in einer verteilten Transaktion verwendet werden kann.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt eine **booleschen** -Wert, der angibt, ob das Konvertieren von SQL-Status zu XOPEN-kompatiblen Status aktiviert ist.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)|Gibt an, ob es sich bei diesem Objekt um einen Wrapper für die angegebene Schnittstelle handelt.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Wert für die **ApplicationIntent** Connection-Eigenschaft.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Anwendungsnamen fest.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) gibt die Art der integrierten Sicherheit Ihrer Anwendung verwenden soll.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Datenbanknamen für die Verbindung fest.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt die Beschreibung der Datenquelle fest.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Namen des Failoverservers, der verwendet wird, in einer Datenbank-Spiegelungskonfiguration.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanzname.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt einen **booleschen** -Wert, der angibt, ob die IntegratedSecurity-Eigenschaft aktiviert ist.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt einen **booleschen** -Wert, der angibt, ob die LastUpdateCount-Eigenschaft aktiviert ist.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt einen **Int** Wert, der die Anzahl von Millisekunden, die gewartet wird, bevor die Datenbank ein Sperrtimeout meldet.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt die Anzahl der Sekunden an, die dieses Datenquellenobjekt gewartet wird, bei dem Versuch, eine Verbindung herzustellen.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt einen zeichenausgabedatenstrom für alle protokollierungs- und Ablaufverfolgungsmeldungen verwendet werden.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Wert für die **MultiSubnetFailover** Connection-Eigenschaft.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt das Kennwort, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt die Portnummer für die Kommunikation zu verwendende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Standardcursortyp, der für alle Resultsets verwendet wird, die mithilfe dieser DataSource-Objekt erstellt werden.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt einen **booleschen** Wert, der angibt senden **Zeichenfolge** Parameter an den Server im Unicode-Format aktiviert ist.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Namen des Computers, der ausgeführt wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt die URL, die für die Verbindung mit der Datenquelle verwendet wird.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt den Benutzernamen ab, das der Datenquelle hergestellt.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) wird der Computername, der für die Verbindung mit der Datenquelle verwendet wird.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(Geerbt von [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) legt einen **booleschen** -Wert, der angibt, ob das Konvertieren von SQL-Status zu XOPEN-kompatiblen Status aktiviert ist.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)|Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource|getPooledConnection|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.XADataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXADataSource-Klasse](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
