---
title: SQLProcedureColumns-Funktion | Microsoft Docs
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
apiname: SQLProcedureColumns
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLProcedureColumns
helpviewer_keywords: SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5d5ceb9f955d8eb583181d789847eeb79d1b0a5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLProcedureColumns** gibt die Liste der Eingabe-und Ausgabeparameter als auch die Spalten, die das Resultset für die angegebenen Prozeduren bilden. Die Informationen, die als Resultset auf der angegebenen Anweisung gibt der Treiber.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Katalogname*  
 [Eingabe] Der Name des Katalogs. Wenn ein Treiber Kataloge unterstützt, bei einigen Prozeduren, jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Prozeduren, die keine Kataloge. *Katalogname* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *CatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *CatalogName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Eingabe] Länge in Zeichen des **CatalogName*.  
  
 *SchemaName*  
 [Eingabe] Zeichenfolge Suchmuster für Prozedur Schemanamen. Wenn ein Treiber Schemas unterstützt, bei einigen Prozeduren, jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Prozeduren, die keine Schemas.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *SchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *SchemaName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength2*  
 [Eingabe] Länge in Zeichen des **SchemaName*.  
  
 *ProcName*  
 [Eingabe] Zeichenfolge Suchmuster für Prozedurnamen.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *ProcName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *ProcName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength3*  
 [Eingabe] Länge in Zeichen des **ProcName*.  
  
 *Spaltenname*  
 [Eingabe] Zeichenfolge Suchmuster für Spaltennamen verfügbar.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *ColumnName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *ColumnName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength4*  
 [Eingabe] Länge in Zeichen des **ColumnName*.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLProcedureColumns** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLProcedureColumns** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" steht die Beschreibungen der vom Treiber zurückgegebene SQLSTATEs vor. -Manager. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLError** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *CatalogName* Argument wurde ein null-Zeiger und der SQL_CATALOG_NAME *Infotyp* gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *SchemaName*, *ProcName*, oder *ColumnName* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese Funktion Aynschronous wurde noch ausgeführt werden, wenn die SQLProcedureColumns-Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge "Name" ist kleiner als 0, aber ungleich-SQL_NTS.<br /><br /> Der Wert eines der Argumente Namen Länge überschritten Wert für maximale Länge für den entsprechenden Katalog, Schema, Prozedur oder Spaltenname.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Eine Prozedur Catalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Eine prozedurschema angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.<br /><br /> Eine Zeichenfolge Suchmuster für prozedurschema, Name der Prozedur oder Spaltenname angegeben wurde, und die Datenquelle unterstützt keine Suchmustern für mindestens eines dieser Argumente.<br /><br /> Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Diese Funktion ist in der Regel vor der anweisungsausführung zum Abrufen von Informationen zu den Prozedurparametern und den Spalten, aus denen das Resultset oder Mengen, die von der Prozedur zurückgegebene ggf. verwendet. Weitere Informationen finden Sie unter [Prozeduren](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  **SQLProcedureColumns** möglicherweise nicht alle Spalten, die von einer Prozedur verwendete zurück. Ein Treiber kann beispielsweise nur Informationen zu den Parametern, die von einer Prozedur und nicht die Spalten in einem Resultset generierten verwendet zurück.  
  
 Die *SchemaName*, *ProcName*, und *ColumnName* Argumente Suchmustern zu akzeptieren. Weitere Informationen zu gültigen Suchmustern, finden Sie unter [Muster Value-Argumenten](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedureColumns** gibt die Ergebnisse als standard Resultset, geordnet nach PROCEDURE_CAT, PROCEDURE_SCHEM PROCEDURE_NAME und COLUMN_TYPE zurück. Spaltennamen sind für jede Prozedur in der folgenden Reihenfolge: den Namen des Rückgabewerts, die Namen der einzelnen Parameter in dem Prozeduraufruf (in Reihenfolge) und dann die Namen der einzelnen Spalten im Resultset, die von der Prozedur (in der Reihenfolge der Spalten) zurückgegeben.  
  
 Anwendungen sollten treiberspezifischen Spalten relativ zum Ende des Resultsets binden. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
 Um die tatsächliche Länge der Spalten PROCEDURE_CAT, PROCEDURE_SCHEM PROCEDURE_NAME und COLUMN_NAME zu bestimmen, kann eine Anwendung aufrufen **SQLGetInfo** mit der SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_ PROCEDURE_NAME_LEN und SQL_MAX_COLUMN_NAME_LEN-Optionen.  
  
 Die folgenden Spalten wurden für ODBC 3. umbenannt. *x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC-3. *x* Spalte|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROZEDUR _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 Das zurückgegebene Resultset wurden die folgenden Spalten hinzugefügt **SQLProcedureColumns** für ODBC 3.. *X*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 19 (IS_NULLABLE) können vom Treiber definiert werden. Eine Anwendung sollte Zugriff auf treiberspezifische Spalten erhalten, beginnend das Ende des Resultsets, anstatt eine explizite Ordnungsposition angeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spaltennummer|Datentyp|Kommentare|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Katalogname der Prozedur; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge bei einigen Prozeduren unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Verfahren aus, denen keine Kataloge vorhanden sind.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Prozedur Schemanamen; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas bei einigen Prozeduren unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Verfahren, die keine Schemas aufweisen.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar, die nicht NULL|Der Name der Prozedur. Für eine Prozedur, die nicht über einen Namen verfügt, wird eine leere Zeichenfolge zurückgegeben.|  
|COLUMN_NAME (ODBC 2.0)|4|Varchar, die nicht NULL|Der Name der Prozedur-Spalte. Der Treiber gibt eine leere Zeichenfolge für eine Prozedurspalte, die nicht über einen Namen verfügt.|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint nicht NULL|Definiert die Prozedurspalte als Parameter oder einer Resultsetspalte an:<br /><br /> SQL_PARAM_TYPE_UNKNOWN: Prozedurspalte ist ein Parameter, deren Typ unbekannt ist. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT: Prozedurspalte ist ein Eingabeparameter. ODBC (1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT: Prozedurspalte ist ein Eingabe-/Ausgabeparameter. ODBC (1.0)<br /><br /> SQL_PARAM_OUTPUT: Prozedurspalte ist ein Output-Parameter. (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE: Prozedurspalte ist der Rückgabewert der Prozedur. (ODBC 2.0)<br /><br /> SQL_RESULT_COL: Prozedurspalte ist einer Resultsetspalte. ODBC (1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint nicht NULL|SQL-Datentyp. Dies kann einen ODBC-SQL-Datentyp oder treiberspezifischen SQL-Datentyp sein. Für "DateTime" und das Intervall Datentypen gibt diese Spalte die präzisen Datentypen (z. B. SQL_TYPE_TIME oder SQL_INTERVAL_YEAR_TO_MONTH) zurück. Eine Liste der gültigen ODBC SQL-Datentypen, finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) in Anhang D:-Datentypen. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.|  
|TYPE_NAME (ODBC 2.0)|7|Varchar, die nicht NULL|Data Source – abhängiger Datentypname; "z. B. CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" oder "CHAR () für BIT-Daten".|  
|COLUMN_SIZE (ODBC 2.0)|8|Integer|Die Spaltengröße der Prozedurspalte für die Datenquelle. Für Datentypen wird NULL zurückgegeben, in denen ist Spaltengröße nicht anwendbar. Weitere Informationen zu Genauigkeit, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|BUFFER_LENGTH (ODBC 2.0)|9|Integer|Die Länge in Bytes der Daten übertragen werden, auf ein **SQLGetData** oder **SQLFetch** Vorgang Wenn SQL_C_DEFAULT angegeben wird. Für numerische Daten möglicherweise anders als die Größe der in der Datenquelle gespeicherten Daten diese Größe. Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), im Anhang D:-Datentypen.|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|Die Dezimalstellen der Spalte Verfahren für die Datenquelle. Für Datentypen wird NULL zurückgegeben, in denen ist Dezimalstellen nicht anwendbar. Weitere Informationen über Dezimalstellen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md), im Anhang D:-Datentypen.|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|Für numerische Datentypen 10 oder 2.<br /><br /> Wenn 10, geben die Werte in der COLUMN_SIZE- und DECIMAL_DIGITS die Anzahl der Dezimalstellen für die Spalte zulässig. Beispielsweise würde eine DECIMAL(12,5) Spalte eine NUM_PREC_RADIX von 10, eine COLUMN_SIZE 12 und eine DECIMAL_DIGITS 5 zurückgegeben. eine Spalte "float" konnte eine NUM_PREC_RADIX von 10, eine COLUMN_SIZE 15 und DECIMAL_DIGITS von NULL zurück.<br /><br /> Wenn 2, geben die Werte in der COLUMN_SIZE- und DECIMAL_DIGITS die Anzahl der Bits, die in der Spalte zulässig. Beispielsweise kann eine Spalte "float" eine NUM_PREC_RADIX 2, eine COLUMN_SIZE 53 und DECIMAL_DIGITS von NULL zurückgeben.<br /><br /> Für Datentypen wird NULL zurückgegeben, in dem kein NUM_PREC_RADIX anwendbar.|  
|NULL-WERTE ZULÄSST (ODBC 2.0)|12|Smallint nicht NULL|Gibt an, ob die Prozedurspalte einen NULL-Wert akzeptiert:<br /><br /> SQL_NO_NULLS: Prozedurspalte akzeptiert keine NULL-Werte.<br /><br /> SQL_NULLABLE: Prozedurspalte lässt NULL-Werte.<br /><br /> SQL_NULLABLE_UNKNOWN: Es ist nicht bekannt, wenn die Prozedurspalte NULL-Werte annimmt.|  
|HINWEISE (ODBC 2.0)|13|Varchar|Eine Beschreibung der Prozedurspalte.|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|Der Standardwert der Spalte.<br /><br /> Wenn NULL als Standardwert angegeben wurde, ist diese Spalte das Wort NULL, nicht in Anführungszeichen eingeschlossen. Wenn der Standardwert ungekürzt dargestellt werden kann, enthält diese Spalte abgeschnitten, durch keine einschließende einfache Anführungszeichen ein. Wenn kein Standardwert angegeben wurde, ist diese Spalte NULL.<br /><br /> Beim Generieren einer neuen Spaltendefinition, außer, wenn der Wert abgeschnitten enthalten, kann der Wert des COLUMN_DEF verwendet werden.|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint nicht NULL|Der Wert der SQL-Datentyp, wie er in das SQL_DESC_TYPE-Feld des Deskriptors wird angezeigt. Diese Spalte entspricht der DATA_TYPE-Spalte, mit Ausnahme von "DateTime" und Interval-Datentypen.<br /><br /> Für die Datentypen "DateTime" und das Intervall SQL_INTERVAL oder SQL_INTERVAL die SQL_DATA_TYPE-Feld im Resultset zurück, und das Feld noch SQL_DATETIME_SUB dem Subcode für den bestimmten Intervall oder Datetime-Datentyp zurück. (Siehe [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NOCH SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|Der Untertypcode für "DateTime" und Interval-Datentypen. Für andere Datentypen gibt diese Spalte einen NULL-Wert zurück.|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|Integer|Die maximale Länge in Bytes von einem Zeichen- oder Binärdaten-Datentypspalte. Bei allen anderen Datentypen gibt diese Spalte einen NULL-Wert zurück.|  
|ORDINAL_POSITION (ODBC 3.0)|18|Integer nicht NULL|Für Eingabe- und Ausgabedateien, die Ordnungsposition des Parameters in der Prozedurdefinition (in zunehmenden Parameterreihenfolge, beginnend mit 1). Nach dem Rückgabewert (sofern vorhanden) wird 0 zurückgegeben. Für Resultset Spalten, die Ordnungsposition der Spalte im Resultset festgelegt, mit der ersten Spalte im Resultset wird Nummer 1. Wenn mehrere Resultsets vorhanden sind, werden die Ordnungsposition der Spalte in einer Weise treiberspezifische zurückgegeben.|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|"Nein", wenn die Spalte keine NULL-Werte enthalten.<br /><br /> "YES", wenn die Spalte NULL-Werte einschließen kann.<br /><br /> Die Spalte gibt eine leere Zeichenfolge zurück, wenn die NULL-Zulässigkeit unbekannt ist.<br /><br /> Die NULL-Zulässigkeit wird gemäß den ISO-Regeln bestimmt. Ein ISO SQL – DBMS kann nicht auf eine leere Zeichenfolge zurückgeben.<br /><br /> Der für diese Spalte zurückgegebene Wert ist ein anderer als der für die NULLABLE-Spalte zurückgegebene Wert. (Siehe die Beschreibung der Spalte NULL-Werte zulässt.)|  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [Prozeduraufrufe](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Zurückgeben einer Liste der Verfahren in einer Datenquelle|[SQLProcedures-Funktion](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
