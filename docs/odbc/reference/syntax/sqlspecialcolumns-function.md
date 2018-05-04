---
title: SQLSpecialColumns-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bae2c5a51d7d16798bc2d7fca0e9d38509a0d6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: Gruppe öffnen  
  
 **Zusammenfassung**  
 **SQLSpecialColumns** Ruft die folgenden Informationen zu Spalten innerhalb einer angegebenen Tabelle ab:  
  
-   Die optimale Gruppe von Spalten, die eine Zeile in der Tabelle eindeutig identifiziert.  
  
-   Spalten, die automatisch aktualisiert werden, wenn ein Wert in der Zeile durch eine Transaktion aktualisiert wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *IdentifierType*  
 [Eingabe] Der Typ des zurückzugebenden Spalte. Dabei muss es sich um einen der folgenden Werte sein:  
  
 SQL_BEST_ROWID: Gibt die optimale(n) Spalte(n) oder eine Gruppe von Spalten, die durch Aufrufen der Werte aus der Spalte bzw. Spalten, eine beliebige Zeile in der angegebenen Tabelle eindeutig identifiziert werden kann. Eine Spalte kann entweder eine Pseudospalte speziell für diesen Zweck (wie Oracle ROWID oder Ingres TID) oder die Spalte(n) eines eindeutigen Index für die Tabelle sein.  
  
 SQL_ROWVER: Gibt die Spalte oder Spalten in der angegebenen Tabelle, sofern vorhanden, die von der Datenquelle automatisch aktualisiert werden, wenn ein Wert in der Zeile durch eine Transaktion (wie SQLBase ROWID oder Sybase TIMESTAMP) aktualisiert wird.  
  
 *Katalogname*  
 [Eingabe] Name des Katalogs für die Tabelle. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, denen keine Kataloge vorhanden sind. *Katalogname* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *CatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *CatalogName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Eingabe] Länge in Zeichen des **CatalogName*.  
  
 *schemaName*  
 [Eingabe] Name des Schemas für die Tabelle. Wenn ein Treiber unterstützt die Schemas für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, die keine Schemas. *SchemaName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *SchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *SchemaName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength2*  
 [Eingabe] Länge in Zeichen des **SchemaName*.  
  
 *TableName*  
 [Eingabe] Tabellenname. Dieses Argument darf nicht null-Zeiger sein. *TableName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *TableName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *TableName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength3*  
 [Eingabe] Länge in Zeichen des **TableName*.  
  
 *Scope*  
 [Eingabe] Mindestens erforderliche Bereich der Rowid. Die zurückgegebene Rowid möglicherweise größerem Umfang aufweisen. Dies muss eine der folgenden Ressourcen sein:  
  
 SQL_SCOPE_CURROW: Die Rowid ist garantiert gültig, allerdings nur, wenn in dieser Zeile positioniert. Eine spätere erneute Auswahl mit der Rowid möglicherweise keine Zeile zurück, wenn die Zeile aktualisiert wurde, oder durch eine andere Transaktion gelöscht.  
  
 SQL_SCOPE_TRANSACTION: Die Rowid wird sichergestellt, dass für die Dauer der aktuellen Transaktion gültig ist.  
  
 SQL_SCOPE_SESSION: Die Rowid garantiert gültig (über Transaktionsgrenzen hinweg) für die Dauer der Sitzung sein.  
  
 *NULL zulassen*  
 [Eingabe] Bestimmt, ob besondere Spalten zurückgeben, die einen Nullwert aufweisen darf. Dies muss eine der folgenden Ressourcen sein:  
  
 SQL_NO_NULLS: Schließen Sie spezielle Spalten, die NULL-Werte haben können. Einige Treiber können nicht SQL_NO_NULLS unterstützen, und diese Treiber SQL_NO_NULLS angegeben wurde ein leeres Resultset zurückgegeben werden. Anwendungen sollten für diese Groß-/Kleinschreibung und die Anforderung SQL_NO_NULLS vorbereitet werden, nur dann, wenn es absolut erforderlich ist.  
  
 SQL_NULLABLE: Spezielle Spalten zurück, auch wenn sie NULL-Werte haben können.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSpecialColumns** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLSpecialColumns** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Die *TableName* Argument wurde ein null-Zeiger.<br /><br /> Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *CatalogName* Argument wurde ein null-Zeiger und der SQL_CATALOG_NAME *Infotyp* gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *SchemaName* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese Funktion wurde weiterhin ausgeführt, wenn **SQLSpecialColumns** aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge ist kleiner als 0, aber ungleich-SQL_NTS.<br /><br /> Der Wert eines der Argumente Länge überschritten, der Wert für die maximale Länge für den entsprechenden Namen. Die maximale Länge des Namens abgerufen werden kann, durch den Aufruf **SQLGetInfo** mit der *Infotyp* Werte: SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN oder SQL_MAX_TABLE_NAME_LEN.|  
