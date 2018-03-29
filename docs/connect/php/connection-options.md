---
title: Verbindungsoptionen | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e9e8d87f7c1da0574264744459070a04b9b959e2
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="connection-options"></a>Verbindungsoptionen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema enthält die Optionen, die im assoziativen Array zulässig sind (bei Verwendung [Sqlsrv_connect](../../connect/php/sqlsrv-connect.md) im SQLSRV-Treiber) oder die Schlüsselwörter, die in der Datenquellenname (Dsn) zulässig sind (bei Verwendung [PDO:: __construct ](../../connect/php/pdo-construct.md) im PDO_SQLSRV-Treiber).  

## <a name="table-of-connection-options"></a>Tabelle der Verbindungsoptionen
|Key|Wert|Description|Standardwert|  
|-------|---------|---------------|-----------|  
|APP|String|Gibt den Namen der Anwendung an, der in der Ablaufverfolgung verwendet wird.|Kein Wert festgelegt.|  
|ApplicationIntent|String|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind „ReadOnly“ und „ReadWrite“.<br /><br />Weitere Informationen zu [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Unterstützung für [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], finden Sie unter [Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|ReadWrite|  
|AttachDBFileName|String|Gibt an, welche Datenbankdatei der Server anfügen soll.|Kein Wert festgelegt.|  
|Authentifizierung|Einer der folgenden Zeichenfolgen:<br /><br />'SqlPassword'<br /><br />'ActiveDirectoryPassword'|Gibt den Authentifizierungsmodus an.|nicht festgelegt werden.|  
|CharacterSet<br /><br />(vom PDO_SQLSRV-Treiber nicht unterstützt)|String|Gibt den Zeichensatz an, mit dem Daten an den Server gesendet werden.<br /><br />Mögliche Werte sind SQLSRV_ENC_CHAR und UTF-8. Weitere Informationen finden Sie unter [How to: Send and Retrieve UTF-8 Data Using Built-In UTF-8 Support](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|SQLSRV_ENC_CHAR|  
|ColumnEncryption<br /><br />(nur in Windows unterstützt)|**Aktiviert** oder **deaktiviert**|Gibt an, ob die Funktion Always Encrypted oder nicht aktiviert ist. |Disabled|  
|ConnectionPooling|1 oder **true** , um Verbindungspooling zu aktivieren.<br /><br />0 oder **false** , um Verbindungspooling zu deaktivieren.|Gibt an, ob die Verbindung aus einem Verbindungspool zugewiesen wird (1 oder **"true"**) oder nicht (0 oder **"false"**).<sup> 1</sup>|**"true"** (1)|  
|ConnectRetryCount|Ganze Zahl zwischen 0 und 255 (inklusiv)|Die maximale Anzahl der Versuche vor dem Allgemeinheit eine unterbrochene Verbindung her. Standardmäßig wird ein einzelner Versuch unternommen, bei unterteilt eine Verbindung her. Der Wert 0 bedeutet, dass keine erneute Verbindung erneut versucht wird.|1|  
|ConnectRetryInterval|Ganze Zahl zwischen 1 und 60 (inklusiv)|Die Zeit in Sekunden zwischen den versuchen, eine Verbindung wiederherzustellen. Die Anwendung versucht, die sofort erneut eine Verbindung herzustellen, eine unterbrochene Verbindung wird erkannt, und wartet dann Connectionretryinterval Sekunden, bevor Sie es erneut zu versuchen. Dieses Schlüsselwort wird ignoriert, wenn ConnectRetryCount gleich 0 ist.|1|  
|Datenbank|String|Gibt den Namen der Datenbank in der Verwendung für die herzustellende Verbindung<sup>2</sup>.|Die Standarddatenbank, die für die Anmeldung verwendet wird.|  
|Treiber|String|Gibt den Microsoft ODBC-Treiber, die zur Kommunikation mit SQL Server verwendet.<br /><br />Folgende Werte sind möglich:<br />ODBC-Treiber 17 für SQLServer<br />Odbcdriver 13 for SQLServer<br />Odbcdriver 11 für SQLServer (nur Windows).|Wenn das Driver-Schlüsselwort nicht angegeben ist, versucht Microsoft Drivers for PHP for SQL Server im System, das Vorhandensein der unterstützten Microsoft ODBC-Treiber suchen beginnend mit der neuesten Version von ODBC und so weiter.|  
|Encrypt|1 oder **true** , um Verschlüsselung zu aktivieren.<br /><br />0 oder **false** , um Verschlüsselung zu deaktivieren.|Gibt an, ob die Kommunikation mit SQL Server verschlüsselt (1 oder **"true"**) oder unverschlüsselt (0 oder **"false"**)<sup>3</sup>.|**"false"** (0)|  
|Failover_Partner|String|Gibt den Server und die Instanz der Spiegelung der Datenbank an (sofern aktiviert und konfiguriert), die verwendet werden soll, wenn der primäre Server nicht verfügbar ist.<br /><br />Es gibt Einschränkungen für die Verwendung von Failover_Partner mit MultiSubnetFailover. Weitere Informationen finden Sie unter [Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Kein Wert festgelegt.|  
|LoginTimeout|Integer (SQLSRV-Treiber)<br /><br />Zeichenfolge (PDO_SQLSRV-Treiber)|Legt die Wartezeit in Sekunden fest, bevor der Verbindungsversuch fehlschlägt.|Kein Timeout.|  
|MultipleActiveResultSets|1 oder **true** zum Verwenden von mehreren aktiven Resultsets.<br /><br />0 oder **false** zum Deaktivieren von mehreren aktiven Resultsets.|Deaktiviert oder aktiviert explizit die Unterstützung für mehrere aktive Resultsets (MARS).<br /><br />Weitere Informationen finden Sie unter [Vorgehensweise: Deaktivieren von mehreren aktiven Resultsets &#40;MARS&#41;](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).|true (1)|  
|MultiSubnetFailover|String|Geben Sie immer **MultiSubnetFailover = Yes** beim Verbinden mit dem verfügbarkeitsgruppenlistener eine [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] verfügbarkeitsgruppe oder einer [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Failoverclusterinstanz. **MultiSubnetFailover = Yes** konfiguriert [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Schnellere Erkennung und Verbindung mit dem (gerade) aktiven Server bereitstellen. Mögliche Werte sind Yes und No.<br /><br />Weitere Informationen zu [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Unterstützung für [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], finden Sie unter [Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|nein|  
|PWD<br /><br />(vom PDO_SQLSRV-Treiber nicht unterstützt)|String|Gibt das Kennwort für die Benutzer-ID, die verwendet werden, bei der Verbindung mit SQL Server-Authentifizierung<sup>4</sup>.|Kein Wert festgelegt.|  
|QuotedId|1 oder **"true"** SQL-92-Regeln verwenden.<br /><br />0 oder **false** , um Legacy-Regeln zu verwenden.|Gibt an, ob SQL-92-Regeln für Bezeichner in Anführungszeichen (1 oder **"true"**) oder ältere Transact-SQL-Regeln (0 oder **"false"**).|**"true"** (1)|  
|ReturnDatesAsStrings<br /><br />(vom PDO_SQLSRV-Treiber nicht unterstützt)|1 oder **true** , um Datums- und Uhrzeittypen als Zeichenfolgen zurückzugeben.<br /><br />0 oder **false** um Datums- und Uhrzeittypen als PHP **DateTime** - Typen zurückzugeben.|Ruft Datums- und Uhrzeittypen (datetime, date, time, datetime2 und datetimeoffset) als Zeichenfolgen oder als PHP-Typen ab. Wenn Sie denPDO_SQLSRV-Treiber verwenden, werden Datumsangaben als Zeichenfolgen zurückgegeben. Der PDO_SQLSRV-Treiber hat keinen **"DateTime"** Typ.<br /><br />Weitere Informationen finden Sie unter [So wird's gemacht: Datums- und Uhrzeittypen mittels des SQLSRV-Treibers als Zeichenfolgen abrufen](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).|**false**|  
|Bildlauffähigkeit|String|„gepuffert“ bedeutet, dass Sie einen clientseitigen (gepufferten) Cursor möchten, mit dem Sie ein komplettes Resultset im Arbeitsspeicher zwischenspeichern können. Weitere Informationen finden Sie unter [Cursortypen &#40;SQLSRV-Treiber&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).|Vorwärtscursor|  
|Server<br /><br />(im SQLSRV-Treiber nicht unterstützt)|String|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz, mit der eine Verbindung hergestellt werden soll.<br /><br />Sie können auch einen virtuellen Netzwerknamen angeben, um eine Verbindung mit einer AlwaysOn-Availability-Gruppe herzustellen. Weitere Informationen zu [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Unterstützung für [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], finden Sie unter [Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|„Server“ ist ein erforderliches Schlüsselwort (wobei es nicht das erste Schlüsselwort in der Verbindungszeichenfolge sein muss). Wenn ein Servername nicht an das Schlüsselwort übergeben wird, wird versucht, eine Verbindung mit der lokalen Instanz herstellen.<br /><br />Der an „Server“ übergebene Wert kann der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz oder die IP-Adresse der Instanz sein. Sie können optional eine Portnummer angeben (z. B. `sqlsrv:server=(local),1033`).<br /><br />Ab Version 3.0 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] können Sie auch eine LocalDB-Instanz mit `server=(localdb)\instancename`angeben. Weitere Informationen finden Sie unter [-Unterstützung für LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).|  
|TraceFile|String|Gibt den Pfad für die Datei an, die für Ablaufverfolgungsdaten verwendet wird.|Kein Wert festgelegt.|  
|TraceOn|1 oder **true** zum Aktivieren der Ablaufverfolgung.<br /><br />0 oder **false** zum Deaktivieren der Ablaufverfolgung.|Gibt an, ob die ODBC-Protokollierung aktiviert ist (1 oder **"true"**) oder deaktiviert (0 oder **"false"**) für die Verbindung aufgebaut werden.|**"false"** (0)|  
|TransactionIsolation|Der SQLSRV-Treiber verwendet die folgenden Werte:<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />Der PDO_SQLSRV-Treiber verwendet die folgenden Werte:<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|Bestimmt die Isolationsstufe für die Transaktionen.<br /><br />Weitere Informationen zur Transaktionsisolation, finden Sie unter [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) in der SQL Server-Dokumentation.|SQLSRV_TXN_READ_COMMITTED<br /><br />oder<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|**Aktiviert** oder **deaktiviert**|Wirkt sich auf die Verbindungssequenz, die Problembehebung der ersten IP-Adresse des dem Hostnamen nicht reagiert und es gibt mehrere IP-Adressen, die den Hostnamen zugeordnet ist.<br /><br />Er interagiert mit MultiSubnetFailover anderen Verbindung Sequenzen angeben. Weitere Informationen finden Sie unter [mithilfe transparenten Netzwerk IP-Auflösung](https://docs.microsoft.com/en-us/sql/connect/odbc/using-transparent-network-ip-resolution).|Aktiviert|
|TrustServerCertificate|1 oder **true** , um dem Zertifikat zu vertrauen.<br /><br />0 oder **false** , um dem Zertifikat nicht zu vertrauen.|Gibt an, ob der Client als vertrauenswürdig behandeln soll (1 oder **"true"**) oder ablehnen (0 oder **"false"**) ein selbst signiertes Serverzertifikat.|**"false"** (0)|  
|UID<br /><br />(vom PDO_SQLSRV-Treiber nicht unterstützt)|String|Gibt an, die Benutzer-ID, die verwendet werden, bei der Verbindung mit SQL Server-Authentifizierung<sup>4</sup>.|Kein Wert festgelegt.|  
|WSID|String|Gibt den Namen des Computers für die Ablaufverfolgung an.|Kein Wert festgelegt.|  

1. Die `ConnectionPooling` Attribut kann nicht verwendet werden, zum Aktivieren/Deaktivieren Verbindungspooling in Linux und Mac Finden Sie unter [Verbindungspooling (Microsoft Drivers for PHP for SQLServer)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).

2. Alle für die hergestellte Verbindung ausgeführten Abfragen erfolgen an der Datenbank, indem angegeben wird, die *Datenbank* Attribut. Wenn der Benutzer die entsprechenden Berechtigungen verfügt, können jedoch Daten in anderen Datenbanken zugegriffen werden mithilfe eines vollqualifizierten Namens. Z. B. wenn die *master* Datenbank festgelegt ist, mit der *Datenbank* Verbindungsattribut, es ist weiterhin möglich, eine Transact-SQL-Abfrage auszuführen, die greift auf die *AdventureWorks.HumanResources.Employee* Tabelle mit dem vollqualifizierten Namen.  

3. Aktivieren von *Verschlüsselung* beeinträchtigt die Leistung einiger Anwendungen aufgrund des aufwändigen Berechnungsprozesses, der erforderlich ist, um Daten zu verschlüsseln.  

4. Die *UID* -Authentifizierung müssen sowohl das *PWD* - als auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Attribut festgelegt sein.  

Viele der unterstützten Schlüssel sind ODBC-Verbindungszeichenfolgen-Attribute. Informationen zu ODBC-Verbindungszeichenfolgen finden Sie unter [Using Connection String Keywords with SQL Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  

## <a name="see-also"></a>Siehe auch  
[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)  
