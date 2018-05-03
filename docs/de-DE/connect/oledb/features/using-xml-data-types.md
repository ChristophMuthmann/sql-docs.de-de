---
title: Verwenden von XML-Datentypen | Microsoft Docs
description: Verwenden von XML-Datentypen mit OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [OLE DB Driver for SQL Server], xml data type
- OLE DB Driver for SQL Server schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- MSOLEDBSQL, XML
- xml data type [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- OLE DB Driver for SQL Server OLE DB interfaces
- XML [SQL Server], OLE DB Driver for SQL Server
- COLUMNS rowset
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 70ecfb39fc13c5180c704af23e446cbcb4790476
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-xml-data-types"></a>Verwenden von XML-Datentypen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]eingeführt ein **Xml** Datentyp, können Sie zum Speichern von XML-Dokumenten und-Fragmenten in, einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank. Die **Xml** -Datentyp ist ein integrierter Datentyp in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], und einige auf ähnliche Weise wie andere integrierten Typen wie **Int** und **Varchar**. Wie andere integrierte Typen können Sie mit der **Xml** -Datentyp als Spaltentyp beim Erstellen einer Tabelle, als Variablentyp, Parametertyp oder Funktionsrückgabetyp; oder in CAST- und CONVERT-Funktionen.  
  
## <a name="programming-considerations"></a>Überlegungen zur Programmierung  
 XML kann selbstbeschreibend sein, da optional ein XML-Header eingefügt werden kann, der die Codierung des Dokuments angibt, zum Beispiel:  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 Der XML-Standard beschreibt, wie ein XML-Prozessor die für ein Dokument verwendete Codierung durch Überprüfen der ersten Bytes des Dokuments erkennen kann. Es ist möglich, dass die von der Anwendung festgelegte Codierung einen Konflikt mit der im Dokument angegebenen Codierung auslöst. Für Dokumente, die als gebundene Parameter übergeben werden, wird XML von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als binäre Daten behandelt, es werden also keine Konvertierungen vorgenommen, und der XML-Parser kann die im Dokument angegebene Codierung problemlos verwenden. Für XML-Daten, die als WSTR gebunden sind, muss die Anwendung jedoch sicherstellen, dass das Dokument in Unicode codiert ist. Dieses Szenario kann zur Folge haben, laden das Dokument in ein DOM, ändern die Codierung in Unicode und das Dokument serialisiert. Wenn dieser Schritt nicht erfolgt, auftreten datenkonvertierungen, was zu ungültigem oder fehlerhaftem XML.  
  
 Konflikte können auch auftreten, wenn XML in Literalen angegeben wird. Folgendes ist beispielsweise ungültig:  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer 
 DBTYPE_XML ist ein neuer Datentyp für XML in der OLE DB-Treiber für SQL Server. Zusätzlich können XML-Daten über die vorhandenen OLE DB-Typen DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT und DBTYPE_IUNKNOWN aufgerufen werden. Daten in Spalten vom XML-Datentyp können aus einer Spalte in einer OLE DB-Treiber für SQL Server-Rowset in den folgenden Formaten abgerufen werden:  
  
-   Textzeichenfolge  
  
-   Ein **einer ISequentialStream-Schnittstelle**  
  
> [!NOTE]  
>  Der OLE DB-Treiber für SQL Server enthält keinen SAX-Reader, aber die **ISequentialStream** SAX und DOM-Objekte in MSXML kann problemlos übergeben werden.  
  
 **ISequentialStream** sollte für den Abruf großer XML-Dokumente verwendet werden. Die für andere große Werttypen verwendeten Techniken gelten auch für XML. Weitere Informationen finden Sie unter [Datentypen mit umfangreichen Werten mithilfe von](../../oledb/features/using-large-value-types.md).  
  
 Daten in Spalten vom Typ XML in einem Rowset auch abgerufen werden kann, eingefügt oder aktualisiert eine Anwendung über die bekannten Schnittstellen wie z. B. **von IRow:: GetColumns**, **irowchange:: SetColumns**, und **ICommand:: Execute**. Auf ähnliche Weise für den Fall abrufen eine Anwendung kann übergeben entweder eine Textzeichenfolge oder ein **ISequentialStream** an den OLE DB-Treiber für SQL Server.  
  
> [!NOTE]  
>  Zum Senden von XML-Daten im Zeichenfolgenformat über die **ISequentialStream** -Schnittstelle, die Sie abrufen müssen **ISequentialStream** durch Angabe von DBTYPE_IUNKNOWN und Festlegen der *pObject* Argument auf null in der Bindung.  
  
 Wenn abgerufene XML-Daten abgeschnitten werden, weil der Consumerpuffer zu klein ist, wird die Länge möglicherweise als 0xffffffff zurückgegeben, was heißt, dass die Länge unbekannt ist. Dieses Verhalten ist konsistent mit der Implementierung als Datentyp, der an den Client gesendet werden, ohne Längeninformationen die tatsächlichen Daten senden. In einigen Fällen die tatsächliche Länge zurückgegeben kann, wenn der Anbieter z. B. den gesamten Wert zwischengespeichert hat **IRowset:: GetData** und, in denen eine Datenkonvertierung durchgeführt wird.  
  
 An SQL Server gesendete XML-Daten werden vom Server als Binärdaten behandelt. Dieses Verhalten verhindert Konvertierungen und ermöglicht die XML-Parser die XML-Codierung automatisch zu erkennen. Dadurch kann ein breiteres Spektrum von XML-Dokumenten (z. B. in UTF-8 codierte Dokumente) als Eingabe für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] akzeptiert werden.  
  
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
  
 <sup>2</sup>würde den Rahmen dieses Artikels sprengen.  
  
 <sup>3</sup>Format ist UTF-16, keine Bye-reihenfolgemarkierung (BOM), keine codierspezifikation, keine null-Terminierung.  
  
 <sup>4</sup>Format ist UTF-16, keine BOM, keine codierspezifikation, null-Terminierung.  
  
 <sup>5</sup>Format enthält Mehrbytezeichen, die in der Clientcodepage mit null-Abschlusszeichen codiert. Konvertierung aus vom Server bereitgestellten Unicode: beschädigte Daten, verursachen, damit diese Bindung abgeraten wird.  
  
 <sup>6</sup>BY_REF kann verwendet werden.  
  
 <sup>7</sup>UTF-16-Daten müssen mit einer BOM starten. Wenn nicht, wird die Codierung möglicherweise nicht ordnungsgemäß vom Server erkannt.  
  
 <sup>8</sup>kann eine Überprüfung stattfinden bei Erstellen des Accessors oder beim Abrufen. Der Fehler ist DB_E_ERRORSOCCURRED, Bindungsstatus ist auf DBBINDSTATUS_UNSUPPORTEDCONVERSION festgelegt.  
  
 <sup>9</sup>Daten werden in Unicode konvertiert, über die Clientcodepage vor dem Senden an den Server. Wenn die Codierung des Dokuments nicht die Clientcodepage übereinstimmt, kann Daten beschädigt werden, damit diese Bindung strengstens abgeraten wird.  
  
 <sup>10</sup>Daten an den Server gesendet wird immer eine BOM hinzugefügt. Wenn die Daten bereits mit einer BOM begonnen, sein vorhanden stehen dann zwei BOMs am Beginn des Puffers. Der Server verwendet die erste BOM, erkennen die Codierung als UTF-16 und wird diese verworfen. Die zweite BOM wird als geschütztes Leerzeichenzeichen mit Nullbreite interpretiert.  
  
 <sup>11</sup>Format ist UTF-16, keine codierspezifikation, wird vom Server empfangenen Daten eine BOM hinzugefügt. Wenn eine leere Zeichenfolge, die vom Server zurückgegeben wird, wird eine BOM noch an die Anwendung zurückgegeben. Wenn die Pufferlänge eine ungerade Anzahl von Bytes ist, werden die Daten ordnungsgemäß abgeschnitten. Wenn Sie der gesamte Wert in Abschnitten zurückgegeben wird, können diese verkettet werden, um den richtigen Wert wieder zusammenzusetzen.  
  
 <sup>12</sup>Ganzzahlüberlauf-Fehler wird gemeldet, wenn die Länge des Puffers, die weniger als zwei Zeichen ist, nicht genügend Speicher für null-Terminierung bietet.  
  
