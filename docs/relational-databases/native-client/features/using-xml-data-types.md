---
title: Verwenden von XML-Datentypen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [SQL Server Native Client], xml data type
- SQL Server Native Client OLE DB schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- SQL Server Native Client OLE DB interfaces
- XML [SQL Server], SQL Server Native Client
- COLUMNS rowset
ms.assetid: a7af5b72-c5c2-418d-a636-ae4ac6270ee5
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 55d4d1870ae0224270384db643640bc5d93fd419
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-xml-data-types"></a>Verwenden von XML-Datentypen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]eingeführt ein **Xml** Datentyp, können Sie zum Speichern von XML-Dokumenten und-Fragmenten in, einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank. Die **Xml** -Datentyp ist ein integrierter Datentyp in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], und einige auf ähnliche Weise wie andere integrierten Typen wie **Int** und **Varchar**. Wie andere integrierte Typen können Sie mit der **Xml** -Datentyp als Spaltentyp beim Erstellen einer Tabelle, als Variablentyp, Parametertyp oder Funktionsrückgabetyp; oder in CAST- und CONVERT-Funktionen.  
  
## <a name="programming-considerations"></a>Überlegungen zur Programmierung  
 XML kann selbstbeschreibend sein, da optional ein XML-Header eingefügt werden kann, der die Codierung des Dokuments angibt, zum Beispiel:  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 Der XML-Standard beschreibt, wie ein XML-Prozessor die für ein Dokument verwendete Codierung durch Überprüfen der ersten Bytes des Dokuments erkennen kann. Es ist möglich, dass die von der Anwendung festgelegte Codierung einen Konflikt mit der im Dokument angegebenen Codierung auslöst. Für Dokumente, die als gebundene Parameter übergeben werden, wird XML von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als binäre Daten behandelt, es werden also keine Konvertierungen vorgenommen, und der XML-Parser kann die im Dokument angegebene Codierung problemlos verwenden. Für XML-Daten, die als WSTR gebunden sind, muss die Anwendung jedoch sicherstellen, dass das Dokument in Unicode codiert ist. Daraufhin wird das Dokument möglicherweise in ein DOM geladen, die Codierung in Unicode geändert und das Dokument serialisiert. Wenn dies nicht gemacht wird, finden eventuell Datenkonvertierungen statt und führen zu ungültigem oder fehlerhaftem XML.  
  
 Konflikte können auch auftreten, wenn XML in Literalen angegeben wird. Folgendes ist beispielsweise ungültig:  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 DBTYPE_XML ist ein neuer Datentyp für XML im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter. Zusätzlich können XML-Daten über die vorhandenen OLE DB-Typen DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT und DBTYPE_IUNKNOWN aufgerufen werden. Daten, die in XML-Spalten gespeichert wurden, können in einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter-Rowset in den folgenden Formaten aus der Spalte abgerufen werden:  
  
-   Textzeichenfolge  
  
-   Ein **einer ISequentialStream-Schnittstelle**  
  
> [!NOTE]  
>  Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter umfasst keinen SAX-Reader, aber die **ISequentialStream** SAX und DOM-Objekte in MSXML kann problemlos übergeben werden.  
  
 **ISequentialStream** verwenden, die für den Abruf großer XML-Dokumente verwendet werden soll. Die für andere große Werttypen verwendeten Techniken gelten auch für XML. Weitere Informationen finden Sie unter [Datentypen mit umfangreichen Werten mithilfe von](../../../relational-databases/native-client/features/using-large-value-types.md).  
  
 Daten in Spalten vom Typ XML in einem Rowset auch abgerufen werden kann, eingefügt oder aktualisiert eine Anwendung über die bekannten Schnittstellen wie z. B. **von IRow:: GetColumns**, **irowchange:: SetColumns**, und **ICommand:: Execute**. Auf ähnliche Weise für den Fall abrufen eine Anwendung kann übergeben entweder eine Textzeichenfolge oder ein **ISequentialStream** auf die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter.  
  
