---
title: SQLServerDataSource-Elemente | Microsoft Docs
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
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65485de46704db4e949eb33f253ecd86271b48dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverdatasource-members"></a>SQLServerDataSource-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  In den folgenden Tabellen enthalten die Elemente, die verfügbar gemacht werden, indem Sie die [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
  
|Name|Description|  
|----------|-----------------|  
|[((SQLServerDataSource)](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|Initialisiert eine neue Instanz der dem [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse.|  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
 Keine.  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|Gibt den Wert der **ApplicationIntent** Connection-Eigenschaft.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|Gibt den Anwendungsnamen zurück.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|Versucht, die zum Herstellen einer Verbindung mit den Daten Datenquelle, die von diesem [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) -Objekt darstellt.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|Gibt den Datenbanknamen zurück.|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverdatasource.md)|Gibt den Wert der **"disablestatementpooling":** Connection-Eigenschaft. Diese Einstellung steuert, ob anweisungspools aktiviert ist oder nicht für diese Verbindung.|  
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|Gibt den Wert der **EnablePrepareOnFirstPreparedStatementCall** Connection-Eigenschaft.|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|Gibt eine **booleschen** Wert, der angibt, ob die Encrypt-Eigenschaft aktiviert ist.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|Gibt eine Beschreibung der Datenquelle zurück.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|Gibt den Namen des Failoverservers zurück, der in einer Datenbankspiegelungskonfiguration verwendet wird.|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|Gibt den Hostnamen zurück, der bei der Überprüfung des Secure Sockets Layer (SSL)-Zertifikats von SQL Server verwendet wird.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|Gibt die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanzname.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|Gibt eine **booleschen** Wert, der angibt, ob die LastUpdateCount-Eigenschaft aktiviert ist.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|Gibt eine **Int** Wert, der angibt, der Anzahl der Millisekunden, die die Datenbank wartet, bevor gemeldet wird, ein Timeout der Sperre.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|Gibt die Anzahl der Sekunden dies [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt wartet, bei dem Versuch, eine Verbindung herzustellen.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|Gibt einen Zeichenausgabedatenstrom für alle Protokollierungs- und Ablaufverfolgungsmeldungen zurück.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|Gibt den Wert der **MultiSubnetFailover** Connection-Eigenschaft.|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|Gibt die aktuelle Netzwerkpaketgröße verwendet, um die Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], angegeben in Bytes.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|Gibt die aktuelle Portnummer zur Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|Gibt einen Verweis auf diese [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|Gibt den antwortpuffermodus für dieses [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|Gibt den Standardcursortyp verwendet für alle Resultsets mit diesem erstellt [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|Gibt eine **booleschen** Wert, der angibt, ob das Senden von Zeichenfolgenparametern an den Server im Unicode-Format aktiviert ist.|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|Gibt die Einstellung von der **SendTimeAsDatetime** Connection-Eigenschaft.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|Gibt den Namen des Computers ausgeführt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|Gibt den Wert der **ServerPreparedStatementDiscardThreshold** Connection-Eigenschaft.|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverdatasource.md)|Gibt die Größe des Caches vorbereitete Anweisung für diese Verbindung zurück.|  
|[getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md)|Gibt den Zeichenfolgenwert der TrustManagerClass Verbindungseigenschaft zurück.|  
|[getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md)|Gibt den Zeichenfolgenwert der TrustManagerConstructorArg Verbindungseigenschaft zurück.|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|Gibt eine **booleschen** Wert, der angibt, ob die TrustServerCertificate-Eigenschaft aktiviert ist.|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|Gibt den Pfad (einschließlich Dateiname) zur trustStore-Zertifikatsdatei zurück.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|Die URL, die zur Verbindung mit der Datenquelle zurückgegeben.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|Gibt den Benutzernamen, die zur Verbindung von der Datenquelle zurück.|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|Sie gibt die Einstellung der useSQLServerBaseDate-Verbindungseigenschaft zurück.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|Gibt den Namen der Name des Clientcomputers zur Verbindung mit der Datenquelle zurück.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|Gibt eine **booleschen** Wert, der angibt, ob das Konvertieren von SQL-Status in XOPEN-kompatiblen Status aktiviert ist.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|Gibt an, ob es sich bei diesem Datenquellenobjekt um einen Wrapper für die angegebene Schnittstelle handelt.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|Legt den Wert für die **ApplicationIntent** Connection-Eigenschaft.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|Legt den Anwendungsnamen fest.|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|Gibt die Art der integrierten Sicherheit an, die für die Anwendung verwendet werden soll.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|Legt den Namen der Datenbank fest, mit der eine Verbindung hergestellt werden soll.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|Legt die Beschreibung der Datenquelle fest.|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverdatasource.md)|Legt fest, anweisungspools auf "true" oder "false".|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|Gibt den neuen Wert, der die **EnablePrepareOnFirstPreparedStatementCall** Connection-Eigenschaft.|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|Legt eine **booleschen** Wert, der angibt, ob die Encrypt-Eigenschaft aktiviert ist.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|Legt den Namen des Failoverservers fest, der in einer Datenbankspiegelungskonfiguration verwendet wird.|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|Legt den Hostnamen fest, der bei der Überprüfung des Secure Sockets Layer (SSL)-Zertifikats von SQL Server verwendet werden soll.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|Legt die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanzname.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|Legt eine **booleschen** Wert, der angibt, ob die IntegratedSecurity-Eigenschaft aktiviert ist.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|Legt eine **booleschen** Wert, der angibt, ob die LastUpdateCount-Eigenschaft aktiviert ist.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|Legt eine **Int** Wert, der angibt, der Anzahl der Millisekunden, die gewartet wird, bevor die Datenbank ein Sperrtimeout meldet.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|Legt die Anzahl der Sekunden, die dies [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt wartet, bei dem Versuch, eine Verbindung herzustellen.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|Legt einen Zeichenausgabedatenstrom für alle Protokollierungs- und Ablaufverfolgungsmeldungen fest.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|Legt den Wert für die **MultiSubnetFailover** Connection-Eigenschaft.|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|Legt die aktuelle Netzwerkpaketgröße verwendet, um die Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], angegeben in Bytes.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|Legt das Kennwort für die Verbindung verwendete [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|Legt die Portnummer, die zur Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|Legt den antwortpuffermodus für Verbindungen mit diesem erstellt [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|Legt den Standardcursortyp verwendet für alle Resultsets mit diesem erstellt [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|Legt eine **booleschen** Wert, der angibt, ob das Senden von Zeichenfolgenparametern an den Server im Unicode-Format aktiviert ist.|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|Gibt die Art und Weise an, wie java.sql.Time-Werte an den Server gesendet werden.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|Legt den Namen des Computers ausgeführt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|Legt den neuen Wert für die **ServerPreparedStatementDiscardThreshold** Connection-Eigenschaft.|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverdatasource.md)|Legt die Größe des Caches für diese Verbindung vorbereiteten Anweisung.|  
|[setTrustManagerClass](../../../connect/jdbc/reference/settrustmanagerclass-method-sqlserverdatasource.md)|Legt den Zeichenfolgenwert der Verbindungseigenschaft TrustManagerClass fest.|  
|[setTrustManagerConstructorArg](../../../connect/jdbc/reference/settrustmanagerconstructorarg-method-sqlserverdatasource.md)|Legt den Zeichenfolgenwert der Verbindungseigenschaft TrustManagerConstructorArg fest.|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|Legt eine **booleschen** Wert, der angibt, ob die TrustServerCertificate-Eigenschaft aktiviert ist.|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|Legt den Pfad (einschließlich Dateiname) zur trustStore-Zertifikatsdatei fest.|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|Legt das Kennwort fest, das zum Überprüfen der Integrität der trustStore-Daten verwendet wird.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|Legt die URL fest, die zum Herstellen einer Verbindung mit der Datenquelle verwendet wird.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|Legt den Benutzernamen verwendet, um der Datenquelle hergestellt.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|Legt den Namen des Clientcomputers fest, der zum Herstellen einer Verbindung mit der Datenquelle verwendet wird.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|Legt eine **booleschen** Wert, der angibt, ob das Konvertieren von SQL-Status in XOPEN-kompatiblen Status aktiviert ist.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