> [!NOTE]  
>  Es werden keine Daten für NULL XML-Werte zurückgegeben.  
  
 Der XML-Standard erfordert, dass UTF-16-codiertes XML mit einer Bytereihenfolge-Marke (BOM), UTF-16-Zeichencode 0xFEFF beginnt. Bei der Arbeit mit WSTR- und BSTR-Bindungen keine OLE DB-Treiber für SQL Server benötigen oder eine BOM hinzufügen, da die Codierung durch die Bindung impliziert ist. Bei der Verwendung von BYTES-, XML- oder IUNKNOWN-Bindungen liegt das Hauptaugenmerk auf der einfachen Zusammenarbeit mit anderen XML-Prozessoren und Speichersystemen. In diesem Fall muss eine BOM vorhanden ist, mit UTF-16-codiertes XML- und die Anwendung nicht kümmern der tatsächlichen Codierung, da die Mehrheit der XML-Prozessoren (einschließlich SQL Server) die Codierung leitet nach Überprüfen des ersten Bytes des Werts. XML-Daten, die von OLE DB-Treiber für SQL Server mithilfe von BYTES, XML, empfangenen oder IUNKNOWN-Bindungen ist immer in UTF-16 mit einer BOM und ohne eingebettete codierdeklaration codiert.  
  
 Datenkonvertierungen durch OLE DB-Basisdienste (**IDataConvert**) sind nicht auf DBTYPE_XML anwendbar.  
  
 Die Überprüfung erfolgt, wenn Daten an den Server gesendet werden. Die clientseitige Validierung und die Codierung von Änderungen sollten von der Anwendung behandelt. Es wird empfohlen, dass Sie die XML-Daten nicht direkt verarbeiten, aber stattdessen einen DOM- oder SAX-Reader verwenden sollten, um verarbeitet werden.  
  
 DBTYPE_NULL und DBTYPE_EMPTY können für Eingabeparameter gebunden werden, aber nicht für Ausgabeparameter oder Ergebnisse. Ist der Status für Eingabeparameter gebunden, muss er auf DBSTATUS_S_ISNULL oder DBSTATUS_S_DEFAULT festgelegt werden.  
  
 DBTYPE_XML kann in DBTYPE_EMPTY und DBTYPE_NULL konvertiert werden, DBTYPE_EMPTY in DBTYPE_XML, aber DBTYPE_NULL kann nicht in DBTYPE_XML konvertiert werden. Dies stimmt mit DBTYPE_WSTR überein.  
  
 DBTYPE_IUNKNOWN ist eine unterstützte Bindung (wie in der obigen Tabelle gezeigt), aber es gibt keine Konvertierungen zwischen DBTYPE_XML und DBTYPE_IUNKNOWN. DBTYPE_IUNKNOWN kann nicht mit DBTYPE_BYREF verwendet werden.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Hinzufügungen und Änderungen am OLE DB-Rowset  
 OLE DB-Treiber für SQL Server fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schemarowsets.  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>Die COLUMNS- und PROCEDURE_PARAMETERS-Schemarowsets  
 Hinzufügungen zu den Spalten und PROCEDURE_PARAMETERS-Schemarowsets unter anderem die folgenden Spalten:  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Name des Katalogs, in dem eine XML-Schemaauflistung definiert ist. NULL für eine nicht-XML-Spalte oder eine nicht typisierte XML-Spalte.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Der Name eines Schemas, in dem eine XML-schemaauflistung definiert ist. NULL für eine nicht-XML-Spalte oder eine nicht typisierte XML-Spalte.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name der XML-Schemaauflistung. NULL für eine nicht-XML-Spalte oder eine nicht typisierte XML-Spalte.|  
  
