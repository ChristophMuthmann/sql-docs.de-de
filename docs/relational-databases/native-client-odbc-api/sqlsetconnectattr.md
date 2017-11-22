---
title: SQLSetConnectAttr | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLSetConnectAttr function
ms.assetid: d21b5cf1-3724-43f7-bc96-5097df0677b4
caps.latest.revision: "106"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b1441eed61d8efba39ee33ff17b8fc81b98a7ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sqlsetconnectattr"></a>SQLSetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ignoriert die Einstellung von SQL_ATTR_CONNECTION_TIMEOUT.  
  
 SQL_ATTR_TRANSLATE_LIB wird ebenfalls ignoriert. Die Angabe einer anderen Übersetzungsbibliothek wird nicht unterstützt. Um eine einfache Portierung von Anwendungen für die Verwendung eines Microsoft ODBC-Treibers für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu ermöglichen, wird jeder mit SQL_ATTR_TRANSLATE_LIB festgelegte Wert in einen Puffer im Treiber-Manager und aus diesem kopiert.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber implementiert wiederholbare Lesetransaktionsisolationen als serialisierbar.  
  
 Mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] wurde die Unterstützung von SQL_COPT_SS_TXN_ISOLATION, eines neuen Attributs für die Transaktionsisolation eingeführt. Durch Festlegen von SQL_COPT_SS_TXN_ISOLATION auf SQL_TXN_SS_SNAPSHOT wird angegeben, dass die Transaktion unter der Momentaufnahmeisolationsstufe ausgeführt wird.  
  
> [!NOTE]  
>  SQL_ATTR_TXN_ISOLATION kann verwendet werden, um alle anderen Isolationsstufen außer SQL_TXN_SS_SNAPSHOT festzulegen. Wenn Sie die Momentaufnahmeisolation verwenden möchten, müssen Sie SQL_TXN_SS_SNAPSHOT über SQL_COPT_SS_TXN_ISOLATION festlegen. Sie können die Isolationsstufe jedoch entweder mithilfe von SQL_ATTR_TXN_ISOLATION oder mithilfe von SQL_COPT_SS_TXN_ISOLATION abrufen.  
  
 Das Heraufstufen von ODBC-Anweisungsattributen auf Verbindungsattribute kann unerwartete Folgen haben. Anweisungsattribute, die Servercursorn für die Verarbeitung von Resultsets anfordern, können auf Verbindungsattribute heraufgestuft werden. Wenn Sie beispielsweise das ODBC-Anweisungsattribut SQL_ATTR_CONCURRENCY auf einen Wert festlegen, der restriktiver ist als der Standardwert, weist SQL_CONCUR_READ_ONLY den Treiber an, für alle Anweisungen, die für die Verbindung übermittelt werden, dynamische Cursor zu verwenden. Beim Ausführen einer ODBC-Katalogfunktion für eine Anweisung für die Verbindung wird SQL_SUCCESS_WITH_INFO und ein Diagnosedatensatz zurückgegeben, der angibt, dass das Cursorverhalten in schreibgeschützt geändert wurde. Beim Ausführen einer Transact-SQL SELECT-Anweisung mit einer COMPUTE-Klausel für dieselbe Verbindung tritt ein Fehler auf.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt eine Anzahl von treiberspezifischen Erweiterungen für ODBC-Verbindungsattribute, die in sqlncli.h definiert sind. Möglicherweise ist es für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber erforderlich, dass das Attribut vor der Verbindung festgelegt werden muss. Möglicherweise wird ein bereits festgelegtes Attribut jedoch ignoriert. In der folgenden Tabelle sind Einschränkungen aufgeführt.  
  
