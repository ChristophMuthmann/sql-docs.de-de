---
title: SQLExtendedFetch Funktion | Microsoft Docs
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
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6c0336d9f7d3495e7e2ef925b86d47c472ff2ec
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: veraltet  
  
 **Zusammenfassung**  
 **SQLExtendedFetch** angegebene Rowset von Daten aus dem Resultset abruft, und gibt Daten für alle gebundenen Spalten zurück. Rowsets können eine absolute oder relative Position oder durch Lesezeichen angegeben werden.  
  
> [!NOTE]  
>  In ODBC 3.*.x*, **SQLExtendedFetch** wurde ersetzt durch **SQLFetchScroll**. ODBC 3.*.x* Anwendungen sollten nicht aufrufen, **SQLExtendedFetch**; sie sollten stattdessen Aufrufen **SQLFetchScroll**. Der Treiber-Manager ordnet **SQLFetchScroll** auf **SQLExtendedFetch** bei der Arbeit mit einer ODBC 2.*.x* Treiber. ODBC 3.*.x* Treiber unterstützen sollte **SQLExtendedFetch** , die mit ODBC 2. arbeiten sollen*.x* Anwendungen, die sie aufrufen. Weitere Informationen finden Sie unter "Kommentare" und [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *FetchOrientation*  
 [Eingabe] Der Typ des Abrufs. Dies ist identisch mit *FetchOrientation* in **SQLFetchScroll**.  
  
 *FetchOffset*  
 [Eingabe] Die Nummer der Zeile abgerufen. Dies ist identisch mit *FetchOffset* in **SQLFetchScroll**, mit einer Ausnahme. Wenn *FetchOrientation* ist SQL_FETCH_BOOKMARK, *FetchOffset* ist ein fester Länge, die Lesezeichen nicht in einem Lesezeichen als Offset. Das heißt, **SQLExtendedFetch** Ruft das Lesezeichen aus dieses Argument, nicht das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut ab. Er unterstützt keine Lesezeichen variabler Länge und unterstützt nicht das Abrufen eines Rowsets mit einem Offset (ungleich 0) in einem Lesezeichen.  
  
 *RowCountPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Anzahl der tatsächlich abgerufenen Zeilen zurückgegeben. Dieser Puffer ist auf die gleiche Weise als durch das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut angegebenen Puffer verwendet. Dieser Puffer ist wird nur von **SQLExtendedFetch**. Er wird nicht verwendet, indem **SQLFetch** oder **SQLFetchScroll**.  
  
 *RowStatusArray*  
 [Ausgabe] Zeiger auf ein Array, in dem den Status der einzelnen Zeilen zurückgegeben. Dieses Array wird auf die gleiche Weise wie das Array, das durch das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR angegeben verwendet.  
  
 Die Adresse dieses Arrays ist jedoch nicht im Feld SQL_DESC_STATUS_ARRAY_PTR in IRD gespeichert. Dieses Array wird weiterhin nur durch verwendet **SQLExtendedFetch** und **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD oder **SQLSetPos**bei Aufruf nach **SQLExtendedFetch**. Er wird nicht verwendet, indem **SQLFetch** oder **SQLFetchScroll**, und er wird nicht verwendet, indem **SQLBulkOperations** oder **SQLSetPos** Wenn sie nach aufgerufen werden **SQLFetch** oder **SQLFetchScroll**. Es ist auch nicht verwendet, wenn **SQLBulkOperations** mit einem *Vorgang* der SQL_ADD wird aufgerufen, bevor alle Fetch-Funktion aufgerufen wird. Es wird also nur in der Anweisung Status S7 verwendet. Es wird nicht in der Anweisung Statuswerte S5 oder a6 verwendet. Weitere Informationen finden Sie unter [Anweisung Übergänge](../../../odbc/reference/appendixes/statement-transitions.md) in Anhang B: ODBC-Übergang-Statustabellen.  
  
 Anwendungen sollten einen gültigen Zeiger im Bereitstellen der *RowStatusArray* Argument; Wenn nicht, das Verhalten des **SQLExtendedFetch** und das Verhalten der Aufrufe an **SQLBulkOperations**oder **SQLSetPos** nachdem durch ein Cursor positioniert wurde hat **SQLExtendedFetch** sind nicht definiert.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLExtendedFetch** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLError**. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLExtendedFetch** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben. Wenn es sich bei Auftreten eines Fehlers in einer einzelnen Spalte **SQLGetDiagField** kann aufgerufen werden, mit einer *DiagIdentifier* von SQL_DIAG_COLUMN_NUMBER, um die Spalte zu bestimmen, der Fehler aufgetreten, andernfalls false ist, und ** SQLGetDiagField** kann aufgerufen werden, mit einem *DiagIdentifier* von SQL_DIAG_ROW_NUMBER Bestimmen der Zeile, die diese Spalte enthält.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL führte Zeichenfolgen- oder Binärdaten, die für eine Spalte zurückgegeben. Falls es sich um einen Zeichenfolgenwert handelt, wurde es rechts abgeschnitten. Falls es sich um einen numerischen Wert handelt, wurde die Nachkommastellen der Zahl gekürzt.  (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 01|Fehler in Zeile|Fehler beim Abrufen von einer oder mehreren Zeilen. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S06|Es wurde versucht abzurufen, bevor das Resultset das erste Rowset zurückgab|Das angeforderte Rowset überlappenden am Anfang, wenn die aktuelle Position hinter der ersten Zeile, und entweder ist das Resultset *FetchOrientation* SQL_PRIOR wurde oder *FetchOrientation* SQL_RELATIVE mit wurde ein negative *FetchOffset* , deren absoluten Wert war kleiner oder gleich der aktuellen SQL_ROWSET_SIZE setzen. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S07|Teilbereiche wurden abgeschnitten.|Für eine Spalte zurückgegebenen Daten wurden abgeschnitten. Für numerische Datentypen und wurde die Nachkommastellen der Zahl gekürzt. Für die Zeit, Zeitstempel und Interval-Datentypen, die eine Komponente enthält wurde der Bruchteil der Zeit abgeschnitten.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Ein Datenwert konnte nicht konvertiert werden, in den C-Datentyp, der vom angegebenen *TargetType* in **SQLBindCol**.|  
|07009|Ungültiger Deskriptorindex|Spalte 0 wurde mit gebundenen **SQLBindCol**, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22002|Anzeigevariable erforderlich, aber nicht angegeben|NULL wurde abgerufene Daten in eine Spalte, deren *StrLen_or_IndPtr* festlegen, indem **SQLBindCol** wurde ein null-Zeiger.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Den numerischen Wert (als numerisch oder Zeichenfolge) für eine oder mehrere Spalten zurückgeben würde die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird vorliegt.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)<br /><br /> Weitere Informationen finden Sie unter [Richtlinien für das Intervall und numerischen Datentypen](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) in Anhang D:-Datentypen.|  
|22007|Ungültiges Datetime-format|Eine Zeichenspalte im Resultset an ein Datum, Uhrzeit oder C-zeitstempelstruktur gebunden wurde, und ein Wert in der Spalte wurde, bzw. ein ungültiges Datum, Uhrzeit oder Zeitstempel.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|22012|Division durch 0 (null)|Ein Wert aus einem arithmetischen Ausdruck wurde von 0 (null) zurückgegeben Division geführt hat.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|22015|Überlauf der Intervall-Feld.|Intervalltyp C aus einer genauen numerischen oder Intervall SQL-Typ zuzuweisen, hat einen Datenverlust von signifikanten Stellen im Feld führende verursacht.<br /><br /> Beim Abrufen von Daten in ein C-Intervalltyp ist keine Darstellung des Werts des SQL-Datentyps in den Intervalltyp C.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte wurde einem Zeichendatentyp; und kein Wert in der Spalte wurde ein gültiger Literal des gebundenen C-Typs.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|24000|Ungültiger Cursorstatus|Die *StatementHandle* wurde in einem ausgeführten Zustand, aber kein Resultset zugeordnet wurde die *StatementHandle*.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLError** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*, und klicken Sie dann die Funktion aufgerufen wurde erneut auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLExtendedFetch** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) dem angegebenen *StatementHandle* war nicht in einem ausgeführten Zustand. Die Funktion wurde aufgerufen, ohne zunächst **SQLExecDirect**, **SQLExecute**, oder eine Katalogfunktion auf.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) **SQLExtendedFetch** wurde aufgerufen, die *StatementHandle* nach **SQLFetch** oder **SQLFetchScroll** aufgerufen wurde und bevor ** SQLFreeStmt** mit der Option SQL_CLOSE aufgerufen wurde.<br /><br /> (DM) **SQLBulkOperations** hieß für eine Anweisung vor dem **SQLFetch**, **SQLFetchScroll**, oder **SQLExtendedFetch** aufgerufen wurde, und Klicken Sie dann **SQLExtendedFetch** wurde aufgerufen, bevor **SQLFreeStmt** mit der Option SQL_CLOSE aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY106|Der Fetchtyp außerhalb des gültigen Bereichs|(DM) der Wert für das Argument angegebene *FetchOrientation* war ungültig. (Siehe "Kommentare".)<br /><br /> Das Argument *FetchOrientation* SQL_FETCH_BOOKMARK wurde, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.<br /><br /> Der Wert der Option-Anweisung SQL_CURSOR_TYPE wurde SQL_CURSOR_FORWARD_ONLY und der Wert des Arguments *FetchOrientation* war nicht SQL_FETCH_NEXT.<br /><br /> Das Argument *FetchOrientation* SQL_FETCH_RESUME wurde.|  
|HY107|Zeilenwert außerhalb des gültigen Bereichs|Mit der Option SQL_CURSOR_TYPE-Anweisung angegebene Wert war SQL_CURSOR_KEYSET_DRIVEN, jedoch mit dem SQL_KEYSET_SIZE Anweisung-Attribut angegebene Wert größer als 0 und kleiner als der Wert mit dem Anweisungsattribut SQL_ROWSET_SIZE setzen angegeben .|  
|HY111|Ungültige lesezeichenwerts|Das Argument *FetchOrientation* SQL_FETCH_BOOKMARK wurde angegeben, und das Lesezeichen in der *FetchOffset* Argument war ungültig.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der angegebene Fetchtyp unterstützt Treiber oder der Datenquelle nicht.<br /><br /> Der Treiber oder die Datenquelle unterstützt nicht die Konvertierung angegeben, durch die Kombination der *TargetType* in **SQLBindCol** und dem SQL-Datentyp der entsprechenden Spalte. Dieser Fehler bezieht sich nur, wenn der SQL-Datentyp der Spalte in einen treiberspezifischen SQL-Datentyp zugeordnet wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Das Verhalten des **SQLExtendedFetch** ist identisch mit dem der **SQLFetchScroll**, mit folgenden Ausnahmen:  
  
