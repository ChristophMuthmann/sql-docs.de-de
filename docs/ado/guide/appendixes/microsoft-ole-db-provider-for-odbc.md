---
title: "Microsoft OLE DB-Anbieter für ODBC | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 44f3131bff34d35b334495c7c718eb513f5d88bf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB-Anbieter für ODBC (Übersicht)
Ein ADO- oder RDS-Programmierer würde idealerweise möglich in dem jede Datenquelle eine OLE DB-Schnittstelle verfügbar macht, damit ADO direkt in der Datenquelle aufrufen kann. Obwohl Datenbankanbieter zunehmend OLE DB-Schnittstellen implementieren, sind einige Datenquellen noch nicht auf diese Weise bereitgestellt. Allerdings können die meisten DBMS-Systeme heute über ODBC zugegriffen werden.

 ODBC-Treiber sind für alle wichtigen DBMS heute, einschließlich Microsoft SQL Server, Microsoft Access (Microsoft Jet-Datenbankmodul) und Microsoft FoxPro, zusätzlich zu den nicht-Microsoft-Produkte wie Oracle verfügbar.

 Der Microsoft ODBC-Anbieter können jedoch ADO zur Verbindung mit einer ODBC-Datenquelle. Der Anbieter Freethread- und Unicode aktiviert ist.

 Der Anbieter unterstützt Transaktionen, obwohl unterschiedliche DBMS-Module verschiedene Typen von transaktionsunterstützung bieten. Microsoft Access unterstützt z. B. bis zu fünf Ebenen tief geschachtelte Transaktionen.

 Dies ist der Standardanbieter für ADO und alle anbieterabhängig ADO-Eigenschaften und Methoden werden unterstützt.

## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen
 Zur Verbindung mit diesem Anbieter Festlegen der **Anbieter =** Argument der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft:

```
MSDASQL
```

 Lesen der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft wird auch dieser Zeichenfolge zurück.

## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge
 Eine typische Verbindungszeichenfolge für diesen Anbieter ist:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 Die Zeichenfolge, die dieser Schlüsselwörter besteht aus:

|Schlüsselwort|Description|
|-------------|-----------------|
|**Anbieter**|Gibt die OLE DB-Anbieter für ODBC.|
|**DSN**|Gibt die Namen der Datenquelle an.|
|**UID**|Gibt den Benutzernamen an.|
|**PWD**|Gibt das Kennwort des Benutzers an.|
|**URL**|Gibt die URL einer Datei oder eines Verzeichnisses in einem Webordner veröffentlicht.|

 Da dies den Standardanbieter für ADO, wenn Sie weglassen, ist die **Provider =** Parameter aus der Verbindungszeichenfolge ADO wird versucht, zum Herstellen einer Verbindung zu diesem Anbieter.

> [!NOTE]
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben **Trusted_Connection = Yes** oder **Integrated Security = SSPI** anstelle von Benutzer-ID und Kennwort die Informationen in der Verbindungszeichenfolge angegeben.

 Der Anbieter unterstützt keine bestimmten Verbindungsparameter zusätzlich zu den von ADO definiert. Allerdings wird der Anbieter nicht ADO Verbindungsparameter an dem ODBC-Treiber-Manager übergeben.

 Da Sie weglassen, können der **Anbieter** Parameter, machen Sie daher eine ADO-Verbindungszeichenfolge, die mit einer ODBC-Verbindungszeichenfolge für die gleiche Datenquelle identisch ist. Verwenden Sie die gleichen Parameternamen (**Treiber =**, **Datenbank =**, **DSN =**usw.), Werte und Syntax wie würden Sie beim Verfassen einer ODBC-Verbindungszeichenfolge. Sie können mit oder ohne vordefinierte Datenquellenname (DSN) oder FileDSN verbinden.