|SQL Server-Attribut|Festlegung vor oder nach Verbindung mit Server|  
|--------------------------|----------------------------------------------|  
|SQL_COPT_SS_ANSI_NPW|vor|  
|SQL_COPT_SS_APPLICATION_INTENT|vor|  
|SQL_COPT_SS_ATTACHDBFILENAME|vor|  
|SQL_COPT_SS_BCP|vor|  
|SQL_COPT_SS_BROWSE_CONNECT|vor|  
|SQL_COPT_SS_BROWSE_SERVER|vor|  
|SQL_COPT_SS_CONCAT_NULL|vor|  
|SQL_COPT_SS_CONNECTION_DEAD|Nach|  
|SQL_COPT_SS_ENCRYPT|vor|  
|SQL_COPT_SS_ENLIST_IN_DTC|Nach|  
|SQL_COPT_SS_ENLIST_IN_XA|Nach|  
|SQL_COPT_SS_FALLBACK_CONNECT|vor|  
|SQL_COPT_SS_FAILOVER_PARTNER|vor|  
|SQL_COPT_SS_INTEGRATED_SECURITY|vor|  
|SQL_COPT_SS_MARS_ENABLED|vor|  
|SQL_COPT_SS_MULTISUBMIT_FAILOVER|vor|  
|SQL_COPT_SS_OLDPWD|vor|  
|SQL_COPT_SS_PERF_DATA|Nach|  
|SQL_COPT_SS_PERF_DATA_LOG|Nach|  
|SQL_COPT_SS_PERF_DATA_LOG_NOW|Nach|  
|SQL_COPT_SS_PERF_QUERY|Nach|  
|SQL_COPT_SS_PERF_QUERY_INTERVAL|Nach|  
|SQL_COPT_SS_PERF_QUERY_LOG|Nach|  
|SQL_COPT_SS_PRESERVE_CURSORS|vor|  
|SQL_COPT_SS_QUOTED_IDENT|Sowohl als auch|  
|SQL_COPT_SS_TRANSLATE|Sowohl als auch|  
|SQL_COPT_SS_TRUST_SERVER_CERTIFICATE|vor|  
|SQL_COPT_SS_TXN_ISOLATION|Sowohl als auch|  
|SQL_COPT_SS_USE_PROC_FOR_PREP|Sowohl als auch|  
|SQL_COPT_SS_USER_DATA|Sowohl als auch|  
|SQL_COPT_SS_WARN_ON_CP_ERROR|vor|  
  
 Wenn ein Vorverbindungsattribut und der äquivalente [!INCLUDE[tsql](../../includes/tsql-md.md)]-Befehl für denselben Sitzung-, Datenbank- oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Status verwendet werden, kann ein unerwartetes Verhalten auftreten. Beispiel:  
  
```  
SQLSetConnectAttr(SQL_COPT_SS_QUOTED_IDENT, SQL_QI_ON) // turn ON via attribute  
SQLDriverConnect(…);  
SQLExecDirect("SET QUOTED_IDENTIFIER OFF") // turn OFF via Transact-SQL  
SQLSetConnectAttr(SQL_ATTR_CURRENT_CATALOG, …) // restores to pre-connect attribute value  
```  
  
## <a name="sqlcoptssansinpw"></a>SQL_COPT_SS_ANSI_NPW  
 SQL_COPT_SS_ANSI_NPW aktiviert oder deaktiviert die Verwendung der ISO-Behandlung von NULL in Vergleichen und Verkettungen, beim Auffüllen von Zeichendatentypen und Warnungen. Weitere Informationen finden Sie unter SET ANSI_NULLS, SET ANSI_PADDING, SET ANSI_WARNINGS und SET CONCAT_NULL_YIELDS_NULL.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_AD_ON|Standard. Die Verbindung verwendet das ANSI-Standardverhalten für die Behandlung von NULL-Vergleichen, für das Auffüllen, für Warnungen sowie für NULL-Verkettungen.|  
|SQL_AD_OFF|Die Verbindung verwendet das in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definierte Verhalten für die Behandlung von NULL, für das Auffüllen von Zeichendatentypen sowie für Warnungen.|  
  
 Wenn Sie Verbindungspooling verwenden, sollte der SQL_COPT_SS_ANSI_NPW in der Verbindungszeichenfolge angegeben werden, anstatt mit SQLSetConnectAttr festgelegt werden. Nach dem Herstellen einer Verbindung tritt ein Fehler ohne Benachrichtigung auf, wenn dieses Attribut bei der Verwendung von Verbindungspooling geändert wird.  
  
