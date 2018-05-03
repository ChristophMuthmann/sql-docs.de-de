---
title: Microsoft OLE DB-Anbieter für Microsoft Indexdienst | Microsoft Docs
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
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08a2ef17e048c66b32b0d3af77e5172ef93350cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB-Anbieter für Microsoft Indexing Service – Übersicht
Microsoft OLE DB-Anbieter für Microsoft Indexdienst bietet programmgesteuerten nur-Lese Zugriff auf System- und Web-Daten, die vom Microsoft Indexdienst indiziert Datei. ADO-Anwendungen können SQL-Abfragen zum Abrufen von Inhalten und Eigenschaftsinformationen ausgeben.

 Der Anbieter Freethread- und UNICODE aktiviert ist.

## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen
 Zur Verbindung mit diesem Anbieter Festlegen der **Anbieter =** Argument an die ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft:

```
MSIDXS
```

 Lesen der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft wird auch dieser Zeichenfolge zurück.

## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge
 Eine typische Verbindungszeichenfolge für diesen Anbieter ist:

```
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 Die Zeichenfolge, die dieser Schlüsselwörter besteht aus:

|Schlüsselwort|Description|
|-------------|-----------------|
|**Provider**|Gibt den OLE DB-Anbieter für Microsoft Indexdienst. In der Regel ist dies das einzige-Schlüsselwort in der Verbindungszeichenfolge angegeben.|
|**Datenquelle**|Gibt den Namen der Indexdienst-Katalog. Wenn dieses Schlüsselwort nicht angegeben ist, wird der Standardkatalog für das System verwendet.|
|**Locale Identifier**|Gibt eine eindeutige 32-Bit-Zahl (z. B. 1033), die Einstellungen im Zusammenhang mit der Sprache des Benutzers angibt. Wenn dieses Schlüsselwort nicht angegeben ist, wird das System Standardgebietsschema-ID verwendet.|

## <a name="command-text"></a>Befehlstext
 Die Indizierung Dienst SQL-Abfragesyntax besteht Erweiterungen für die SQL-92 **wählen** Anweisung und die zugehörige **FROM** und **, in denen** Klauseln. Die Ergebnisse der Abfrage zurückgegeben werden, über den OLE DB-Rowsets, die von ADO verwendet und als bearbeitet werden können [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte.

 Sie können nach Wörtern oder Ausdrücken suchen oder Platzhalter verwenden, um Muster oder Wortstämmen suchen. Die Suchlogik kann für boolesche Entscheidungen, gewichteten Begriffen oder Nähe zu den anderen Wörtern basieren. Sie können auch suchen, indem die Übereinstimmungen werden basierend auf der Bedeutung, anstatt genauen Wörter findet "freiem Text".

 Der spezifische Befehlsdialekt wird vollständig in die Abfragesprachen zum Indexdienst-Dokumentation dokumentiert.

 Der Anbieter akzeptiert keine Aufrufe von gespeicherten Prozeduren oder einfache Tabellennamen (z. B. die [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) Eigenschaft werden immer **AdCmdText**).

## <a name="recordset-behavior"></a>Recordset-Verhalten
 Die folgenden Tabellen enthalten die Funktionen zur Verfügung, mit einem **Recordset** Objekt mit diesem Anbieter geöffnet. Nur der statische Cursor-Datentyp (**AdOpenStatic**) verfügbar ist.

 Ausführlichere Informationen zu **Recordset** Verhalten für die Anbieterkonfiguration kann durch Ausführen der [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode und für das Auflisten der [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von der **Recordset** zu bestimmen, ob die anbieterspezifische dynamische Eigenschaften vorhanden sind.

 **Verfügbarkeit von ADO-Recordset Standardeigenschaften:**

|Eigenschaft|Verfügbarkeit|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|Lese-/Schreibzugriff|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|Lese-/Schreibzugriff|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Schreibgeschützt|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Schreibgeschützt|
|[Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md)*|Lese-/Schreibzugriff|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|Lese-/Schreibzugriff|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|immer **AdUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|immer **AdOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|immer **AdEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|Schreibgeschützt|
|[Filter](../../../ado/reference/ado-api/filter-property.md)|Lese-/Schreibzugriff|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Lese-/Schreibzugriff|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|Nicht verfügbar|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|Lese-/Schreibzugriff|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|Schreibgeschützt|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|Lese-/Schreibzugriff|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Schreibgeschützt|
|[Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md)|Lese-/Schreibzugriff|
|[Status](../../../ado/reference/ado-api/state-property-ado.md)|Schreibgeschützt|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Schreibgeschützt|

 \*Lesezeichen müssen aktiviert sein, auf den Anbieter, damit diese Funktion vorhanden sein, auf die **Recordset**.

 **Verfügbarkeit von Standardmethoden für die ADO-Recordset:**

|Methode|Verfügbar?|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|nein|
|[Abbrechen](../../../ado/reference/ado-api/cancel-method-ado.md)|ja|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|nein|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|nein|
|[Klon](../../../ado/reference/ado-api/clone-method-ado.md)|ja|
|[Schließen](../../../ado/reference/ado-api/close-method-ado.md)|ja|
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|nein|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|ja|
|[Verschieben](../../../ado/reference/ado-api/move-method-ado.md)|ja|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|ja|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|ja|
|[Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)|ja|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|ja|
|[Erneut synchronisieren](../../../ado/reference/ado-api/resync-method.md)|ja|
|[Unterstützt](../../../ado/reference/ado-api/supports-method.md)|ja|
|[Update](../../../ado/reference/ado-api/update-method.md)|nein|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|nein|

 Bestimmte Implementierungsdetails und funktionalen Informationen zu den Microsoft OLE DB-Anbieter für Microsoft Indexdienst finden Sie in der [OLE DB Programmer's Guide](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx), oder besuchen Sie die Web Services-Seite von den Windows NT Server-Webdienst Standort.

## <a name="see-also"></a>Siehe auch
 [CommandType-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Anbietereigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [ Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [unterstützt-Methode](../../../ado/reference/ado-api/supports-method.md)
