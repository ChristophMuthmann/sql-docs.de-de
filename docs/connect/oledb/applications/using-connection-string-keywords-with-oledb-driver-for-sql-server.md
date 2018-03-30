---
title: Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQLServer | Microsoft Docs
description: Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 776562d89a12b544d6edbe475358067b39b58988
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Einige OLE DB-Treiber für SQL Server-APIs mit der Angabe von Verbindungsattributen Verbindungszeichenfolgen. Verbindungszeichenfolgen sind Listen von Schlüsselwörtern und zugehörigen Werten. Jedes Schlüsselwort bezeichnet ein spezielles Verbindungsattribut.  
  
> **Hinweis:** OLE DB-Treiber für SQL Server ermöglicht Mehrdeutigkeit in Verbindungszeichenfolgen zur Abwärtskompatibilität (z. B. einige Schlüsselwörter können mehr als einmal angegeben werden, und konfliktverursachende Schlüsselwörter können mit einer Auflösung basierend auf beiden Seiten zulässig sein, oder Rangfolge). Zukünftige Versionen von OLE DB-Treiber für SQL Server u. u. nicht Mehrdeutigkeit in Verbindungszeichenfolgen zu. Es wird empfohlen, beim Ändern von Anwendungen, OLE DB-Treiber für SQL Server zu verwenden, um eine Abhängigkeit von Mehrdeutigkeit von Verbindungszeichenfolgen zu vermeiden.  
  
 In den folgenden Abschnitten werden die Schlüsselwörter, die mit dem OLE DB-Treiber für SQL Server und ActiveX Data Objects (ADO) verwendet werden können bei Verwendung von OLE DB-Treiber für SQL Server als Datenanbieter beschrieben.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB Driver Connection String Keywords  
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
|**Adresse**|SSPROP_INIT_NETWORKADDRESS|Die Netzwerkadresse des Servers, auf dem eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird. **Adresse** ist normalerweise der Netzwerkname des Servers, jedoch andere Namen, z. B. einer Pipe, eine IP-Adresse oder eine TCP/IP-Port und eine Socketadresse Adresse.<br /><br /> Wenn Sie eine IP-Adresse angeben, stellen Sie im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Manager sicher, dass die Protokolle für TCP/IP oder Named Pipes aktiviert sind.<br /><br /> Der Wert der **Adresse** hat Vorrang vor der an übergebene Wert **Server** in Verbindungszeichenfolgen, die bei Verwendung von OLE DB-Treiber für SQL Server. Beachten Sie, dass `Address=;` wird mit den im Servernamen angegebenen Verbinden der **Server** -Schlüsselwort, wohingegen `Address= ;, Address=.;`, `Address=localhost;`, und `Address=(local);` alle dazu führen, dass eine Verbindung mit dem lokalen Server.<br /><br /> Die vollständige Syntax für die **Adresse** Schlüsselwort lautet wie folgt:<br /><br /> [*Protokoll ***:**]*Adresse*[**, *** Port &#124;\pipe\pipename*]<br /><br /> *Protokoll* kann Folgendes sein: **tcp** (TCP/IP), **lpc** (Shared Memory) oder **np** (Named Pipes). Weitere Informationen zu Protokollen finden Sie unter [Konfigurieren von Clientprotokollen](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Wenn weder *Protokoll* noch die **Netzwerk** -Schlüsselwort angegeben wird, OLE DB-Treiber für SQL Server verwendet die Protokollreihenfolge im angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *Port* ist der Port für die Verbindung, auf dem angegebenen Server. In der Standardeinstellung verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] den Port 1433.|   
|**APP**|SSPROP_INIT_APPNAME|Die Zeichenfolge, die die Anwendung identifiziert.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.<br /><br /> Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu OLE DB-Treiber für SQL Server Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Der Name der Primärdatenbank (einschließlich des vollständigen Pfadnamens) einer anfügbaren Datenbank. Mit **AttachDBFileName**, müssen Sie auch den Datenbanknamen angeben, mit der Datenbank Schlüsselwort Anbieterzeichenfolge angegeben. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an (die angefügte Datenbank wird standardmäßig für die Verbindung verwendet).|  
|**Automatisch übersetzen**|SSPROP_INIT_AUTOTRANSLATE|Synonym für "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Konfiguriert die OEM-/ANSI-Zeichenübersetzung. Gültige Werte sind "yes" und "no".|  
|**Datenbank**|DBPROP_INIT_CATALOG|Der Datenbankname.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Gibt den Modus des datentypverarbeitung Verwendung. Zulässig sind der Wert "0" für Anbieterdatentypen und der Wert "80" für SQL Server 2000-Datentypen.|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|Gibt an, ob Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen. Mögliche Werte sind "yes" und "no". Der Standardwert lautet "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Der Name des für die Datenbankspiegelung zu verwendenden Failoverservers.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Eine leere Zeichenfolge bewirkt, dass OLE DB-Treiber für SQL Server standardmäßig vom Anbieter generierten SPN verwendet.|  
|**Sprache**|SSPROPT_INIT_CURRENTLANGUAGE|Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprache.|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung, wenn auf dem Server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird. Mögliche Werte sind "yes" und "no". Der Standardwert lautet "no".|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|Synonym für "Network".|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|Die Netzwerkbibliothek, die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation verwendet wird.|  
|**Netzwerkbibliothek**|SSPROP_INIT_NETWORKLIBRARY|Synonym für "Network".|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|Netzwerkpaketgröße. Der Standardwert ist 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Akzeptiert die Zeichenfolgen "yes" und "no" als Werte. Wenn "no" angegeben wird, darf das Datenquellenobjekt keine vertraulichen Authentifizierungsinformationen persistent speichern.|  
|**PWD**|DBPROP_AUTH_PASSWORD|Das Anmeldekennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz. Als Wert muss entweder der Name eines Servers im Netzwerk, eine IP-Adresse oder der Aliasname eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurations-Managers angegeben werden.<br /><br /> Ohne Angabe eines Namens wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Die **Adresse** Schlüsselwort überschreibt die **Server** Schlüsselwort.<br /><br /> Sie können eine Verbindung mit der Standardinstanz auf dem lokalen Server herstellen, durch Angabe einer der folgenden:<br /><br /> **Server =;**<br /><br /> **Server=.;**<br /><br /> **Server=(Local);;**<br /><br /> **Server=(Local);;**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(LocalDB)\\**  *Instancename* **;**<br /><br /> Weitere Informationen zur Unterstützung von LocalDB finden Sie unter [OLE DB-Treiber für SQL Server-Unterstützung für LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md).<br /><br /> Angeben eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Anfügen  **\\ ***InstanceName*.<br /><br /> Wenn kein Server angegeben ist, wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Wenn Sie eine IP-Adresse angeben, stellen Sie sicher, dass die TCP/IP oder named Pipes, in aktiviert sind [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> Die vollständige Syntax für die **Server** Schlüsselwort lautet wie folgt:<br /> <br /> **Server =**[*Protokoll***:**] *Server*[**, *** Port*]<br /><br /> *Protokoll* kann Folgendes sein: **tcp** (TCP/IP), **lpc** (Shared Memory) oder **np** (Named Pipes).<br /><br /> Im folgenden Beispiel wird die Angabe einer Named Pipe veranschaulicht:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Diese Zeile gibt das Named Pipe-Protokoll, eine Named Pipe auf dem lokalen Computer (`\\.\pipe`), den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz (`MSSQL$MYINST01`) und den Standardnamen der Named Pipe (`sql/query`) an.<br /><br /> Wenn weder ein *Protokoll* noch die **Netzwerk** -Schlüsselwort angegeben wird, OLE DB-Treiber für SQL Server verwendet die Protokollreihenfolge im angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *Port* ist der Port für die Verbindung, auf dem angegebenen Server. In der Standardeinstellung verwendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] den Port 1433.<br /><br /> Leerzeichen werden ignoriert, am Anfang der an übergebene Wert **Server** in Verbindungszeichenfolgen, die bei Verwendung von OLE DB-Treiber für SQL Server.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Eine leere Zeichenfolge bewirkt, dass OLE DB-Treiber für SQL Server standardmäßig vom Anbieter generierten SPN verwendet.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Der Zeitraum (in Sekunden), der bis zum Abschluss der Datenquelleninitialisierung abgewartet werden soll.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Wenn weist "yes" wird der OLE DB-Treiber für SQL Server, Windows-Authentifizierungsmodus zur Überprüfung der Anmeldung zu verwenden. Andernfalls weist der OLE DB-Treiber für SQL Server verwendet eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Benutzernamens und Kennworts für die Überprüfung der Anmeldung und die Schlüsselwörter UID und PWD angegeben werden.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Akzeptiert die Zeichenfolgen "yes" und "no" als Werte. Der Standardwert lautet "no" und bedeutet, dass das Serverzertifikat überprüft wird.|  
|**UID**|DBPROP_AUTH_USERID|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldename.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Dieses Schlüsselwort ist veraltet, und seine Einstellung wird von der OLE DB-Treiber für SQL Server ignoriert.|  
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
|**Anwendungszweck**|SSPROP_INIT_APPLICATIONINTENT|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.<br /><br /> Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu OLE DB-Treiber für SQL Server Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Automatisch übersetzen**|SSPROP_INIT_AUTOTRANSLATE|Synonym für "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Konfiguriert die OEM-/ANSI-Zeichenübersetzung. Zulässig sind die Werte "true" und "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Der Zeitraum (in Sekunden), der bis zum Abschluss der Datenquelleninitialisierung abgewartet werden soll.|  
|**Aktuelle Sprache**|SSPROPT_INIT_CURRENTLANGUAGE|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprachenname.|  
|**Datenquelle**|DBPROP_INIT_DATASOURCE|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz in der Organisation.<br /><br /> Ohne Angabe eines Namens wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Server** -Schlüsselwort, in diesem Thema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Gibt den Modus des datentypverarbeitung Verwendung. Zulässig sind der Wert "0" für Anbieterdatentypen und der Wert "80" für [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]-Datentypen.|  
|**Failoverpartner**|SSPROP_INIT_FAILOVERPARTNER|Der Name des für die Datenbankspiegelung zu verwendenden Failoverservers.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Eine leere Zeichenfolge bewirkt, dass OLE DB-Treiber für SQL Server standardmäßig vom Anbieter generierten SPN verwendet.|  
|**Anfangskatalog**|DBPROP_INIT_CATALOG|Der Datenbankname.|  
|**Anfangsdateiname**|SSPROP_INIT_FILENAME|Der Name der Primärdatenbank (einschließlich des vollständigen Pfadnamens) einer anfügbaren Datenbank. Mit **AttachDBFileName**, müssen Sie auch den Datenbanknamen angeben, mit der Datenbank Schlüsselwort Anbieterzeichenfolge angegeben. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an (die angefügte Datenbank wird standardmäßig für die Verbindung verwendet).|  
|**Integrierte Sicherheit**|DBPROP_AUTH_INTEGRATED|Akzeptiert den Wert "SSPI" für die Windows-Authentifizierung.|  
|**MARS-Verbindung**|SSPROP_INIT_MARSCONNECTION|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung. Zulässig sind die Werte "true" und "false". Der Standardwert lautet "false".|  
|**Netzwerkadresse**|SSPROP_INIT_NETWORKADDRESS|Die Netzwerkadresse einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Adresse** -Schlüsselwort, in diesem Thema.|  
|**Netzwerkbibliothek**|SSPROP_INIT_NETWORKLIBRARY|Die Netzwerkbibliothek, die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation verwendet wird.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Netzwerkpaketgröße. Der Standardwert ist 4096.|  
|**Kennwort**|DBPROP_AUTH_PASSWORD|Das Anmeldekennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Sicherheitsinformationen permanent speichern**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Wenn "false", wird das Datenquellenobjekt darf keine vertraulichen Authentifizierungsinformationen persistent speichern|  
|**Provider**||Dies sollte für OLE DB-Treiber für SQL Server "MSOLEDBSQL" sein.|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Eine leere Zeichenfolge bewirkt, dass OLE DB-Treiber für SQL Server standardmäßig vom Anbieter generierten SPN verwendet.|  
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
|**Anwendungszweck**|SSPROP_INIT_APPLICATIONINTENT|Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **ReadOnly** und **ReadWrite**.<br /><br /> Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu OLE DB-Treiber für SQL Server Unterstützung für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], finden Sie unter [OLE DB-Treiber für SQL Server-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**ApplicationName**|SSPROP_INIT_APPNAME|Die Zeichenfolge, die die Anwendung identifiziert.|  
|**Automatisch übersetzen**|SSPROP_INIT_AUTOTRANSLATE|Synonym für "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Konfiguriert die OEM-/ANSI-Zeichenübersetzung. Zulässig sind die Werte "true" und "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Der Zeitraum (in Sekunden), der bis zum Abschluss der Datenquelleninitialisierung abgewartet werden soll.|  
|**Aktuelle Sprache**|SSPROPT_INIT_CURRENTLANGUAGE|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sprachenname.|  
|**Datenquelle**|DBPROP_INIT_DATASOURCE|Der Name einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz in der Organisation.<br /><br /> Ohne Angabe eines Namens wird eine Verbindung mit der Standardinstanz auf dem lokalen Computer hergestellt.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Server** -Schlüsselwort, in diesem Thema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Gibt den Modus der zu verwendenden Datentypbehandlung an. Zulässig sind der Wert "0" für Anbieterdatentypen und der Wert "80" für SQL Server 2000-Datentypen.|  
|**Failoverpartner**|SSPROP_INIT_FAILOVERPARTNER|Der Name des für die Datenbankspiegelung zu verwendenden Failoverservers.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge. Eine leere Zeichenfolge bewirkt, dass OLE DB-Treiber für SQL Server standardmäßig vom Anbieter generierten SPN verwendet.|  
|**Anfangskatalog**|DBPROP_INIT_CATALOG|Der Datenbankname.|  
|**Anfangsdateiname**|SSPROP_INIT_FILENAME|Der Name der Primärdatenbank (einschließlich des vollständigen Pfadnamens) einer anfügbaren Datenbank. Mit **AttachDBFileName**, müssen Sie auch den Datenbanknamen angeben, mit der Datenbank Schlüsselwort Anbieterzeichenfolge angegeben. Wenn die Datenbank zuvor angefügt worden war, fügt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sie nicht erneut an (die angefügte Datenbank wird standardmäßig für die Verbindung verwendet).|  
|**Integrierte Sicherheit**|DBPROP_AUTH_INTEGRATED|Akzeptiert den Wert "SSPI" für die Windows-Authentifizierung.|  
|**MARS-Verbindung**|SSPROP_INIT_MARSCONNECTION|Ermöglicht oder unterbindet die Verwendung von mehreren aktiven Resultsets (MARS) bei einer Verbindung, wenn auf dem Server [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird. Zulässig sind die Werte "true" und "false". Der Standardwert lautet "false".|  
|**Netzwerkadresse**|SSPROP_INIT_NETWORKADDRESS|Die Netzwerkadresse einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation.<br /><br /> Weitere Informationen zur Syntax einer gültigen Adresse finden Sie unter der Beschreibung der **Adresse** -Schlüsselwort, in diesem Thema.|  
|**Netzwerkbibliothek**|SSPROP_INIT_NETWORKLIBRARY|Die Netzwerkbibliothek, die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Organisation verwendet wird.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Netzwerkpaketgröße. Der Standardwert ist 4096.|  
|**Kennwort**|DBPROP_AUTH_PASSWORD|Das Anmeldekennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Sicherheitsinformationen permanent speichern**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Wenn "false" angegeben wird, darf das Datenquellenobjekt keine vertraulichen Authentifizierungsinformationen persistent speichern.|  
|**Provider**||Dies sollte für OLE DB-Treiber für SQL Server "MSOLEDBSQL" sein.|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge. Eine leere Zeichenfolge bewirkt, dass OLE DB-Treiber für SQL Server standardmäßig vom Anbieter generierten SPN verwendet.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Akzeptiert die Zeichenfolgen "true" und "false" als Werte. Der Standardwert lautet "false" und bedeutet, dass das Serverzertifikat überprüft wird.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Gibt an, ob Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen. Mögliche Werte sind "true" und "false". Der Standardwert ist "false".|  
|**Benutzer-ID**|DBPROP_AUTH_USERID|Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldename.|  
|**Arbeitsstations-ID**|SSPROP_INIT_WSID|Der Bezeichner der Arbeitsstation.|  
  
 **Hinweis** In der Verbindungszeichenfolge, die "Old Password-Eigenschaft legt SSPROP_AUTH_OLD_PASSWORD fest, dies entspricht dem aktuellen (möglicherweise abgelaufenen) Kennwort, die nicht über eine anbieterzeichenfolgen-Eigenschaft verfügbar ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit OLE DB-Treiber für SQLServer](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