-   **SQLExtendedFetch** und **SQLFetchScroll** unterschiedliche Methoden verwenden, um die Anzahl der abgerufenen Zeilen zurückzugeben. **SQLExtendedFetch** gibt die Anzahl der Zeilen, die abgerufen * \*RowCountPtr*; **SQLFetchScroll** gibt die Anzahl der Zeilen, die direkt in den Puffer, der auf das SQL_ATTR_ROWS_FETCHED_PTR abgerufen. Weitere Informationen finden Sie unter der *RowCountPtr* Argument.  
  
-   **SQLExtendedFetch** und **SQLFetchScroll** Rückgabestatus der einzelnen Zeilen in verschiedenen Arrays aus. Weitere Informationen finden Sie unter der *RowStatusArray* Argument.  
  
-   **SQLExtendedFetch** und **SQLFetchScroll** unterschiedliche Methoden verwenden, um das Lesezeichen abzurufen beim *FetchOrientation* SQL_FETCH_BOOKMARK wird. **SQLExtendedFetch** variabler Länge Lesezeichen oder das Abrufen von Rowsets mit einem Offset ungleich 0 in einem Lesezeichen nicht unterstützt. Weitere Informationen finden Sie unter der *FetchOffset* Argument.  
  
-   **SQLExtendedFetch** und **SQLFetchScroll** anderes Rowset Größen verwenden. **SQLExtendedFetch** verwendet den Wert des Attributs Anweisung SQL_ROWSET_SIZE setzen und **SQLFetchScroll** verwendet den Wert des Attributs SQL_ATTR_ROW_ARRAY_SIZE-Anweisung.  
  