#### <a name="the-providertypes-schema-rowset"></a>Das PROVIDER_TYPES-Schemarowset  
 Im PROVIDER_TYPES-Schemarowset ist der COLUMN_SIZE-Wert 0 für die **Xml** -Datentyp, und DATA_TYPE ist DBTYPE_XML.  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>Das SS_XMLSCHEMA-Schemarowset  
 Ein neues Schemarowset SS_XMLSCHEMA wird eingeführt, mit dem Clients XML-Schema-Informationen abrufen können. Das SS_XMLSCHEMA-Rowset enthält die folgenden Spalten:  
  
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
 OLE DB-Treiber für SQL Server fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Eigenschaft legt.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>Die DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe  
 Um die Unterstützung der **Xml** -Datentyp über OLE DB, OLE DB-Treiber für SQL Server implementiert die neue DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe, die folgenden Werte enthält.  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Name des Katalogs (Datenbank), in dem eine XML-Schemaauflistung definiert ist. Ein Teil der SQL dreiteilige Namensbezeichner.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Der Name eines XML-Schemas in der Schemaauflistung. Teil des dreiteiligen SQL-Namensbezeichners.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name der XML-Schemaauflistung im Katalogteil A des dreiteiligen SQL-Namensbezeichners.|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>Die DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe  
 Unterstützt die Erstellung von Tabellen in der **ITableDefinition** -Schnittstelle, OLE DB-Treiber für SQL Server die DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe drei neue Spalten hinzugefügt.  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|Bei typisierten XML-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem das XML-Schema gespeichert ist. Für andere Spaltentypen gibt diese Eigenschaft eine leere Zeichenfolge.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|Bei typisierten XML-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des XML-Schemas angibt, das diese Spalte definiert.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|Bei typisierten XML-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen der XML-Schemaauflistung angibt, die den Wert definiert.|  
  
 Wie die SSPROP_PARAM-Werte sind all diese Eigenschaften optional und standardmäßig leer. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME und SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME können nur angegeben werden, wenn SSPROP_COL_XML_SCHEMACOLLECTIONNAME angegeben ist. Bei der Übergabe von XML an den Server werden diese Werte (falls vorhanden) auf ihr Vorhandensein in der aktuellen Datenbank überprüft, und die Instanzdaten werden mit dem Schema verglichen. In jedem Fall müssen sie entweder alle leer oder alle ausgefüllt sein, um gültig zu sein.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Schnittstelle  
 OLE DB-Treiber für SQL Server fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schnittstellen.  
  