## <a name="syntax-with-a-dsn-or-filedsn"></a>Die Syntax mit einem DSN oder FileDSN:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>-Syntax ohne einen DSN (DSN-lose Verbindung):

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>Hinweise
 Bei Verwendung einer **DSN** oder **FileDSN**, er muss über die ODBC-Datenquellen-Administrator in der Windows-Systemsteuerung definiert werden. Im Microsoft Windows 2000 befindet sich der ODBC-Administrator unter Verwaltung. In früheren Versionen von Windows das Symbol "ODBC-Administrator" heißt **32-Bit-ODBC-** oder einfach **ODBC**.

 Als Alternative zum Festlegen einer **DSN**, können Sie angeben, den ODBC-Treiber (**Treiber =**), z. B. "SQLServer;" den Namen des Servers (**SERVER =**); und den Datenbanknamen (**Datenbank =**).

 Sie können auch einen Benutzernamen für das Konto angeben (**UID =**), und das Kennwort für das Benutzerkonto (**PWD =**) in den ODBC-spezifischen Parametern oder im Standard ADO definierten *Benutzer* und *Kennwort* Parameter.

 Obwohl eine **DSN** bereits Definition gibt eine Datenbank, Sie können angeben, *eine* *Datenbank* Parameter zusätzlich zu eine **DSN** eine Verbindung herstellen mit einer anderen Datenbank. Es ist eine gute Idee, beziehen Sie immer *der* *Datenbank* Parameter bei Verwendung einer **DSN**. Dadurch wird sichergestellt, dass Sie eine Verbindung mit der richtigen Datenbank herstellen, wenn ein anderer Benutzer den Standardparameter für die Datenbank geändert, da Sie der letzten Überprüfung der **DSN** Definition.

## <a name="provider-specific-connection-properties"></a>Anbieter-spezifischen Verbindungseigenschaften
 Der OLE DB-Anbieter für ODBC fügt verschiedene Eigenschaften, die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von der **Verbindung** Objekt. In der folgenden Tabelle sind diese Eigenschaften mit dem entsprechenden OLE DB-Eigenschaftsnamen in Klammern aufgeführt.

|Eigenschaftsname|Description|
|-------------------|-----------------|
|Zugegriffen werden Prozeduren (KAGPROP_ACCESSIBLEPROCEDURES)|Gibt an, ob der Benutzer den Zugriff auf gespeicherte Prozeduren.|
|Zugänglich Tabellen (KAGPROP_ACCESSIBLETABLES)|Gibt an, ob der Benutzer die Berechtigung zum Ausführen von SELECT-Anweisungen für Tabellen der Datenbank.|
|Aktive Anweisungen (KAGPROP_ACTIVESTATEMENTS)|Gibt die Anzahl der Handles, die ein ODBC-Treiber für eine Verbindung unterstützen kann.|
|Treibername (KAGPROP_DRIVERNAME)|Gibt den Dateinamen des ODBC-Treibers an.|
|ODBC-Treiberversion (KAGPROP_DRIVERODBCVER)|Gibt an, die diesen Treiber unterstützt ODBC-Version.|
|Verwendung der Datei (KAGPROP_FILEUSAGE)|Gibt an, wie der Treiber eine Datei in einer Datenquelle behandelt. als eine Tabelle oder eines Katalogs.|
|Wie Escape-Klausel (KAGPROP_LIKEESCAPECLAUSE)|Gibt an, ob der Treiber die Definition und Verwendung eines Escapezeichens unterstützt für das Prozentzeichen (%) und das Unterstrichzeichen (_) im LIKE-Prädikat einer WHERE-Klausel.|
|Max-Spalten in Group By (KAGPROP_MAXCOLUMNSINGROUPBY)|Gibt die maximale Anzahl von Spalten, die in der GROUP BY-Klausel einer SELECT-Anweisung aufgeführt werden können.|
|Maximale Anzahl von Spalten im Index (KAGPROP_MAXCOLUMNSININDEX)|Gibt die maximale Anzahl von Spalten, die in einem Index aufgenommen werden kann.|
|Maximale Anzahl von Spalten in der Order By (KAGPROP_MAXCOLUMNSINORDERBY)|Gibt die maximale Anzahl von Spalten, die in der ORDER BY-Klausel einer SELECT-Anweisung aufgeführt werden können.|
|Maximale Anzahl von Spalten in Select (KAGPROP_MAXCOLUMNSINSELECT)|Gibt die maximale Anzahl von Spalten, die in der SELECT-Teil einer SELECT-Anweisung aufgeführt werden können.|
|Maximale Anzahl von Spalten in der Tabelle (KAGPROP_MAXCOLUMNSINTABLE)|Gibt die maximale Anzahl zulässiger Spalten in einer Tabelle an.|
|Numerische Funktionen (KAGPROP_NUMERICFUNCTIONS)|Gibt an, welche numerischen Funktionen der ODBC-Treiber unterstützt werden. Eine Liste der Funktionsnamen und die zugehörigen Werte, die in dieser Bitmaske verwendet, finden Sie unter [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), in der ODBC-Dokumentation.|
|Outer Join-Funktionen (KAGPROP_OJCAPABILITY)|Gibt die Typen von ÄUßEREN JOINs vom Anbieter unterstützt werden.|
|Äußere Joins (KAGPROP_OUTERJOINS)|Gibt an, ob der Anbieter ÄUßEREN JOINs unterstützt.|
|Sonderzeichen (KAGPROP_SPECIALCHARACTERS)|Gibt an, welche Zeichen für den ODBC-Treiber eine besondere Bedeutung haben.|
|Gespeicherte Prozeduren (KAGPROP_PROCEDURES)|Gibt an, ob gespeicherte Prozeduren für die Verwendung mit diesem ODBC-Treiber verfügbar sind.|
|Zeichenfolgenfunktionen (KAGPROP_STRINGFUNCTIONS)|Gibt an, welche Zeichenfolgenfunktionen vom ODBC-Treiber unterstützt werden. Eine Liste der Funktionsnamen und die zugehörigen Werte, die in dieser Bitmaske verwendet, finden Sie unter [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), in der ODBC-Dokumentation.|
|Systemfunktionen (KAGPROP_SYSTEMFUNCTIONS)|Gibt an, welche Systemfunktionen vom ODBC-Treiber unterstützt werden. Eine Liste der Funktionsnamen und die zugehörigen Werte, die in dieser Bitmaske verwendet, finden Sie unter [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), in der ODBC-Dokumentation.|
|Datums-/Funktionen (KAGPROP_TIMEDATEFUNCTIONS)|Gibt an, welche Funktionen für Datum und Uhrzeit der ODBC-Treiber unterstützt werden. Eine Liste der Funktionsnamen und die zugehörigen Werte, die in dieser Bitmaske verwendet, finden Sie unter [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), in der ODBC-Dokumentation.|
|Unterstützung für SQL-Grammatik (KAGPROP_ODBCSQLCONFORMANCE)|Gibt an, die SQL-Grammatik, die der ODBC-Treiber unterstützt.|