## <a name="sqlcoptssapplicationintent"></a>SQL_COPT_SS_APPLICATION_INTENT  
 Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Mögliche Werte sind **Readonly** und **ReadWrite**. Beispiel:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_APPLICATION_INTENT, TEXT("Readonly"), SQL_NTS)  
```  
  
 Die Standardeinstellung ist **ReadWrite**. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] Testreihen, finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqlcoptssattachdbfilename"></a>SQL_COPT_SS_ATTACHDBFILENAME  
 SQL_COPT_SS_ATTACHDBFILENAME gibt den Namen der primären Datei für eine anfügbare Datenbank an. Diese Datenbank wird angefügt und als Standarddatenbank für die Verbindung verwendet. Verwendung von SQL_COPT_SS_ATTACHDBFILENAME müssen Geben Sie den Namen der Datenbank als der Wert des Verbindungsattributs SQL_ATTR_CURRENT_CATALOG oder im DATABASE =-Parameter von einem [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md). Wenn die Datenbank bereits vorher angefügt wurde, wird sie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht erneut angefügt.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQLPOINTER auf eine Zeichenfolge|Die Zeichenfolge enthält den Namen der primären Datei für die anzufügende Datenbank. Sie enthält den Namen des vollständigen Pfads der Datei.|  
  
## <a name="sqlcoptssbcp"></a>SQL_COPT_SS_BCP  
 SQL_COPT_SS_BCP aktiviert Funktionen zum Massenkopieren für eine Verbindung. Weitere Informationen finden Sie unter [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md).  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_BCP_OFF|Standard. Funktionen zum Massenkopieren sind für die Verbindung nicht verfügbar.|  
|SQL_BCP_ON|Funktionen zum Massenkopieren sind für die Verbindung verfügbar.|  
  
## <a name="sqlcoptssbrowseconnect"></a>SQL_COPT_SS_BROWSE_CONNECT  
 Dieses Attribut wird verwendet, um zurückgegebenes Resultset anzupassen [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md). SQL_COPT_SS_BROWSE_CONNECT aktiviert oder deaktiviert die Rückgabe von weiteren Informationen von einer aufgelisteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Diese Informationen können Angaben dazu enthalten, ob sich der Server in einem Cluster befindet, und die Namen anderer Instanzen sowie die Versionsnummer angeben.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_MORE_INFO_NO|Standard. Gibt eine Liste mit Servern zurück.|  
|SQL_MORE_INFO_YES|**SQLBrowseConnect** eine erweiterte Zeichenfolge mit Servereigenschaften zurück.|  
  
## <a name="sqlcoptssbrowseserver"></a>SQL_COPT_SS_BROWSE_SERVER  
 Dieses Attribut wird verwendet, um zurückgegebenes Resultset anzupassen **SQLBrowseConnect**. SQL_COPT_SS_BROWSE_SERVER gibt den Servernamen für die **SQLBrowseConnect** gibt Informationen zurück.  
  
|Wert|Description|  
|-----------|-----------------|  
|computername|**SQLBrowseConnect** gibt eine Liste von Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem angegebenen Computer. Doppelten umgekehrten Schrägstriche (\\\\) sollte nicht für den Namen des Servers verwendet werden (z. B. anstelle von \\\MyServer "EigenerServer" verwendet werden soll).|  
|NULL|Standard. **SQLBrowseConnect** Informationen für alle Server in der Domäne zurückgegeben.|  
  
## <a name="sqlcoptssconcatnull"></a>SQL_COPT_SS_CONCAT_NULL  
 SQL_COPT_SS_CONCAT_NULL aktiviert oder deaktiviert die Verwendung der ISO-Behandlung von NULL beim Verketten von Zeichenfolgen. Weitere Informationen finden Sie unter SET CONCAT_NULL_YIELDS_NULL.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_CN_ON|Standard. Beim Verketten von Zeichenfolgen verwendet die Verbindung das ISO-Standardverhalten zum Behandeln von NULL-Werten.|  
|SQL_CN_OFF|Beim Verketten von Zeichenfolgen verwendet die Verbindung das in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definierte Verhalten zum Behandeln von NULL-Werten.|  
  
## <a name="sqlcoptssencrypt"></a>SQL_COPT_SS_ENCRYPT  
 Steuert die Verschlüsselung für eine Verbindung.  
  
 Bei der Verschlüsselung wird das Zertifikat auf dem Server verwendet. Dies muss von einer Zertifizierungsstelle überprüft werden, außer das Verbindungsattribut SQL_COPT_SS_TRUST_SERVER_CERTIFICATE ist auf SQL_TRUST_SERVER_CERTIFICATE_YES festgelegt oder die Verbindungszeichenfolge enthält "TrustServerCertificate=yes". Falls eine dieser Bedingungen zutrifft, kann ein vom Server generiertes und signiertes Zertifikat zum Verschlüsseln der Verbindung verwendet werden, wenn sich kein Zertifikat auf dem Server befindet.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_EN_ON|Die Verbindung wird verschlüsselt.|  
|SQL_EN_OFF|Die Verbindung wird nicht verschlüsselt. Dies ist die Standardeinstellung.|  
  
## <a name="sqlcoptssenlistindtc"></a>SQL_COPT_SS_ENLIST_IN_DTC  
 Der Client Ruft den Microsoft Distributed Transaction Coordinator (MS DTC) OLE DB- **ITransactionDispenser:: BeginTransaction** darstellt, die eine MS DTC-Transaktion zu starten und eine MS DTC-Transaktionsobjekt zu erstellen, die die Transaktion. Die Anwendung ruft dann **SQLSetConnectAttr** mit der SQL_COPT_SS_ENLIST_IN_DTC-Option, um die ODBC-Verbindung das Transaktionsobjekt zuzuordnen. Alle entsprechenden Datenbankaktivitäten werden unter dem Schutz der MS DTC-Transaktion durchgeführt. Ruft die Anwendung **SQLSetConnectAttr** mit SQL_DTC_DONE auf, um die Verbindung DTC-Zuordnung zu beenden.  
  
|Wert|Description|  
|-----------|-----------------|  
|DTC-Objekt*|Das MS DTC OLE-Transaktionsobjekt, das die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu exportierende Transaktion angibt.|  
|SQL_DTC_DONE|Begrenzt das Ende einer DTC-Transaktion.|  
  
## <a name="sqlcoptssenlistinxa"></a>SQL_COPT_SS_ENLIST_IN_XA  
 Um eine XA-Transaktion mit einem XA-kompatiblen Transaktion Prozessor (TP) beginnen, ruft der Client die Open Group **Tx_begin** Funktion. Die Anwendung ruft dann **SQLSetConnectAttr** mit SQL_COPT_SS_ENLIST_IN_XA-Parameter auf "true", die ODBC-Verbindung die XA-Transaktion zugeordnet werden soll. Alle entsprechenden Datenbankaktivitäten werden unter dem Schutz der XA-Transaktion durchgeführt. Um eine XA-Zuordnung mit einer ODBC-Verbindung zu beenden, muss der Client Aufrufen **SQLSetConnectAttr** mit SQL_COPT_SS_ENLIST_IN_XA-Parameter auf "false". Weitere Informationen finden Sie in der Dokumentation zu Microsoft Distributed Transaction Coordinator.  
  
## <a name="sqlcoptssfallbackconnect"></a>SQL_COPT_SS_FALLBACK_CONNECT  
 Dieses Attribut wird nicht mehr unterstützt.  
  
## <a name="sqlcoptssfailoverpartner"></a>SQL_COPT_SS_FAILOVER_PARTNER  
 Wird zum Angeben oder Abrufen des Namens des Failoverpartners verwendet, der für die Datenbankspiegelung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird. Hierbei handelt es sich um eine auf NULL endende Zeichenfolge, die vor dem Herstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] festgelegt werden muss.  
  
 Nach dem Herstellen der Verbindung kann die Anwendung Abfragen, dieses Attribut mithilfe [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) auf die Identität des Failoverpartners festzustellen. Wenn der primäre Server über keinen Failoverpartner verfügt, gibt diese Eigenschaft eine leere Zeichenfolge zurück. Dies ermöglicht einer intelligenten Anwendung den aktuell festgestellten Sicherungsserver in den Cache zu speichern. Jedoch sollte bei solchen Anwendungen darauf geachtet werden, dass die Informationen nur aktualisiert werden, wenn die Verbindung zum ersten Mal hergestellt (oder zurückgesetzt, falls in einem Pool) wird, und bei Langzeitverbindungen veralten kann.  
  
 Weitere Informationen finden Sie unter [verwenden der Datenbankspiegelung](../../relational-databases/native-client/features/using-database-mirroring.md).  
  
## <a name="sqlcoptssintegratedsecurity"></a>SQL_COPT_SS_INTEGRATED_SECURITY  
 SQL_COPT_SS_INTEGRATED_SECURITY erzwingt die Verwendung der Windows-Authentifizierung für die Überprüfung des Zugriffs bei der Serveranmeldung. Wenn Windows-Authentifizierung verwendet wird, ignoriert der Treiber als Teil der bereitgestellten Werte für Benutzer-ID und Kennwort **SQLConnect**, [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), oder [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)verarbeiten.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_IS_OFF|Standard. Zum Überprüfen von Benutzer-ID und Kennwort bei der Anmeldung wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.|  
|SQL_IS_ON|Zum Überprüfen der Zugriffsrechte eines Benutzers auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird der Windows-Authentifizierungsmodus verwendet.|  
  
## <a name="sqlcoptssmarsenabled"></a>SQL_COPT_SS_MARS_ENABLED  
 Dieses Attribut aktiviert oder deaktiviert MARS (Multiple Active Result Sets). MARS ist standardmäßig deaktiviert. Dieses Attribut muss vor dem Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] festgelegt werden. Nach dem Öffnen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bleibt MARS für die Dauer der Verbindung aktiviert oder deaktiviert.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_MARS_ENABLED_NO|Standard. MARS (Multiple Active Result Sets) ist deaktiviert.|  
|SQL_MARS_ENABLED_YES|MARS ist aktiviert.|  
  
 Weitere Informationen zu MARS finden Sie unter [mithilfe von Multiple Active Result Sets &#40; MARS &#41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
## <a name="sqlcoptssmultisubnetfailover"></a>SQL_COPT_SS_MULTISUBNET_FAILOVER  
 Wenn die Anwendung eine Verbindung zu einer [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Verfügbarkeitsgruppe in unterschiedlichen Subnetzen herstellt, wird durch diese Verbindungseigenschaft der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client so konfiguriert, dass der (gegenwärtig) aktive Server schneller erkannt und eine Verbindung schneller hergestellt wird. Beispiel:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MULTISUBMIT_FAILOVER, SQL_IS_ON, SQL_IS_INTEGER)  
```  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Unterstützung für [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] Testreihen, finden Sie unter [SQL Server Native Client unterstützt für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_IS_ON|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ermöglicht im Falle eines Failovers eine schnellere Wiederverbindung.|  
|SQL_IS_OFF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client stellt im Falle eines Failovers keine schnellere Wiederverbindung bereit.|  
  
## <a name="sqlcoptssoldpwd"></a>SQL_COPT_SS_OLDPWD  
 Der Ablauf von Kennwörtern bei der SQL Server-Authentifizierung wurde mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführt. Das SQL_COPT_SS_OLDPWD-Attribut wurde hinzugefügt, damit der Client sowohl das alte als auch das neue Kennwort für die Verbindung angeben kann. Wenn diese Eigenschaft festgelegt ist, verwendet der Anbieter für die erste Verbindung oder für nachfolgende Verbindungen keinen Verbindungspool, da die Verbindungszeichenfolge das "alte Kennwort" enthält, das inzwischen geändert wurde.  
  
 Weitere Informationen finden Sie unter [Kennwörter programmgesteuert ändern](../../relational-databases/native-client/features/changing-passwords-programmatically.md).  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_COPT_SS_OLD_PASSWORD|SQLPOINTER auf eine Zeichenfolge, die das alte Kennwort enthält. Dieser Wert ist lesegeschützt und muss vor der Verbindung mit dem Server festgelegt werden.|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA startet oder beendet die Protokollierung von Leistungsdaten. Der Name der Datenprotokolldatei muss vor Beginn der Datenprotokollierung festgelegt werden. Siehe SQL_COPT_SS_PERF_DATA_LOG weiter unten.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_PERF_START|Sorgt dafür, dass der Treiber mit dem Aufzeichnen von Leistungsdaten beginnt.|  
|SQL_PERF_STOP|Sorgt dafür, dass die Leistungsindikatoren die Aufzeichnung von Leistungsdaten beenden.|  
  
 Weitere Informationen finden Sie unter [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md).  
  
## <a name="sqlcoptssperfdatalog"></a>SQL_COPT_SS_PERF_DATA_LOG  
 SQL_COPT_SS_PERF_DATA_LOG weist den Namen der Protokolldatei zu, der verwendet wird, um Leistungsdaten aufzuzeichnen. Der Name der Protokolldatei ist je nach der Kompilierung der Anwendung eine auf NULL endende ANSI- oder Unicode-Zeichenfolge. Die *StringLength* -Argument sollte SQL_NTS sein.  
  
## <a name="sqlcoptssperfdatalognow"></a>SQL_COPT_SS_PERF_DATA_LOG_NOW  
 SQL_COPT_SS_PERF_DATA_LOG_NOW weist den Treiber an, einen Statistikprotokolleintrag auf den Datenträger zu schreiben. Die *StringLength* -Argument sollte SQL_NTS sein.  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 SQL_COPT_SS_PERF_QUERY startet oder beendet die Protokollierung für Abfragen mit langer Ausführungszeit. Der Name der Abfrageprotokolldatei muss vor Beginn der Protokollierung angegeben werden. Die Anwendung kann die "lange Ausführungszeit" durch Festlegen des Intervalls für die Protokollierung definieren.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_PERF_START|Startet die Protokollierung von Abfragen mit langer Ausführungszeit.|  
|SQL_PERF_STOP|Beendet die Protokollierung von Abfragen mit langer Ausführungszeit.|  
  
 Weitere Informationen finden Sie unter [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md).  
  
## <a name="sqlcoptssperfqueryinterval"></a>SQL_COPT_SS_PERF_QUERY_INTERVAL  
 SQL_COPT_SS_PERF_QUERY_INTERVAL legt den Schwellenwert für die Abfrageprotokollierung in Millisekunden fest. Abfragen, die nicht innerhalb des Schwellenwertes aufgelöst werden, werden in der Protokolldatei für Abfragen mit langer Ausführungszeit aufgezeichnet. Für den Abfrageschwellenwert gibt es keinen oberen Grenzwert. Bei einem Abfrageschwellenwert von Null werden alle Abfragen protokolliert.  
  
## <a name="sqlcoptssperfquerylog"></a>SQL_COPT_SS_PERF_QUERY_LOG  
 SQL_COPT_SS_PERF_QUERY_LOG weist den Namen einer Protokolldatei für die Aufzeichnung von Daten für eine Abfrage mit langer Ausführungszeit zu. Der Name der Protokolldatei ist je nach der Kompilierung der Anwendung eine auf NULL endende ANSI- oder Unicode-Zeichenfolge. Die *StringLength* -Argument sollte SQL_NTS oder die Länge der Zeichenfolge in Bytes.  
  
## <a name="sqlcoptsspreservecursors"></a>SQL_COPT_SS_PRESERVE_CURSORS  
 Mit diesem Attribut können Sie abfragen und festlegen, ob die Verbindung beim Durchführen eines Commits/Rollbacks für eine Transaktion den bzw. die Cursor beibehält. Die Einstellung ist entweder SQL_PC_ON oder SQL_PC_OFF. Der Standardwert ist SQL_PC_OFF. Diese Einstellung steuert, und zwar unabhängig davon, ob der Treiber die Cursor schließt für Sie geschlossen wird, wenn Sie aufrufen [SQLEndTran](../../relational-databases/native-client-odbc-api/sqlendtran.md) (oder SQLTransact).  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_PC_OFF|Standard. Cursor werden geschlossen, wenn die Transaktion einen Commit oder Rollback ist sichern mit **SQLEndTran**.|  
|SQL_PC_ON|Cursor werden nicht geschlossen, wenn die Transaktion einen Commit oder Rollback ist sichern mit **SQLEndTran**, es sei denn, einen statische oder keysetgesteuerte Cursor im asynchronen Modus verwendet. Wenn ein Rollback ausgegeben wird und das Auffüllen des Cursors noch nicht abgeschlossen ist, wird der Cursor geschlossen.|  
  
## <a name="sqlcoptssquotedident"></a>SQL_COPT_SS_QUOTED_IDENT  
 SQL_COPT_SS_QUOTED_IDENT lässt Bezeichner in Anführungszeichen in ODBC- und Transact-SQL-Anweisungen zu, die für die Verbindung übermittelt werden. Durch die Bereitstellung von Bezeichnern in Anführungszeichen lässt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ansonsten ungültige Objektnamen mit Leerzeichen wie "Meine Tabelle" zu. Weitere Informationen finden Sie unter SET QUOTED_IDENTIFIER.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_QI_OFF|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindung lässt keine Bezeichner in Anführungszeichen in gesendetem [!INCLUDE[tsql](../../includes/tsql-md.md)] zu.|  
|SQL_QI_ON|Standard. Die Verbindung lässt Bezeichner in Anführungszeichen in gesendetem [!INCLUDE[tsql](../../includes/tsql-md.md)] zu.|  
  
## <a name="sqlcoptsstranslate"></a>SQL_COPT_SS_TRANSLATE  
 SQL_COPT_SS_TRANSLATE bewirkt, dass der Treiber beim Austausch von MBCS-Daten Zeichen zwischen den Client- und Servercodeseiten übersetzt. Das Attribut wirkt sich nur in gespeicherte Daten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Char**, **Varchar**, und **Text** Spalten.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_XL_OFF|Der Treiber übersetzt beim Austausch von Zeichendaten zwischen dem Client und dem Server keine Zeichen von einer Codeseite in eine andere.|  
|SQL_XL_ON|Standard. Der Treiber übersetzt beim Austausch von Zeichendaten zwischen dem Client und dem Server Zeichen von einer Codeseite in eine andere. Der Treiber konfiguriert die Zeichenübersetzung automatisch und ermittelt dabei die auf dem Server installierte sowie die vom Client verwendete Codeseite.|  
  
## <a name="sqlcoptsstrustservercertificate"></a>SQL_COPT_SS_TRUST_SERVER_CERTIFICATE  
 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE bewirkt, dass der Treiber bei der Verwendung der Verschlüsselung die Zertifikatüberprüfung aktiviert oder deaktiviert. Bei diesem Attribut handelt es sich um einen Lese-/Schreibwert. Wenn er nach dem Herstellen einer Verbindung festgelegt wird, hat er jedoch keine Auswirkungen.  
  
 Clientanwendungen können diese Eigenschaft abfragen, nachdem eine Verbindung zur Feststellung der tatsächlich verwendeten Verschlüsselungs- und Validierungseigenschaften geöffnet wurde.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_TRUST_SERVER_CERTIFICATE_NO|Standard. Verschlüsselung ohne Zertifikatüberprüfung wird nicht aktiviert.|  
|SQL_TRUST_SERVER_CERTIFICATE_YES|Verschlüsselung ohne Zertifikatüberprüfung wird aktiviert.|  
  
## <a name="sqlcoptsstxnisolation"></a>SQL_COPT_SS_TXN_ISOLATION  
 SQL_COPT_SS_TXN_ISOLATION legt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifische Attribut für die Momentaufnahmeisolation fest. Momentaufnahmeisolation kann nicht mit SQL_ATTR_TXN_ISOLATION festgelegt werden, da es sich hierbei um einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen Wert handelt. Sie kann jedoch mit SQL_ATTR_TXN_ISOLATION oder mit SQL_COPT_SS_TXN_ISOLATION abgerufen werden.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_TXN_SS_SNAPSHOT|Gibt an, dass Sie von einer Transaktion aus keine Änderungen sehen können, die an anderen Transaktionen vorgenommen wurden, und dass Sie Änderungen auch dann nicht sehen können, wenn Sie diese erneut abfragen.|  
  
 Weitere Informationen zur momentaufnahmeisolation finden Sie unter [arbeiten mit Snapshot-Isolation](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="sqlcoptssuseprocforprep"></a>SQL_COPT_SS_USE_PROC_FOR_PREP  
 Dieses Attribut wird nicht mehr unterstützt.  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA legt den Benutzerdatenzeiger fest. Benutzerdaten werden im clienteigenen Arbeitsspeicher gespeichert und pro Verbindung aufgezeichnet.  
  
 Weitere Informationen finden Sie unter [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md).  
  
## <a name="sqlcoptsswarnoncperror"></a>SQL_COPT_SS_WARN_ON_CP_ERROR  
 Dieses Attribut legt fest, ob eine Warnung angezeigt wird, wenn bei der Konvertierung einer Codeseite Daten verloren gehen. Dies gilt nur für Daten, die vom Server stammen.  
  
|Wert|Description|  
|-----------|-----------------|  
|SQL_WARN_YES|Generiert Warnungen, wenn während der Codepagekonvertierung Daten verloren gehen.|  
|SQL_WARN_NO|(Standard) Generiert keine Warnungen, wenn während der Codepagekonvertierung Daten verloren gehen.|  
  
## <a name="sqlsetconnectattr-support-for-service-principal-names-spns"></a>SQLSetConnectAttr-Unterstützung für Dienstprinzipalnamen (SPNs)  
 SQLSetConnectAttr kann verwendet werden, um den Wert der neuen Verbindungsattribute SQL_COPT_SS_SERVER_SPN und SQL_COPT_SS_FAILOVER_PARTNER_SPN festzulegen. Diese Attribute können nicht festgelegt werden, wenn die Verbindung geöffnet ist. Wenn Sie versuchen, diese Attribute bei geöffneter Verbindung festzulegen, wird der Fehler HY011 mit der Meldung "Der Vorgang ist zu diesem Zeitpunkt ungültig" zurückgegeben. (SQLSetConnectOption kann auch verwendet werden, um diese Werte festgelegt wird.)  
  
 Weitere Informationen zu SPNs finden Sie unter [Dienstprinzipalnamen &#40; Dienstprinzipalnamen &#41; in Clientverbindungen &#40; ODBC &#41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 Dieses Attribut ist schreibgeschützt.  
  
 Weitere Informationen zu SQL_COPT_SS_CONNECTION_DEAD finden Sie unter [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) und [Herstellen einer Verbindung mit einer Datenquelle &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel werden Leistungsdaten protokolliert.  
  
```  
SQLPERF*     pSQLPERF;  
SQLINTEGER   nValue;  
  
// See if you are already logging. SQLPERF* will be NULL if not.  
SQLGetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA, &pSQLPERF,  
    sizeof(SQLPERF*), &nValue);  
  
if (pSQLPERF == NULL)  
    {  
    // Set the performance log file name.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG,  
        (SQLPOINTER) "\\My LogDirectory\\MyServerLog.txt", SQL_NTS);  
  
    // Start logging...  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
        (SQLPOINTER) SQL_PERF_START, SQL_IS_INTEGER);  
    }  
else  
    {  
    // Take a snapshot now so that your performance statistics are discernible.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
    }  
  
    // ...perform some action...  
  
// ...take a performance data snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
    // ...perform more actions...  
  
// ...take another snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
// ...and disable logging.  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
    (SQLPOINTER) SQL_PERF_STOP, SQL_IS_INTEGER);  
  
// Continue on...  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQLSetConnectAttr-Funktion](http://go.microsoft.com/fwlink/?LinkId=59368)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40; Transact-SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SQLPrepare-Funktion](http://go.microsoft.com/fwlink/?LinkId=59360)   
 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
  
