---
title: SQLGetTypeInfo-Funktion | Microsoft Docs
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
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7411a992bfbcb56a05e8ada5e4849a24ab8d2894
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetTypeInfo** gibt Informationen zu Datentypen, die von der Datenquelle unterstützt. Der Treiber zurückgegeben die Informationen in Form von einer SQL-Resultset. Die Datentypen sind für die Verwendung in Anweisungen (Data Definition Language, Datendefinitionssprache) vorgesehen.  
  
> [!IMPORTANT]  
>  Anwendungen müssen die Typnamen in der TYPE_NAME-Spalte der zurückgegebenen verwenden die **SQLGetTypeInfo** Resultset **ALTER TABLE** und **CREATE TABLE** Anweisungen. **SQLGetTypeInfo** möglicherweise mehr als eine Zeile mit demselben Wert in der DATA_TYPE-Spalte zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle für das Resultset.  
  
 *Datentyp*  
 [Eingabe] Der SQL-Datentyp. Diese Angabe muss einen der Werte in der [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) Abschnitt Anhang D: Datentypen oder treiberspezifischen SQL-Datentyp. SQL_ALL_TYPES gibt an, dass Informationen zu allen Datentypen zurückgegeben werden sollen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetTypeInfo** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* SQL _HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetTypeInfo** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Der Optionswert wurde geändert|Ein Attribut angegebene Anweisung war ungültig aufgrund Implementierung Arbeitsbedingungen, damit ein ähnlichen Wert vorübergehend ersetzt wurde. (Rufen **SQLGetStmtAttr** vorübergehend ersetzten Werts bestimmt.) Der Ersatzwert ist gültig für die *StatementHandle* , bis der Cursor geschlossen wird. Sind die Anweisungsattribute, die geändert werden können: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT und SQL_ATTR_SIMULATE_CURSOR. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle,* und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Resultset wurde geöffnet, auf die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Fehler bei der zugeordnete Verbindung während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY004|Ungültiger SQL-Datentyp|Der Wert für das Argument angegebene *DataType* war weder eine gültige ODBC SQL-Datentypbezeichner noch eine treiberspezifische Typ-ID, die vom Treiber unterstützt.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*, klicken Sie dann die Funktion aufgerufen wurde und, bevor es ausgeführt wurden, **SQLCancel** oder **SQLCancelHandle** wurde wird aufgerufen, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde und bevor es Ausführung abgeschlossen **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLGetTypeInfo** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber entspricht der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLGetTypeInfo** gibt die Ergebnisse als standard Resultset, sortiert nach DATA_TYPE und dann nach wie stark die Daten mit dem entsprechenden ODBC SQL-Datentyp zurück. Von der Datenquelle definierte Datentypen haben Vorrang vor benutzerdefinierten Datentypen. Folglich kann die Sortierreihenfolge ist nicht notwendigerweise konsistent jedoch zunächst als DATA_TYPE generalisiert, gefolgt von TYPE_NAME, beide Aufsteigend. Nehmen wir beispielsweise an, dass eine Datenquelle Integer- und LEISTUNGSINDIKATOR Datentypen definiert, in denen LEISTUNGSINDIKATOR automatisch erhöht wird, und auch ein benutzerdefinierten Datentyp WHOLENUM definiert wurde. Diese würden in der Reihenfolge WHOLENUM, ganze Zahl zurückgegeben werden und Zähler, da WHOLENUM Maps eng mit der ODBC-SQL-SQL_INTEGER, geben Sie während Geben Sie die Daten automatisch erhöht, obwohl von der Datenquelle unterstützt entspricht keinem eng eines ODBC SQL-Datentyps. Informationen, wie diese Informationen verwendet werden können, finden Sie unter [DDL-Anweisungen](../../../odbc/reference/develop-app/ddl-statements.md).  
  
 Wenn die *DataType* Argument gibt einen Datentyp, die für die Version von ODBC, die vom Treiber unterstützten gültig ist, jedoch wird vom Treiber nicht unterstützt, und es wird ein leeres Resultset zurückgegeben.  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Die folgenden Spalten wurden für ODBC 3 umbenannt. *x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC-3. *x* Spalte|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 Das zurückgegebene Resultset wurden die folgenden Spalten hinzugefügt **SQLGetTypeInfo** für ODBC 3.* X*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 19 (INTERVAL_PRECISION) können vom Treiber definiert werden. Eine Anwendung sollte Zugriff auf treiberspezifische Spalten erhalten, beginnend das Ende des Resultsets, anstatt eine explizite Ordnungsposition angeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** möglicherweise nicht alle Datentypen zurück. Beispielsweise kann ein Treiber keinen benutzerdefinierten Datentypen zurück. Clientanwendungen können einen beliebigen gültigen Datentyp aufweisen, unabhängig davon, ob sie von zurückgegeben werden **SQLGetTypeInfo**. Die Datentypen zurückgegebenes **SQLGetTypeInfo** werden von der Datenquelle unterstützt. Sie werden zur Verwendung in Anweisungen (Data Definition Language, Datendefinitionssprache) gedacht. Treiber können Rückgabedaten Resultset mit Datentypen, außer von zurückgegebenen Typen **SQLGetTypeInfo**. Erstellen Sie das Resultset für eine Katalogfunktion auf, kann der Treiber einen Datentyp, der nicht unterstützt wird von der Datenquelle verwenden.  
  
