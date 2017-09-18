---
title: "Microsoft OLE DB-Anbieter für SQLServer | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 11f9d1d69332e1d32b1d6bbabd804ed222b620e1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Microsoft OLE DB-Anbieter für SQL Server-Übersicht
Microsoft OLE DB-Anbieter für SQL Server, SQLOLEDB, ermöglicht ADO, Microsoft SQL Server anzumelden.

## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen
 Zur Verbindung mit diesem Anbieter Festlegen der *Anbieter* Argument an die ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft:

```
SQLOLEDB
```

 Dieser Wert kann auch festlegen oder lesen, mit der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft.

## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge
 Eine typische Verbindungszeichenfolge für diesen Anbieter ist:

```
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 Die Zeichenfolge, die dieser Schlüsselwörter besteht aus:

|Schlüsselwort|Description|
|-------------|-----------------|
|**Anbieter**|Gibt die OLE DB-Anbieter für SQLServer an.|
|**Datenquelle** oder **Server**|Gibt den Namen eines Servers.|
|**Anfangskatalog** oder **Datenbank**|Gibt den Namen einer Datenbank auf dem Server.|
|**Benutzer-ID** oder **Uid**|Gibt den Benutzernamen (für SQL Server-Authentifizierung).|
|**Kennwort** oder **Pwd**|Gibt das Kennwort des Benutzers (für SQL Server-Authentifizierung).|

> [!NOTE]
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben **Trusted_Connection = Yes** oder **Integrated Security = SSPI** anstelle von Benutzer-ID und Kennwort die Informationen in der Verbindungszeichenfolge angegeben.

## <a name="provider-specific-connection-parameters"></a>Anbieterspezifische Verbindungsparameter
 Der Anbieter unterstützt zusätzlich zu den von ADO definierten verschiedene anbieterspezifische Verbindungsparameter. Mit den Eigenschaften der ADO-Verbindung dieser Anbieter-spezifischen Eigenschaften festgelegt werden können, über die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von einer [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) oder als Teil der festgelegt werden die **"ConnectionString"**.

|Parameter|Description|
|---------------|-----------------|
|Trusted_Connection|Gibt den Authentifizierungsmodus für den Benutzer an. Dies kann festgelegt werden, um **Ja** oder **keine**. Der Standardwert ist **keine**. Wenn diese Eigenschaft, um festgelegt wird **Ja**, SQLOLEDB verwendet Microsoft Windows NT-Authentifizierungsmodus zum Autorisieren von Benutzerzugriff auf die SQL Server-Datenbank, die gemäß der **Speicherort** und [Datasource ](../../../ado/reference/ado-api/datasource-property-ado.md) Eigenschaftswerte. Wenn diese Eigenschaft, um festgelegt wird **keine**, SQLOLEDB im gemischten Modus zum Autorisieren des Benutzerzugriffs auf SQL Server-Datenbank verwendet. Der SQL Server-Anmeldenamen und das Kennwort werden angegeben, der **Benutzer-Id** und **Kennwort** Eigenschaften.|
|Aktuelle Sprache|Gibt den Namen einer SQL Server-Sprache an. Identifiziert die für die Auswahl und Formatierung von Systemnachrichten verwendete Sprache. Die Sprache muss auf dem SQL-Server installiert werden andernfalls öffnen, die die Verbindung schlägt fehl.|
|Netzwerkadresse|Gibt die Netzwerkadresse des durch angegebenen SQL-Server an den **Speicherort** Eigenschaft.|
|Netzwerkbibliothek|Gibt den Namen der Netzwerkbibliothek (DLL), die zur Kommunikation mit SQL Server verwendet. Der Name sollte weder den Pfad noch die DLL-Dateinamenerweiterung enthalten. Der Standardwert wird durch die SQL Server-Clientkonfiguration bereitgestellt.|
|Verfahren für Vorbereitung verwenden|Bestimmt, ob SQL Server temporäre gespeicherte Prozeduren erstellt, wenn Befehle vorbereitet werden (durch die **Prepared** Eigenschaft).|
|Automatisch übersetzen|Gibt an, ob OEM-/ANSI-Zeichen konvertiert werden. Diese Eigenschaft kann festgelegt werden, um **"true"** oder **"false"**. Der Standardwert lautet **True**. Wenn diese Eigenschaft, um festgelegt wird **"true"**, SQLOLEDB führt OEM-/ANSI-zeichenkonvertierung aus, wenn Multibyte-Zeichenfolgen aus abgerufen werden, oder mit SQL Server gesendet. Wenn diese Eigenschaft, um festgelegt wird **"false"**, SQLOLEDB keine OEM-ANSI-zeichenkonvertierung für Multi-Byte-Zeichen von Zeichenfolgendaten ausgeführt.|
|Packet Size|Gibt eine Netzwerkpaketgröße in Bytes an. Der Paketgrößen-Eigenschaftswert muss zwischen 512 und 32767 liegen. Die standardnetzwerkpaketgröße SQLOLEDB ist 4096.|
|ApplicationName|Gibt den Namen der Clientanwendung an.|
|Workstation ID|Eine Zeichenfolge, die die Arbeitsstation identifiziert.|

## <a name="command-object-usage"></a>Befehlsobjekt-Verwendung
 SQLOLEDB akzeptiert ein Zusammenschluss von ODBC, ANSI und SQL Server-spezifische Transact-SQL als gültige Syntax. Die folgende SQL-Anweisung beispielsweise verwendet eine ODBC SQL-Escapesequenz, um die LCASE-Zeichenfolgenfunktion anzugeben:

```
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE gibt eine Zeichenfolge zurück und konvertiert alle Großbuchstaben in ihre kleingeschriebenen Entsprechungen. Der ANSI SQL-Zeichenfolgenfunktion LOWER führt den gleichen Vorgang, daher ist die folgende SQL-Anweisung entspricht der ODBC-Anweisung, die weiter oben vorgestellten ANSI:

