---
title: SQLColumns-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLColumns
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLColumns
helpviewer_keywords: SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7cb9d78a2ee194779f9e01dfd313ae4846d5a804
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcolumns-function"></a>SQLColumns-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: Gruppe öffnen  
  
 **Zusammenfassung**  
 **SQLColumns** gibt die Liste der Spaltennamen in angegebenen Tabellen zurück. Der Treiber gibt diese Informationen als ein Resultset, auf dem angegebenen *StatementHandle*.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Katalogname*  
 [Eingabe] Name des Katalogs. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt an, die Tabellen, denen keine Kataloge vorhanden sind. *Katalogname* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
> [!NOTE]  
>  Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *CatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *CatalogName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Eingabe] Länge in Zeichen des **CatalogName*.  
  
 *SchemaName*  
 [Eingabe] Zeichenfolge Suchmuster für Schemanamen. Wenn ein Treiber unterstützt die Schemas für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt an, die Tabellen, die keine Schemas aufweisen.  
  
> [!NOTE]  
>  Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *SchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *SchemaName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength2*  
 [Eingabe] Länge in Zeichen des **SchemaName*.  
  
 *Tabellenname*  
 [Eingabe] Zeichenfolge Suchmuster für Tabellennamen auf Richtigkeit.  
  
> [!NOTE]  
>  Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *TableName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *TableName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength3*  
 [Eingabe] Länge in Zeichen des **TableName*.  
  
 *Spaltenname*  
 [Eingabe] Zeichenfolge Suchmuster für Spaltennamen verfügbar.  
  
> [!NOTE]  
>  Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *ColumnName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *ColumnName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength4*  
 [Eingabe] Länge in Zeichen des **ColumnName*.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLColumns** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLColumns** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle* jedoch **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund einer Ressourcendeadlock mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *CatalogName* Argument wurde ein null-Zeiger und der SQL_CATALOG_NAME *Infotyp* gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *SchemaName*, *TableName*, oder *ColumnName* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLColumns** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge "Name" ist kleiner als 0, aber ungleich-SQL_NTS.|  
