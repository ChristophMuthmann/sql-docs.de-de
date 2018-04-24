---
title: Microsoft OLE DB-Anbieter für Microsoft Jet | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 253de8c53055269efb6a9e15c9d9a5ca940606e8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft OLE DB-Anbieter für Microsoft Jet-Übersicht
Der OLE DB-Anbieter für Microsoft Jet können ADO auf Microsoft Jet-Datenbanken zugreifen.

## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen
 Zur Verbindung mit diesem Anbieter Festlegen der *Anbieter* Argument der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) -Eigenschaft wie folgt:

```
Microsoft.Jet.OLEDB.4.0
```

 Lesen der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft wird auch dieser Zeichenfolge zurück.

## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge
 Eine typische Verbindungszeichenfolge für diesen Anbieter ist:

```
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 Die Zeichenfolge, die dieser Schlüsselwörter besteht aus:

|Schlüsselwort|Description|
|-------------|-----------------|
|**Provider**|Gibt die OLE DB-Anbieter für Microsoft Jet.|
|**Datenquelle**|Gibt den Datenbanknamen Pfad und Dateinamen an (z. B. `c:\Northwind.mdb`).|
|**Benutzer-ID**|Gibt den Benutzernamen an. Wenn dieses Schlüsselwort nicht angegeben ist, die Zeichenfolge "`admin`", wird standardmäßig verwendet.|
|**Kennwort**|Gibt das Kennwort des Benutzers an. Wenn dieses Schlüsselwort nicht angegeben ist, die leere Zeichenfolge (""), wird standardmäßig verwendet.|

> [!NOTE]
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben **Trusted_Connection = Yes** oder **Integrated Security = SSPI** anstelle von Benutzer-ID und Kennwort die Informationen in der Verbindungszeichenfolge angegeben.

## <a name="provider-specific-connection-parameters"></a>Anbieterspezifische Verbindungsparameter
 Der OLE DB-Anbieter für Microsoft Jet unterstützt verschiedene anbieterspezifische Eigenschaften zusätzlich zu den, die vom ADO definiert sind. Wie bei allen anderen **Verbindung** sie können Parameter, festgelegt werden mithilfe der **Eigenschaften** Auflistung von der **Verbindung** Objekt oder als Teil der Verbindungszeichenfolge.

 In der folgenden Tabelle sind diese Eigenschaften zusammen mit den entsprechenden OLE DB-Eigenschaftsnamen in Klammern aufgeführt.

|Parameter|Description|
|---------------|-----------------|
|Jet OLEDB:Compact freigegebenen Speicherplatz Betrag (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|Gibt eine Schätzung des belegten Speicherplatz in Bytes, der freigegeben werden können, durch die Komprimierung der Datenbank an. Dieser Wert ist nur gültig, nachdem eine Verbindung hergestellt wurde.|
|Jet-OLEDB:Connection-Steuerelement (DBPROP_JETOLEDB_CONNECTIONCONTROL)|Gibt an, ob Benutzer eine Verbindung mit der Datenbank herstellen können.|
|Jet OLEDB: Systemdatenbank (DBPROP_JETOLEDB_CREATESYSTEMDATABASE) erstellen|Gibt an, ob eine Systemdatenbank erstellt werden soll, wenn eine neue Datenquelle zu erstellen.|
|Jet OLEDB: Database Sperrverhalten (DBPROP_JETOLEDB_DATABASELOCKMODE)|Gibt das Sperrverhalten für diese Datenbank an. Der erste Benutzer beim Öffnen der Datenbank bestimmt den Modus verwendet, während die Datenbank geöffnet ist.|
|Jet OLEDB: Database Password (DBPROP_JETOLEDB_DATABASEPASSWORD)|Gibt das Datenbankkennwort an.|
|Jet OLEDB: Kopieren Sie keine Gebietsschema auf Compact (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|Gibt an, ob Jet Gebietsschemainformationen beim Komprimieren einer Datenbank kopieren soll.|
|Jet OLEDB: Verschlüsseln der Datenbank (DBPROP_JETOLEDB_ENCRYPTDATABASE)|Gibt an, ob eine komprimierte Datenbank verschlüsselt werden soll. Wenn diese Eigenschaft nicht festgelegt ist, wird die komprimierte Datenbank verschlüsselt werden, wenn die ursprüngliche Datenbank ebenfalls verschlüsselt wurde.|
|Jet OLEDB:Engine Typ (DBPROP_JETOLEDB_ENGINE)|Gibt an, das Speichermodul verwendet, um die aktuellen Daten zuzugreifen.|
|Jet Exclusive Async Verzögerung (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|Gibt die maximale Zeitspanne in Millisekunden, die Jet verzögern kann asynchrone Schreibvorgänge auf Datenträger, wenn die Datenbank exklusiv genutzt wird.<br /><br /> Diese Eigenschaft wird ignoriert, es sei denn, **Jet OLEDB: Flush Transaktionstimeout** auf 0 festgelegt ist.|
|Jet OLEDB: Flush Transaktionstimeout (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|Gibt die Menge an Zeit warten, bevor Daten in einem Cache zum asynchronen schreiben tatsächlich geschrieben werden auf den Datenträger. Diese Einstellung überschreibt die Werte für **Jet OLEDB: Shared Async Delay** und **Jet Exclusive Async Delay**.|
|Jet OLEDB: globale Massentransaktionen (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|Gibt an, ob SQL Massentransaktionen sind.|
|Jet OLEDB: globale partielle Bulk Operations (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|Gibt das Kennwort, das beim Öffnen der Datenbank verwendet.|
|Jet OLEDB: ausdrückliches Commit-Synchronisierung (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|Gibt an, ob Änderungen, die in internen implizite Transaktionen vorgenommen wurden, im Modus für synchrone oder asynchrone geschrieben werden.|
|Jet OLEDB:Lock Verzögerung (DBPROP_JETOLEDB_LOCKDELAY)|Gibt die Anzahl der Millisekunden, die gewartet wird, bevor Sie versuchen, eine Sperre abzurufen, nachdem ein vorheriger Versuch fehlgeschlagen ist.|
|Jet OLEDB:Lock Wiederholung (DBPROP_JETOLEDB_LOCKRETRY)|Gibt an, wie oft versucht wird, eine gesperrte Seite zuzugreifen, wiederholt wird.|
|Jet OLEDB:Max Puffergröße (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Gibt die maximale Menge an Arbeitsspeicher in Kilobyte, Jet können vor dem Beginn Änderungen auf einem Datenträger gespeichert.|
|Jet OLEDB:Max Sperren pro Datei (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Gibt die maximale Anzahl von Sperren für eine Datenbank Jet platzieren kann. Der Standardwert ist 9500.|
|Jet OLEDB: neue Datenbankkennwort (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|Gibt das neue Kennwort für diese Datenbank festgelegt werden. Das alte Kennwort befindet sich in **Jet OLEDB: Database Password**.|
|Jet OLEDB: ODBC-Befehl-Timeout (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Gibt an, dass die Anzahl der Millisekunden, bevor eine ODBC-Remoteabfrage von Jet einen Timeout beendet wird.|
|Jet OLEDB:Page Sperren auf Tabellensperre (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Gibt an, wie viele Seiten innerhalb einer Transaktion gesperrt werden müssen, bevor Jet versucht wird, um die Sperre auf eine Tabellensperre höher zu stufen. Wenn dieser Wert 0 ist, wird die Sperre nie höher gestuft.|
|Jet OLEDB:Page Timeout (DBPROP_JETOLEDB_PAGETIMEOUT)|Gibt die Anzahl der Millisekunden, die Jet gewartet wird, bevor geprüft wird, ob der Cache mit der Datenbankdatei veraltet ist.|
|Jet OLEDB:Recycle Long-Wert-Seiten (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Gibt an, ob Jet aggressiv versuchen soll, um BLOB-Seiten freizugeben, wenn sie freigegeben werden.|
|Jet OLEDB:Registry Pfad (DBPROP_JETOLEDB_REGPATH)|Gibt an, die Windows-Registrierungsschlüssel, der Werte für das Jet-Datenbankmodul enthält.|
|Jet OLEDB:Reset ISAM Stats (DBPROP_JETOLEDB_RESETISAMSTATS)|Gibt an, ob das Schema **Recordset** DBSCHEMA_JETOLEDB_ISAMSTATS sollten Leistungsindikatoren zurücksetzen, nachdem er Leistungsinformationen zurückgegeben.|
|Jet OLEDB: Shared Async Verzögerung (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|Gibt die maximale Menge an Zeit in Millisekunden, Jet asynchrone Schreibvorgänge auf Datenträger, wenn die Datenbank, in den Mehrbenutzermodus geöffnet wird verzögern kann.|
|Jet OLEDB: System Database (DBPROP_JETOLEDB_SYSDBPATH)|Gibt den Pfad und Dateiname für Arbeitsgruppen-Informationsdatei (Systemdatenbank) an.|
|Jet OLEDB:Transaction Commit-Modus (DBPROP_JETOLEDB_TXNCOMMITMODE)|Gibt an, ob Jet Daten synchron auf den Datenträger schreibt, oder asynchron, wenn eine Transaktion ein Commit ausgeführt wird.|
|Jet OLEDB:User Commit Synchronisierung (DBPROP_JETOLEDB_USERCOMMITSYNC)|Gibt an, ob Änderungen, die in Transaktionen vorgenommen wurden, im Modus für synchrone oder asynchrone geschrieben werden.|

## <a name="provider-specific-recordset-and-command-properties"></a>Anbieterspezifische Recordset und Befehlseigenschaften
 Jet-Anbieters unterstützt auch mehrere anbieterspezifische **Recordset** und **Befehl** Eigenschaften. Diese Eigenschaften werden abgerufen, und legen Sie über die **Eigenschaften** Auflistung von der **Recordset** oder **Befehl** Objekt. Die Tabelle enthält den Namen der ADO-Eigenschaft und dem entsprechenden Namen der OLE DB-Eigenschaft in Klammern.

|Eigenschaftsname|Description|
|-------------------|-----------------|
|Jet OLEDB:Bulk Transaktionen (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|Gibt an, ob SQL-Massenvorgänge durchgeführt werden. Umfangreicher Massenvorgänge können fehlschlagen, wenn aufgrund von Verzögerungen bei der Ressource durchgeführt.|
|Jet OLEDB: Enable Fat Cursor (DBPROP_JETOLEDB_ENABLEFATCURSOR)|Gibt an, ob mehrere Zeilen beim Auffüllen eines Recordsets für remote Zeilenquellen Jet zwischengespeichert werden soll.|
|Jet OLEDB:Fat Cursor Cachegröße (DBPROP_JETOLEDB_FATCURSORMAXROWS)|Gibt die Anzahl der Zeilen in Cache an, wenn Remotedaten Zwischenspeichern verwenden. Dieser Wert wird ignoriert, es sei denn, **Jet OLEDB: Enable Fat Cursor** ist "true".|
|Jet OLEDB: inkonsistente (DBPROP_JETOLEDB_INCONSISTENT)|Gibt an, ob Abfrageergebnisse inkonsistente Updates zulassen.|
|Jet OLEDB: (DBPROP_JETOLEDB_LOCKGRANULARITY)-Granularität der Sperren|Gibt an, ob eine Tabelle mit der Sperren auf Zeilenebene geöffnet wird.|
|Jet OLEDB: ODBC Pass-Through-Anweisung (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Gibt an, dass Jet in den SQL-Text übergeben soll eine **Befehl** -Objekt, das Back-End unverändert.|
|Jet OLEDB:Partial Bulk Operations (DBPROP_JETOLEDB_BULKPARTIAL)|Gibt an des Jet-Verhalten, wenn SQL-DML-Vorgänge fehlschlagen.|
|Jet-OLEDB:Pass über Abfrage Bulk-Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|Gibt an, ob Abfragen, die keine Zurückgeben einer **Recordset** an die Datenquelle übergeben werden nicht verändert.|
|Jet OLEDB:Pass über Query-Verbindungszeichenfolge (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|Gibt an, die Jet-Verbindungszeichenfolge verwendet für die Verbindung mit einem remote-Datenspeicher. Dieser Wert wird ignoriert, es sei denn, **Jet OLEDB: ODBC Pass-Through-Anweisung** ist "true".|
|Jet OLEDB: gespeicherte Abfrage (DBPROP_JETOLEDB_STOREDQUERY)|Gibt an, ob der Befehlstext als gespeicherte Abfrage anstelle einer SQL-Befehl interpretiert werden sollen.|
|Jet OLEDB: Überprüfen Sie die Regeln im Satz (DBPROP_JETOLEDB_VALIDATEONSET)|Gibt an, ob die Jet-Validierungsregeln ausgewertet werden, wenn Spaltendaten festgelegt ist oder wenn die Änderungen an die Datenbank übergeben werden.|

 Standardmäßig wird der OLE DB-Anbieter für Microsoft Jet Microsoft Jet-Datenbanken im Lese-/Schreibmodus geöffnet. Um eine Datenbank im schreibgeschützten Modus geöffnet wird, legen Sie die [Modus](../../../ado/reference/ado-api/mode-property-ado.md) -Eigenschaft für das ADO **Verbindung** -Objekt **AdModeRead**.

## <a name="command-object-usage"></a>Befehlsobjekt-Verwendung
 Befehlstext in der [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt wird den Microsoft Jet-SQL-Dialekt verwendet. Sie können Abfragen Zeile zurückgeben, Aktionsabfragen und Tabellennamen im Befehlstext angeben. Allerdings werden die gespeicherte Prozeduren werden nicht unterstützt und sollte nicht angegeben werden.

## <a name="recordset-behavior"></a>Recordset-Verhalten
 Dynamische Cursor werden von der Microsoft Jet-Datenbankmodul nicht unterstützt. Der OLE DB-Anbieter für Microsoft Jet unterstützt daher keine der **AdLockDynamic** Cursortyp. Ein dynamic-Cursor angefordert wird, der Anbieter einen Keyset-Cursor zurück und Zurücksetzen der [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) Eigenschaft an, dass der Typ des [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) zurückgegeben. Wenn eine aktualisierbare darüber hinaus **Recordset** angefordert wird (**LockType** ist **AdLockOptimistic**, **AdLockBatchOptimistic**, oder **AdLockPessimistic**) des Anbieters ebenfalls einen Keyset-Cursor zurück und Zurücksetzen der **CursorType** Eigenschaft.

## <a name="dynamic-properties"></a>Dynamische Eigenschaften
 Der OLE DB-Anbieter für Microsoft Jet fügt verschiedene Eigenschaften in der **Eigenschaften** Auflistung von der geöffnete [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), und [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekte.

 Die folgenden Tabellen sind ein Cross-Index der ADO und OLE DB-Namen für jede dynamische Eigenschaft. Der OLE DB Programmer's Reference bezieht sich auf den Namen einer ADO-Eigenschaft von der Begriff "Description". Weitere Informationen zu diesen Eigenschaften finden Sie in der OLE DB Programmer's Reference.

## <a name="connection-dynamic-properties"></a>Dynamische Eigenschaften der Verbindung
 Die folgenden Eigenschaften werden hinzugefügt, um die **Eigenschaften** Auflistung von der **Verbindung** Objekt.

|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|
|-----------------------|--------------------------|
|Aktive Sitzungen|DBPROP_ACTIVESESSIONS|
|Asynchroner Abbruch|DBPROP_ASYNCTXNABORT|
|Asynchroner Commit|DBPROP_ASYNCTNXCOMMIT|
|Autocommit Isolation Levels|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|Speicherort des Katalogs|DBPROP_CATALOGLOCATION|
|Katalogbegriff|DBPROP_CATALOGTERM|
|Spaltendefinition|DBPROP_COLUMNDEFINITION|
|Aktuellen Katalog|DBPROP_CURRENTCATALOG|
|Datenquelle|DBPROP_INIT_DATASOURCE|
|Datenquellenname|RÜCKGABEWERT|
|Datenquellenobjekt Threadingmodell|DBPROP_DSOTHREADMODEL|
|Der DBMS-Name|DBPROP_DBMSNAME|
|DBMS-Version|DBPROP_DBMSVER|
|GROUP BY-Unterstützung|DBPROP_GROUPBY|
|Unterstützung von heterogenen Tabellen|DBPROP_HETEROGENEOUSTABLES|
|Bezeichner Groß-/Kleinschreibung|DBPROP_IDENTIFIERCASE|
|Isolationsstufen|DBPROP_SUPPORTEDTXNISOLEVELS|
|Isolation Aufbewahrung|DBPROP_SUPPORTEDTXNISORETAIN|
|Locale Identifier|DBPROP_INIT_LCID|
|Maximale Indexgröße|DBPROP_MAXINDEXSIZE|
|Maximale Zeilengröße|DBPROP_MAXROWSIZE|
|Maximale Zeilengröße schließt BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Maximale Anzahl von Tabellen in SELECT|DBPROP_MAXTABLESINSELECT|
|Modus|DBPROP_INIT_MODE|
|Mehrere Parametersätze|DBPROP_MULTIPLEPARAMSETS|
|Mehrere Ergebnisse|DBPROP_MULTIPLERESULTS|
|Mehrere Speicherobjekte|DBPROP_MULTIPLESTORAGEOBJECTS|
|Update mit mehreren Tabellen|DBPROP_MULTITABLEUPDATE|
|NULL-Sortierung|DBPROP_NULLCOLLATION|
|NULL-Verkettungsverhalten|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB-Version|DBPROP_PROVIDEROLEDBVER|
|Unterstützung für OLE-Objekt|DBPROP_OLEOBJECTS|
|Öffnen Sie die Schemarowset-Unterstützung|DBPROP_OPENROWSETSUPPORT|
|ORDER BY-Spalten in der Select-Liste|DBPROP_ORDERBYCOLUMNSINSELECT|
|Verfügbarkeit der Ausgabeparameter|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Übergeben von Ref Accessoren|DBPROP_BYREFACCESSORS|
|Kennwort|DBPROP_AUTH_PASSWORD|
|Persistenter ID-Typ|DBPROP_PERSISTENTIDTYPE|
|Abbruchverhalten vorbereiten|DBPROP_PREPAREABORTBEHAVIOR|
|Vorbereiten der Commitverhalten|DBPROP_PREPARECOMMITBEHAVIOR|
|Prozedur-Begriff|DBPROP_PROCEDURETERM|
|Eingabeaufforderung|DBPROP_INIT_PROMPT|
|Name des Anbieters|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|Version des Anbieters|DBPROP_PROVIDERVER|
|Nur-Lese Datenquelle|DBPROP_DATASOURCEREADONLY|
|Rowset-Konvertierungen zum Befehl ""|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|Schema-Begriff|DBPROP_SCHEMATERM|
|Schema-Verwendung|DBPROP_SCHEMAUSAGE|
|SQL-Unterstützung|DBPROP_SQLSUPPORT|
|Strukturierten Speicher|DBPROP_STRUCTUREDSTORAGE|
|Unterstützung für Unterabfragen|DBPROP_SUBQUERIES|
|Tabelle-Begriff|DBPROP_TABLETERM|
|DDL-Transaktion|DBPROP_SUPPORTEDTXNDDL|
|Benutzer-ID|DBPROP_AUTH_USERID|
|Benutzername|DBPROP_USERNAME|
|Das Fensterhandle|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Recordset dynamische Eigenschaften
 Die folgenden Eigenschaften werden hinzugefügt, um die **Eigenschaften** Auflistung von der **Recordset** Objekt.

|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|
|-----------------------|--------------------------|
|Access-Reihenfolge|DBPROP_ACCESSORDER|
|Nur Anhängen-Rowset|DBPROP_APPENDONLY|
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Lesezeichen sortiert|DBPROP_ORDEREDBOOKMARKS|
|Verzögerte Spalten Zwischenspeichern|DBPROP_CACHEDEFERRED|
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|
|Schreibbare Spalte|DBPROP_MAYWRITECOLUMN|
|Verzögern der Spalte|DBPROP_DEFERRED|
|Verzögerung Speicher Objekt Updates|DBPROP_DELAYSTORAGEOBJECTS|
|Rückwärts abrufen|DBPROP_CANFETCHBACKWARDS|
|Halten Sie Zeilen|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Nicht Mobile Zeilen|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|Auf das IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Literal Lesezeichen|DBPROP_LITERALBOOKMARKS|
|Literal Zeilenidentität|DBPROP_LITERALIDENTITY|
|Maximale Anzahl geöffneter Zeilen|DBPROP_MAXOPENROWS|
|Maximale Anzahl ausstehender Zeilen|DBPROP_MAXPENDINGROWS|
|Maximale Zeilenanzahl|DBPROP_MAXROWS|
|Speicherauslastung|DBPROP_MEMORYUSAGE|
|Benachrichtigung Granularität|DBPROP_NOTIFICATIONGRANULARITY|
|Benachrichtigungsphasen|DBPROP_NOTIFICATIONPHASES|
|Transaktive Objekte|DBPROP_TRANSACTEDOBJECT|
|Andere Änderungen sichtbar|DBPROP_OTHERUPDATEDELETE|
|Andere Einfügungen sichtbar|DBPROP_OTHERINSERT|
|Eigene Änderungen sichtbar zu machen|DBPROP_OWNUPDATEDELETE|
|Eigenen Einfügevorgänge sichtbar|DBPROP_OWNINSERT|
|Bei Abbruch erhalten|DBPROP_ABORTPRESERVE|
|Nach dem Commit beibehalten|DBPROP_COMMITPRESERVE|
|Schnelle Neustart|DBPROP_QUICKRESTART|
|Reentrant-Ereignisse|DBPROP_REENTRANTEVENTS|
|Entfernen von gelöschten Zeilen|DBPROP_REMOVEDELETED|
|Mehrere Änderungen zu melden|DBPROP_REPORTMULTIPLECHANGES|
|Ausstehende Einfügungen zurückgeben|DBPROP_RETURNPENDINGINSERTS|
|Zeile löschen-Benachrichtigung|DBPROP_NOTIFYROWDELETE|
|Benachrichtigung zur ersten Zeile|DBPROP_NOTIFYROWFIRSTCHANGE|
|Benachrichtigung für Zeile einfügen|DBPROP_NOTIFYROWINSERT|
|Zeile Berechtigungen|DBPROP_ROWRESTRICT|
|Zeile Neusynchronisierung-Benachrichtigung|DBPROP_NOTIFYROWRESYNCH|
|Zeile Threadingmodell|DBPROP_ROWTHREADMODEL|
|Zeile rückgängig-Änderungsbenachrichtigung|DBPROP_NOTIFYROWUNDOCHANGE|
|Delete-Benachrichtigung für Zeile rückgängig machen|DBPROP_NOTIFYROWUNDODELETE|
|Zeile rückgängig-Benachrichtigung|DBPROP_NOTIFYROWUNDOINSERT|
|Zeile Updatebenachrichtigung|DBPROP_NOTIFYROWUPDATE|
|Rowset-Fetch Position Änderungsbenachrichtigung|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Rowset-Freigabe-Benachrichtigung|DBPROP_NOTIFYROWSETRELEASE|
|Führen Sie einen Bildlauf rückwärts|DBPROP_CANSCROLLBACKWARDS|
|Gelöschte Lesezeichen überspringen|DBPROP_BOOKMARKSKIPPED|
|Starke Zeilenidentität|DBPROP_STRONGITDENTITY|
|Aktualisierbarkeit|DBPROP_UPDATABILITY|
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Dynamische Eigenschaften der Befehl
 Die folgenden Eigenschaften werden hinzugefügt, um die **Eigenschaften** Auflistung von der **Befehl** Objekt.

|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|
|-----------------------|--------------------------|
|Access-Reihenfolge|DBPROP_ACCESSORDER|
|Nur Anhängen-Rowset|DBPROP_APPENDONLY|
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|
|Verzögern der Spalte|DBPROP_DEFERRED|
|Verzögerung Speicher Objekt Updates|DBPROP_DELAYSTORAGEOBJECTS|
|Rückwärts abrufen|DBPROP_CANFETCHBACKWARDS|
|Halten Sie Zeilen|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Nicht Mobile Zeilen|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|Auf das IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Literal Lesezeichen|DBPROP_LITERALBOOKMARKS|
|Literal Zeilenidentität|DBPROP_LITERALIDENTITY|
|Sperrmodus|DBPROP_LOCKMODE|
|Maximale Anzahl geöffneter Zeilen|DBPROP_MAXOPENROWS|
|Maximale Anzahl ausstehender Zeilen|DBPROP_MAXPENDINGROWS|
|Maximale Zeilenanzahl|DBPROP_MAXROWS|
|Benachrichtigung Granularität|DBPROP_NOTIFICATIONGRANULARITY|
|Benachrichtigungsphasen|DBPROP_NOTIFICATIONPHASES|
|Transaktive Objekte|DBPROP_TRANSACTEDOBJECT|
|Andere Änderungen sichtbar|DBPROP_OTHERUPDATEDELETE|
|Andere Einfügungen sichtbar|DBPROP_OTHERINSERT|
|Eigene Änderungen sichtbar zu machen|DBPROP_OWNUPDATEDELETE|
|Eigenen Einfügevorgänge sichtbar|DBPROP_OWNINSERT|
|Bei Abbruch erhalten|DBPROP_ABORTPRESERVE|
|Nach dem Commit beibehalten|DBPROP_COMMITPRESERVE|
|Schnelle Neustart|DBPROP_QUICKRESTART|
|Reentrant-Ereignisse|DBPROP_REENTRANTEVENTS|
|Entfernen von gelöschten Zeilen|DBPROP_REMOVEDELETED|
|Mehrere Änderungen zu melden|DBPROP_REPORTMULTIPLECHANGES|
|Ausstehende Einfügungen zurückgeben|DBPROP_RETURNPENDINGINSERTS|
|Zeile löschen-Benachrichtigung|DBPROP_NOTIFYROWDELETE|
|Benachrichtigung zur ersten Zeile|DBPROP_NOTIFYROWFIRSTCHANGE|
|Benachrichtigung für Zeile einfügen|DBPROP_NOTIFYROWINSERT|
|Zeile Berechtigungen|DBPROP_ROWRESTRICT|
|Zeile Neusynchronisierung-Benachrichtigung|DBPROP_NOTIFYROWRESYNCH|
|Zeile Threadingmodell|DBPROP_ROWTHREADMODEL|
|Zeile rückgängig-Änderungsbenachrichtigung|DBPROP_NOTIFYROWUNDOCHANGE|
|Delete-Benachrichtigung für Zeile rückgängig machen|DBPROP_NOTIFYROWUNDODELETE|
|Zeile rückgängig-Benachrichtigung|DBPROP_NOTIFYROWUNDOINSERT|
|Zeile Updatebenachrichtigung|DBPROP_NOTIFYROWUPDATE|
|Rowset-Fetch Position Änderungsbenachrichtigung|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|Rowset-Freigabe-Benachrichtigung|DBPROP_NOTIFYROWSETRELEASE|
|Führen Sie einen Bildlauf rückwärts|DBPROP_CANSCROLLBACKWARDS|
|Serverdaten bei Einfügevorgang|DBPROP_SERVERDATAONINSERT|
|Gelöschte Lesezeichen überspringen|DBPROP_BOOKMARKSKIP|
|Starke Zeilenidentität|DBPROP_STRONGIDENTITY|
|Aktualisierbarkeit|DBPROP_UPDATABILITY|
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|

 Bestimmte Implementierungsdetails und funktionalen Informationen zu den OLE DB-Anbieter für Microsoft Jet finden Sie unter [Jet-Anbieters](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) in der OLE DB-Dokumentation.