|Spaltenname|Column<br /><br /> number|Datentyp|Kommentare|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar, die nicht NULL|Name der Daten-Quelle vom Änderungsmanagement angeforderten Datentyp; z. B. "CHAR()", "VARCHAR()", "MONEY", "LONG VARBINARY" oder "CHAR () für BIT-Daten". Anwendungen müssen verwenden Sie diesen Namen in **CREATE TABLE** und **ALTER TABLE** Anweisungen.|  
|DATA_TYPE (ODBC 2.0)|2|Smallint nicht NULL|SQL-Datentyp. Dies kann einen ODBC-SQL-Datentyp oder treiberspezifischen SQL-Datentyp sein. Für "DateTime" oder ein Zeitintervall Datentypen gibt diese Spalte den präzise-Datentyp (z. B. SQL_TYPE_TIME oder SQL_INTERVAL_YEAR_TO_MONTH) zurück. Eine Liste der gültigen ODBC SQL-Datentypen, finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) in Anhang D:-Datentypen. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|Die maximale Spaltengröße, die der Server für diesen Datentyp unterstützt. Für numerische Daten ist dies die maximale Genauigkeit. Bei Zeichenfolgendaten ist dies die Länge in Zeichen. Für Datetime-Datentypen ist dies die Länge in Zeichen der Zeichenfolgendarstellung (vorausgesetzt, die maximale zulässige Genauigkeit der Sekundenbruchteil-Komponente). Für Datentypen wird NULL zurückgegeben, in denen ist Spaltengröße nicht anwendbar. Für Interval-Datentypen, ist dies die Anzahl der Zeichen in die zeichendarstellung des Intervalls literal (gemäß der Definition von der Genauigkeit für anführenden Intervallwert; finden Sie unter [Intervall Datentyplänge](../../../odbc/reference/appendixes/interval-data-type-length.md) in Anhang D:-Datentypen).<br /><br /> Weitere Informationen zu Spaltengröße, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|LITERAL_PREFIX-ZEICHEN (ODBC 2.0)|4|Varchar|Zeichen oder Zeichen als Präfix für ein Literal verwendet. Angenommen, ein einfaches Anführungszeichen (') für Zeichendatentypen oder 0 X für binäre Datentypen; Für Datentypen wird NULL zurückgegeben, in denen ist ein Zeichenfolgenliteral-Präfix nicht anwendbar.|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|Zeichen oder Zeichen verwendet, um ein Literal zu beenden. Angenommen, ein einfaches Anführungszeichen (') für Zeichendatentypen; Für Datentypen wird NULL zurückgegeben, in denen ist eines literalen Suffixes nicht anwendbar.|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|Eine Liste von Schlüsselwörtern, die durch Kommas getrennt, für jeden Parameter, die die Anwendung in Klammern angeben kann, wenn der Name verwendet wird, die in der TYPE_NAME-Feld zurückgegeben wird. Die Schlüsselwörter in der Liste können eine der folgenden sein: Länge, Genauigkeit oder Dezimalstellen. In der Reihenfolge, in die Syntax zur zu verwendenden benötigt werden. CREATE_PARAMS für DEZIMALPUNKT wäre beispielsweise "Precision, Scale"; CREATE_PARAMS für VARCHAR würde "Length". gleich. NULL wird zurückgegeben, wenn keine Parameter für die die Datentypdefinition vorhanden sind; beispielsweise ganze Zahl.<br /><br /> Der Treiber stellt den CREATE_PARAMS Text in der Sprache des Land/Region, in dem er verwendet wird.|  
|NULL-WERTE ZULÄSST (ODBC 2.0)|7|Smallint nicht NULL|Gibt an, ob der Datentyp NULL-Wert zulässt:<br /><br /> SQL_NO_NULLS, wenn der Datentyp NULL-Werte nicht zulässig sind.<br /><br /> SQL_NULLABLE, wenn der Datentyp NULL-Werte zulässt.<br /><br /> SQL_NULLABLE_UNKNOWN, wenn nicht bekannt ist, ob die Spalte NULL-Werte annimmt.|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint nicht NULL|Gibt an, ob ein Zeichendatentyp in Sortierungen und Vergleiche Groß-/Kleinschreibung ist:<br /><br /> SQL_TRUE, wenn der Datentyp ein Zeichendatentyp ist und Groß-/Kleinschreibung beachtet.<br /><br /> SQL_FALSE, wenn der Datentyp keinen Zeichendatentyp oder ist nicht in der Groß-/Kleinschreibung beachtet.|  
|DURCHSUCHBARE (ODBC 2.0)|9|Smallint nicht NULL|Verwendung der Datentyp in einen **, in denen** Klausel:<br /><br /> SQL_PRED_NONE, wenn die Spalte kann, in verwendet werden einem **, in denen** Klausel. (Dies ist identisch mit der SQL_UNSEARCHABLE-Wert in ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR, ob die Spalte kann, in verwendet werden eine **, in denen** -Klausel, aber nur mit der **wie** Prädikat. (Dies ist identisch mit der SQL_LIKE_ONLY-Wert in ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC, ob die Spalte kann, in verwendet werden eine **, in denen** -Klausel mit allen Vergleichsoperatoren mit Ausnahme **wie** (Vergleichsoperatoren, quantifizierte Vergleich **BETWEEN**, ** UNTERSCHIEDLICHE**, **IN**, **Übereinstimmung**, und **UNIQUE**). (Dies ist identisch mit der SQL_ALL_EXCEPT_LIKE-Wert in ODBC 2. *x*.)<br /><br /> SQL_SEARCHABLE, ob die Spalte kann, in verwendet werden einem **, in dem** -Klausel mit jedem Vergleichsoperator.|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|Gibt an, ob der Datentyp kein Vorzeichen aufweist:<br /><br /> SQL_TRUE, wenn der Datentyp kein Vorzeichen aufweist.<br /><br /> SQL_FALSE, wenn der Datentyp ein Vorzeichen aufweist.<br /><br /> NULL wird zurückgegeben, wenn das Attribut nicht für den Datentyp gilt oder der Datentyp nicht numerisch ist.|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint nicht NULL|Gibt an, ob der Datentyp vordefiniert wurde behoben, Genauigkeit und Dezimalstellen (die Daten datenquellenspezifischen sind), z. B. einen Money-Datentyp:<br /><br /> SQL_TRUE, wenn sie mit fester Genauigkeit und Dezimalstellenanzahl vordefiniert wurde.<br /><br /> SQL_FALSE, wenn sie nicht über vordefinierte feste Genauigkeit und Dezimalstellen verfügt.|  
|AUTO_UNIQUE_VALUE ENTHÄLT (ODBC 2.0)|12|Smallint|Gibt an, ob der Datentyp eine automatische Inkrementierung ist:<br /><br /> SQL_TRUE, wenn der Datentyp automatische Inkrementierung ist.<br /><br /> SQL_FALSE, wenn der Datentyp nicht automatische Inkrementierung ist.<br /><br /> NULL wird zurückgegeben, wenn das Attribut nicht für den Datentyp gilt oder der Datentyp nicht numerisch ist.<br /><br /> Eine Anwendung können Sie die Werte in einer Spalte mit diesem Attribut einfügen, aber die Werte in der Spalte in der Regel kann nicht aktualisiert werden.<br /><br /> Wenn eine Einfügung in eine automatisch inkrementierte Spalte ausgeführt wird, wird ein eindeutiger Wert zum Zeitpunkt des Einfügens in die Spalte eingefügt. Das Inkrement ist nicht definiert, aber Daten datenquellenspezifischen ist. Eine Anwendung sollte nicht davon ausgehen, dass eine automatisch inkrementierte Spalte bei bestimmten Zeitpunkt kein(e) Inkremente ausnahmslos bestimmten startet.|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|Lokalisierte Version der Quelle vom Änderungsmanagement angeforderten den Namen des Datentyps. NULL wird zurückgegeben, wenn ein lokalisierter Name nicht von der Datenquelle unterstützt wird. Dieser Name dient zur Anzeige nur, z. B. Dialogfelder.|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|Die mindestdezimalstellen des Datentyps bezüglich der Datenquelle. Weist ein Datentyp Feste Dezimalstellen, enthalten die Spalten MINIMUM_SCALE und MAXIMUM_SCALE dieser Wert auf. Z. B. möglicherweise eine SQL_TYPE_TIMESTAMP-Spalte festen Dezimalstellen für Sekundenbruchteile. NULL wird zurückgegeben, wenn Dezimalstellen auf den Datentyp nicht anwendbar sind. Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|Die maximalen Dezimalstellen des Datentyps für die Datenquelle. NULL wird zurückgegeben, wenn Dezimalstellen auf den Datentyp nicht anwendbar sind. Wenn die maximale Dezimalstellen für die Datenquelle nicht separat definiert, aber es und stattdessen definiert wurde, wurden dass Sie der maximalen Genauigkeit entsprechen, enthält diese Spalte den gleichen Wert wie die COLUMN_SIZE-Spalte. Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint nicht NULL|Der Wert der SQL-Datentyp, wie er in das SQL_DESC_TYPE-Feld des Deskriptors wird angezeigt. Diese Spalte entspricht der DATA_TYPE-Spalte mit Ausnahme der Datentypen Intervall und "DateTime".<br /><br /> Für Intervall und Datetime-Datentypen SQL_INTERVAL oder SQL_INTERVAL die SQL_DATA_TYPE-Feld im Resultset zurück, und das Feld noch SQL_DATETIME_SUB dem Subcode für den bestimmten Intervall oder Datetime-Datentyp zurück. (Siehe [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NOCH SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|Wenn der Wert der SQL_DATA_TYPE SQL_DATETIME oder SQL_INTERVAL hat, enthält diese Spalte den Subcode für Datetime-Intervall. Für Datentypen als "DateTime" und das Intervall ist dieses Feld NULL.<br /><br /> Intervall oder Datetime-Datentypen SQL_INTERVAL oder SQL_INTERVAL die SQL_DATA_TYPE-Feld im Resultset zurück, und das Feld noch SQL_DATETIME_SUB dem Subcode für den bestimmten Intervall oder Datetime-Datentyp zurück. (Siehe [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|Wenn der Datentyp einen ungefähren numerischen Typ ist, enthält diese Spalte den Wert 2, um anzugeben, dass die COLUMN_SIZE gibt eine Anzahl von Bits an. Bei exakten numerischen Datentypen enthält diese Spalte den Wert 10, um anzugeben, dass die COLUMN_SIZE gibt eine Anzahl von Dezimalstellen an. Andernfalls ist diese Spalte NULL.|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|Wenn der Datentyp ein Intervall-Datentyp ist, enthält diese Spalte den Wert der die führenden Intervall-Genauigkeit. (Siehe [Intervall-Datentyp, Genauigkeit](../../../odbc/reference/appendixes/interval-data-type-precision.md) in Anhang D:-Datentypen.) Andernfalls ist diese Spalte NULL.|  
  
 Informationen über Bildattribute kann Datentypen oder bestimmte Spalten in einem Resultset angewendet. **SQLGetTypeInfo** gibt Informationen zu Datentypen; zugeordneten Attribute zurück **SQLColAttribute** gibt Informationen zu Spalten in einem Resultset zugeordneten Attribute zurück.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLColAttribute-Funktion](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Zurückgeben von Informationen zu einer Datenquelle oder Treiber|[SQLGetInfo-Funktion](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