|||Der Wert eines der Argumente Länge Namen überschritten Wert für maximale Länge für den entsprechenden Katalog oder Namen. Die maximale Länge der einzelnen Katalog oder der Name abgerufen werden kann, durch den Aufruf **SQLGetInfo** mit der *Infotyp* Werte. (Siehe "Kommentare".)|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Ein Katalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Ein Schemaname angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.<br /><br /> Eine Zeichenfolge Suchmuster für Schemaname, Tabellen- oder Spaltenname angegeben wurde, und die Datenquelle unterstützt keine Suchmustern für mindestens eines dieser Argumente.<br /><br /> Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Diese Funktion ist in der Regel vor der anweisungsausführung zum Abrufen von Informationen zu Spalten, die für eine Tabelle oder Tabellen aus der Datenquelle Katalog verwendet. **SQLColumns** dient zum Abrufen von Daten für alle Typen von von zurückgegebenen Elementen **SQLTables**. Zusätzlich zu den Basistabellen identisch, dies eventuell (aber nicht beschränkt auf) Sichten, Synonymen Systemtabellen und So weiter. Im Gegensatz dazu, die Funktionen **SQLColAttribute** und **SQLDescribeCol** beschreiben die Spalten in einem Resultset und die Funktion **SQLNumResultCols** gibt die Anzahl der Spalten in einem Resultset. Weitere Informationen finden Sie unter [der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLColumns** gibt die Ergebnisse als standard Resultset, geordnet nach TABLE_CAT, nach "TABLE_SCHEM", TABLE_NAME und ORDINAL_POSITION zurück.  
  
> [!NOTE]  
>  Wenn eine Anwendung mit einer ODBC 2. funktioniert. *x* -Treiber keine ORDINAL_POSITION-Spalte im Resultset zurückgegeben. Als Ergebnis wird beim Arbeiten mit ODBC-2. *x* Treiber, die Reihenfolge der Spalten in der Spaltenliste zurückgegebenes **SQLColumns** ist nicht unbedingt identisch mit der Reihenfolge der Spalten zurückgegeben, wenn die Anwendung auf allen eine SELECT-Anweisung ausführt Spalten in dieser Tabelle.  
  
> [!NOTE]  
>  **SQLColumns** möglicherweise nicht alle Spalten zurück. Beispielsweise könnte ein Treiber nicht Informationen zu Pseudospalten, z. B. Oracle ROWID zurück. Anwendungen können eine beliebige gültige Spalte, ob sie von zurückgegeben werden **SQLColumns**.  
>   
>  Einige Spalten, die von zurückgegeben werden können **SQLStatistics** werden nicht zurückgegeben **SQLColumns**. Beispielsweise **SQLColumns** keinen Spalten in einem Index erstellt, die über einen Ausdruck oder einen Filter, z. B. Gehalt + Vorteile oder DEPT zurückgibt 0012 =.  
  
 Die Länge von VARCHAR-Spalten werden nicht in der Tabelle angezeigt; die tatsächliche Länge hängen von der Datenquelle ab. Um zu bestimmen, die tatsächliche Länge der Spalten TABLE_CAT, nach "TABLE_SCHEM" Tabellenname und Spaltenname, eine Anwendung aufrufen kann **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, und SQL_MAX_COLUMN_NAME_LEN-Optionen.  
  
 Die folgenden Spalten wurden für ODBC 3. umbenannt. *x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC-3. *x* Spalte|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Die folgenden Spalten wurden zurückgegebenes Resultset hinzugefügt **SQLColumns** für ODBC 3.. *X*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 18 (IS_NULLABLE) können vom Treiber definiert werden. Eine Anwendung sollte treiberspezifischen Spalten zuzugreifen, beginnend am Ende das Resultset statt eine explizite Ordnungsposition anzugeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spalte<br /><br /> number|Datentyp|Kommentare|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Name des Katalogs; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, denen keine Kataloge vorhanden sind.|  
|NACH "TABLE_SCHEM" (ODBC 1.0)|2|Varchar|Schemanamen; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, die keine Schemas aufweisen.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar, die nicht NULL|Tabellenname.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar, die nicht NULL|Spaltenname. Der Treiber gibt eine leere Zeichenfolge für eine Spalte, die nicht über einen Namen verfügt.|  
|DATA_TYPE (ODBC 1.0)|5|Smallint nicht NULL|SQL-Datentyp. Dies kann einen ODBC-SQL-Datentyp oder treiberspezifischen SQL-Datentyp sein. Für "DateTime" und das Intervall Datentypen gibt diese Spalte den präzise-Datentyp (z. B. SQL_TYPE_DATE oder SQL_INTERVAL_YEAR_TO_MONTH, statt die nonconcise Datentyp z. B. SQL_DATETIME oder SQL_INTERVAL) zurück. Eine Liste der gültigen ODBC SQL-Datentypen, finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) in Anhang D:-Datentypen. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.<br /><br /> Die Datentypen für ODBC 3. zurückgegeben. *x* und ODBC 2. *X* Anwendungen können unterschiedlich sein. Weitere Informationen finden Sie unter [Abwärtskompatibilität und zur Einhaltung von Standards](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|TYPE_NAME (ODBC 1.0)|6|Varchar, die nicht NULL|Data Source – abhängiger Datentypname; "z. B. CHAR", "VARCHAR", "MONEY", "LONG VARBINAR" oder "CHAR () für BIT-Daten".|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|Wenn DATA_TYPE SQL_CHAR oder SQL_VARCHAR ist, enthält diese Spalte die maximale Länge in Zeichen der Spalte an. Für Datetime-Datentypen ist dies die Gesamtanzahl von Zeichen erforderlich sind, um den Wert anzuzeigen, wenn er in Zeichen konvertiert wird. Für numerische Datentypen ist dies entweder die Gesamtzahl der Ziffern oder die Gesamtanzahl der Bits, die in der Spalte zulässigen gemäß der NUM_PREC_RADIX-Spalte. Für Interval-Datentypen, ist dies die Anzahl der Zeichen in die zeichendarstellung des Intervalls literal (gemäß der Definition von der Genauigkeit für anführenden Intervallwert, finden Sie unter [Intervall Datentyplänge](../../../odbc/reference/appendixes/interval-data-type-length.md) in Anhang D:-Datentypen). Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|Die Länge in Bytes der Daten, die in einen Vorgang SQLGetData, SQLFetch oder SQLFetchScroll übertragen werden, wenn SQL_C_DEFAULT angegeben wird. Für numerische Daten abweichen diese Größe von der Größe der in der Datenquelle gespeicherten Daten. Dieser Wert kann von COLUMN_SIZE-Spalte für Zeichendaten abweichen. Weitere Informationen zu Länge, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|Die Gesamtanzahl von signifikanten Stellen rechts vom Dezimaltrennzeichen an. SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP enthält diese Spalte die Anzahl der Ziffern in der Komponente für Sekundenbruchteile. Für andere Datentypen ist dies die Dezimalstellen der Spalte in der Datenquelle. Für Interval-Datentypen, die eine Zeitkomponente enthalten, enthält diese Spalte die Anzahl der Ziffern rechts vom Dezimaltrennzeichen (Sekundenbruchteile). Für Interval-Datentypen, die keine Zeitangabe enthalten, ist diese Spalte 0. Weitere Informationen über Dezimalstellen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen. Für Datentypen wird NULL zurückgegeben, in dem kein DECIMAL_DIGITS anwendbar.|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|Für numerische Datentypen 10 oder 2. Wenn es sich um 10 handelt, geben die Werte in der COLUMN_SIZE- und DECIMAL_DIGITS die Anzahl der Dezimalstellen für die Spalte zulässig. Beispielsweise würde eine DECIMAL(12,5) Spalte eine NUM_PREC_RADIX von 10, eine COLUMN_SIZE 12 und eine DECIMAL_DIGITS 5 zurückgegeben. eine Spalte "float" konnte eine NUM_PREC_RADIX von 10, eine COLUMN_SIZE 15 und DECIMAL_DIGITS von NULL zurück.<br /><br /> Wenn 2 ist, geben die Werte in der COLUMN_SIZE- und DECIMAL_DIGITS die Anzahl der Bits, die in der Spalte zulässig. Beispielsweise kann eine Spalte "float" ein Basis 2, eine COLUMN_SIZE 53 und DECIMAL_DIGITS von NULL zurückgeben.<br /><br /> Für Datentypen wird NULL zurückgegeben, in dem kein NUM_PREC_RADIX anwendbar.|  
|NULL-WERTE ZULÄSST (ODBC 1.0)|11|Smallint nicht NULL|SQL_NO_NULLS, wenn die Spalte keine NULL-Werte enthalten kann.<br /><br /> SQL_NULLABLE, wenn die Spalte NULL-Werte annimmt.<br /><br /> SQL_NULLABLE_UNKNOWN, wenn nicht bekannt ist, ob die Spalte NULL-Werte annimmt.<br /><br /> Für diese Spalte zurückgegebene Wert unterscheidet sich von der für die Spalte IS_NULLABLE zurückgegebene Wert. Gibt an, die NULLABLE-Spalte mit Sicherheit, dass eine Spalte NULL-Werte akzeptieren kann, aber nicht mit Sicherheit, dass eine Spalte keine NULL-Werte akzeptiert angeben. Die IS_NULLABLE-Spalte gibt an, mit Sicherheit, dass eine Spalte kann keine NULL-Werte akzeptieren, jedoch nicht mit Sicherheit, dass eine Spalte NULL-Werte akzeptiert angeben.|  
|HINWEISE (ODBC 1.0)|12|Varchar|Eine Beschreibung der Spalte.|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|Der Standardwert der Spalte. Der Wert in dieser Spalte sollten als Zeichenfolge interpretiert werden, wenn er in Anführungszeichen eingeschlossen ist.<br /><br /> Wenn NULL als Standardwert angegeben wurde, ist diese Spalte das Wort NULL, nicht in Anführungszeichen eingeschlossen. Wenn der Standardwert ungekürzt dargestellt werden kann, enthält diese Spalte abgeschnitten, ohne das einfache Anführungszeichen einschließen. Wenn kein Standardwert angegeben wurde, ist diese Spalte NULL.<br /><br /> Beim Generieren einer neuen Spaltendefinition, außer, wenn der Wert abgeschnitten enthalten, kann der Wert des COLUMN_DEF verwendet werden.|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint nicht NULL|SQL-Datentyp, wie er im Feld Datensatz SQL_DESC_TYPE in IRD angezeigt wird. Dies kann einen ODBC-SQL-Datentyp oder treiberspezifischen SQL-Datentyp sein. Diese Spalte entspricht der DATA_TYPE-Spalte, mit Ausnahme von "DateTime" und Interval-Datentypen. Diese Spalte gibt den nonconcise-Datentyp (z. B. SQL_DATETIME oder SQL_INTERVAL) anstelle des präzise-Datentyp (z. B. SQL_TYPE_DATE oder SQL_INTERVAL_YEAR_TO_MONTH) für "DateTime" und die Interval-Datentypen zurück. Wenn diese Spalte SQL_DATETIME oder SQL_INTERVAL zurückgibt, kann im speziellen Datentyp aus der Spalte noch SQL_DATETIME_SUB ermittelt werden. Eine Liste der gültigen ODBC SQL-Datentypen, finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) in Anhang D:-Datentypen. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.<br /><br /> Die Datentypen für ODBC 3. zurückgegeben. *x* und ODBC 2. *X* Anwendungen können unterschiedlich sein. Weitere Informationen finden Sie unter [Abwärtskompatibilität und zur Einhaltung von Standards](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).|  
|NOCH SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|Der Untertypcode für "DateTime" und Interval-Datentypen. Für andere Datentypen gibt diese Spalte einen NULL-Wert zurück. Weitere Informationen zu "DateTime" und das Intervall Untercodes, finden Sie unter "SQL_DESC_DATETIME_INTERVAL_CODE" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|Die maximale Länge in Bytes von einem Zeichen- oder Binärdaten-Datentypspalte. Bei allen anderen Datentypen gibt diese Spalte einen NULL-Wert zurück.|  
|ORDINAL_POSITION (ODBC 3.0)|17|Integer nicht NULL|Die Ordnungsposition einer Spalte innerhalb der Tabelle. Die erste Spalte in der Tabelle ist die Zahl 1.|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|"Nein", wenn die Spalte keine NULL-Werte enthalten.<br /><br /> "YES", wenn die Spalte NULL-Werte einschließen kann.<br /><br /> Die Spalte gibt eine leere Zeichenfolge zurück, wenn die NULL-Zulässigkeit unbekannt ist.<br /><br /> Die NULL-Zulässigkeit wird gemäß den ISO-Regeln bestimmt. Ein ISO SQL – DBMS kann nicht auf eine leere Zeichenfolge zurückgeben.<br /><br /> Für diese Spalte zurückgegebene Wert unterscheidet sich von der für die NULLABLE-Spalte zurückgegebene Wert. (Siehe die Beschreibung der Spalte NULL-Werte zulässt.)|  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel deklariert eine Anwendung Puffer für das zurückgegebene Resultset **SQLColumns**. Sie ruft **SQLColumns** zur Beschreibung von jede Spalte in der EMPLOYEE-Tabelle ein Resultset zurückgegeben. Er ruft dann **SQLBindCol** zum Binden von Spalten im Resultset den Puffern. Zum Schluss die Anwendung ruft jede Zeile der Daten mit **SQLFetch** und verarbeitet es.  
  
```  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Berechtigungen für eine Spalte oder Spalten|[SQLColumnPrivileges-Funktion](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Das Abrufen mehrerer Datenzeilen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Zurückgeben von Spalten, die eine Zeile eindeutig zu identifizieren oder Spalten, die durch eine Transaktion automatisch aktualisiert|[SQLSpecialColumns-Funktion](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|Zurückgeben von Tabellenstatistiken und Indizes|[SQLStatistics-Funktion](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Zurückgeben einer Liste von Tabellen in einer Datenquelle|[SQLTables-Funktion](../../../odbc/reference/syntax/sqltables-function.md)|  
|Zurückgeben von Berechtigungen für eine Tabelle oder Tabellen|[SQLTablePrivileges-Funktion](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