|HY097|Spaltentyp außerhalb des gültigen Bereichs|(DM) eine ungültige *IdentifierType* Wert angegeben wurde.|  
|HY098|Bereichstyp außerhalb des gültigen Bereichs|(DM) eine ungültige *Bereich* Wert angegeben wurde.|  
|HY099|Nullable-Typ außerhalb des gültigen Bereichs|(DM) eine ungültige *Nullable* Wert angegeben wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Ein Katalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Ein Schema angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.<br /><br /> Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle, die das angeforderte Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Wenn die *IdentifierType* Argument ist SQL_BEST_ROWID, **SQLSpecialColumns** gibt die Spalte oder Spalten, die jede Zeile in der Tabelle eindeutig identifizieren. Diese Spalten können immer verwendet werden, einem *Select-Liste* oder **, in denen** Klausel. **SQLColumns**, der verwendet wird, um eine Vielzahl von Informationen für die Spalten einer Tabelle zurückzugeben ist nicht unbedingt zurück, die Spalten, die jede Zeile eindeutig identifizieren oder Spalten, die automatisch aktualisiert werden, wenn ein in der Zeile Wert wird aktualisiert, indem ein die Transaktion. Beispielsweise **SQLColumns** möglicherweise nicht die Oracle-Pseudospalte ROWID zurück. Deswegen **SQLSpecialColumns** wird verwendet, um diese Spalten zurück. Weitere Informationen finden Sie unter [der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Wenn es sind keine Spalten, die jede Zeile in der Tabelle eindeutig identifizieren **SQLSpecialColumns** gibt ein Rowset mit keine Zeilen; ein nachfolgender Aufruf von **SQLFetch** oder **SQLFetchScroll**für die Anweisung gibt SQL_NO_DATA zurück.  
  
 Wenn die *IdentifierType*, *Bereich*, oder *Nullable* Argumente angeben, Eigenschaften, die nicht von der Datenquelle unterstützt werden **SQLSpecialColumns**  gibt ein leeres Resultset zurück.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist die *CatalogName*, *SchemaName*, und *TableName* Argumente werden als Bezeichner, behandelt, sodass sie ein null-Zeiger in bestimmten Situationen kann festgelegt werden. (Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).)  
  
 **SQLSpecialColumns** gibt die Ergebnisse als standard Resultset, geordnet nach Bereich zurück.  
  
 Die folgenden Spalten wurden umbenannt für ODBC 3.*.x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC 3.*.x* Spalte|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 Um die tatsächliche Länge der COLUMN_NAME-Spalte zu bestimmen, kann eine Anwendung aufrufen **SQLGetInfo** mit der Option SQL_MAX_COLUMN_NAME_LEN.  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 8 (PSEUDO_COLUMN) können vom Treiber definiert werden. Eine Anwendung sollte Zugriff auf treiberspezifische Spalten erhalten, beginnend das Ende des Resultsets, anstatt eine explizite Ordnungsposition angeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spaltennummer|Datentyp|Kommentare|  
