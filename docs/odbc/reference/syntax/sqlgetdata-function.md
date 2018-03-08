---
title: SQLGetData-Funktion | Microsoft Docs
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
apiname: SQLGetData
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetData
helpviewer_keywords: SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
caps.latest.revision: "46"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0a23ddb9ee932b67bddd35edfcc9d64228b36f18
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdata-function"></a>SQLGetData-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetData** Ruft Daten für eine einzelne Spalte im Resultset oder für einen einzelnen Parameter nach **SQLParamData** SQL_PARAM_DATA_AVAILABLE zurückgibt. Es kann mehrere Male aufgerufen werden zum Abrufen von Daten mit variabler Länge in Teilen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Col_or_Param_Num*  
 [Eingabe] Zum Abrufen von Spaltendaten, ist es die Anzahl der Spalte, für die Daten zurückgegeben werden sollen. Resultset-Spalten werden in der zunehmenden Spaltenreihenfolge, beginnend mit 1 nummeriert. Die Lesezeichenspalte ist die Nummer der Spalte 0; Dies kann nur angegeben werden, wenn das Lesezeichen aktiviert sind.  
  
 Zum Abrufen von Parameterdaten, ist es die Ordnungszahl des Parameters, der bei 1 beginnt.  
  
 *TargetType*  
 [Eingabe] Der Typbezeichner des C-Datentyp, der die **TargetValuePtr* Puffer. Eine Liste der gültigen C-Datentypen und Typ-IDs, finden Sie unter der [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) Abschnitt im Anhang D:-Datentypen.  
  
 Wenn *TargetType* SQL_ARD_TYPE, verwendet der Treiber, die Typ-ID im Feld SQL_DESC_CONCISE_TYPE der ARD angegeben, ist. Wenn *TargetType* ist SQL_APD_TYPE, **SQLGetData** verwendet die C-Datentyp an, die im angegebenen **SQLBindParameter**. Andernfalls der C-Datentyp angegeben, **SQLGetData** überschreibt die C-Datentyp, der im angegebenen **SQLBindParameter**. Wenn SQL_C_DEFAULT ist, wählt der Treiber die Standard-C-Datentyp basierend auf der SQL-Datentyp, der Quelle an.  
  
 Sie können auch einen erweiterte C-Datentyp angeben. Weitere Informationen finden Sie unter [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Ausgabe] Zeiger auf den Puffer, in dem die Daten zurückgegeben.  
  
 *TargetValuePtr* darf nicht NULL sein.  
  
 *Pufferlänge*  
 [Eingabe] Länge der **TargetValuePtr* Puffers in Bytes.  
  
 Verwendet der Treiber *Pufferlänge* zur Vermeidung von Schreiben nach dem Ende der \* *TargetValuePtr* beim Zurückgeben von Daten mit variabler Länge, z. B. Zeichen- oder Binärdaten gepuffert werden sollen. Beachten Sie, dass der Treiber die Null-Abschlusszeichen betrachtet, bei der Rückgabe von Zeichendaten in \* *TargetValuePtr*. **TargetValuePtr* muss daher keine Leerzeichen nach dem Zeichen Null-Terminierung oder der Treiber die Daten abgeschnitten werden.  
  
 Der Treiber Daten fester Länge, z. B. eine ganze Zahl oder eine Datumsstruktur Rückkehr ignoriert der Treiber *Pufferlänge* und davon aus, dass der Puffer groß genug ist, um die Daten aufzunehmen. Es ist wichtig, dass die Anwendung auf einen ausreichend großen Puffer für Daten fester Länge zuzuordnen, oder der Treiber wird hinter das Ende des Puffers geschrieben.  
  
 **SQLGetData** SQLSTATE HY090 zurückgegeben (ungültige Zeichenfolgen- oder Pufferlänge.) Wenn *Pufferlänge* ist kleiner als 0, jedoch nicht, wenn *Pufferlänge* ist 0.  
  
 *StrLen_or_IndPtr*  
 [Ausgabe] Zeiger auf den Puffer, in dem die Länge bzw. der Indikatorwert Wert zurückgegeben. Wenn dies ein null-Zeiger ist, wird keine Länge bzw. der Indikatorwert Wert zurückgegeben. Dies gibt einen Fehler zurück, wenn die abgerufenen Daten NULL ist.  
  
 **SQLGetData** können die folgenden Werte in die Längen-/Indikatorpuffers zurück:  
  