#### <a name="the-isscommandwithparameters-interface"></a>Die ISSCommandWithParameters-Schnittstelle  
 Um unterstützen die **Xml** -Datentyp über OLE DB, OLE DB-Treiber für SQL Server implementiert eine Reihe von Änderungen, z. B. das Hinzufügen der [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) Schnittstelle. Diese neue Schnittstelle erbt von der OLE DB-Kernschnittstelle **ICommandWithParameters**. Zusätzlich zu den drei von geerbten Methoden **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, und **SetParameterInfo**; **ISSCommandWithParameters** bietet die [GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) und [SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) Methoden, mit denen serverspezifische behandeln Datentypen.  
  
> [!NOTE]  
>  Die **ISSCommandWithParameters** -Schnittstelle nutzt auch verwenden, die neue ssparamprops Struktur.  
  
#### <a name="the-icolumnsrowset-interface"></a>Die IDBColumnsRowset-Schnittstelle  
 OLE DB-Treiber für SQL Server fügt die folgenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-bestimmte Spalten in das zurückgegebene Rowset die **IColumnRowset:: GetColumnsRowset** Methode. Diese Spalten enthalten den dreiteiligen Namen einer XML-Schemaauflistung. Für Nicht-XML-Spalten oder nicht typisierte XML-Spalten nehmen alle drei Spalten den Standardwert von NULL an.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Der Katalog, zu dem eine XML-Schemaauflistung gehört.<br /><br /> Andernfalls NULL.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Das Schema, zu dem eine XML-Schemaauflistung gehört. Andernfalls NULL.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Der Name einer XML-Schemaauflistung für typisierte XML-Spalten, andernfalls NULL.|  
  
