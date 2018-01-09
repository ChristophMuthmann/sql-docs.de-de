---
title: "Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
caps.latest.revision: "81"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a2fa102ad8d3161d1311978048a4b272253671a3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Bei einigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client APIs werden Verbindungszeichenfolgen zur Angabe von Verbindungsattributen verwendet. Verbindungszeichenfolgen sind Listen von Schlüsselwörtern und zugehörigen Werten. Jedes Schlüsselwort bezeichnet ein spezielles Verbindungsattribut.  
  
> **Hinweis:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client lässt Mehrdeutigkeit in Verbindungszeichenfolgen zur Abwärtskompatibilität (z. B. einige Schlüsselwörter können mehr als einmal angegeben werden, und konfliktverursachende Schlüsselwörter können mit einer Auflösung basierend auf beiden Seiten zugelassen werden oder Rangfolge). Zukünftige Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client lassen möglicherweise keine Mehrdeutigkeit in Verbindungszeichenfolgen zu. Es empfiehlt sich beim Ändern von Anwendungen, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu verwenden, um eine Abhängigkeit von der Mehrdeutigkeit von Verbindungszeichenfolgen zu umgehen.  
  
 In den folgenden Abschnitten werden die Schlüsselwörter beschrieben, die mit dem OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, dem ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und ADO (ActiveX Data Objects) verwendet werden können, wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client als Datenanbieter verwendet wird.  
  
## <a name="odbc-driver-connection-string-keywords"></a>ODBC-Treiber Schlüsselwörter für Verbindungszeichenfolgen  
 ODBC-Anwendungen verwenden die Verbindungszeichenfolgen als Parameter an die [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) und [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) Funktionen.  
  
 Die für ODBC verwendeten Verbindungszeichenfolge haben folgende Syntax:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Attributwerte können optional in geschweifte Klammern eingeschlossen werden, und es wird empfohlen, dies zu tun. Dadurch werden Probleme vermieden, wenn Attributwerte andere Zeichen als alphanumerische Zeichen enthalten. Da die erste rechte geschweifte Klammer als Endzeichen des Werts interpretiert wird, können Werte keine rechten geschweiften Klammern enthalten.  
  
 In der folgenden Tabelle werden die Schlüsselwörter beschrieben, die in einer ODBC-Verbindungszeichenfolge verwendet werden können.  
  