```
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB verarbeitet beide Formen der Anweisung beim als Text für einen Befehl angegeben.

## <a name="stored-procedures"></a>Gespeicherte Prozeduren
 Verwenden Sie die ODBC-Prozedur Call-Escapesequenz im Befehlstext, beim Ausführen einer SQL Server gespeicherten Prozedur mit einem SQLOLEDB-Befehl. SQLOLEDB verwendet dann den remoteprozeduraufrufsmechanismus von SQL Server, um die befehlsverarbeitung zu optimieren. Beispielsweise ist die folgende ODBC SQL-Anweisung bevorzugter Befehlstext über das Transact-SQL-Formular:

## <a name="odbc-sql"></a>ODBC SQL

```
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server-Funktionen
 ADO können mit SQL Server kann XML für **Befehl** eingeben und Abrufen der Ergebnisse im XML-Stream-Format statt in **Recordset** Objekte. Weitere Informationen finden Sie unter [mit Streams für die Eingabe des Befehls](../../../ado/guide/data/command-streams.md) und [Resultsets in Streams abrufen](../../../ado/guide/data/retrieving-resultsets-into-streams.md).

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>Zugreifen auf Sql_variant-Daten, die mit MDAC 2.7, MDAC 2.8 oder Windows DAC 6.0
 Microsoft SQL Server hat den Datentyp, der aufgerufen **Sql_variant**. OLE DB ähnelt **DBTYPE_VARIANT**, **Sql_variant** -Datentyp kann mehrere unterschiedliche Datentypen speichern. Es gibt jedoch einige wichtige Unterschiede zwischen **DBTYPE_VARIANT** und **Sql_variant**. ADO verarbeitet auch gespeicherte Daten einen **Sql_variant** Wert anders als wie andere Datentypen verarbeitet. Die folgende Liste beschreibt Aspekte zu berücksichtigen, beim Zugriff auf SQL Server-Daten in Spalten vom Typ gespeicherte **Sql_variant**.

-   In MDAC 2.7, MDAC 2.8 und Windows Data Access Components (Windows DAC) 6.0, der OLE DB-Anbieter für SQL Server unterstützt die **Sql_variant** Typ. Der OLE DB-Anbieter für ODBC wird nicht verwendet.

-   Die **Sql_variant** Typ entspricht nicht genau der **DBTYPE_VARIANT** -Datentyp.  Die **Sql_variant** Typ unterstützt einige neue Untertypen von nicht unterstützten **DBTYPE_VARIANT,** einschließlich **GUID**, **ANSI** (nicht-UNICODE) Zeichenfolgen, und **"bigint"**. Mithilfe von Untertypen außer funktionieren den zuvor aufgeführten ordnungsgemäß.

