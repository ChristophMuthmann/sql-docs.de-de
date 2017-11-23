---
title: ADO-dynamische Property-Index | Microsoft Docs
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: f126cc040174725ded02bd320e54a76536c0d516
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="ado-dynamic-property-index"></a>ADO-dynamische Property-Index
Datenanbieter, Dienstanbieter und Dienstkomponenten können dynamische Eigenschaften zum Hinzufügen der **Eigenschaften** Sammlungen von der geöffnete [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) und [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekte. Ein angegebenen Anbieter möglicherweise auch weitere Eigenschaften einfügen, wenn diese Objekte geöffnet werden. Einige dieser Eigenschaften sind aufgeführt, der [dynamische Eigenschaften der ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md) Abschnitt. Weitere sind aufgeführt, unter bestimmten Anbieter in der [Anhang A: Anbieter](../../../ado/guide/appendixes/appendix-a-providers.md) Abschnitt.  
  
 Die folgenden Tabellen sind Cross-indexes der ADO und OLE DB-Namen für jede dynamische Eigenschaft der standard OLE DB-Anbieter. Ihr Anbieter möglicherweise mehr Eigenschaften als aufgelisteten hier hinzufügen. Spezifische Informationen zur anbieterspezifischen dynamischen Eigenschaften finden Sie in der Dokumentation Ihres Anbieters.  
  
 Der OLE DB Programmer's Reference bezieht sich auf den Namen einer ADO-Eigenschaft von der Begriff "Description". Weitere Informationen zu diesen standard Eigenschaften suchen, oder Durchsuchen Sie den Index in der [OLE DB-Dokumentation](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)für die OLE DB-Eigenschaft mit dem Namen.  
  
## <a name="connection-dynamic-properties"></a>Dynamische Eigenschaften der Verbindung  
  
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
|Speicherort|DBPROP_INIT_LOCATION|  
|Maximale Indexgröße|DBPROP_MAXINDEXSIZE|  
|Maximale Zeilengröße|DBPROP_MAXROWSIZE|  
|Maximale Zeilengröße schließt BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|  
|Maximale Anzahl von Tabellen in SELECT|DBPROP_MAXTABLESINSELECT|  
|Mode|DBPROP_INIT_MODE|  
|Mehrere Parametersätze|DBPROP_MULTIPLEPARAMSETS|  
|Mehrere Ergebnisse|DBPROP_MULTIPLERESULTS|  
|Mehrere Speicherobjekte|DBPROP_MULTIPLESTORAGEOBJECTS|  
|Update mit mehreren Tabellen|DBPROP_MULTITABLEUPDATE|  
|NULL-Sortierung|DBPROP_NULLCOLLATION|  
|NULL-Verkettungsverhalten|DBPROP_CONCATNULLBEHAVIOR|  
|OLE DB-Dienste|DBPROP_INIT_OLEDBSERVICES|  
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
 Beachten Sie, dass die **dynamische Eigenschaften** von der **Recordset** Objekt wechseln, die außerhalb des gültigen Bereichs (nicht mehr verfügbar) Wenn Sie die **Recordset** geschlossen wird.  
  
|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|' Irowsetfind '|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh abgelöst|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|Auf das IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|Access-Reihenfolge|DBPROP_ACCESSORDER|  
|Nur Anhängen-Rowset|DBPROP_APPENDONLY|  
|Asynchrone Rowsetverarbeitung|DBPROP_ROWSET_ASYNCH|  
|Automatische Neuberechnung|DBPROP_ADC_AUTORECALC|  
|Hintergrund Abrufgröße|DBPROP_ASYNCHFETCHSIZE|  
|Background Thread Priority|DBPROP_ASYNCHTHREADPRIORITY|  
|Batchgröße|DBPROP_ADC_BATCHSIZE|  
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|  
|Bookmarkable|DBPROP_IROWSETLOCATE|  
|Lesezeichen sortiert|DBPROP_ORDEREDBOOKMARKS|  
|Zwischenspeichern von untergeordneten Zeilen|DBPROP_ADC_CACHECHILDROWS|  
|Verzögerte Spalten Zwischenspeichern|DBPROP_CACHEDEFERRED|  
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|  
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|  
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|  
|Schreibbare Spalte|DBPROP_MAYWRITECOLUMN|  
|Timeout des Befehls|DBPROP_COMMANDTIMEOUT|  
|Cursor-Modulversion|DBPROP_ADC_CEVER|  
|Verzögern der Spalte|DBPROP_DEFERRED|  
|Verzögerung Speicher Objekt Updates|DBPROP_DELAYSTORAGEOBJECTS|  
|Rückwärts abrufen|DBPROP_CANFETCHBACKWARDS|  
|Filtervorgänge|DBPROP_FILTERCOMPAREOPS|  
|Suchen von Vorgängen|DBPROP_FINDCOMPAREOPS|  
|Ausgeblendete Spalten (Anzahl)|DBPROP_HIDDENCOLUMNS|  
|Halten Sie Zeilen|DBPROP_CANHOLDROWS|  
|Nicht Mobile Zeilen|DBPROP_IMMOBILEROWS|  
|Anfängliche Abrufgröße|DBPROP_ASYNCHPREFETCHSIZE|  
|Literal Lesezeichen|DBPROP_LITERALBOOKMARKS|  
|Literal Zeilenidentität|DBPROP_LITERALIDENTITY|  
|Verwalten von Änderungsstatus|DBPROP_ADC_MAINTAINCHANGESTATUS|  
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
|Private1||  
|Schnelle Neustart|DBPROP_QUICKRESTART|  
|Reentrant-Ereignisse|DBPROP_REENTRANTEVENTS|  
|Entfernen von gelöschten Zeilen|DBPROP_REMOVEDELETED|  
|Mehrere Änderungen zu melden|DBPROP_REPORTMULTIPLECHANGES|  
|Umstrukturieren von Namen|DBPROP_ADC_RESHAPENAME|  
|Resync-Befehl|DBPROP_ADC_CUSTOMRESYNCH|  
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
|Gelöschte Lesezeichen überspringen|DBPROP_BOOKMARKSKIPPED|  
|Starke Zeilenidentität|DBPROP_STRONGIDENTITY|  
|Eindeutige Katalog|DBPROP_ADC_UNIQUECATALOG|  
|Eindeutige Zeilen|DBPROP_UNIQUEROWS|  
|Eindeutiges Schema|DBPROP_ADC_UNIQUESCHEMA|  
|Eindeutige Tabelle|DBPROP_ADC_UNIQUETABLE|  
|Aktualisierbarkeit|DBPROP_UPDATABILITY|  
|Aktualisieren von Kriterien|DBPROP_ADC_UPDATECRITERIA|  
|Aktualisieren Sie die erneute Synchronisierung|DBPROP_ADC_UPDATERESYNC|  
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|