> [!NOTE]  
>  Zum Senden von XML-Daten im Zeichenfolgenformat über die **ISequentialStream** -Schnittstelle, die Sie abrufen müssen **ISequentialStream** durch Angabe von DBTYPE_IUNKNOWN und Festlegen der *pObject* Argument auf null in der Bindung.  
  
 Wenn abgerufene XML-Daten abgeschnitten werden, weil der Consumerpuffer zu klein ist, wird die Länge möglicherweise als 0xffffffff zurückgegeben, was heißt, dass die Länge unbekannt ist. Dies ist mit der Implementierung als Datentyp, der als Datenstrom an den Client gesendet wird, ohne Längeninformationen vorab zu senden, konsistent. In einigen Fällen die tatsächliche Länge zurückgegeben kann, wenn der Anbieter z. B. den gesamten Wert zwischengespeichert hat **IRowset:: GetData** und, in denen eine Datenkonvertierung durchgeführt wird.  
  
 An SQL Server gesendete XML-Daten werden vom Server als Binärdaten behandelt. Dies verhindert Konvertierungen und ermöglicht es dem XML-Parser, die XML-Codierung automatisch zu erkennen. Dadurch kann ein breiteres Spektrum von XML-Dokumenten (z. B. in UTF-8 codierte Dokumente) als Eingabe für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] akzeptiert werden.  
  
 Wenn die XML-Eingabe als DBTYPE_WSTR gebunden ist, muss die Anwendung sicherstellen, dass sie bereits in Unicode codiert wurde, um mögliche Beschädigungen durch Datenkonvertierung zu verhindern.  
  
### <a name="data-bindings-and-coercions"></a>Datenbindungen und -umwandlungen  
 Die folgende Tabelle beschreibt die Bindung und Umwandlung bei Verwendung der aufgeführten Datentypen mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Xml** -Datentyp.  
  
|Datentyp|Zu Server<br /><br /> **XML**|Zu Server<br /><br /> **Nicht-XML-**|Von Server<br /><br /> **XML**|Von Server<br /><br /> **Nicht-XML-**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|Pass-through-<sup>6 7</sup>|Fehler<sup>1</sup>|OK<sup>11, 6</sup>|Fehler<sup>8</sup>|  
|DBTYPE_BYTES|Pass-through-<sup>6 7</sup>|N/A<sup>2</sup>|OK <sup>11, 6</sup>|N/A <sup>2</sup>|  
|DBTYPE_WSTR|Pass-through-<sup>6,10</sup>|N/A <sup>2</sup>|OK<sup>4, 6, 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_BSTR|Pass-through-<sup>6,10</sup>|N/A <sup>2</sup>|OK <sup>3</sup>|N/A <sup>2</sup>|  
|DBTYPE_STR|OK<sup>6, 9, 10</sup>|N/A <sup>2</sup>|OK<sup>5, 6, 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_IUNKNOWN|Bytedatenstrom über **ISequentialStream**<sup>7</sup>|N/A <sup>2</sup>|Bytedatenstrom über **ISequentialStream**<sup>11</sup>|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Pass-through-<sup>6 7</sup>|N/A <sup>2</sup>|–|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Pass-through-<sup>6,10</sup>|N/A <sup>2</sup>|OK<sup>3</sup>|N/A <sup>2</sup>|  
  
 <sup>1</sup>, wenn ein anderer Servertyp als DBTYPE_XML mit Indexparametern **ICommandWithParameters:: SetParameterInfo** und ist der Accessortyp DBTYPE_XML, ein Fehler auftritt, wenn die Anweisung ausgeführt wird (DB_E_ERRORSOCCURRED, der Parameterstatus ist DBSTATUS_E_BADACCESSOR); andernfalls werden die Daten an den Server gesendet, der Server gibt jedoch einen Fehler bedeutet, dass keine implizite Konvertierung aus XML-Datentyp des Parameters.  
  
 <sup>2</sup>Gegenstand dieses Themas.  
  
 <sup>3</sup>Format ist UTF-16, keine Bye-reihenfolgemarkierung (BOM), keine codierspezifikation, keine null-Terminierung.  
  
 <sup>4</sup>Format ist UTF-16, keine BOM, keine codierspezifikation, null-Terminierung.  
  
 <sup>5</sup>Format enthält Mehrbytezeichen, die in der Clientcodepage mit null-Abschlusszeichen codiert. Konvertierung aus vom Server bereitgestelltem Unicode verursacht möglicherweise Datenbeschädigung, daher wird diese Bindung nicht empfohlen.  
  
 <sup>6</sup>BY_REF kann verwendet werden.  
  
 <sup>7</sup>UTF-16-Daten müssen mit einer BOM starten. Wenn nicht, wird die Codierung möglicherweise nicht ordnungsgemäß vom Server erkannt.  
  
 <sup>8</sup>kann eine Überprüfung stattfinden bei Erstellen des Accessors oder beim Abrufen. Der Fehler ist DB_E_ERRORSOCCURRED, Bindungsstatus ist auf DBBINDSTATUS_UNSUPPORTEDCONVERSION festgelegt.  
  
 <sup>9</sup>Daten werden in Unicode konvertiert, über die Clientcodepage vor dem Senden an den Server. Falls die Dokumentcodierung nicht mit der Clientcodepage übereinstimmt, kann es zu Datenbeschädigungen kommen, daher wird diese Bindung nicht empfohlen.  
  
 <sup>10</sup>Daten an den Server gesendet wird immer eine BOM hinzugefügt. Falls die Daten bereits mit einer BOM begonnen haben, stehen dann zwei BOMs am Beginn des Puffers. Der Server verwendet die erste BOM, erkennen die Codierung als UTF-16 und wird diese verworfen. Die zweite BOM wird als geschütztes Leerzeichenzeichen mit Nullbreite interpretiert.  
  
 <sup>11</sup>Format ist UTF-16, keine codierspezifikation, wird vom Server empfangenen Daten eine BOM hinzugefügt. Wenn eine leere Zeichenfolge, die vom Server zurückgegeben wird, wird eine BOM noch an die Anwendung zurückgegeben. Wenn die Pufferlänge eine ungerade Anzahl von Bytes ist, werden die Daten ordnungsgemäß abgeschnitten. Wenn Sie der gesamte Wert in Abschnitten zurückgegeben wird, können diese verkettet werden, um den richtigen Wert wieder zusammenzusetzen.  
  
 <sup>12</sup>Ganzzahlüberlauf-Fehler wird gemeldet, wenn die Länge des Puffers ist kleiner als zwei Zeichen, das ist nicht genügend Speicher für null-Terminierung bietet.  
  
