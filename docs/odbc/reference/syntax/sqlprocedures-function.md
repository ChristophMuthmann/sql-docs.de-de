---
title: SQLProcedures-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2790087b4a8ea0518a81f540da6b3887933a4ef6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprocedures-function"></a>SQLProcedures-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLProcedures** gibt die Liste der Prozedurnamen in einer bestimmten Datenquelle gespeichert. *Prozedur* ist ein generischer Begriff, die zum Beschreiben einer *ausführbares Objekt*, oder eine benannte Entität, die mithilfe von Eingabe-und Ausgabeparametern aufgerufen werden kann. Weitere Informationen zu Verfahren finden Sie unter der [Prozeduren](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Katalogname*  
 [Eingabe] Prozedur-Katalog. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, denen keine Kataloge vorhanden sind. *Katalogname* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
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
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLProcedures** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLProcedures** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *CatalogName* Argument wurde ein null-Zeiger und der SQL_CATALOG_NAME *Infotyp* gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *SchemaName* oder *ProcName* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Dieser asynchrone Funktion war weiterhin ausgeführt, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge "Name" ist kleiner als 0, aber ungleich-SQL_NTS.<br /><br /> Der Wert eines der Argumente Länge Namen überschritten, der Wert für die maximale Länge für den entsprechenden Namen.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Eine Prozedur Catalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Eine prozedurschema angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.<br /><br /> Eine Zeichenfolge Suchmuster für das prozedurschema oder der Name der Prozedur angegeben wurde, und die Datenquelle unterstützt keine Suchmustern für mindestens eines dieser Argumente.<br /><br /> Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle, die das angeforderte Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* diese Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLProcedures** Listet alle Prozeduren im angeforderten Bereich. Ein Benutzer kann oder möglicherweise nicht über die Berechtigung zum Ausführen eines dieser Verfahren. Um Zugriff zu überprüfen, kann eine Anwendung aufrufen **SQLGetInfo** und überprüfen Sie den Wert der SQL_ACCESSIBLE_PROCEDURES-Informationen. Die Anwendung muss, andernfalls können Sie mit der jeweiligen Situation, in denen der Benutzer eine Prozedur auswählt, die nicht ausgeführt werden kann. Informationen, wie diese Informationen verwendet werden können, finden Sie unter [Prozeduren](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedures** gibt die Ergebnisse als standard Resultset, geordnet nach PROCEDURE_CAT PROCEDURE_SCHEMA und PROCEDURE_NAME zurück.  
  
> [!NOTE]  
>  **SQLProcedures** möglicherweise nicht alle Prozeduren zurück. Anwendungen können eine beliebige gültige Prozedur unabhängig davon, ob sie von zurückgegeben werden **SQLProcedures**.  
  
 Die folgenden Spalten wurden umbenannt für ODBC 3.*.x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC 3.*.x* Spalte|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROZEDUR _OWNER|PROZEDUR _SCHEM|  
  
 Um die tatsächliche Länge der PROCEDURE_CAT PROCEDURE_SCHEM und PROCEDURE_NAME Spalten zu bestimmen, kann eine Anwendung aufrufen **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN und SQL_MAX_PROCEDURE_ NAME_LEN-Optionen.  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 8 (PROCEDURE_TYPE) können vom Treiber definiert werden. Eine Anwendung sollte Zugriff auf treiberspezifische Spalten erhalten, beginnend das Ende des Resultsets, anstatt eine explizite Ordnungsposition angeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spaltennummer|Datentyp|Kommentare|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Prozedur-Katalog-Bezeichner. NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge bei einigen Prozeduren unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Verfahren aus, denen keine Kataloge vorhanden sind.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Prozedur-Schema-Bezeichner. NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas bei einigen Prozeduren unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Verfahren, die keine Schemas aufweisen.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar, die nicht NULL|Prozedur-Bezeichner.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|–|Zur künftigen Verwendung reserviert. Anwendungen sollten nicht auf die Daten in diese Ergebnisspalten verlassen.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|–|Zur künftigen Verwendung reserviert. Anwendungen sollten nicht auf die Daten in diese Ergebnisspalten verlassen.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|–|Zur künftigen Verwendung reserviert. Anwendungen sollten nicht auf die Daten in diese Ergebnisspalten verlassen.|  
|HINWEISE (ODBC 2.0)|7|Varchar|Eine Beschreibung der Prozedur.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|Definiert den Prozedurtyp an:<br /><br /> SQL_PT_UNKNOWN: Es kann nicht ermittelt werden, ob die Prozedur einen Wert zurückgibt.<br /><br /> SQL_PT_PROCEDURE: Das zurückgegebene Objekt ist kein Verfahren; Er hat, also keinen Wert zurückgegeben.<br /><br /> SQL_PT_FUNCTION: Das zurückgegebene Objekt ist eine Funktion. d. h. verfügt es über einen Rückgabewert.|  
  
 Die *SchemaName* und *ProcName* Argumente Suchmustern zu akzeptieren. Weitere Informationen zu gültigen Suchmustern, finden Sie unter [Muster Value-Argumenten](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [Prozeduraufrufe](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Zurückgeben von Informationen zu einer Datenquelle oder Treiber|[SQLGetInfo-Funktion](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Resultsetspalten zurückgeben, die Parameter und das Ergebnis einer Prozedur|[SQLProcedureColumns-Funktion](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|Die Syntax zum Aufrufen von gespeicherten Prozeduren|[Ausführen von Anweisungen](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