-   Die **Sql_variant** Untertyp **numerischen** entspricht nicht der **DBTYPE_DECIMAL** Größe.

-   Mehrere Datentypumwandlungen führt Typen, die nicht übereinstimmen. Z. B. Koersion eine **Sql_variant** mit einem Untertyp des **GUID** auf eine **DBTYPE_VARIANT** führt einen Untertyp von **Safearray**(Bytes) . Konvertieren von dieses Typs zurück, an eine **Sql_variant** führt zu einer neuen Untertyp des **Array**(Bytes).

-   **Recordset** Felder mit **Sql_variant** Daten können Remote ausgeführt werden (gemarshallt) oder persistenten nur, wenn die **Sql_variant** bestimmte Untertypen enthält. Der Versuch, Remote oder beibehalten von Daten mit den folgenden nicht unterstützten Untertypen verursacht einen Laufzeitfehler (nicht unterstützte Konvertierung) aus der Persistenz-Provider von Microsoft (MSPersist): **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **"VT_BSTR"**, und **VT_DISPATCH.**

-   Der OLE DB-Anbieter für SQL Server in MDAC 2.7, MDAC 2.8 und Windows DAC 6.0 verfügt über eine dynamische Eigenschaft mit dem Namen **ermöglichen systemeigene Varianten** , wie der Name schon sagt, womit Entwicklern den Zugriff auf die **Sql_variant** in Im Gegensatz zu ihrer systemeigenen Form einer **DBTYPE_VARIANT**. Wenn diese Eigenschaft festgelegt ist, und eine **Recordset** wird geöffnet, mit der Client-Cursormoduls (**AdUseClient**), wird die **Recordset.Open** Aufruf fehl. Wenn diese Eigenschaft festgelegt ist und eine **Recordset** mit Servercursor geöffnet wird (**AdUseServer**), wird die **Recordset.Open** Aufruf erfolgreich ausgeführt, aber den Zugriff auf Spalten des Typs **Sql_variant** , löst einen Fehler.

-   In Clientanwendungen, MDAC 2.5 verwenden **Sql_variant** Daten mit Abfragen für Microsoft SQL Server verwendet werden können. Allerdings die Werte der **Sql_variant** Daten werden als Zeichenfolgen behandelt. Derartige Clientanwendungen sollte MDAC 2.7, MDAC 2.8 oder Windows DAC 6.0 aktualisiert werden.

## <a name="recordset-behavior"></a>Recordset-Verhalten
 SQL Server-Cursor können SQLOLEDB unterstützt mehrere-Ergebnis von zahlreichen Befehlen generiert. Wenn ein Consumer ein Recordset, erfordern die Unterstützung für SQL Server-Cursor angefordert wird, tritt ein Fehler auf, wenn der Befehlstext zum mehr als einem einzigen Recordset als Ergebnis generiert.

 Bildlauffähige SQLOLEDB Recordsets werden von SQL Server-Cursor unterstützt. SQL Server erzwingt Einschränkungen für Cursor, die von anderen Benutzern der Datenbank vorgenommenen Änderungen berücksichtigt werden. Insbesondere die Zeilen in einigen Cursorn nicht sortiert werden, und möchten, erstellen Sie ein Recordset mit einem Befehl, eine SQL ORDER BY-Klausel enthält, kann fehlschlagen.