> [!NOTE]  
>  Es werden keine Daten für NULL XML-Werte zurückgegeben.  
  
 Der XML-Standard erfordert, dass UTF-16-codiertes XML mit einer Bytereihenfolge-Marke (BOM), UTF-16-Zeichencode 0xFEFF beginnt. Bei der Arbeit mit WSTR- und BSTR-Bindungen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client erforderlich ist oder eine BOM hinzufügen, da die Codierung durch die Bindung impliziert ist. Bei der Verwendung von BYTES-, XML- oder IUNKNOWN-Bindungen liegt das Hauptaugenmerk auf der einfachen Zusammenarbeit mit anderen XML-Prozessoren und Speichersystemen. In diesem Fall sollte für UTF-16-codiertes XML eine BOM vorhanden sein, und die Anwendung sollte sich nicht um die eigentliche Codierung kümmern, da die Mehrheit der XML-Prozessoren (einschließlich SQL Server) die Codierung nach Überprüfen des ersten Bytes des Wertes ableitet. XML-Daten aus empfangenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mit der BYTES, XML- oder IUNKNOWN ist immer Bindungen in UTF-16 mit einer BOM und ohne eingebettete codierdeklaration codiert.  
  
 Datenkonvertierungen durch OLE DB-Basisdienste (**IDataConvert**) sind nicht auf DBTYPE_XML anwendbar.  
  
 Die Überprüfung erfolgt, wenn Daten an den Server gesendet werden. Die clientseitige Gültigkeitsprüfung und Codierungsänderungen sollten von Ihrer Anwendung ausgeführt werden. Es wird nachdrücklich empfohlen, die XML-Daten nicht direkt zu verarbeiten, sondern einen DOM- oder SAX-Reader zur Verarbeitung zu verwenden.  
  
 DBTYPE_NULL und DBTYPE_EMPTY können für Eingabeparameter gebunden werden, aber nicht für Ausgabeparameter oder Ergebnisse. Ist der Status für Eingabeparameter gebunden, muss er auf DBSTATUS_S_ISNULL oder DBSTATUS_S_DEFAULT festgelegt werden.  
  
 DBTYPE_XML kann in DBTYPE_EMPTY und DBTYPE_NULL konvertiert werden, DBTYPE_EMPTY in DBTYPE_XML, aber DBTYPE_NULL kann nicht in DBTYPE_XML konvertiert werden. Dies stimmt mit DBTYPE_WSTR überein.  
  
 DBTYPE_IUNKNOWN ist eine unterstützte Bindung (wie in der Tabelle oben gezeigt), aber es gibt keine Konvertierungen zwischen DBTYPE_XML und DBTYPE_IUNKNOWN. DBTYPE_IUNKNOWN kann nicht mit DBTYPE_BYREF verwendet werden.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Hinzufügungen und Änderungen am OLE DB-Rowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schemarowsets.  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>Die COLUMNS- und PROCEDURE_PARAMETERS-Schemarowsets  
 Den COLUMNS- und PROCEDURE_PARAMETERS-Schemarowsets wurden unter anderem die folgenden Spalten hinzugefügt.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Name des Katalogs, in dem eine XML-Schemaauflistung definiert ist. NULL für eine Nicht-XML-Spalte oder nicht typisierte XML-Spalte.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Der Name eines Schemas, in dem eine XML-schemaauflistung definiert ist. NULL für eine Nicht-XML-Spalte oder nicht typisierte XML-Spalte.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name der XML-Schemaauflistung. NULL für eine Nicht-XML-Spalte oder nicht typisierte XML-Spalte.|  
  