#### <a name="the-irowset-interface"></a>Die IRowset-Schnittstelle  
 Eine XML-Instanz in eine XML-Spalte wird abgerufen, bis die **IRowset:: GetData** Methode. Je nach Bindung, die vom Client angegeben ist, kann eine XML-Instanz als DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES oder als Schnittstelle über DBTYPE_IUNKNOWN abgerufen werden. Falls der Consumer DBTYPE_BSTR, DBTYPE_WSTR oder DBTYPE_VARIANT angibt, konvertiert der Anbieter die XML-Instanz in den vom Benutzer angeforderten Typ und legt ihn an dem in der zugehörigen Bindung angegebenen Speicherort ab.  
  
 Wenn der Consumer DBTYPE_IUNKNOWN angibt und legt die *pObject* Argument auf NULL, oder legt die *pObject* -Argument auf IID_ISequentialStream setzt, gibt der Anbieter zurück ein **ISequentialStream** -Schnittstelle an den Consumer, sodass der Consumer, die XML-Daten aus der Spalte streamen kann. **ISequentialStream** gibt dann die XML-Daten als Unicode-zeichendatenstrom zurück.  
  
 Wenn ein an DBTYPE_IUNKNOWN gebundener XML-Wert zurückgegeben wird, meldet der Anbieter einen Größenwert von `sizeof (IUnknown *)`. Dieses Verhalten ist konsistent mit dem Ansatz ausgeführt, wenn eine Spalte als DBTYPE_IUnknown oder DBTYPE_IDISPATCH und DBTYPE_IUNKNOWN/ISequentialStream gebunden ist, wenn die genaue Spaltengröße nicht bestimmt werden kann.  
  
#### <a name="the-irowsetchange-interface"></a>Die IRowsetChange-Schnittstelle  
 Es gibt zwei Methoden, wie ein Consumer eine XML-Instanz in einer Spalte aktualisieren kann. Die erste Methode erfolgt durch das Speicherobjekt **ISequentialStream** vom Anbieter erstellt. Der Consumer aufrufen kann die **ISequentialStream:: Write** Methode, um die vom Anbieter zurückgegebene XML-Instanz direkt zu aktualisieren.  
  
 Der zweite Ansatz ist die **IRowsetChange:: SetData** oder **IRowsetChange:: InsertRow** Methoden. Bei dieser Vorgehensweise kann eine XML-Instanz im Consumerpuffer in einer Bindung vom Typ DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML oder DBTYPE_IUNKNOWN angegeben werden.  
  
 Wenn DBTYPE_BSTR, DBTYPE_WSTR oder DBTYPE_VARIANT angegeben wird, speichert der Anbieter die XML-Instanz im Consumerpuffer in der entsprechenden Spalte befinden.  
  
 Wenn DBTYPE_IUNKNOWN/ISequentialStream, angegeben wird Wenn der Consumer keine Speicherobjekt angibt, muss der Consumer erstellen eine **ISequentialStream** im Voraus Objekt, das XML-Dokument mit dem Objekt binden und übergeben Sie dann die Objekt an den Anbieter über das **IRowsetChange:: SetData** Methode. Der Consumer kann auch ein Speicherobjekt erstellen Objekt, das pObject-Argument auf IID_ISequentialStream festgelegt, erstellen Sie eine **ISequentialStream** Objekt, und übergeben Sie dann die **ISequentialStream** -Objekt an die **IRowsetChange:: SetData** Methode. In beiden Fällen kann der Anbieter das XML-Objekt durch Abrufen der **ISequentialStream** -Objekt und fügen Sie ihn in die entsprechende Spalte.  
  
#### <a name="the-irowsetupdate-interface"></a>Die IRowsetUpdate-Schnittstelle  
 **IRowsetUpdate** Schnittstelle stellt Funktionalität für verzögerte Updates bereit. Die Daten in den Rowsets zur Verfügung gestellt werden nicht zur Verfügung gestellt andere Transaktionen bis ruft der Consumer die **IRowsetUpdate:: Update** Methode.  
  
#### <a name="the-irowsetfind-interface"></a>Die IRowsetFind-Schnittstelle  
 Die **irowsetfind:: FindNextRow** -Methode funktioniert nicht mit der **Xml** -Datentyp. Wenn **irowsetfind:: FindNextRow** aufgerufen wird und die *hAccessor* Argument gibt eine Spalte von DBTYPE_XML, wird DB_E_BADBINDINFO zurückgegeben. Dies tritt unabhängig vom Typ der Spalte auf, die durchsucht wird. Für andere Bindungstyp die **FindNextRow** mit DB_E_BADCOMPAREOP schlägt fehl, wenn die Spalte zu durchsuchenden der **Xml** -Datentyp.  
 
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Funktionen](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