|Schlüsselwort|Description|  
|-------------|-----------------|  
|**Addr**|Synonym für "Address".|  
|**Adresse**|Die Netzwerkadresse des Servers, auf dem eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird. **Adresse** ist normalerweise der Netzwerkname des Servers, jedoch andere Namen, z. B. einer Pipe, eine IP-Adresse oder eine TCP/IP-Port und eine Socketadresse Adresse.<br /><br /> Wenn Sie eine IP-Adresse angeben, stellen Sie im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Manager sicher, dass die Protokolle für TCP/IP oder Named Pipes aktiviert sind.<br /><br /> Der Wert der **Adresse** hat Vorrang vor der an übergebene Wert **Server** in ODBC-Verbindungszeichenfolgen Verwendung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Beachten Sie, dass `Address=;` wird mit den im Servernamen angegebenen Verbinden der **Server** -Schlüsselwort, wohingegen `Address= ;, Address=.;`, `Address=localhost;`, und `Address=(local);` alle dazu führen, dass eine Verbindung mit dem lokalen Server.<br /><br /> Die vollständige Syntax für die **Adresse** Schlüsselwort lautet wie folgt:<br /><br /> [*Protokoll***:**]*Adresse*[**,***-Ports &#124; \pipe\pipename*]<br /><br /> *Protokoll* kann Folgendes sein: **tcp** (TCP/IP), **lpc** (Shared Memory) oder **np** (Named Pipes). Weitere Informationen zu Protokollen finden Sie unter [Konfigurieren von Clientprotokollen](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Wenn weder *Protokoll* noch die **Netzwerk** Schlüsselwort angegeben ist, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwendet die Protokollreihenfolge im angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *Port* ist der Port für die Verbindung, auf dem angegebenen Server. In der Standardeinstellung verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] den Port 1433.|  
|**AnsiNPW**|Bei Angabe von "yes" verwendet der Treiber die im ANSI-Standard definierten Verhaltensweisen zum Behandeln von NULL-Vergleichen, Auffüllung mit Zeichendaten, Warnungen und NULL-Verkettungen. Bei Angabe von "no", werden die im ANSI-Standard definierten Verhaltensweisen nicht verwendet. Weitere Informationen zum Ansinpw-Verhalten finden Sie unter [Effekte von ISO-Optionen](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**APP**|Name der aufrufenden Anwendung [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) (optional). Wenn angegeben, wird dieser Wert gespeichert, der **master.dbo.sysprocesses** Spalte **Program_name** und wird zurückgegeben, indem [Sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) und [APP_NAME](../../../t-sql/functions/app-name-transact-sql.md) Funktionen.|  
|**ApplicationIntent**|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**. Die Standardeinstellung ist **ReadWrite**.  Beispiel:<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|Name der primären Datei einer anfügbaren Datenbank. Geben Sie den vollständigen Pfad an, und versehen Sie sämtliche umgekehrten Schrägstriche (\) mit Escapezeichen, wenn eine C-Zeichenfolgenvariable verwendet wird:<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> Diese Datenbank wird angefügt und als Standarddatenbank für die Verbindung verwendet. Mit **AttachDBFileName** müssen Sie auch den Datenbanknamen angeben, entweder in der [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) Datenbankparameter oder SQL_COPT_CURRENT_CATALOG-Verbindungsattribut. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an. Die angefügte Datenbank wird standardmäßig für die Verbindung verwendet.|  
|**"Autotranslate"**|Bei der Angabe von "yes" werden ANSI-Zeichenfolgen übersetzt, die zwischen Client und Server übermittelt werden, indem sie über Unicode konvertiert werden, um so Probleme bei der Zuordnung von Sonderzeichen zwischen den Codeseiten auf Client und Server zu minimieren.<br /><br /> SQL_C_CHAR-Clientdaten gesendet, um eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Char**, **Varchar**, oder **Text** Variablen,-Parameter oder-Spalten aus Zeichen in Unicode konvertiert, die Client-ANSI-Codepage (ACP) verwenden, wird eine Konvertierung von Unicode in Zeichen mithilfe der ACP des Servers.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**Char**, **Varchar**, oder **Text** an eine Clientvariable gesendete Daten von Zeichen in Unicode konvertiert, mit der Server-ACP ist, dann aus, wenn Zeichen mithilfe des Clients-ACP Unicode konvertiert.<br /><br /> Diese Konvertierungen werden vom ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client auf dem Client durchgeführt. Dies erfordert, dass auf dem Client die gleiche ACP verfügbar ist, die auf dem Server verwendet wird.<br /><br /> Diese Einstellungen haben keine Auswirkungen auf die Konvertierungen, die für diese Übertragungen stattfinden:<br /><br /> \*Unicode SQL_C_WCHAR-Clientdaten an gesendet **Char**, **Varchar**, oder **Text** auf dem Server.<br /><br /> \***Char**, **Varchar**, oder **Text** Serverdaten, die an eine Unicode SQL_C_WCHAR-Variable auf dem Client gesendet.<br /><br /> \*ANSI SQL_C_CHAR-Clientdaten in Unicode gesendet **Nchar**, **Nvarchar**, oder **Ntext** auf dem Server.<br /><br /> \*Unicode **Nchar**, **Nvarchar**, oder **Ntext** Serverdaten, die an eine ANSI-SQL_C_CHAR-Variable auf dem Client gesendet.<br /><br /> Bei Angabe von "no" wird keine Zeichenübersetzung durchgeführt.<br /><br /> Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber übersetzt keine Client ANSI-Zeichen SQL_C_CHAR-Daten gesendet, um **Char**, **Varchar**, oder **Text** Variablen, Parameter oder Spalten auf dem Server. Erfolgt keine Übersetzung auf **Char**, **Varchar**, oder **Text** an SQL_C_CHAR-Variablen, auf dem Client vom Server gesendeten Daten.<br /><br /> Wenn der Client und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterschiedliche ACPs verwenden, können Sonderzeichen falsch interpretiert werden.|  
|**Datenbank**|Der Name der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Standarddatenbank, die für die Verbindung verwendet wird. Wenn **Datenbank** nicht angegeben ist, die für die Anmeldung definierte Standarddatenbank verwendet. Die Standarddatenbank der ODBC-Datenquelle überschreibt die für die Anmeldung definierte Standarddatenbank. Die Datenbank muss eine vorhandene Datenbank sein, es sei denn, **AttachDBFileName** ist ebenfalls angegeben. Wenn **AttachDBFileName** ebenfalls angegeben wird, die primäre Datei, die er zeigt, angefügt und erhalten von der angegebene Datenbankname **Datenbank**.|  
|**Treiber**|Name des Treibers zurückgegebene [SQLDrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md). Der Schlüsselwortwert für den ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client lautet "{SQL Server Native Client 11.0}". Die **Server** -Schlüsselwort ist erforderlich, wenn **Treiber** angegeben ist und **DriverCompletion** auf SQL_DRIVER_NOPROMPT festgelegt.<br /><br /> Weitere Informationen zu Treibernamen finden Sie unter [unter Verwendung des SQL Server Native Client-Header und Bibliotheksdateien](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md).|  
|**DSN**|Der Name einer vorhandenen ODBC-Benutzer- oder Systemdatenquelle. Dieses Schlüsselwort überschreibt alle Werte, die in angegeben werden, können die **Server**, **Netzwerk**, und **Adresse** Schlüsselwörter.|  
|**Verschlüsseln**|Gibt an, ob Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen. Mögliche Werte sind "yes" und "no". Der Standardwert lautet "no".|  
|**Fallback**|Dieses Schlüsselwort ist veraltet, und seine Einstellung wird vom ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ignoriert.|  
|**Failover_Partner**|Name des Failoverpartnerservers, der verwendet werden soll, wenn keine Verbindung mit dem primären Server hergestellt werden kann.|  
|**FailoverPartnerSPN**|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Treiber generierten SPN verwendet.|  
|**Datei-DSN**|Der Name einer vorhandenen ODBC-Dateidatenquelle.|  
|**Sprache**|Name der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprache (optional). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]kann Nachrichten in mehreren Sprachen speichern **Sysmessages**. Wenn das Herstellen einer Verbindung mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit mehreren Sprachen **Sprache** gibt an, welcher Satz an Meldungen für die Verbindung verwendet werden.|  
|**MARS_Connection**|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung. Gültige Werte sind "yes" und "no". Der Standardwert ist "no".|  
|**MultiSubnetFailover**|Geben Sie immer **MultiSubnetFailover = Yes** beim Verbinden mit dem verfügbarkeitsgruppenlistener eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verfügbarkeitsgruppe oder einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failoverclusterinstanz. **MultiSubnetFailover = Yes** konfiguriert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client Schnellere Erkennung und Verbindung mit dem (gerade) aktiven Server bereitstellen. Mögliche Werte sind **Yes** und **No**. Die Standardeinstellung ist **keine**. Beispiel:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**NET**|Synonym für "Network".|  
|**Netzwerk**|Gültige Werte sind **Dbnmpntw** (named Pipes) und **Dbmssocn** (TCP/IP).<br /><br /> Es ist ein Fehler auf, geben Sie einen Wert für die **Netzwerk** Schlüsselwort auch einen Protokollpräfix auf die **Server** Schlüsselwort.|  
|**PWD**|Das Kennwort für das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldekonto, das im UID-Parameter angegeben ist. **PWD** muss nicht angegeben werden, wenn die Anmeldung ein NULL-Kennwort wurde oder bei Verwendung der Windows-Authentifizierung (`Trusted_Connection = yes`).|  
|**QueryLog_On**|Bei Angabe von "yes", wird die Protokollierung von langwierigen Abfragen für die Verbindung aktiviert. Bei Angabe von "no" werden keine Daten über langwierige Abfragen protokolliert.|  
|**QueryLogFile**|Vollständiger Pfad- und Dateiname einer Datei, die zur Protokollierung von Daten über Abfragen mit langer Ausführungsdauer verwendet werden soll.|  
|**QueryLogTime**|Ziffernzeichenfolge, die den Schwellenwert (in Millisekunden) zum Protokollieren von langwierigen Abfragen angibt. Jede Abfrage, die nicht innerhalb eines gewissen Zeitraums eine Antwort vom Server erhält, wird in die Protokolldatei für Abfragen langer Ausführungsdauer geschrieben.|  
|**QuotedId**|Bei Angabe von "yes" wird QUOTED_IDENTIFIER für die Verbindung auf ON festgelegt, und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] befolgt die ISO-Regeln hinsichtlich der Verwendung von Anführungszeichen in SQL-Anweisungen. Andernfalls wird QUOTED_IDENTIFIERS für die Verbindung auf OFF gesetzt. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] befolgt anschließend die [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Legacyregeln im Hinblick auf die Verwendung von Anführungszeichen in SQL-Anweisungen. Weitere Informationen finden Sie unter [Effekte von ISO-Optionen](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**Land/Region**|Bei Angabe von "yes" verwendet der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client die Clienteinstellungen, wenn Währungs-, Datums- oder Zeitdaten in Zeichendaten konvertiert werden. Die Konvertierung ist unidirektional. Der Treiber erkennt nur ODBC-Standardformate in zu konvertierenden Datumszeichenfolgen oder Währungswerten, beispielsweise Parameter in einer INSERT- oder UPDATE-Anweisung. Bei Angabe von "no" verwendet der Treiber ODBC-Standardzeichenfolgen zur Darstellung von Währungs-, Datums- und Zeitdaten, die in Zeichendaten konvertiert werden.|  
|**SaveFile**|Der Name einer ODBC-Datenquellendatei, in der die Attribute der aktuellen Verbindung gespeichert werden, wenn die Verbindung erfolgreich hergestellt wurde.|  
|**Server**|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz. Als Wert muss entweder der Name eines Servers im Netzwerk, eine IP-Adresse oder der Aliasname eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Managers angegeben werden.<br /><br /> Die **Adresse** Schlüsselwort überschreibt die **Server** Schlüsselwort.<br /><br /> Sie können eine Verbindung mit der Standardinstanz auf dem lokalen Server herstellen, durch Angabe einer der folgenden:<br /><br /> **Server =;**<br /><br /> **Server =.;**<br /><br /> **Server=(Local);;**<br /><br /> **Server=(Local);;**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(LocalDB)\\**  *Instancename* **;**<br /><br /> Weitere Informationen zur Unterstützung von LocalDB finden Sie unter [SQL Server Native Clientunterstützung für LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md).<br /><br /> Angeben eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Anfügen  **\\**  *InstanceName*.<br /><br /> Ohne Angabe eines Servers wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Wenn Sie eine IP-Adresse angeben, stellen Sie im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Manager sicher, dass die Protokolle für TCP/IP oder Named Pipes aktiviert sind.<br /><br /> Die vollständige Syntax für die **Server** Schlüsselwort lautet wie folgt:<br /><br /> **Server =**[*Protokoll***:**]*Server*[**,***Port*]<br /><br /> *Protokoll* kann Folgendes sein: **tcp** (TCP/IP), **lpc** (Shared Memory) oder **np** (Named Pipes).<br /><br /> Im folgenden Beispiel wird die Angabe einer Named Pipe veranschaulicht:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Diese Zeile gibt das Named Pipe-Protokoll, eine Named Pipe auf dem lokalen Computer (`\\.\pipe`), den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz (`MSSQL$MYINST01`) und den Standardnamen der Named Pipe (`sql/query`) an.<br /><br /> Wenn weder ein *Protokoll* noch die **Netzwerk** Schlüsselwort angegeben ist, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwendet die Protokollreihenfolge im angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *Port* ist der Port für die Verbindung, auf dem angegebenen Server. In der Standardeinstellung verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] den Port 1433.<br /><br /> Leerzeichen werden ignoriert, am Anfang der an übergebene Wert **Server** in ODBC-Verbindungszeichenfolgen Verwendung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**ServerSPN**|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Treiber generierten SPN verwendet.|  
|**StatsLog_On**|Durch die Angabe von "yes" wird die Aufzeichnung von Leistungsdaten zum ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native aktiviert. Wenn "no" angegeben wird, sind die Leistungsdaten zum ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client nicht für die Verbindung verfügbar.|  
|**StatsLogFile**|Der vollständige Pfad- und Dateiname einer Datei, die zum Aufzeichnen der statistischen Daten zur Leistung des ODBC-Treibers von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwendet werden soll.|  
|**Trusted_Connection**|Durch die Angabe von "yes" wird der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Native Client angewiesen, den Windows-Authentifizierungsmodus zur Überprüfung der Anmeldung zu verwenden. Andernfalls wird der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Native Client angewiesen, einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Benutzernamen und ein Kennwort zur Überprüfung der Anmeldung zu verwenden, und in diesem Fall müssen die Schlüsselwörter UID und PWD angegeben werden.|  
|**"TrustServerCertificate"**|Bei Verwendung mit **Encrypt**, wird die Verschlüsselung mit einem selbstsignierten Serverzertifikat aktiviert.|  
|**UID**|Ein gültiges [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldekonto. Bei Verwendung der Windows-Authentifizierung muss nicht UID angegeben werden.|  
|**UseProcForPrepare**|Dieses Schlüsselwort ist veraltet, und seine Einstellung wird ignoriert, durch die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber.|  
|**WSID**|Die ID der Arbeitsstation. Normalerweise ist dies der Netzwerkname des Computers, auf dem sich die Anwendung befindet (optional). Wenn angegeben, wird dieser Wert gespeichert, der **master.dbo.sysprocesses** Spalte **Hostname** und wird zurückgegeben, indem [Sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) und [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) Funktion.|  
  
> **Hinweis:** regionale Konvertierungseinstellungen gelten für währungs-, numerischen, Datums- und Uhrzeitdatentypen. Die Konvertierungseinstellung gilt nur für Ausgabekonvertierungen und ist nur sichtbar, wenn Währungs-, Zahlen-, Datums- oder Uhrzeitwerte in Zeichenfolgen konvertiert werden.  
  
 Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Native Client verwendet die für den aktuellen Benutzer geltenden Registrierungseinstellungen für das Gebietsschema. Der Treiber berücksichtigt das Gebietsschema des aktuellen Threads nicht, wenn die Anwendung nach der Verbindung durch, z. B. wird aufrufen **SetThreadLocale**.  
  
 Das Verändern des regionalen Verhaltens einer Datenquelle kann Anwendungsfehler verursachen. Eine Anwendung, die Datumszeichenfolgen analysiert und erwartet Datumszeichenfolgen angezeigt werden, gemäß der Definition von ODBC, kann beeinträchtigt werden, durch die Änderung dieses Werts.  
  
## <a name="ole-db-provider-connection-string-keywords"></a>Verbindungszeichenfolgen-Schlüsselwörter für den OLE DB-Anbieter  
 OLE DB-Anwendungen können Datenquellenobjekte auf zweierlei Weise initialisieren:  
  
-   **IDBInitialize:: Initialize**  
  
-   **IDataInitialize:: GetDatasource**  
  
 Im ersten Fall kann die Anbieterzeichenfolge zum Initialisieren der Verbindungseigenschaften verwendet werden, indem die DBPROP_INIT_PROVIDERSTRING-Eigenschaft im DBPROPSET_DBINIT-Eigenschaftensatz festgelegt wird. Im zweiten Fall kann eine Initialisierungszeichenfolge an übergeben werden **IDataInitialize:: GetDatasource** Methode, um die Verbindungseigenschaften zu initialisieren. Beide Methoden initialisieren die gleichen OLE DB-Verbindungseigenschaften, es werden jedoch andere Sätze von Schlüsselwörtern verwendet. Der Satz von Schlüsselwörtern, die verwendet werden, indem **IDataInitialize:: GetDatasource** ist mindestens die Beschreibung der Eigenschaften in der Gruppe der Initialisierungseigenschaften.  
  
 Bei jeder Anbieterzeichenfolgeneinstellung, für die eine zugehörige OLE DB-Eigenschaft vorhanden ist, die auf einen bestimmten Standardwert festgelegt ist oder auf einen spezifischen Wert festgelegt wird, überschreibt der OLE DB-Eigenschaftswert die Einstellung in der Anbieterzeichenfolge.  
  
 Für boolesche Eigenschaften, die in Anbieterzeichenfolgen über DBPROP_INIT_PROVIDERSTRING-Werte festgelegt werden, werden die Werte "yes" und "no" angegeben. Boolesche Eigenschaften in Initialisierungszeichenfolgen über **IDataInitialize:: GetDatasource** festgelegt werden, werden die Werte-"True" und "false".  
  
 Anwendungen mit **IDataInitialize:: GetDatasource** können auch von verwendeten Schlüsselwörter **IDBInitialize:: Initialize** jedoch nur für Eigenschaften, die nicht über einen Standardwert verfügen. Wenn eine Anwendung sowohl verwendet die **IDataInitialize:: GetDatasource** Schlüsselwort und die **IDBInitialize:: Initialize** Schlüsselwort in der Initialisierungszeichenfolge der **IDataInitialize:: GetDatasource** -schlüsselworteinstellung verwendet. Es wird dringend empfohlen, dass Anwendungen keine benutzen **IDBInitialize:: Initialize** Schlüsselwörter in **IDataInitialize: GetDatasource** Verbindungszeichenfolgen, da dieses Verhalten nicht in zukünftigen Versionen beibehalten werden kann.  
  
> [!NOTE]  
>  Eine Verbindungszeichenfolge übergeben **IDataInitialize:: GetDatasource** wird in Eigenschaften konvertiert und über angewendet **IDBProperties:: SetProperties**. Wenn Komponentendienste die eigenschaftenbeschreibung in gefunden **GetPropertyInfo**, wird diese Eigenschaft als eigenständige Eigenschaft angewendet werden. Andernfalls wird sie mithilfe der DBPROP_PROVIDERSTRING-Eigenschaft angewendet. Wenn Sie angeben, dass die Verbindungszeichenfolge z. B. **Data Source = server1; Server = server2**, **Datenquelle** wird als eine Eigenschaft festgelegt werden, aber **Server** geht in eine Anbieterzeichenfolge übernommen.  
  
 Wenn Sie mehrere Instanzen derselben anbieterspezifischen Eigenschaft angeben, wird der erste Wert der ersten Eigenschaft verwendet werden.  
  
 OLE DB-Anwendungen, die mit DBPROP_INIT_PROVIDERSTRING mit verwendeten Verbindungszeichenfolge **IDBInitialize:: Initialize** haben folgende Syntax:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Attributwerte können optional in geschweifte Klammern eingeschlossen werden, und es wird empfohlen, dies zu tun. Dadurch werden Probleme vermieden, wenn Attributwerte andere Zeichen als alphanumerische Zeichen enthalten. Da die erste rechte geschweifte Klammer als Endzeichen des Werts interpretiert wird, können Werte keine rechten geschweiften Klammern enthalten.  
  
 Ein Leerzeichen, nach dem Gleichheitszeichen (=) der ein Schlüsselwort für Verbindungszeichenfolgen als Literal interpretiert wird, selbst wenn der Wert in Anführungszeichen eingeschlossen ist.  
  
 In der folgenden Tabelle werden die Schlüsselwörter beschrieben, die mit DBPROP_INIT_PROVIDERSTRING verwendet werden können.  
  
|Schlüsselwort|Initialisierungseigenschaft|Description|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|Synonym für "Address".|  
|**Adresse**|SSPROP_INIT_NETWORKADDRESS|Die Netzwerkadresse einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Adresse** ODBC-Schlüsselworts weiter unten in diesem Thema.|  
|**APP**|SSPROP_INIT_APPNAME|Die Zeichenfolge, die die Anwendung identifiziert.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.<br /><br /> Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Der Name der Primärdatenbank (einschließlich des vollständigen Pfadnamens) einer anfügbaren Datenbank. Mit **AttachDBFileName**, müssen Sie auch den Datenbanknamen angeben, mit der Datenbank Schlüsselwort Anbieterzeichenfolge angegeben. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an (die angefügte Datenbank wird standardmäßig für die Verbindung verwendet).|  
|**Automatisch übersetzen**|SSPROP_INIT_AUTOTRANSLATE|Synonym für "AutoTranslate".|  
|**"Autotranslate"**|SSPROP_INIT_AUTOTRANSLATE|Konfiguriert die OEM-/ANSI-Zeichenübersetzung. Gültige Werte sind "yes" und "no".|  
|**Datenbank**|DBPROP_INIT_CATALOG|Der Datenbankname.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Gibt den Modus des datentypverarbeitung Verwendung. Zulässig sind der Wert "0" für Anbieterdatentypen und der Wert "80" für SQL Server 2000-Datentypen.|  
|**Verschlüsseln**|SSPROP_INIT_ENCRYPT|Gibt an, ob Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen. Mögliche Werte sind "yes" und "no". Der Standardwert lautet "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Der Name des für die Datenbankspiegelung zu verwendenden Failoverservers.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN verwendet.|  
|**Sprache**|SSPROPT_INIT_CURRENTLANGUAGE|Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprache.|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung, wenn auf dem Server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird. Mögliche Werte sind "yes" und "no". Der Standardwert lautet "no".|  
|**NET**|SSPROP_INIT_NETWORKLIBRARY|Synonym für "Network".|  
|**Netzwerk**|SSPROP_INIT_NETWORKLIBRARY|Die Netzwerkbibliothek, die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation verwendet wird.|  
|**Netzwerkbibliothek**|SSPROP_INIT_NETWORKLIBRARY|Synonym für "Network".|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|Netzwerkpaketgröße. Der Standardwert ist 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Akzeptiert die Zeichenfolgen "yes" und "no" als Werte. Wenn "no" angegeben wird, darf das Datenquellenobjekt keine vertraulichen Authentifizierungsinformationen persistent speichern.|  
|**PWD**|DBPROP_AUTH_PASSWORD|Das Anmeldekennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz in der Organisation.<br /><br /> Ohne Angabe eines Namens wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Server** ODBC-Schlüsselworts in diesem Thema.|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN verwendet.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Der Zeitraum (in Sekunden), der bis zum Abschluss der Datenquelleninitialisierung abgewartet werden soll.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Durch die Angabe von "yes" wird der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Native Client angewiesen, den Windows-Authentifizierungsmodus zur Überprüfung der Anmeldung zu verwenden. Andernfalls wird der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Native Client angewiesen, einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Benutzernamen und ein Kennwort zur Überprüfung der Anmeldung zu verwenden, und in diesem Fall müssen die Schlüsselwörter UID und PWD angegeben werden.|  
|**"TrustServerCertificate"**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Akzeptiert die Zeichenfolgen "yes" und "no" als Werte. Der Standardwert lautet "no" und bedeutet, dass das Serverzertifikat überprüft wird.|  
|**UID**|DBPROP_AUTH_USERID|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldename.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Dieses Schlüsselwort ist veraltet, und seine Einstellung wird vom OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ignoriert.|  
|**WSID**|SSPROP_INIT_WSID|Der Bezeichner der Arbeitsstation.|  
  
 OLE DB-Anwendungen verwendeten Verbindungszeichenfolge **IDataInitialize:: GetDatasource** haben folgende Syntax:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 Die Verwendung von Eigenschaften muss der jeweils dafür zulässigen Syntax entsprechen.  Beispielsweise **WSID** geschweifte Klammern (**"{}"**) Anführungszeichen und **Anwendungsname** verwendet einzelne (**"**)" oder "double (**"**) Anführungszeichen. Es können nur Zeichenfolgeneigenschaften in Anführungszeichen gesetzt werden. Wenn Sie versuchen, eine ganze Zahl oder eine aufgezählte Eigenschaft in Anführungszeichen zu setzen, wird der Fehler angezeigt, dass die Verbindungszeichenfolge keiner OLE DB-Spezifikation entspricht.  
  
 Attributwerte können optional in einfache oder doppelte Anführungszeichen gesetzt werden, und es wird empfohlen, dies zu tun. Dadurch werden Probleme vermieden, wenn Werte andere Zeichen als alphanumerische Zeichen enthalten. Das verwendete Anführungszeichen kann auch innerhalb von Werten stehen, vorausgesetzt, dass es doppelt angegeben wird.  
  
 Ein Leerzeichen, nach dem Gleichheitszeichen (=) der ein Schlüsselwort für Verbindungszeichenfolgen als Literal interpretiert wird, selbst wenn der Wert in Anführungszeichen eingeschlossen ist.  
  
 Wenn eine Verbindungszeichenfolge mehrere der in der folgenden Tabelle aufgeführten Eigenschaften aufweist, wird der Wert der letzten Eigenschaft verwendet.  
  
 Die folgende Tabelle beschreibt die Schlüsselwörter, die mit verwendet wird, **IDataInitialize:: GetDatasource**:  
  
|Schlüsselwort|Initialisierungseigenschaft|Description|  
|-------------|-----------------------------|-----------------|  
|**ApplicationName**|SSPROP_INIT_APPNAME|Die Zeichenfolge, die die Anwendung identifiziert.|  
|**Anwendungszweck**|SSPROP_INIT_APPLICATIONINTENT|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.<br /><br /> Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Automatisch übersetzen**|SSPROP_INIT_AUTOTRANSLATE|Synonym für "AutoTranslate".|  
|**"Autotranslate"**|SSPROP_INIT_AUTOTRANSLATE|Konfiguriert die OEM-/ANSI-Zeichenübersetzung. Zulässig sind die Werte "true" und "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Der Zeitraum (in Sekunden), der bis zum Abschluss der Datenquelleninitialisierung abgewartet werden soll.|  
|**Aktuelle Sprache**|SSPROPT_INIT_CURRENTLANGUAGE|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprachenname.|  
|**Datenquelle**|DBPROP_INIT_DATASOURCE|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz in der Organisation.<br /><br /> Ohne Angabe eines Namens wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Server** ODBC-Schlüsselworts weiter unten in diesem Thema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Gibt den Modus des datentypverarbeitung Verwendung. Zulässig sind der Wert "0" für Anbieterdatentypen und der Wert "80" für [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]-Datentypen.|  
|**Failoverpartner**|SSPROP_INIT_FAILOVERPARTNER|Der Name des für die Datenbankspiegelung zu verwendenden Failoverservers.|  
|**Failoverpartner-SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN verwendet.|  
|**Anfangskatalog**|DBPROP_INIT_CATALOG|Der Datenbankname.|  
|**Anfangsdateiname**|SSPROP_INIT_FILENAME|Der Name der Primärdatenbank (einschließlich des vollständigen Pfadnamens) einer anfügbaren Datenbank. Mit **AttachDBFileName**, müssen Sie auch den Datenbanknamen angeben, mit der Datenbank Schlüsselwort Anbieterzeichenfolge angegeben. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an (die angefügte Datenbank wird standardmäßig für die Verbindung verwendet).|  
|**Integrierte Sicherheit**|DBPROP_AUTH_INTEGRATED|Akzeptiert den Wert "SSPI" für die Windows-Authentifizierung.|  
|**MARS-Verbindung**|SSPROP_INIT_MARSCONNECTION|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung. Zulässig sind die Werte "true" und "false". Der Standardwert lautet "false".|  
|**Netzwerkadresse**|SSPROP_INIT_NETWORKADDRESS|Die Netzwerkadresse einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Adresse** ODBC-Schlüsselworts weiter unten in diesem Thema.|  
|**Netzwerkbibliothek**|SSPROP_INIT_NETWORKLIBRARY|Die Netzwerkbibliothek, die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation verwendet wird.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Netzwerkpaketgröße. Der Standardwert ist 4096.|  
|**Kennwort**|DBPROP_AUTH_PASSWORD|Das Anmeldekennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Wenn "false", wird das Datenquellenobjekt darf keine vertraulichen Authentifizierungsinformationen persistent speichern|  
|**Anbieter**||Bei der Verwendung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sollte die Angabe "SQLNCLI11" lauten.|  
|**Server-SPN**|SSPROP_INIT_SERVERSPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN verwendet.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Der Standardwert lautet "false" und bedeutet, dass das Serverzertifikat überprüft wird.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Gibt an, ob Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen. Mögliche Werte sind "true" und "false". Der Standardwert ist "false".|  
|**Benutzer-ID**|DBPROP_AUTH_USERID|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldename.|  
|**Arbeitsstations-ID**|SSPROP_INIT_WSID|Der Bezeichner der Arbeitsstation.|  
  
 **Hinweis** In der Verbindungszeichenfolge, die "Old Password-Eigenschaft legt SSPROP_AUTH_OLD_PASSWORD fest, dies entspricht dem aktuellen (möglicherweise abgelaufenen) Kennwort, die nicht über eine anbieterzeichenfolgen-Eigenschaft verfügbar ist.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Schlüsselwörter für ActiveX Data Objects (ADO)-Verbindungszeichenfolgen  
 ADO-Anwendungen legen die **"ConnectionString"** Eigenschaft **ADODBConnection** -Objekten fest oder stellen Sie eine Verbindungszeichenfolge als Parameter an die **öffnen** Methode **ADODBConnection** Objekte.  
  
 ADO-Anwendungen können auch die Schlüsselwörter verwendet die OLE DB- **IDBInitialize:: Initialize** Methode, jedoch nur für Eigenschaften, die nicht über einen Standardwert verfügen. Wenn eine Anwendung sowohl ADO-Schlüsselwörter verwendet und die **IDBInitialize:: Initialize** in der Initialisierungszeichenfolge angibt, die ADO-Schlüsselwörter verwendet werden. Es wird dringend empfohlen, dass Anwendungen nur Schlüsselwörter für ADO-Verbindungszeichenfolgen verwenden.  
  
 Die für ADO verwendeten Verbindungszeichenfolge haben folgende Syntax:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Attributwerte können optional in doppelte Anführungszeichen eingeschlossen werden, und es wird empfohlen, dies zu tun. Dadurch werden Probleme vermieden, wenn Werte andere Zeichen als alphanumerische Zeichen enthalten. Attributwerte dürfen keine doppelten Anführungszeichen enthalten.  
  
 In der folgenden Tabelle werden die Schlüsselwörter beschrieben, die in einer ADO-Verbindungszeichenfolge verwendet werden können.  
  
|Schlüsselwort|Initialisierungseigenschaft|Description|  
|-------------|-----------------------------|-----------------|  
|**Anwendungszweck**|SSPROP_INIT_APPLICATIONINTENT|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.<br /><br /> Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**ApplicationName**|SSPROP_INIT_APPNAME|Die Zeichenfolge, die die Anwendung identifiziert.|  
|**Automatisch übersetzen**|SSPROP_INIT_AUTOTRANSLATE|Synonym für "AutoTranslate".|  
|**"Autotranslate"**|SSPROP_INIT_AUTOTRANSLATE|Konfiguriert die OEM-/ANSI-Zeichenübersetzung. Zulässig sind die Werte "true" und "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Der Zeitraum (in Sekunden), der bis zum Abschluss der Datenquelleninitialisierung abgewartet werden soll.|  
|**Aktuelle Sprache**|SSPROPT_INIT_CURRENTLANGUAGE|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprachenname.|  
|**Datenquelle**|DBPROP_INIT_DATASOURCE|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz in der Organisation.<br /><br /> Ohne Angabe eines Namens wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Server** ODBC-Schlüsselworts in diesem Thema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Gibt den Modus der zu verwendenden Datentypbehandlung an. Zulässig sind der Wert "0" für Anbieterdatentypen und der Wert "80" für SQL Server 2000-Datentypen.|  
|**Failoverpartner**|SSPROP_INIT_FAILOVERPARTNER|Der Name des für die Datenbankspiegelung zu verwendenden Failoverservers.|  
|**Failoverpartner-SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN verwendet.|  
|**Anfangskatalog**|DBPROP_INIT_CATALOG|Der Datenbankname.|  
|**Anfangsdateiname**|SSPROP_INIT_FILENAME|Der Name der Primärdatenbank (einschließlich des vollständigen Pfadnamens) einer anfügbaren Datenbank. Mit **AttachDBFileName**, müssen Sie auch den Datenbanknamen angeben, mit der Datenbank Schlüsselwort Anbieterzeichenfolge angegeben. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an (die angefügte Datenbank wird standardmäßig für die Verbindung verwendet).|  
|**Integrierte Sicherheit**|DBPROP_AUTH_INTEGRATED|Akzeptiert den Wert "SSPI" für die Windows-Authentifizierung.|  
|**MARS-Verbindung**|SSPROP_INIT_MARSCONNECTION|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung, wenn auf dem Server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird. Zulässig sind die Werte "true" und "false". Der Standardwert lautet "false".|  
|**Netzwerkadresse**|SSPROP_INIT_NETWORKADDRESS|Die Netzwerkadresse einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Adresse** ODBC-Schlüsselworts in diesem Thema.|  
|**Netzwerkbibliothek**|SSPROP_INIT_NETWORKLIBRARY|Die Netzwerkbibliothek, die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation verwendet wird.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Netzwerkpaketgröße. Der Standardwert ist 4096.|  
|**Kennwort**|DBPROP_AUTH_PASSWORD|Das Anmeldekennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Wenn "false" angegeben wird, darf das Datenquellenobjekt keine vertraulichen Authentifizierungsinformationen persistent speichern.|  
|**Anbieter**||Bei der Verwendung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sollte die Angabe "SQLNCLI11" lauten.|  
|**Server-SPN**|SSPROP_INIT_SERVERSPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Die Angabe einer leeren Zeichenfolge bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN verwendet.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Der Standardwert lautet "false" und bedeutet, dass das Serverzertifikat überprüft wird.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Gibt an, ob Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen. Mögliche Werte sind "true" und "false". Der Standardwert ist "false".|  
|**Benutzer-ID**|DBPROP_AUTH_USERID|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldename.|  
|**Arbeitsstations-ID**|SSPROP_INIT_WSID|Der Bezeichner der Arbeitsstation.|  
  
 **Hinweis** In der Verbindungszeichenfolge, die "Old Password-Eigenschaft legt SSPROP_AUTH_OLD_PASSWORD fest, dies entspricht dem aktuellen (möglicherweise abgelaufenen) Kennwort, die nicht über eine anbieterzeichenfolgen-Eigenschaft verfügbar ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
