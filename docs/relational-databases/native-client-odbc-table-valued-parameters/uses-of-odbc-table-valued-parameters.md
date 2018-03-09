---
title: Verwendungen von ODBC-Tabellenwertparameter | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), scenarios
- ODBC, table-valued parameters
ms.assetid: f1b73932-4570-4a8a-baa0-0f229d9c32ee
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 050d0e33419b2f73fba8e5e7fd011d786fcb9f21
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="uses-of-odbc-table-valued-parameters"></a>Verwendungen von ODBC-Tabellenwertparametern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Thema werden die wichtigsten Benutzerszenarien für die Verwendung von Tabellenwertparametern mit ODBC erläutert:  
  
-   Tabellenwertparameter mit vollständig gebundenen mehrzeiligen Puffern (Senden von Daten als Tabellenwertparameter mit allen Werten im Arbeitsspeicher)  
  
-   Tabellenwertparameter mit Zeilenstreaming (Senden von Daten als Tabellenwertparameter mithilfe von Data-at-Execution)  
  
-   Abrufen von Tabellenwertparameter-Metadaten aus dem Systemkatalog  
  
-   Abrufen von Tabellenwertparameter-Metadaten für eine vorbereitete Anweisung  
  
## <a name="table-valued-parameter-with-fully-bound-multirow-buffers-send-data-as-a-tvp-with-all-values-in-memory"></a>Tabellenwertparameter mit vollständig gebundenen mehrzeiligen Puffern (Senden von Daten als Tabellenwertparameter mit allen Werten im Arbeitsspeicher)  
 Bei der Verwendung mit vollständig gebundenen mehrzeiligen Puffern sind alle Parameterwerte im Arbeitsspeicher verfügbar. Dies ist beispielsweise für eine OLTP-Transaktion typisch, bei der Tabellenwertparameter in eine einzeln gespeicherte Prozedur gepackt werden können. Ohne Tabellenwertparameter wären mehrere Serveraufrufe oder die dynamische Generierung eines komplexen Batches mit mehreren Anweisungen erforderlich.  
  
 Der Tabellenwertparameter selbst gebunden ist, indem [SQLBindParameter](http://go.microsoft.com/fwlink/?LinkId=59328) zusammen mit den anderen Parametern. Nachdem alle Parameter gebunden wurde, wird die Anwendung legt das parameterfokusattribut SQL_SOPT_SS_PARAM_FOCUS für jede Tabellenwertparameter fest und ruft SQLBindParameter für die Spalten der Tabellenwertparameter.  
  
 Der Servertyp für Tabellenwertparameter ist SQL_SS_TABLE, ein neuer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischer Typ. Der C-Bindungstyp für SQL_SS_TABLE muss stets SQL_C_DEFAULT sein. Für den gebundenen Parameter des Tabellenwertparameters werden keine Daten übertragen. Dieser wird zur Übergabe von Tabellenmetadaten und zur Steuerung der Datenübergabe in die einzelnen Spalten des Tabellenwertparameters verwendet.  
  
 Die Länge des Tabellenwertparameters ist auf die Anzahl der an den Server gesendeten Zeilen festgelegt. Die *ColumnSize* -Parameter von SQLBindParameter für einen Tabellenwertparameter gibt die maximale Anzahl von Zeilen, die gesendet werden kann; dies ist die Arraygröße der Spaltenpuffer. *ParameterValuePtr* ist der Parameterpuffer für einen Tabellenwertparameter in SQLBindParameter. *ParameterValuePtr* und die zugehörigen *Pufferlänge* werden verwendet, um den Typnamen des Parameters Tabellenwert-im Bedarfsfall übergeben. Der Typname wird nicht für gespeicherte Prozeduraufrufe benötigt, er ist jedoch für SQL-Anweisungen erforderlich.  
  
 Wenn ein Tabellenwertparameter-Typnamen bei einem Aufruf von SQLBindParameter angegeben ist, muss es als Unicode-Wert, auch bei Anwendungen angegeben werden, die als ANSI-Anwendungen erstellt werden. Wenn Sie einen Tabellenwertparameter-Typnamen mit SQLSetDescField angeben, können Sie ein Literal verwenden, die die Methode entspricht, die die Anwendung erstellt wurde. Der ODBC-Treiber-Manager führt die eventuell erforderliche Unicode-Konvertierung aus.  
  
 Metadaten für Tabellenwertparameter und Tabellenwertparameter-Spalten kann individuell und explizit mithilfe von SQLGetDescRec, SQLSetDescRec SQLGetDescField und SQLSetDescField bearbeitet werden. Allerdings SQLBindParameter überladen ist in der Regel praktischer und erfordert keinen expliziten Deskriptor Zugriff in den meisten Fällen. Dieser Ansatz ist konsistent mit der Definition von SQLBindParameter für andere Datentypen, mit dem Unterschied, dass für einen Tabellenwert-Parameter die betroffenen deskriptorfelder geringfügig sind.  
  
 Manchmal verwendet eine Anwendung einen Tabellenwertparameter mit dynamischem SQL, und der Name des Tabellenwertparameters muss bereitgestellt werden. Wenn dies der Fall ist, und der Tabellenwertparameter nicht im aktuellen Standardschema für die Verbindung definiert ist, müssen SQL_CA_SS_TYPE_CATALOG_NAME und SQL_CA_SS_TYPE_SCHEMA_NAME mithilfe von SQLSetDescField festgelegt werden. Da Tabellentypdefinitionen und Tabellenwertparameter in derselben Datenbank vorliegen müssen, darf SQL_CA_SS_TYPE_CATALOG_NAME nicht festgelegt werden, wenn die Anwendung Tabellenwertparameter verwendet. Andernfalls meldet SQLSetDescField einen Fehler.  
  
 Beispielcode für dieses Szenario finden Sie in der Prozedur `demo_fixed_TVP_binding` in [Tabellenwertparametern &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="table-valued-parameter-with-row-streaming-send-data-as-a-tvp-using-data-at-execution"></a>Tabellenwertparameter mit Zeilenstreaming (Senden von Daten als Tabellenwertparameter mithilfe von Data-at-Execution)  
 In diesem Szenario stellt die Anwendung dem Treiber Zeilen nach Anforderung bereit. Diese werden an den Server gestreamt. Hierdurch wird das Puffern aller Zeilen im Arbeitsspeicher vermieden. Dies ist für Masseneinfügungs-/-updateszenarien repräsentativ. Tabellenwertparameter bieten eine Leistungsfähigkeit, die zwischen Parameterarrays und Massenkopieren liegt. Tabellenwertparameter sind ebenso einfach zu programmieren wie Parameterarrays, sie bieten jedoch eine größere Flexibilität auf dem Server.  
  
 Das Binden des Tabellenwertparameters und der zugehörigen Spalten erfolgt wie im vorherigen Abschnitt "Tabellenwertparameter mit vollständig gebundenen mehrzeiligen Puffern" beschrieben, der Längenindikator des Tabellenwertparameters selbst wird jedoch auf SQL_DATA_AT_EXEC festgelegt. Der Treiber antwortet auf SQLExecute oder SQLExecuteDirect auf die übliche Weise für Data-at-Execution-Parameter – d. h. gibt SQL_NEED_DATA. Wenn der Treiber zum Annehmen von Daten für einen Tabellenwertparameter bereit ist, gibt SQLParamData den Wert der *ParameterValuePtr* in SQLBindParameter.  
  
 Eine Anwendung verwendet SQLPutData für einen Tabellenwertparameter, um die Verfügbarkeit von Daten für die einzelnen Tabellenwertparameter-Spalten anzugeben. Wenn SQLPutData für einen Tabellenwertparameter aufgerufen wird *DataPtr* muss immer null sein und *StrLen_or_Ind* muss 0 oder eine Zahl kleiner oder gleich der Arraygröße für Tabellenwertparameter Parameter-Puffer (die *ColumnSize* -Parameter von SQLBindParameter). Der Wert 0 gibt an, dass keine weiteren Zeilen für den Tabellenwertparameter vorhanden sind, und der Treiber fährt mit der Verarbeitung des nächsten tatsächlichen Prozedurparameters fort. Wenn *StrLen_or_Ind* ist nicht 0 ist, verarbeitet der Treiber die einzelnen Tabellenwertparameter-Spalten auf die gleiche Weise wie nicht-Tabellenwertparametern Parameter gebundene: jede Tabellenwertparameter-Spalte kann die eigentlichen Daten angegeben Länge, SQL_NULL_DATA oder sie können Data at-Execution über seine Längen-/Indikatorpuffer angeben. Tabellenwertparameter-Spalte, die Werte können, durch übergeben werden wiederholte Aufrufe von SQLPutData wie üblich, wird ein Zeichen oder Binärwert stückweise übergeben werden.  
  
 Nachdem alle Tabellenwertparameter-Spalten verarbeitet wurden, kehrt der Treiber zum Tabellenwertparameter zurück, um weitere Tabellenwertparameter-Datenzeilen zu verarbeiten. Bei Data-at-Execution-Tabellenwertparametern führt der Treiber daher nicht den üblichen sequenziellen Scan gebundener Parameter durch. Ein gebundener Tabellenwertparameter wird abgerufen, bis SQLPutData aufgerufen wird, mit *StrLen_Or_IndPtr* gleich 0 (null) zu diesem Zeitpunkt der Treiber Tabellenwertparameter-Spalten übersprungen und wechselt zum nächsten tatsächlich gespeicherten Prozedurparameter.  Wenn SQLPutData einen Indikatorwert größer als oder gleich 1 übergibt, verarbeitet der Treiber Tabellenwertparameter-Spalten und Zeilen sequenziell, bis sie Werte für alle gebundenen Zeilen und Spalten enthält. Anschließend kehrt der Treiber zum Tabellenwertparameter zurück. Zwischen den Empfang von Token für den Tabellenwertparameter von SQLParamData und SQLPutData (Befehls beschäftigt, NULL, n) für einen Tabellenwertparameter aufgerufen wird, die Anwendung muss festgelegt konstituierenden Tabellenwertparameter-Spaltendaten und Indikator Inhalt des Puffers für die nächste Zeile bzw. Zeilen, die an den Server übergeben werden.  
  
 Beispielcode für dieses Szenario finden Sie in der Routine `demo_variable_TVP_binding` in [Tabellenwertparametern &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-from-the-system-catalog"></a>Abrufen von Tabellenwertparameter-Metadaten aus dem Systemkatalog  
 Wenn eine Anwendung SQLProcedureColumns für eine Prozedur, die Tabellenwertparameter-Parameter verfügt aufruft, DATA_TYPE als SQL_SS_TABLE und TYPE_NAME ist der Name des Tabellentyps für den Tabellenwertparameter zurückgegeben. SQLProcedureColumns zurückgegebene Resultset werden zwei zusätzliche Spalten hinzugefügt: SS_TYPE_CATALOG_NAME gibt den Namen des Katalogs, in dem der Tabellentyp des Parameters Tabellenwerts definiert ist und SS_TYPE_SCHEMA_NAME gibt den Namen des Schemas zurück, in dem die Gibt an, in der Tabellentyp des Parameters Tabellenwerts definiert ist. In Übereinstimmung mit der ODBC-Spezifikation werden SS_TYPE_CATALOG_NAME und SS_TYPE_SCHEMA_NAME vor allen treiberspezifischen Spalten angezeigt, die in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzugefügt wurden sowie nach allen Spalten, die von ODBC selbst benötigt werden.  
  
 Die neuen Spalten werden nicht nur für Tabellenwertparameter, sondern auch für Parameter des CLR-benutzerdefinierten Typs aufgefüllt. Die vorhandenen Schema- und Katalogspalten von Parametern des benutzerdefinierten Typs werden noch aufgefüllt, in Zukunft wird die Anwendungsentwicklung jedoch durch gemeinsame Schema- und Katalogspalten für Datentypen, die diese erfordern, erleichtert. (Beachten Sie, dass XML-Schemaauflistungen einige Unterschiede aufweisen und nicht in dieser Änderung enthalten sind.)  
  
 Eine Anwendung verwendet SQLTables die Namen der Tabellentypen wird die gleiche Weise ermittelt, wie für persistente Tabellen, Systemtabellen und Ansichten. Die Einführung eines neuen Tabellentyps ? TABLE TYPE ? ermöglicht es einer Anwendung, Tabellentypen zu identifizieren, die mit Tabellenwertparametern verbunden sind. Tabellentypen und reguläre Tabellen verwenden unterschiedliche Namespaces. Daher können Sie den gleichen Namen für einen Tabellentyp und eine tatsächliche Tabelle verwenden. Für diesen Fall wurde ein neues Anweisungsattribut ? SQL_SOPT_SS_NAME_SCOPE ? eingeführt. Dieses Attribut gibt an, ob SQLTables und andere Katalogfunktionen, die einen Tabellennamen als Parameter akzeptieren den Tabellennamen als den Namen einer tatsächlichen Tabelle oder den Namen eines Tabellentyps interpretieren sollen.  
  
 Eine Anwendung verwendet SQLColumns, um die Spalten für einen Tabellentyp auf die gleiche Weise zu bestimmen, wird für persistente Tabellen, aber müssen zunächst SQL_SOPT_SS_NAME_SCOPE festlegen, um anzugeben, dass sie Tabellentypen anstatt von tatsächlichen Tabellen gearbeitet wird. SQLPrimaryKeys können auch mit Tabellentypen, ebenfalls mithilfe von SQL_SOPT_SS_NAME_SCOPE verwendet werden.  
  
 Beispielcode für dieses Szenario finden Sie in der Routine `demo_metadata_from_catalog_APIs` in [Tabellenwertparametern &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="retrieving-table-valued-parameter-metadata-for-a-prepared-statement"></a>Abrufen von Tabellenwertparameter-Metadaten für eine vorbereitete Anweisung  
 In diesem Szenario verwendet eine Anwendung SQLNumParameters und SQLDescribeParam, um Metadaten für Tabellenwertparameter abzurufen.  
  
 Das IPD-Feld SQL_CA_SS_TYPE_NAME wird verwendet, um den Typnamen für den Tabellenwertparameter abzurufen. Die IPD-Felder SQL_CA_SS_TYPE_SCHEMA_NAME und SQL_CA_SS_TYPE_CATALOG_NAME werden zum Abrufen seines Katalogs bzw. Schemas verwendet.  
  
 Tabellentypdefinitionen und Tabellenwertparameter müssen sich in der gleichen Datenbank befinden. SQLSetDescField meldet einen Fehler aus, wenn eine Anwendung beim Verwenden von Tabellenwertparametern SQL_CA_SS_TYPE_CATALOG_NAME festlegt.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME und SQL_CA_SS_TYPE_SCHEMA_NAME können auch verwendet werden, um den Katalog und das Schema abzurufen, die mit Parametern des CLR-benutzerdefinierten Typs verbunden sind. SQL_CA_SS_TYPE_CATALOG_NAME und SQL_CA_SS_TYPE_SCHEMA_NAME sind Alternativen zu den vorhandenen typspezifischen Katalogschemaattributen für CLR-benutzerdefinierte Typen.  
  
 Eine Anwendung verwendet SQLColumns zum Abrufen von Spaltenmetadaten für Tabellenwertparameter in diesem Szenario, da SQLDescribeParam Metadaten für die Spalten einer Tabellenwertparameter-Spalte zurückgegeben wird.  
  
 Beispielcode für diesen Anwendungsfall finden Sie in der Routine `demo_metadata_from_prepared_statement` in [Tabellenwertparametern &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/use-table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