-   Die Länge der zurückzugebenden verfügbaren Daten  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Weitere Informationen finden Sie unter [mit Längenindikator/Werten](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) und "Kommentare" in diesem Thema.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetData** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetData** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Nicht alle Daten für die angegebene Spalte *Col_or_Param_Num*, in einem einzigen Aufruf der Funktion abgerufen werden konnte. SQL_NO_TOTAL oder die Länge der Daten in der angegebenen Spalte vor dem aktuellen Aufruf von verbleibenden **SQLGetData** wird zurückgegeben, \* *StrLen_or_IndPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)<br /><br /> Weitere Informationen zur Verwendung von mehreren Aufrufen an **SQLGetData** für eine einzelne Spalte finden Sie unter "Kommentare".|  
|01S07|Teilbereiche wurden abgeschnitten.|Die Daten für eine oder mehrere Spalten zurückgegeben wurden abgeschnitten. Für numerische Datentypen und wurde die Nachkommastellen der Zahl gekürzt. Für die Zeit, Zeitstempel und Interval-Datentypen, die eine Komponente enthält wurde der Bruchteil der Zeit abgeschnitten.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert einer Spalte im Resultset kann nicht konvertiert werden, um den C-Datentyp, der durch das Argument angegebenen *TargetType*.|  
|07009|Ungültiger Deskriptorindex|Der Wert für das Argument angegebene *Col_or_Param_Num* 0 wurde, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.<br /><br /> Der Wert für das Argument angegebene *Col_or_Param_Num* war größer als die Anzahl der Spalten im Resultset.<br /><br /> Die *Col_or_Param_Num* Wert war nicht gleich bei der Ordnungszahl des Parameters, der verfügbar ist.<br /><br /> (DM) die angegebene Spalte gebunden wurde. Diese Beschreibung gilt nicht für Treiber, die die SQL_GD_BOUND Bitmaske für die Option SQL_GETDATA_EXTENSIONS in zurückgeben **SQLGetInfo**.<br /><br /> Die Anzahl der angegebenen Spalte (DM) war kleiner als oder gleich der Anzahl der höchsten gebundenen Spalte. Diese Beschreibung gilt nicht für Treiber, die die SQL_GD_ANY_COLUMN Bitmaske für die Option SQL_GETDATA_EXTENSIONS in zurückgeben **SQLGetInfo**.<br /><br /> (DM) die Anwendung wurde bereits aufgerufen. **SQLGetData** für die aktuelle Zeile; die Anzahl der im aktuellen Aufruf der angegebenen Spalte war kleiner als die Anzahl der in den vorhergehenden Aufruf; angegebenen Spalte und der Treiber gibt nicht den SQL_ zurück GD_ANY_ORDER Bitmaske für die Option SQL_GETDATA_EXTENSIONS in **SQLGetInfo**.<br /><br /> (DM) die *TargetType* Argument war SQL_ARD_TYPE, und die *Col_or_Param_Num* anwendungsparameterdeskriptor-Datensatz in die ARD Fehler bei der konsistenzprüfung.<br /><br /> (DM) die *TargetType* Argument SQL_ARD_TYPE, und der Wert im Feld SQL_DESC_COUNT der ARD war kleiner als das *Col_or_Param_Num* Argument.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22002|Anzeigevariable erforderlich, aber nicht angegeben|*StrLen_or_IndPtr* wurde ein null-Zeiger und NULL-Daten abgerufen wurde.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Den numerischen Wert (als numerisch oder Zeichenfolge) für die Spalte zurückgeben würde die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird vorliegt.<br /><br /> Weitere Informationen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Ungültiges Datetime-format|Die Zeichenspalte im Resultset an eine C-Datum, Uhrzeit oder Timestamp-Struktur gebunden wurde, und der Wert in der Spalte wurde ein ungültiges Datum, Uhrzeit oder Zeitstempel. Weitere Informationen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Division durch 0 (null)|Ein Wert aus einem arithmetischen Ausdruck mit der Division durch 0 (null) zurückgegeben wurde.|  
|22015|Überlauf der Intervall-Feld.|Intervalltyp C aus einer genauen numerischen oder Intervall SQL-Typ zuzuweisen, hat einen Datenverlust von signifikanten Stellen im Feld führende verursacht.<br /><br /> Beim Zurückgeben der Daten an eine C#-Intervalltyp gab es keine Darstellung des Werts des SQL-Datentyps in den Intervalltyp C.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Im Resultset eine Spalte mit dem Zeichen an der Zeichenpuffer C zurückgegeben wurde, und die Spalte enthalten, ein Zeichen, die für die es keine Darstellung des Zeichensatzes des Puffers war.<br /><br /> Der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte wurde einem Zeichendatentyp; und kein Wert in der Spalte wurde ein gültiger Literal des gebundenen C-Typs.|  
|24000|Ungültiger Cursorstatus|(DM) die Funktion wurde aufgerufen, ohne zunächst **SQLFetch** oder **SQLFetchScroll** zur Positionierung des Cursors in die Zeile der Daten erforderlich sind.<br /><br /> (DM) die *StatementHandle* wurde in einem ausgeführten Zustand, aber kein Resultset zugeordnet wurde die *StatementHandle*.<br /><br /> Ein Cursor geöffnet wurde die *StatementHandle* und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde, aber der Cursor wurde vor dem Start des Resultsets oder nach der das Ende des Resultsets.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der *MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY003|Typ des Programms außerhalb des gültigen Bereichs|(DM) das Argument *TargetType* war kein gültiger Datentyp, SQL_C_DEFAULT, SQL_ARD_TYPE (bei Abrufen von Spaltendaten) und SQL_APD_TYPE (bei abrufen Parameterdaten an).<br /><br /> (DM) das Argument *Col_or_Param_Num* wurde von 0 und dem Argument *TargetType* war nicht SQL_C_BOOKMARK für ein Lesezeichen mit fester Länge oder SQL_C_VARBOOKMARK für ein Lesezeichen variabler Länge.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*, und klicken Sie dann die Funktion aufgerufen wurde erneut auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung, und klicken Sie dann auf die Funktion wurde erneut aufgerufen, auf die *StatementHandle*.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) das Argument *TargetValuePtr* wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) dem angegebenen *StatementHandle* war nicht in einem ausgeführten Zustand. Die Funktion wurde aufgerufen, ohne zunächst **SQLExecDirect**, **SQLExecute** oder eine Katalogfunktion auf.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLGetData** Funktion aufgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) die *StatementHandle* wurde in einem ausgeführten Zustand, aber kein Resultset zugeordnet wurde die *StatementHandle*.<br /><br /> Ein Aufruf von **SQLExeceute**, **SQLExecDirect**, oder **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE, zurückgegeben, aber **SQLGetData** wurde aufgerufen , anstelle von **SQLParamData**.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *Pufferlänge* war kleiner als 0.<br /><br /> Die für Argument angegebenen Wert *Pufferlänge* kleiner als 4 ist, wurde die *Col_or_Param_Num* Argument auf 0 festgelegt wurde, und der Treiber wurde von einer ODBC 2.*.x* Treiber.|  
|HY109|Ungültige Cursorposition|Der Cursor positioniert wurde (durch **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, oder **SQLBulkOperations**) auf eine Zeile, die gelöscht wurden oder konnte nicht abgerufen werden.<br /><br /> Der Cursor wurde ein Vorwärtscursor, und die Rowsetgröße war größer als 1.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt keine Verwendung von **SQLGetData** mit mehreren Zeilen in **SQLFetchScroll**. Diese Beschreibung gilt nicht für Treiber, die die SQL_GD_BLOCK Bitmaske für die Option SQL_GETDATA_EXTENSIONS in zurückgeben **SQLGetInfo**.<br /><br /> Der Treiber oder die Datenquelle unterstützt nicht die Konvertierung angegeben, durch die Kombination der *TargetType* Argument und der SQL-Datentyp der entsprechenden Spalte. Dieser Fehler bezieht sich nur, wenn der SQL-Datentyp der Spalte in einen treiberspezifischen SQL-Datentyp zugeordnet wurde.<br /><br /> Der Treiber unterstützt nur ODBC 2.*.x*, und das Argument *TargetType* war es eines der folgenden:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> und das Intervall C-Datentypen in [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) in Anhang D:-Datentypen.<br /><br /> Der Treiber unterstützt nur die ODBC-Versionen vor 3.50 und dem Argument *TargetType* SQL_C_GUID wurde.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber entspricht der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLGetData** Daten in einer angegebenen Spalte zurück. **SQLGetData** kann aufgerufen werden, erst nach einer oder mehreren Zeilen aus dem Resultset von abgerufen wurden **SQLFetch**, **SQLFetchScroll**, oder **SQLExtendedFetch** . Wenn Daten variabler Länge in einem einzigen Aufruf zurückzugebenden zu groß ist **SQLGetData** (aufgrund einer Einschränkung in der Anwendung) **SQLGetData** in Teilen abrufen können. Es ist möglich, einige Spalten in einer Zeile und der Aufruf binden **SQLGetData** für andere, obwohl dies einigen Einschränkungen unterliegt. Weitere Informationen finden Sie unter [Abrufen von Long-Daten](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Informationen zur Verwendung **SQLGetData** mit gestreamte Output-Parameter finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Mithilfe von SQLGetData  
 Wenn der Treiber keine Erweiterungen unterstützt **SQLGetData**, die Funktion kann zurückgeben nur Daten für ungebundene Spalten mit einer Zahl größer als der letzten gebundenen Spalte. Darüber hinaus innerhalb eine Zeile mit Daten, den Wert von der *Col_or_Param_Num* Argument in jedem Aufruf von **SQLGetData** muss größer als oder gleich dem Wert des *Col_or_Param_Num*in den vorhergehenden Aufruf; d. h. müssen Daten in aufsteigender Spaltenreihenfolge abgerufen werden. Abschließend, wenn keine Erweiterungen unterstützt werden, **SQLGetData** kann nicht aufgerufen werden, wenn die Rowsetgröße größer als 1 ist.  
  
 Treiber können diese Einschränkungen weniger streng gehandhabt. Um zu bestimmen, welche Einschränkungen lockert die ein Treiber, eine Anwendung ruft **SQLGetInfo** mit den folgenden SQL_GETDATA_EXTENSIONS-Optionen:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** aufgerufen werden, um die Werte der Ausgabeparameter zurückgeben. Weitere Informationen finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Wenn diese Option zurückgegeben wird, **SQLGetData** für alle ungebundenen Spalten, einschließlich der vor der letzten Spalte gebundenen aufgerufen werden kann.  
  
-   SQL_GD_ANY_ORDER. Wenn diese Option zurückgegeben wird, **SQLGetData** für ungebundene Spalten in einer beliebigen Reihenfolge aufgerufen werden können.  
  
-   SQL_GD_BLOCK. Wenn diese Option zurückgegebene **SQLGetInfo** für die Informationsart SQL_GETDATA_EXTENSIONS unterstützt der Treiber Aufrufe an **SQLGetData** Wenn die Rowsetgröße größer als 1 ist, und die Anwendung kann Aufrufen**SQLSetPos** mit der Option SQL_POSITION zur Positionierung des Cursors auf die richtige Zeile vor dem Aufruf **SQLGetData.**  
  
-   SQL_GD_BOUND. Wenn diese Option zurückgegeben wird, **SQLGetData** für gebundene Spalten kann aufgerufen werden, als auch ungebundene Spalten.  
  
 Es gibt zwei Ausnahmen von dieser Einschränkungen sowie einen Treiber Möglichkeit, diese zu lockern. Erstens **SQLGetData** sollte nie für einen Vorwärtscursor aufgerufen werden, wenn die Rowsetgröße größer als 1 ist. Zweitens, wenn ein Treiber Lesezeichen unterstützt, es muss immer unterstützen die Möglichkeit, rufen Sie **SQLGetData** für die Spalte 0, auch wenn dies nicht zulässt, dass aufrufen, **SQLGetData** für andere Spalten vor dem letzten gebundene Spalte. (Wenn eine Anwendung mit einer ODBC 2. funktioniert*.x* -Treiber **SQLGetData** wird erfolgreich ein Lesezeichen bei einem Aufruf mit zurückgeben *Col_or_Param_Num* gleich 0 nach einem Aufruf von **SQLFetch**, da **SQLFetch** zugeordnet ist, indem die ODBC 3.*.x* Treiber-Manager auf **SQLExtendedFetch** mit einem  *FetchOrientation* sql_fetch_next, und **SQLGetData** mit einem *Col_or_Param_Num* 0 zugeordnet, indem die ODBC 3.*.x* Treiber-Manager **SQLGetStmtOption** mit einem *fOption* von SQL_GET_BOOKMARK.)  
  
 **SQLGetData** kann nicht verwendet werden, um das Lesezeichen für eine Zeile durch Aufrufen von gerade eingefügten abrufen **SQLBulkOperations** mit der Option sql_add, da sich der Cursor nicht in der Zeile positioniert ist. Eine Anwendung kann das Lesezeichen für eine solche Zeile abrufen, indem binden Spalte 0 vor dem Aufruf **SQLBulkOperations** mit SQL_ADD, in diesem Fall **SQLBulkOperations** gibt das Lesezeichen in den gebundenen Puffer zurück. **SQLFetchScroll** kann dann mit SQL_FETCH_BOOKMARK positioniert den Cursor in dieser Zeile aufgerufen werden.  
  
 Wenn die *TargetType* Argument ist ein Intervall-Datentyp, der Intervall führende standardgenauigkeit (2) und die standardmäßige Intervall Sekunden Genauigkeit (6), wie in den Feldern SQL_DESC_DATETIME_INTERVAL_PRECISION und SQL_DESC_PRECISION des festgelegt die ARD, sind für die Daten verwendet. Wenn die *TargetType* Argument ist ein Datentyp SQL_C_NUMERIC wird die standardgenauigkeit (treiberdefinierten) und standardmäßig über Dezimalstellen (0), wie in die Felder SQL_DESC_PRECISION und SQL_DESC_SCALE der ARD festgelegt, für die Daten verwendet werden. Wenn alle Standardwerte für die Genauigkeit oder Dezimalstellen nicht geeignet ist, die Anwendung sollten explizit festlegen der entsprechenden Deskriptorfeld durch einen Aufruf von **SQLSetDescField** oder **SQLSetDescRec**. Sie kann SQL_C_NUMERIC und rufen Sie das Feld SQL_DESC_CONCISE_TYPE festgelegt **SQLGetData** mit einem *TargetType* Argument SQL_ARD_TYPE, wodurch die Genauigkeit und Dezimalstellenanzahl Werte in die deskriptorfelder verwendet werden.  
  
> [!NOTE]  
>  In ODBC 2.*.x*, Anwendungen legen *TargetType* SQL_C_DATE, SQL_C_TIME oder SQL_C_TIMESTAMP, um anzugeben, dass \* *TargetValuePtr* ist ein Datum und die Uhrzeit oder Timestamp-Struktur. In ODBC 3.*.x*, Anwendungen legen *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME oder SQL_C_TYPE_TIMESTAMP. Der Treiber-Manager stellt passenden Zuordnungen Wenn erforderlich, je nachdem, auf die Anwendungs- und Treibersoftware Version.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Abrufen von Daten mit variabler Länge in Teilen  
 **SQLGetData** dient zum Abrufen von Daten aus einer Spalte, die Daten variabler Länge in Teilen enthält – d. h., wenn der Bezeichner der der SQL-Datentyp der Spalte ist SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY oder einen Bezeichner treiberspezifische für Typen mit variabler Länge.  
  
 Abrufen von Daten aus einer Spalte in Teilen die Anwendung ruft **SQLGetData** mehrmals nacheinander für dieselbe Spalte. Bei jedem Aufruf **SQLGetData** der nächste Teil der Daten. Es ist Aufgabe der Anwendung zum Segmentieren der Teile, achten Sie darauf, um die Null-Abschlusszeichen aus intermediate Teile von Zeichendaten zu entfernen. Wenn weitere zurückgeben werden Daten oder nicht genügend Puffer belegt wurde, für das abschließende Nullzeichen **SQLGetData** SQL_SUCCESS_WITH_INFO und SQLSTATE 01004 (Daten abgeschnitten). Den letzten Teil der Daten Rückkehr **SQLGetData** gibt SQL_SUCCESS zurück. SQL_NO_TOTAL weder 0 (null) kann auf der letzten gültigen Aufruf zum Abrufen von Daten aus einer Spalte zurückgegeben werden, da die Anwendung dann, dass keine Möglichkeit müsste, zu wissen, welcher Anteil der Daten in den Anwendungspuffer gültig ist. Wenn **SQLGetData** wird aufgerufen, anschließend, es gibt SQL_NO_DATA zurück. Weitere Informationen finden Sie im nächsten Abschnitt, "Abrufen von Daten mit SQLGetData."  
  
 Lesezeichen mit variabler Länge zurückgegeben werden können, in Teilen von **SQLGetData**. Wie bei anderen Daten, die einen Aufruf von **SQLGetData** zurückzugebenden variabler Länge Lesezeichen in Teilen gibt SQLSTATE 01004 (Zeichenfolgendaten, rechts abgeschnitten) und SQL_SUCCESS_WITH_INFO zurück, wenn weitere Daten zurückgegeben werden. Dies ist die Groß-/Kleinschreibung unterscheiden, wenn ein Lesezeichen variabler Länge, durch einen Aufruf von abgeschnitten werden **SQLFetch** oder **SQLFetchScroll**, womit SQL_ERROR und SQLSTATE 22001 (Zeichenfolgendaten, rechts abgeschnitten).  
  
 **SQLGetData** kann nicht in Teilen die zurückzugebenden Daten fester Länge verwendet werden. Wenn **SQLGetData** ist mehr als einmal in einer Zeile für eine Spalte mit Daten fester Länge aufgerufen, es gibt SQL_NO_DATA zurück, für alle Aufrufe nach dem ersten.  
  
## <a name="retrieving-streamed-output-parameters"></a>Abrufen von gestreamte Output-Parameter  
 Wenn ein Treiber gestreamte Output-Parameter unterstützt, kann eine Anwendung aufrufen **SQLGetData** mit einem kleinen Puffer häufig um einen großen Parameterwert abzurufen. Weitere Informationen zu gestreamte Output-Parameter, finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Abrufen von Daten mit SQLGetData  
 Zum Zurückgeben von Daten für die angegebene Spalte **SQLGetData** führt die folgende Sequenz von Schritten:  
  
1.  Gibt SQL_NO_DATA zurück, wenn bereits alle Daten für die Spalte zurückgegeben wurden.  
  
2.  Legt \* *StrLen_or_IndPtr* auf SQL_NULL_DATA, wenn die Daten NULL sind. Wenn die Daten NULL sind und *StrLen_or_IndPtr* wurde ein null-Zeiger **SQLGetData** SQLSTATE 22002 (Indikatorvariable erforderlich, jedoch nicht bereitgestellt) zurückgegeben.  
  
     Wenn die Daten für die Spalte ungleich NULL ist, **SQLGetData** mit Schritt 3 fortgesetzt wird.  
  
3.  Wenn das SQL_ATTR_MAX_LENGTH-Anweisungsattribut auf einen Wert ungleich NULL festgelegt ist, wenn die Spalte Zeichen- oder Binärdaten enthält, und wenn **SQLGetData** zuvor nicht aufgerufen wurde für die Spalte, die Daten auf SQL_ATTR_MAX_LENGTH abgeschnitten Bytes.  
  
    > [!NOTE]  
    >  Das SQL_ATTR_MAX_LENGTH-Anweisungsattribut soll den Netzwerkverkehr zu reduzieren. Es ist in der Regel von der Datenquelle implementiert, die die Daten abgeschnitten werden, vor der Rückgabe über das Netzwerk. Treiber und Datenquellen werden nicht zu ihrer Unterstützung erforderlich. Aus diesem Grund um zu gewährleisten, dass die Daten auf eine bestimmte Größe abgeschnitten werden, eine Anwendung sollte ein Puffer der Größe und geben Sie die Größe in der *Pufferlänge* Argument.  
  
4.  Konvertiert die Daten in dem im angegebenen Typ *TargetType*. Die Daten erhält die Standardwerte für Genauigkeit und Dezimalstellen für diesen Datentyp. Wenn *TargetType* ist SQL_ARD_TYPE, die Daten in das Feld SQL_DESC_CONCISE_TYPE der ARD wird verwendet. Wenn *TargetType* SQL_ARD_TYPE ist, die Daten erhält die Genauigkeit und Dezimalstellen in der SQL_DESC_DATETIME_INTERVAL_PRECISION SQL_DESC_PRECISION, und SQL_DESC_SCALE Felder ARD, abhängig von den Daten geben die SQL_DESC_CONCISE _Geben-Feld. Wenn alle Standardwerte für die Genauigkeit oder Dezimalstellen nicht geeignet ist, die Anwendung sollten explizit festlegen der entsprechenden Deskriptorfeld durch einen Aufruf von **SQLSetDescField** oder **SQLSetDescRec**.  
  
5.  Wenn die Daten in einen Datentyp variabler Länge, z. B. Zeichen oder binär, konvertiert wurde **SQLGetData** überprüft, ob die Länge der Daten überschreitet *Pufferlänge*. Überschreitet die Länge der Zeichendaten (einschließlich der Null-Abschlusszeichen) *Pufferlänge*, **SQLGetData** schneidet die Daten *Pufferlänge* abzüglich der Länge von einer Null-Abschlusszeichen. Sie beendet Null-dann die Daten. Die Länge der binären Daten überschreitet die Länge des Datenpuffers **SQLGetData** , schneidet *Pufferlänge* Bytes.  
  
     Wenn die zur Verfügung gestellte Datenpuffer zu klein für das Null-Terminierung Zeichen ist **SQLGetData** SQL_SUCCESS_WITH_INFO und SQLSTATE 01004 zurückgegeben.  
  
     **SQLGetData** nie schneidet Daten in Daten fester Länge Typen konvertiert, wird immer vorausgesetzt, dass die Länge des **TargetValuePtr* ist die Größe des Datentyps.  
  
6.  Platziert die konvertierte (und möglicherweise abgeschnitten) Daten im \* *TargetValuePtr*. Beachten Sie, dass **SQLGetData** kann keine Daten aus der Zeile zurückgeben.  
  
7.  Legt die Länge der Daten in \* *StrLen_or_IndPtr*. Wenn *StrLen_or_IndPtr* wurde ein null-Zeiger **SQLGetData** gibt die Länge nicht zurück.  
  
    -   Für Zeichen- oder Binärdaten darstellen, ist dies die Länge der Daten nach der Konvertierung und vor dem Abschneiden aufgrund *Pufferlänge*. Wenn der Treiber die Länge der Daten nach der Konvertierung nicht ermitteln kann manchmal bei long-Daten der Fall ist, gibt SQL_SUCCESS_WITH_INFO zurück und legt die Länge auf SQL_NO_TOTAL fest. (Der letzte Aufruf von **SQLGetData** müssen immer die Länge der Daten, nicht 0 (null) oder SQL_NO_TOTAL zurück.) Wenn Daten abgeschnitten wurden, da die Anweisung SQL_ATTR_MAX_LENGTH Attribut ist, wird den Wert dieses Attributs – im Gegensatz zu der tatsächlichen Länge – befindet sich im \* *StrLen_or_IndPtr*. Dies ist dieses Attribut ist darauf ausgelegt, zum Abschneiden von Daten auf dem Server vor der Konvertierung, damit der Treiber keine Möglichkeit zu ermitteln hat, welche die tatsächliche Länge ist. Wenn **SQLGetData** ist die gleiche Spalte mehrmals nacheinander aufgerufen, dies ist die Länge der verfügbaren Daten zu Beginn des aktuellen Aufrufs; d. h. die Länge nimmt mit jedem nachfolgenden Aufruf.  
  
    -   Für alle anderen Datentypen ist dies die Länge der Daten nach der Konvertierung; d. h., ist es die Größe des Typs, der die Daten konvertiert wurde.  
  
8.  Wenn während der Konvertierung werden die Daten ohne Verlust von "significance" abgeschnitten werden (z. B. die reelle Zahl-1,234 wird abgeschnitten, wenn auf die ganze Zahl 1 konvertiert), oder weil *Pufferlänge* zu klein ist (z. B. die Zeichenfolge "Abcdef" befindet in einem 4-Byte-Puffer) **SQLGetData** SQLSTATE 01004 (Daten abgeschnitten) und SQL_SUCCESS_WITH_INFO zurückgegeben. Wenn Daten, ohne Verlust von "significance" aufgrund der SQL_ATTR_MAX_LENGTH-Anweisungsattribut abgeschnitten werden **SQLGetData** gibt SQL_SUCCESS zurück, und gibt keinen SQLSTATE 01004 (Daten abgeschnitten) zurück.  
  
 Der Inhalt des Puffers gebundenen Daten (Wenn **SQLGetData** für eine gebundene Spalte aufgerufen wird) und die Längen-/Indikatorpuffers ist nicht definiert, wenn **SQLGetData** keinen SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgibt.  
  
 Aufeinander folgende Aufrufe von **SQLGetData** Abrufen von Daten aus der letzten Spalte angefordert werden; vorherige Offsets werden ungültig. Beispielsweise, wenn die folgende Sequenz ausgeführt wird:  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 der zweite Aufruf von SQLGetData(icol=n) Ruft Daten ab, ab dem Anfang der n-Spalte. Alle Offset in den Daten aufgrund von früheren Aufrufen auf **SQLGetData** für die Spalte nicht mehr gültig ist.  
  
## <a name="descriptors-and-sqlgetdata"></a>Deskriptoren und SQLGetData  
 **SQLGetData** interagieren nicht direkt mit Descriptor-Felder.  
  
 Wenn *TargetType* ist SQL_ARD_TYPE, die Daten in das Feld SQL_DESC_CONCISE_TYPE der ARD wird verwendet. Wenn *TargetType* SQL_ARD_TYPE oder SQL_C_DEFAULT, die Daten erhält die Genauigkeit und Dezimalstellen in der SQL_DESC_DATETIME_INTERVAL_PRECISION SQL_DESC_PRECISION, und SQL_DESC_SCALE Felder ARD, abhängig von den Daten geben im Feld "SQL_DESC_CONCISE_TYPE".  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel führt eine Anwendung eine **wählen** Anweisung ein Resultset des Kunden-IDs, Namen, zurückgeben und Telefonnummern, sortiert nach Name, ID und Telefonnummer. Für jede Datenzeile ruft **SQLFetch** zur Positionierung des Cursors zur nächsten Zeile. Sie ruft **SQLGetData** zum Abrufen der abgerufenen Daten; die Puffer für die Daten und die zurückgegebene Anzahl von Bytes im Aufruf angegeben werden **SQLGetData**. Schließlich gibt sie Name, ID und Telefonnummer des Mitarbeiters.  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Zuweisen von Speicher für eine Spalte in einem Resultset|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ausführen von Massenvorgängen, die nicht auf die Cursorposition Block beziehen|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Eine einzelne Zeile mit Daten oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Senden der Parameterdaten zum Zeitpunkt der Ausführung|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Positionieren den Cursor, Aktualisieren von Daten im Rowset aktualisieren oder Löschen von Daten im rowset|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [Abrufen von Ausgabeparametern mithilfe von SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