-   **SQLExtendedFetch** verfügt über etwas andere Semantik auf als die Fehlerbehandlung **SQLFetchScroll**. Weitere Informationen finden Sie unter "Fehlerbehandlung" im Abschnitt "Kommentare" der [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** Bindung-Offsets (SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut) nicht unterstützt.  
  
-   Aufrufe von **SQLExtendedFetch** kann nicht kombiniert werden, durch Aufrufe von **SQLFetch** oder **SQLFetchScroll**, und wenn **SQLBulkOperations** wird aufgerufen Bevor eine Fetch-Funktion aufgerufen wird, **SQLExtendedFetch** kann nicht aufgerufen werden, bis der Cursor geschlossen und erneut geöffnet wird. D. h. **SQLExtendedFetch** kann nur in der Anweisung Status S7 aufgerufen werden. Weitere Informationen finden Sie unter [Anweisung Übergänge](../../../odbc/reference/appendixes/statement-transitions.md) in Anhang B: ODBC-Übergang-Statustabellen.  
  
 Wenn eine Anwendung ruft **SQLFetchScroll** beim Verwenden einer ODBC 2.*.x* Treiber, der Treiber-Manager ordnet diesen Aufruf an **SQLExtendedFetch**. Weitere Informationen finden Sie unter "SQLFetchScroll und ODBC 2*.x* Treiber" im [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 In ODBC 2.*.x*, **SQLExtendedFetch** wurde aufgerufen, um mehrere Zeilen abzurufen und **SQLFetch** wurde aufgerufen, um eine einzelne Zeile abgerufen werden. In ODBC 3.*.x*, andererseits, **SQLFetch** aufgerufen werden, um mehrere Zeilen abzurufen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ausführen von Bulk Insert, Update oder Delete-Vorgänge|[SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLDescribeCol-Funktion](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Zurückgeben der Anzahl der Ergebnis Resultsetspalten|[SQLNumResultCols-Funktion](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Positionieren den Cursor, Aktualisieren von Daten im Rowset aktualisieren oder Löschen von Daten im Resultset|[SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