## <a name="provider-specific-recordset-and-command-properties"></a>Anbieterspezifische Recordset und Befehlseigenschaften
 Der OLE DB-Anbieter für ODBC fügt verschiedene Eigenschaften, die **Eigenschaften** Auflistung von der **Recordset** und **Befehl** Objekte. In der folgenden Tabelle sind diese Eigenschaften mit dem entsprechenden OLE DB-Eigenschaftsnamen in Klammern aufgeführt.

|Eigenschaftsname|Description|
|-------------------|-----------------|
|Abfragebasiert Aktualisierungen/Löschungen/Einfügevorgänge (KAGPROP_QUERYBASEDUPDATES)|Gibt an, ob Updates, löschungen und einfügungen mithilfe von SQL-Abfragen ausgeführt werden können.|
|ODBC-Parallelitätstyp (KAGPROP_CONCURRENCY)|Gibt die Methode zum Reduzieren der möglichen Problemen aufgrund von zwei Benutzern, die versuchen, gleichzeitig auf dieselben Daten aus der Datenquelle verwendet.|
|BLOB-Zugriff auf die Forward-Only-Cursor (KAGPROP_BLOBSONFOCURSOR)|Gibt an, ob BLOB- **Felder** kann zugegriffen werden, wenn ein Vorwärtscursor verwenden.|
|Schließen Sie SQL_FLOAT, SQL_DOUBLE und SQL_REAL in QBU WHERE-Klauseln (KAGPROP_INCLUDENONEXACT)|Gibt an, ob SQL_FLOAT, SQL_DOUBLE und SQL_REAL Werte in einer QBU WHERE-Klausel aufgenommen werden können.|
|Position in der letzten Zeile nach dem Einfügen (KAGPROP_POSITIONONNEWROW)|Gibt an, dass die letzte Zeile in der Tabelle nach dem Einfügen eines neuen Datensatzes in einer Tabelle werden stammen von der aktuellen Zeile.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|Gibt an, ob die **IRowsetChange** Schnittstelle bietet Informationen zur erweiterten Unterstützung.|
|ODBC-Cursortyps (KAGPROP_CURSOR)|Gibt den Typ der Cursor, mit dem durch die **Recordset**.|
|Generieren ein Rowsets, die gemarshallt werden kann (KAGPROP_MARSHALLABLE)|Gibt an, dass der ODBC-Treiber eine Datensatzgruppe generiert, die gemarshallt werden kann|