#### <a name="the-providertypes-schema-rowset"></a>Das PROVIDER_TYPES-Schemarowset  
 Im PROVIDER_TYPES-Schemarowset ist der COLUMN_SIZE-Wert 0 für die **Xml** -Datentyp, und DATA_TYPE ist DBTYPE_XML.  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>Das SS_XMLSCHEMA-Schemarowset  
 Ein neues Schemarowset SS_XMLSCHEMA wird eingeführt, mit dem Clients XML-Schema-Informationen abrufen können. Das SS_XMLSCHEMA-Rowset enthält folgende Spalten.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Katalog, zu dem eine XML-Auflistung gehört.|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Das Schema, zu dem eine XML-Auflistung gehört.|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name einer XML-schemaauflistung für typisierte XML-Spalten, andernfalls NULL.|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|Der Zielnamespace eines XML-Schemas.|  
|SCHEMACONTENT|DBTYPE_WSTR|Der Inhalt der XML-Schemas.|  
  
 Jedes XML-Schema wird nach Katalogname, Schemaname, Schemaauflistung und Zielnamespace-URI (Uniform Resource Identifier) einem Bereich zugeordnet. Außerdem wird eine neue GUID mit dem Namen DBSCHEMA_XML_COLLECTIONS definiert. Die Anzahl von Einschränkungen und eingeschränkten Spalten für das SS_XMLSCHEMA-Schemarowset wird wie folgt definiert.  
  