|-----------------|-------------------|---------------|--------------|  
|BEREICH (ODBC 1.0)|1|Smallint|Der Bereich der Rowid. Enthält die folgenden Werte:<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> NULL wird zurückgegeben, wenn *IdentifierType* SQL_ROWVER ist. Eine Beschreibung der einzelnen Werten, finden Sie unter der Beschreibung der *Bereich* in "Syntax" weiter oben in diesem Abschnitt.|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar, die nicht NULL|Spaltenname. Der Treiber gibt eine leere Zeichenfolge für eine Spalte, die nicht über einen Namen verfügt.|  
|DATA_TYPE (ODBC 1.0)|3|Smallint nicht NULL|SQL-Datentyp. Dies kann einen ODBC-SQL-Datentyp oder treiberspezifischen SQL-Datentyp sein. Eine Liste der gültigen ODBC SQL-Datentypen, finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md). Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.|  
|TYPE_NAME (ODBC 1.0)|4|Varchar, die nicht NULL|Data Source – abhängiger Datentypname; "z. B. CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" oder "CHAR () für BIT-Daten".|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|Die Größe der Spalte in der Datenquelle. Weitere Informationen über die Spaltengröße finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|Die Länge in Bytes der Daten übertragen werden, auf ein **SQLGetData** oder **SQLFetch** Vorgang Wenn SQL_C_DEFAULT angegeben wird. Für numerische Daten möglicherweise anders als die Größe der in der Datenquelle gespeicherten Daten diese Größe. Dieser Wert ist identisch mit der COLUMN_SIZE-Spalte für Zeichen- oder Binärdaten darstellen. Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|Die Dezimalstellen der Spalte in der Datenquelle. Für Datentypen wird NULL zurückgegeben, in denen sind Dezimalstellen nicht anwendbar. Weitere Informationen über Dezimalstellen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|Gibt an, ob die Spalte eine Pseudospalte, z. B. Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **Hinweis:** für eine optimale Interoperabilität Pseudospalten sollte nicht in Anführungszeichen eingeschlossen werden mit dem Bezeichner Anführungszeichen zurückgegebenes **SQLGetInfo**.|  
  
 Nachdem die Anwendung für SQL_BEST_ROWID Ruft Werte ab, die Anwendung können diese Werte Sie diese Zeile innerhalb des definierten Bereichs erneut. Die **wählen** Anweisung wird sichergestellt, dass keine Zeilen oder eine Zeile zurückgegeben.  
  
 Wenn eine Anwendung eine Zeile, die auf Grundlage des Rowid-Spalte oder Spalten reselects aus, und die Zeile wurde nicht gefunden, kann die Anwendung davon ausgehen, dass die Zeile gelöscht wurde oder die Rowid Spalten geändert wurden. Das Gegenteil trifft nicht zu: auch wenn die Rowid nicht geändert hat, können die anderen Spalten in der Zeile geändert haben.  
  
 Spalten, die für den Spaltentyp SQL_BEST_ROWID eignen sich für Anwendungen, vorwärts und zurück in ein Resultset zum Abrufen der neuesten Daten aus einem Satz von Zeilen zurückgegeben werden. Die Spalte oder Spalten der Rowid garantiert nicht geändert werden, während in dieser Zeile positioniert.  
  
 Die Spalte oder Spalten der Rowid möglicherweise gültig bleiben, selbst wenn der Cursor sich nicht auf die Zeile befindet; die Anwendung kann dies durch Überprüfen der Spalte "Umfang" im Resultset bestimmen.  
  
 Für Spaltentyp SQL_ROWVER eignen sich für Anwendungen, die Möglichkeit zu überprüfen, ob alle Spalten in einer bestimmten Zeile aktualisiert wurden, während die Zeile wieder aktiviert wurde, mit der Rowid zurückgegebenen Spalten. Nach dem Auswählen einer Zeile mit der Rowid, kann die Anwendung z. B. die vorherigen Werte in den Spalten SQL_ROWVER den gerade abgerufenen Werten vergleichen. Der Wert in einer Spalte SQL_ROWVER aus dem vorherigen Wert unterscheidet, kann die Anwendung den Benutzer eine Warnung ausgegeben, den Daten in der Anzeige geändert wurden.  
  
## <a name="code-example"></a>Codebeispiel  
 Ein Codebeispiel eine ähnliche Funktion, finden Sie unter [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Spalten in einer Tabelle oder Tabellen|[SQLColumns-Funktion](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Die Spalten des Primärschlüssels zurückgegeben werden|[SQLPrimaryKeys-Funktion](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