## <a name="dynamic-properties"></a>Dynamische Eigenschaften
 Microsoft OLE DB-Anbieter für SQL Server fügt verschiedene Eigenschaften in der **Eigenschaften** Auflistung von der geöffnete [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), und [ Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekte.

 Die folgenden Tabellen sind ein Cross-Index der ADO und OLE DB-Namen für jede dynamische Eigenschaft. Der OLE DB Programmer's Reference bezieht sich auf den Namen einer ADO-Eigenschaft von der Begriff "Description". Weitere Informationen zu diesen Eigenschaften finden Sie in der OLE DB Programmer's Reference. Suchen Sie nach den Namen des OLE DB-Eigenschaft im Index oder finden Sie unter [Anhang C: OLE DB-Eigenschaften](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

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
|Verbindungstimeout|DBPROP_INIT_TIMEOUT|
|Aktuellen Katalog|DBPROP_CURRENTCATALOG|
|Datenquelle|DBPROP_INIT_DATASOURCE|
|Datenquellenname|RÜCKGABEWERT|
|Datenquellenobjekt Threadingmodell|DBPROP_DSOTHREADMODEL|
|Der DBMS-Name|DBPROP_DBMSNAME|
|DBMS-Version|DBPROP_DBMSVER|
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|
|GROUP BY-Unterstützung|DBPROP_GROUPBY|
|Unterstützung von heterogenen Tabellen|DBPROP_HETEROGENEOUSTABLES|
|Bezeichner Groß-/Kleinschreibung|DBPROP_IDENTIFIERCASE|
|Anfangskatalog|DBPROP_INIT_CATALOG|
|Isolationsstufen|DBPROP_SUPPORTEDTXNISOLEVELS|
|Isolation Aufbewahrung|DBPROP_SUPPORTEDTXNISORETAIN|
|Locale Identifier|DBPROP_INIT_LCID|
|Maximale Indexgröße|DBPROP_MAXINDEXSIZE|
|Maximale Zeilengröße|DBPROP_MAXROWSIZE|
|Maximale Zeilengröße schließt BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Maximale Anzahl von Tabellen in SELECT|DBPROP_MAXTABLESINSELECT|
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
|Sicherheitsinformationen permanent speichern|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|
|Timeout des Befehls|DBPROP_COMMANDTIMEOUT|
|Verzögern der Spalte|DBPROP_DEFERRED|
|Verzögerung Speicher Objekt Updates|DBPROP_DELAYSTORAGEOBJECTS|
|Rückwärts abrufen|DBPROP_CANFETCHBACKWARDS|
|Halten Sie Zeilen|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Nicht Mobile Zeilen|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Literal Lesezeichen|DBPROP_LITERALBOOKMARKS|
|Literal Zeilenidentität|DBPROP_LITERALIDENTITY|
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
|Rowset-Fetch Position Änderungsbenachrichtigung|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Rowset-Freigabe-Benachrichtigung|DBPROP_NOTIFYROWSETRELEASE|
|Führen Sie einen Bildlauf rückwärts|DBPROP_CANSCROLLBACKWARDS|
|Servercursor|DBPROP_SERVERCURSOR|
|Gelöschte Lesezeichen überspringen|DBPROP_BOOKMARKSKIPPED|
|Starke Zeilenidentität|DBPROP_STRONGITDENTITY|
|Eindeutige Zeilen|DBPROP_UNIQUEROWS|
|Aktualisierbarkeit|DBPROP_UPDATABILITY|
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Dynamische Eigenschaften der Befehl
 Die folgenden Eigenschaften werden hinzugefügt, um die **Eigenschaften** Auflistung von der **Befehl** Objekt.

|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|
|-----------------------|--------------------------|
|Access-Reihenfolge|DBPROP_ACCESSORDER|
|Basispfad|SSPROP_STREAM_BASEPATH|
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|
|Inhaltstyp|SSPROP_STREAM_CONTENTTYPE|
|Cursor-Auto-Fetch|SSPROP_CURSORAUTOFETCH|
|Verzögern der Spalte|DBPROP_DEFERRED|
|Vorbereitung zurückstellen|SSPROP_DEFERPREPARE|
|Verzögerung Speicher Objekt Updates|DBPROP_DELAYSTORAGEOBJECTS|
|Rückwärts abrufen|DBPROP_CANFETCHBACKWARDS|
|Halten Sie Zeilen|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Nicht Mobile Zeilen|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
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
|Ausgabe-Encoding-Eigenschaft|DBPROP_OUTPUTENCODING|
|Stream Ausgabeeigenschaft|DBPROP_OUTPUTSTREAM|
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
|Servercursor|DBPROP_SERVERCURSOR|
|Serverdaten bei Einfügevorgang|DBPROP_SERVERDATAONINSERT|
|Gelöschte Lesezeichen überspringen|DBPROP_BOOKMARKSKIP|
|Starke Zeilenidentität|DBPROP_STRONGIDENTITY|
|Aktualisierbarkeit|DBPROP_UPDATABILITY|
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|
|XML-Stamm|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Bestimmte Implementierungsdetails und funktionalen Informationen zu Microsoft SQL Server OLE DB-Anbieter finden Sie in der [SQL Server-Anbieter](http://msdn.microsoft.com/en-us/adf1d6c4-5930-444a-9248-ff1979729635).

## <a name="see-also"></a>Siehe auch
 [ConnectionString-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Anbietereigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