|GUID|Anzahl der Einschränkungen|Eingeschränkte Spalten|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Eigenschaftengruppe  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Eigenschaft legt.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>Die DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe  
 Um die Unterstützung der **Xml** -Datentyp über OLE DB [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementiert die neue DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe, die folgenden Werte enthält.  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Name des Katalogs (Datenbank), in dem eine XML-Schemaauflistung definiert ist. Ein Teil der SQL dreiteilige Namensbezeichner.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Der Name eines XML-Schemas in der Schemaauflistung. Teil des dreiteiligen SQL-Namensbezeichners.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name der XML-Schemaauflistung im Katalogteil A des dreiteiligen SQL-Namensbezeichners.|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>Die DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe  
 Unterstützt die Erstellung von Tabellen in der **ITableDefinition** Schnittstelle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client der DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe drei neue Spalten hinzugefügt.  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|Bei typisierten XML-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem das XML-Schema gespeichert ist. Für andere Spaltentypen gibt diese Eigenschaft eine leere Zeichenfolge zurück.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|Bei typisierten XML-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des XML-Schemas angibt, das diese Spalte definiert.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|Bei typisierten XML-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen der XML-Schemaauflistung angibt, die den Wert definiert.|  
  
 Wie die SSPROP_PARAM-Werte sind all diese Eigenschaften optional und standardmäßig leer. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME und SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME können nur angegeben werden, wenn SSPROP_COL_XML_SCHEMACOLLECTIONNAME angegeben ist. Bei der Übergabe von XML an den Server werden diese Werte (falls vorhanden) auf ihr Vorhandensein in der aktuellen Datenbank überprüft, und die Instanzdaten werden mit dem Schema verglichen. In jedem Fall müssen sie entweder alle leer oder alle ausgefüllt sein, um gültig zu sein.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Schnittstelle  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schnittstellen.  
  
#### <a name="the-isscommandwithparameters-interface"></a>Die ISSCommandWithParameters-Schnittstelle  
 Um unterstützen die **Xml** -Datentyp über OLE DB [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementiert eine Reihe von Änderungen, z. B. das Hinzufügen der [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) Schnittstelle. Diese neue Schnittstelle erbt von der OLE DB-Kernschnittstelle **ICommandWithParameters**. Zusätzlich zu den drei von geerbten Methoden **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, und **SetParameterInfo**; **ISSCommandWithParameters** bietet die [GetParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) und [SetParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) Methoden, die verwendet werden, um Datentypen zu behandeln.  
  
> [!NOTE]  
>  Die **ISSCommandWithParameters** -Schnittstelle nutzt auch verwenden, die neue ssparamprops Struktur.  
  
#### <a name="the-icolumnsrowset-interface"></a>Die IDBColumnsRowset-Schnittstelle  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt die folgenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-bestimmte Spalten in das zurückgegebene Rowset die **IColumnRowset:: GetColumnsRowset** Methode. Diese Spalten enthalten den dreiteiligen Namen einer XML-Schemaauflistung. Für Nicht-XML-Spalten oder nicht typisierte XML-Spalten nehmen alle drei Spalten den Standardwert von NULL an.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Katalog, zu dem eine XML-Schemaauflistung gehört.<br /><br /> Andernfalls NULL.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Das Schema, zu dem eine XML-Schemaauflistung gehört. Andernfalls NULL.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name einer XML-Schemaauflistung für typisierte XML-Spalten, andernfalls NULL.|  
  
#### <a name="the-irowset-interface"></a>Die IRowset-Schnittstelle  
 Eine XML-Instanz in eine XML-Spalte wird abgerufen, bis die **IRowset:: GetData** Methode. Je nach Bindung, die vom Client angegeben ist, kann eine XML-Instanz als DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES oder als Schnittstelle über DBTYPE_IUNKNOWN abgerufen werden. Falls der Consumer DBTYPE_BSTR, DBTYPE_WSTR oder DBTYPE_VARIANT angibt, konvertiert der Anbieter die XML-Instanz in den vom Benutzer angeforderten Typ und legt ihn an dem in der zugehörigen Bindung angegebenen Speicherort ab.  
  
 Wenn der Consumer DBTYPE_IUNKNOWN angibt und legt die *pObject* Argument auf NULL, oder legt die *pObject* -Argument auf IID_ISequentialStream setzt, gibt der Anbieter zurück ein **ISequentialStream** -Schnittstelle an den Consumer, sodass der Consumer, die XML-Daten aus der Spalte streamen kann. **ISequentialStream** gibt dann die XML-Daten als Unicode-zeichendatenstrom zurück.  
  
 Wenn ein an DBTYPE_IUNKNOWN gebundener XML-Wert zurückgegeben wird, meldet der Anbieter einen Größenwert von `sizeof (IUnknown *)`. Dies stimmt mit der Vorgehensweise für Spalten überein, die als DBTYPE_IUnknown oder DBTYPE_IDISPATCH gebunden sind, sowie für DBTYPE_IUNKNOWN/ISequentialStream, wenn die genaue Spaltengröße nicht bestimmt werden kann.  
  
#### <a name="the-irowsetchange-interface"></a>Die IRowsetChange-Schnittstelle  
 Es gibt zwei Methoden, wie ein Consumer eine XML-Instanz in einer Spalte aktualisieren kann. Die erste Methode erfolgt durch das Speicherobjekt **ISequentialStream** vom Anbieter erstellt. Der Consumer aufrufen kann die **ISequentialStream:: Write** Methode, um die vom Anbieter zurückgegebene XML-Instanz direkt zu aktualisieren.  
  
 Der zweite Ansatz ist die **IRowsetChange:: SetData** oder **IRowsetChange:: InsertRow** Methoden. Bei dieser Vorgehensweise kann eine XML-Instanz im Consumerpuffer in einer Bindung vom Typ DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML oder DBTYPE_IUNKNOWN angegeben werden.  
  
 Im Falle von DBTYPE_BSTR, DBTYPE_WSTR oder DBTYPE_VARIANT speichert der Anbieter die XML-Instanz, die sich im Consumerpuffer befindet, in der entsprechenden Spalte.  
  
 Im Fall von DBTYPE_IUNKNOWN/ISequentialStream, wenn der Consumer keine Speicherobjekt der Consumer muss erstellen eine **ISequentialStream** im Voraus-Objekt, das XML-Dokument mit dem Objekt binden und übergeben Sie das Objekt an dem Anbieter über das **IRowsetChange:: SetData** Methode. Der Consumer kann auch ein Speicherobjekt erstellen Objekt, das pObject-Argument auf IID_ISequentialStream festgelegt, erstellen Sie eine **ISequentialStream** Objekt, und übergeben Sie dann die **ISequentialStream** -Objekt an die **IRowsetChange:: SetData** Methode. In beiden Fällen kann der Anbieter das XML-Objekt durch Abrufen der **ISequentialStream** -Objekt und fügen Sie ihn in die entsprechende Spalte.  
  
#### <a name="the-irowsetupdate-interface"></a>Die IRowsetUpdate-Schnittstelle  
 **IRowsetUpdate** Schnittstelle stellt Funktionalität für verzögerte Updates bereit. Die Daten in den Rowsets zur Verfügung gestellt werden nicht zur Verfügung gestellt andere Transaktionen bis ruft der Consumer die **IRowsetUpdate: Update** Methode.  
  
#### <a name="the-irowsetfind-interface"></a>Die IRowsetFind-Schnittstelle  
 Die **irowsetfind:: FindNextRow** -Methode funktioniert nicht mit der **Xml** -Datentyp. Wenn **irowsetfind:: FindNextRow** aufgerufen wird und die *hAccessor* Argument gibt eine Spalte von DBTYPE_XML, wird DB_E_BADBINDINFO zurückgegeben. Dies tritt unabhängig vom Typ der Spalte auf, die durchsucht wird. Für andere Bindungstyp die **FindNextRow** mit DB_E_BADCOMPAREOP schlägt fehl, wenn die Spalte zu durchsuchenden der **Xml** -Datentyp.  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 In der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber eine Reihe von Änderungen vorgenommen wurden verschiedene Funktionen zur Unterstützung der **Xml** -Datentyp.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Die [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md) Funktion verfügt über drei neue Feldbezeichner, einschließlich SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME und SQL_CA_SS _XML_SCHEMACOLLECTION_NAME.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber meldet SQL_SS_LENGTH_UNLIMITED für die SQL_DESC_DISPLAY_SIZE- und SQL_DESC_LENGTH-Spalten.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 Die [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) Funktion verfügt über drei neue Spalten: SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SS_XML_SCHEMACOLLECTION_SCHEMA_NAME und SS_XML_SCHEMACOLLECTION_NAME. Die vorhandene TYPE_NAME-Spalte dient zur Angabe des Namens des XML-Typs, und DATA_TYPE für eine Spalte oder einen Parameter vom XML-Typ ist SQL_SS_XML.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber meldet SQL_SS_LENGTH_UNLIMITED für COLUMN_SIZE- und CHAR_OCTET_LENGTH-Werte.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber meldet SQL_SS_LENGTH_UNLIMITED, wenn die Größe der Spalte kann, in bestimmt werden der [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) Funktion.  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber meldet SQL_SS_LENGTH_UNLIMITED als maximum für COLUMN_SIZE für den **Xml** -Datentyp in der [SQLGetTypeInfo](../../../relational-databases/native-client-odbc-api/sqlgettypeinfo.md) Funktion.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 Die [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) Funktion weist die gleichen zusätzlichen Spalten wie die **SQLColumns** Funktion.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber meldet SQL_SS_LENGTH_UNLIMITED als maximum für COLUMN_SIZE für den **Xml** -Datentyp.  
  
### <a name="supported-conversions"></a>Unterstützte Umwandlungen  
 Bei der Umwandlung von SQL- in C-Datentypen können SQL_C_WCHAR, SQL_C_BINARY und SQL_C_CHAR unter folgenden Bedingungen in SQL_SS_XML umgewandelt werden:  
  
-   SQL_C_WCHAR: Format ist UTF-16, keine Bytereihenfolge-Marke (BOM), mit NULL-Terminierung.  
  
-   SQL_C_BINARY: Format ist UTF-16, ohne NULL-Terminierung. Den vom Server empfangenen Daten wird immer eine BOM hinzugefügt. Wenn eine leere Zeichenfolge vom Server zurückgegeben wird, wird trotzdem eine BOM an die Anwendung zurückgegeben. Wenn die Pufferlänge eine ungerade Anzahl von Bytes ist, werden die Daten ordnungsgemäß abgeschnitten. Wenn der ganze Wert in Abschnitten zurückgegeben wird, können diese verkettet werden, um wieder den richtigen Wert zusammenzusetzen.  
  
-   SQL_C_CHAR: Format enthält Mehrbytezeichen, die in der Clientcodepage mit NULL-Terminierung codiert sind. Konvertierung aus vom Server bereitgestelltem UTF-16 verursacht möglicherweise Datenbeschädigung, daher wird diese Bindung nicht empfohlen.  
  
 Bei der Umwandlung von C- in SQL-Datentypen können SQL_C_WCHAR, SQL_C_BINARY und SQL_C_CHAR unter folgenden Bedingungen in SQL_SS_XML umgewandelt werden:  
  
-   SQL_C_WCHAR: Den an den Server gesendeten Daten wird immer eine BOM hinzugefügt. Falls die Daten bereits mit einer BOM begonnen haben, stehen dann zwei BOMs am Beginn des Puffers. Der Server verwendet die erste BOM, um die Codierung als UTF-16 zu erkennen, und verwirft sie dann. Die zweite BOM wird als geschütztes Leerzeichenzeichen mit Nullbreite interpretiert.  
  
-   SQL_C_BINARY: Es wird keine Konvertierung ausgeführt, und die Daten werden unverändert an den Server übergeben. UTF-16-Daten müssen mit einer BOM starten. Wenn nicht, wird die Codierung möglicherweise nicht ordnungsgemäß vom Server erkannt.  
  
-   SQL_C_CHAR: Die Daten werden auf dem Client in UTF-16 konvertiert und als SQL_C_WCHAR an den Server gesendet (einschließlich der hinzugefügten BOM). Wenn XML nicht in der Clientcodepage codiert ist, kann dies zu Datenbeschädigungen führen.  
  
 Der XML-Standard erfordert, dass UTF-16-codiertes XML mit einer Bytereihenfolge-Marke (BOM), UTF-16-Zeichencode 0xFEFF beginnt. Bei der Arbeit mit einer Bindung SQL_C_BINARY [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client erforderlich ist oder eine BOM hinzufügen, da die Codierung durch die Bindung impliziert ist. Das Hauptaugenmerk liegt auf der einfachen Zusammenarbeit mit anderen XML-Prozessoren und Speichersystemen. In diesem Fall sollte für UTF-16-codiertes XML eine BOM vorhanden sein, und die Anwendung sollte sich nicht um die eigentliche Codierung kümmern, da die Mehrheit der XML-Prozessoren (einschließlich [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) die Codierung nach Überprüfen des ersten Bytes des Wertes ableitet. XML-Daten aus empfangenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unter Verwendung von SQL_C_BINARY sind immer Bindungen in UTF-16 mit einer BOM und ohne eingebettete codierdeklaration codiert.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