## <a name="command-text"></a>Befehlstext
 Verwendung der [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt hängt zum größten Teil der Datenquelle, und welche Art von Abfrage oder einen Befehl-Anweisung akzeptiert.

 ODBC stellt eine spezielle Syntax zum Aufrufen von gespeicherter Prozeduren bereit. Für die [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft eine **Befehl** -Objekt, der *CommandText* Argument an die **Execute** Methode auf eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt, oder die *Quelle* Argument an die **öffnen** Methode auf eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt übergibt eine Zeichenfolge mit folgender Syntax:

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , … ]] ) ] }"
```

 Jede **?** verweist auf ein Objekt in der [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung. Die erste **?** Verweise **Parameter**(0), den nächsten **?** Verweise **Parameter**(1), und so weiter.

 Die Parameterverweise sind optional und hängen von der Struktur der gespeicherten Prozedur. Wenn eine gespeicherte Prozedur aufrufen, die keine Parameter definiert werden sollen, würde die Zeichenfolge wie folgt aussehen:

```
"{ call procedure }"
```

 Wenn Sie zwei Abfrageparameter haben, würde die Zeichenfolge folgendermaßen aussehen:

```
"{ call procedure ( ?, ? ) }"
```

 Wenn die gespeicherte Prozedur einen Wert zurückgibt, wird der Rückgabewert als ein anderer Parameter behandelt. Wenn Sie keine Abfrageparameter aufweisen, aber Sie verfügen über einen Rückgabewert, würde die Zeichenfolge folgendermaßen aussehen:

```
"{ ? = call procedure }"
```

 Abschließend, wenn Sie einen Rückgabewert haben, und zwei Abfrageparameter, die Zeichenfolge ähnelt der folgenden:

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>Recordset-Verhalten
 Die folgenden Tabellen enthalten die standard ADO-Methoden und Eigenschaften verfügbar, auf eine **Recordset** Objekt mit diesem Anbieter geöffnet.

 Ausführlichere Informationen zu **Recordset** Verhalten für die Anbieterkonfiguration kann durch Ausführen der [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode und für das Auflisten der **Eigenschaften** Auflistung von der **Recordset** zu bestimmen, ob die anbieterspezifische dynamische Eigenschaften vorhanden sind.

 Verfügbarkeit des standardmäßigen ADO **Recordset** Eigenschaften:

|Eigenschaft|"ForwardOnly"|Dynamic|Keyset|STATIC-Cursor|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|Nicht verfügbar|Nicht verfügbar|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|Nicht verfügbar|Nicht verfügbar|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|
|[Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md)|Nicht verfügbar|Nicht verfügbar|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|["PageCount"](../../../ado/reference/ado-api/pagecount-property-ado.md)|Lese-/Schreibzugriff|Nicht verfügbar|Schreibgeschützt|Schreibgeschützt|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Lese-/Schreibzugriff|Nicht verfügbar|Schreibgeschützt|Schreibgeschützt|
|[Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md)|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|Lese-/Schreibzugriff|
|[Status](../../../ado/reference/ado-api/state-property-ado.md)|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|Schreibgeschützt|

 Die [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) und [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) Eigenschaften sind schreibgeschützt, wenn ADO mit Version 1.0 von der Microsoft OLE DB-Anbieter für ODBC verwendet wird.

 Verfügbarkeit des standardmäßigen ADO **Recordset** Methoden:

|Methode|"ForwardOnly"|Dynamic|Keyset|STATIC-Cursor|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|ja|ja|ja|ja|
|[Abbrechen](../../../ado/reference/ado-api/cancel-method-ado.md)|ja|ja|ja|ja|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|ja|ja|ja|ja|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|ja|ja|ja|ja|
|[Klon](../../../ado/reference/ado-api/clone-method-ado.md)|nein|nein|ja|ja|
|[Schließen](../../../ado/reference/ado-api/close-method-ado.md)|ja|ja|ja|ja|
|[Löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|ja|ja|ja|ja|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|ja|ja|ja|ja|
|[Verschieben](../../../ado/reference/ado-api/move-method-ado.md)|ja|ja|ja|ja|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|ja|ja|ja|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|nein|ja|ja|ja|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|ja|ja|ja|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|nein|ja|ja|ja|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|ja|ja|ja|ja|
|[Datei](../../../ado/reference/ado-api/open-method-ado-recordset.md)|ja|ja|ja|ja|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|ja|ja|ja|ja|
|[Erneut synchronisieren](../../../ado/reference/ado-api/resync-method.md)|nein|nein|ja|ja|
|[Unterstützt](../../../ado/reference/ado-api/supports-method.md)|ja|ja|ja|ja|
|[Update](../../../ado/reference/ado-api/update-method.md)|ja|ja|ja|ja|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|ja|ja|ja|ja|

 * Nicht für Microsoft Access-Datenbanken unterstützt.

## <a name="dynamic-properties"></a>Dynamische Eigenschaften
 Microsoft OLE DB-Anbieter für ODBC fügt verschiedene Eigenschaften in der **Eigenschaften** Auflistung von der geöffnete [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), und [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekte.

 Die folgenden Tabellen sind ein Cross-Index der ADO und OLE DB-Namen für jede dynamische Eigenschaft. Der OLE DB Programmer's Reference bezieht sich auf den Namen einer ADO-Eigenschaft von der Begriff "Description". Weitere Informationen zu diesen Eigenschaften finden Sie in der OLE DB Programmer's Reference. Suchen Sie nach den Namen des OLE DB-Eigenschaft im Index oder finden Sie unter [Anhang C: OLE DB-Eigenschaften](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Dynamische Eigenschaften der Verbindung
 Die folgenden Eigenschaften werden hinzugefügt, um die **Verbindung** des Objekts **Eigenschaften** Auflistung.

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
|Kennwort|DBPROP_AUTH_PASSWORD|
|Übergeben von Ref Accessoren|DBPROP_BYREFACCESSORS|
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
 Die folgenden Eigenschaften werden hinzugefügt, um die **Recordset** des Objekts **Eigenschaften** Auflistung.

|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|
|-----------------------|--------------------------|
|Access-Reihenfolge|DBPROP_ACCESSORDER|
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Eindeutige Zeilen|DBPROP_UNIQUEROWS|
|Aktualisierbarkeit|DBPROP_UPDATABILITY|
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Dynamische Eigenschaften der Befehl
 Die folgenden Eigenschaften werden hinzugefügt, um die **Befehl** des Objekts **Eigenschaften** Auflistung.

|Name der ADO-Eigenschaft|Name der OLE DB-Eigenschaft|
|-----------------------|--------------------------|
|Access-Reihenfolge|DBPROP_ACCESSORDER|
|Blockieren von Speicherobjekten|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Bookmark-Typ|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Ändern der eingefügte Zeilen|DBPROP_CHANGEINSERTEDROWS|
|Spaltenprivileginformationen|DBPROP_COLUMNRESTRICT|
|Spalte Set-Benachrichtigung|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Gelöschte Lesezeichen überspringen|DBPROP_BOOKMARKSKIP|
|Starke Zeilenidentität|DBPROP_STRONGIDENTITY|
|Aktualisierbarkeit|DBPROP_UPDATABILITY|
|Verwenden von Lesezeichen|DBPROP_BOOKMARKS|

 Weitere Informationen zur Implementierung und funktionalen Informationen zu den Microsoft OLE DB-Anbieter für ODBC, finden Sie unter der [OLE DB Programmer's Reference](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) oder besuchen Sie die Data Access and Storage Developer Center Web Site auf MSDN.

## <a name="see-also"></a>Siehe auch
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [ausführen Methode (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) [Parameters-Auflistung (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Anbietereigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [unterstützt-Methode](../../../ado/reference/ado-api/supports-method.md)
