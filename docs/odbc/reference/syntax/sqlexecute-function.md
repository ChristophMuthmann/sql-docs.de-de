---
title: SQLExecute-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLExecute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecute
helpviewer_keywords:
- SQLExecute function [ODBC]
ms.assetid: 9286a01d-cde2-4b90-af94-9fd7f8da48bf
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0b1660fbd60346aff1c4ef24dcba32a778a00d5e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlexecute-function"></a>SQLExecute-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLExecute** führt eine vorbereitete Anweisung, die die aktuellen Werte der Parameter Marker Variablen verwenden, wenn einem Parametermarker in der Anweisung vorhanden sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE oder SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLExecute** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLExecute** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01001|Konflikt beim Cursorvorgang|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthaltenen ein positioniertes update oder delete-Anweisung und keine Zeilen oder mehr als eine Zeile aktualisiert oder gelöscht wurden. (Weitere Informationen über Updates auf mehr als eine Zeile, finden Sie unter der Beschreibung der SQL_ATTR_SIMULATE_CURSOR *Attribut* in **SQLSetStmtAttr**.)<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01003|NULL-Wert wurde in der Set-Funktion gelöscht|Die vorbereitete Anweisung zugeordneten *StatementHandle* enthalten eine Set-Funktion (z. B. **AVG**, **MAX**, **MIN**usw.), aber nicht die **Anzahl** festgelegt-Funktion und NULL-Argument Werte wurden entfernt, bevor die Funktion angewendet wurde. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL führte Zeichenfolgen- oder Binärdaten für ein Output-Parameter zurückgegeben. Falls es sich um einen Zeichenfolgenwert handelt, wurde es rechts abgeschnitten. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01006|Berechtigung nicht aufgehoben.|Die vorbereitete Anweisung zugeordneten der *StatementHandle* wurde eine **widerrufen** -Anweisung und der Benutzer verfügte nicht über die angegebene Berechtigung. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01007|Berechtigung nicht gewährt.|Die vorbereitete Anweisung zugeordneten der *StatementHandle* wurde eine **GRANT** -Anweisung und der Benutzer konnte nicht erteilt werden die angegebene Berechtigung.|  
|01 S 02|Der Optionswert wurde geändert|Ein Attribut angegebene Anweisung war ungültig aufgrund Implementierung Arbeitsbedingungen, damit ein ähnlichen Wert vorübergehend ersetzt wurde. (**SQLGetStmtAttr** aufgerufen werden können, um zu bestimmen, was vorübergehend ersetzten Werts ist.) Der Ersatzwert ist gültig für die *StatementHandle* , bis der Cursor geschlossen wird, an welchem Punkt das Anweisungsattribut zurückgesetzt auf seinen ursprünglichen Wert. Sind die Anweisungsattribute, die geändert werden können: SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE, SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT und SQL_ATTR_SIMULATE_CURSOR. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S07|Teilbereiche wurden abgeschnitten.|Die Daten für eine Eingabe/Ausgabe zurückgegeben oder Output-Parameter wurde abgeschnitten, dass der Bruchteil der Zeitkomponente eines Datentyps Zeit, Timestamp- oder Intervall abgeschnitten wurde oder der Bruchteil der einen numerischen Datentyp abgeschnitten wurde.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07002|COUNT-Feld ist ungültig.|Die angegebene Anzahl von Parametern **SQLBindParameter** ist kleiner als die Anzahl von Parametern in der SQL-Anweisung, die in enthaltenen \* *StatementText*.<br /><br /> **SQLBindParameter** aufgerufen wurde, wobei *ParameterValuePtr* auf ein null-Zeiger festgelegt *StrLen_or_IndPtr* nicht auf SQL_NULL_DATA oder SQL_DATA_AT_EXEC, festgelegt und  *InputOutputType* nicht, dass die Anzahl von Parametern in angegeben festgelegt SQL_PARAM_OUTPUT, **SQLBindParameter** war größer als die Anzahl von Parametern in der SQL-Anweisung, die in enthaltenen **StatementText*.|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert durch identifiziert die *ValueType* Argument in **SQLBindParameter** für der gebundene Parameter nicht in den identifizierten Datentyp konvertiert werden konnte die *ParameterType*Argument in **SQLBindParameter**.<br /><br /> Der Datenwert zurückgegeben, für einen Parameter gebunden werden, wie SQL_PARAM_INPUT_OUTPUT oder SQL_PARAM_OUTPUT nicht in der identifizierten Datentyp konvertiert werden konnte die *ValueType* Argument in **SQLBindParameter**.<br /><br /> (Wenn die Datenwerte für eine oder mehrere Zeilen nicht konvertiert werden konnte, aber eine oder mehrere Zeilen wurden erfolgreich zurückgegeben, diese Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07007|Restricted-Parameters Wert Verletzung|Der Parametertyp SQL_PARAM_INPUT_OUTPUT_STREAM wird nur für einen Parameter verwendet, die Daten sendet und empfängt in Teilen. Ein gebundener Eingabepuffer ist für diesen Parameter nicht zulässig.<br /><br /> Dieser Fehler tritt auf, wenn der Parametertyp SQL_PARAM_INPUT_OUTPUT ist, und die \* *StrLen_or_IndPtr* im angegebenen **SQLBindParameter** stimmt nicht mit SQL_NULL_DATA SQL_DEFAULT_ PARAM, SQL_LEN_DATA_AT_EXEC(len) oder SQL_DATA_AT_EXEC.|  
|07S01|Ungültige Verwendung des Standardparameters|Legen Sie ein Parameterwert mit **SQLBindParameter**, SQL_DEFAULT_PARAM und der entsprechende Parameter wurde nicht für eine kanonische Prozeduraufruf ODBC-Parameter.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|21S02|Die Spaltenzahl der abgeleiteten Tabelle stimmt nicht mit Spaltenliste überein.|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthalten eine **CREATE VIEW** -Anweisung und der nicht qualifizierte Spaltenliste (die angegebene Anzahl von Spalten für die Ansicht in der  *Spaltenbezeichner* Argumente der SQL-Anweisung) enthalten mehrere Namen als die Anzahl der Spalten in der abgeleiteten Tabelle definiert werden, indem Sie die *-Abfragespezifikation* Argument der SQL-Anweisung.|  
|22001|Die Zeichenfolgedaten rechts abgeschnitten.|Die Zuweisung von einem Zeichen- oder binären Wert einer Spalte führte zu NichtLeer (Zeichen) oder ungleich Null (binären) Zeichen oder Bytes wird abgeschnitten.|  
|22002|Anzeigevariable erforderlich, aber nicht angegeben|NULL-Daten an ein Output-Parameter gebunden wurde, deren *StrLen_or_IndPtr* festlegen, indem **SQLBindParameter** wurde ein null-Zeiger.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthalten einen gebundenen numerischen Parameter, und der Wert des Parameters verursacht die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird, wenn die zugeordnete zugewiesen Tabellenspalte.<br /><br /> Einen numerischen Wert (als numerisch oder Zeichenfolge) für einen oder mehrere Parameter für Eingabe/Ausgabe- oder Ausgabeparameter zurückgeben würde die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abzuschneidende vorliegt.|  
|22007|Ungültiges Datetime-format|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthalten eine SQL-Anweisung, die ein Datum, Uhrzeit oder Timestamp-Struktur als gebundene Parameter enthalten, und der Parameter war, bzw. ein ungültiges Datum, Zeit, oder Zeitstempel.<br /><br /> Ein Eingabe/Ausgabe- oder Ausgabe-Parameter an ein Datum, Uhrzeit oder C-zeitstempelstruktur gebunden wurde, und ein Wert im Parameters zurückgegeben wurde, bzw. ein ungültiges Datum, Uhrzeit oder Zeitstempel. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|22008|Überlauf der DateTime-Feld.|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthaltenen eine SQL-Anweisung, die einen Datetime-Ausdruck enthalten, wenn berechnete führte zu einem Datum, Uhrzeit oder Zeitstempel, die Struktur war ungültig.<br /><br /> Ein Datetime-Ausdruck für eine Eingabe/Ausgabe berechnet oder Ausgabeparameter Verzeichnisdiensts ist ein Datum, Uhrzeit oder C-zeitstempelstruktur, die ungültig war.|  
|22012|Division durch 0 (null)|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthaltenen einen arithmetischen Ausdruck, die Division durch 0 (null) verursacht.<br /><br /> Ein arithmetischer Ausdruck für eine Eingabe/Ausgabe berechnet oder Ausgabeparameter Verzeichnisdiensts Division durch 0 (null).|  
|22015|Überlauf der Intervall-Feld.|*\*StatementText* einen genauen numerischen oder Intervall-Parameter enthalten, wenn auf ein Intervall SQL-Datentyp konvertiert wird, verursacht einen Verlust signifikanter Ziffern.<br /><br /> *\*StatementText* einen Intervall-Parameter mit mehr als ein Feld enthalten, dass bei der Konvertierung in einen numerischen Datentyp in einer Spalte keine Darstellung im numerischen Datentyp aufweisen.<br /><br /> *\*StatementText* enthielt Parameterdaten, die, der auf ein Intervall SQL-Typ zugewiesen wurde, und es wurde keine Darstellung des Werts der C-Typ im Intervall SQL-Typ.<br /><br /> Zuweisen eines Eingabe/Ausgabe- oder Ausgabe-Parameters, die einen genauen numerischen oder einen Zeitraum SQL-Typ in einen C-Intervalltyp hat einen Datenverlust von signifikanten Stellen verursacht wurde.<br /><br /> Wenn ein Eingabe/Ausgabe- oder Ausgabe-Parameter auf ein Intervall C-Struktur zugewiesen wurde, gab es keine Darstellung der Daten in der Datenstruktur Intervall.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|*\*StatementText* einen C-Typ enthalten, die eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp wurde; der SQL-Typ der Spalte eines Zeichendatentyps; und der Wert in der Spalte nicht wurde ein gültiger Literal des gebundenen C-Typs.<br /><br /> Wenn ein Parameter Eingabe/Ausgabe- oder Ausgabeparameter zurückgegeben wurde, war der SQL-Typ eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp. der C-Typ wurde SQL_C_CHAR; und kein Wert in der Spalte wurde ein gültiger Literal des gebundenen SQL-Typs.|  
|22019|Ungültiges Escapezeichen|Der vorbereiteten Anweisung zugeordnet *StatementHandle* enthalten eine **wie** Prädikat mit einer **mit Escapezeichen versehen** in der **, in dem** -Klausel, und die Länge der folgenden Zeichen Escape **ESCAPE** war nicht gleich 1.|  
|22025|Ungültige Escapesequenz|Die vorbereitete Anweisung zugeordneten *StatementHandle* enthaltenen "**wie** *Musterwert* **ESCAPE** *Escapezeichen Zeichen*"in der **, in dem** -Klausel, und folgende Escape-Zeichen in den Musterwert Zeichen gehörte nicht zu"%"oder"_".|  
|23000|Einschränkungsverletzung Integrität|Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthalten einen Parameter. Der Wert des Parameters NULL für eine Spalte als NOT NULL in der zugeordneten Spalte definiert wurde, wurde ein doppelter Wert für eine Spalte, die nur eindeutige Werte enthalten eingeschränkte angegeben oder einige andere integritätseinschränkung wurde verletzt.|  
|24000|Ungültiger Cursorstatus|Ein Cursor positioniert wurde die *StatementHandle* von **SQLFetch** oder **SQLFetchScroll**. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*.<br /><br /> Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthalten ein positioniertes Update oder Delete Statemen "," t "und" der Cursor vor dem Start des Resultsets oder nach dem Ende des Resultsets positioniert wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|42000|Syntaxfehler oder zugriffsverletzung|Der Benutzer keine Berechtigung zum Ausführen der vorbereiteten Anweisung zugeordneten der *StatementHandle*.|  
|44000|WITH CHECK OPTION-Verstoß|Die vorbereitete Anweisung zugeordneten *StatementHandle* enthalten eine **einfügen** -Anweisung für eine Tabelle ausgeführt oder eine Tabelle aus der Tabelle, die erstellt wurde, indem Sie abgeleitet**WITH CHECK OPTION**, sodass eine oder mehrere Zeilen auswirkt der **einfügen** Anweisung wird nicht mehr in der Tabelle vorhanden sein.<br /><br /> Die vorbereitete Anweisung zugeordneten der *StatementHandle* enthalten eine **UPDATE** -Anweisung für eine Tabelle ausgeführt oder eine Tabelle aus der Tabelle, die erstellt wurde, indem Sie abgeleitet**WITH CHECK OPTION**, sodass eine oder mehrere Zeilen auswirkt der **UPDATE** Anweisung wird nicht mehr in der Tabelle vorhanden sein.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLExecute** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) die *StatementHandle* wurde nicht vorbereitet.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Legen Sie ein Parameterwert mit **SQLBindParameter**wurde ein null-Zeiger und der Wert des Parameters Länge wurde nicht 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM oder kleiner oder gleich SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Legen Sie ein Parameterwert mit **SQLBindParameter**, war ein null-Zeiger; der C-Datentyp SQL_C_BINARY oder SQL_C_CHAR; und der Wert des Parameters Länge wurde jedoch kleiner als 0 war nicht SQL_NTS, SQL_NULL_DATA, SQL_DEFAULT_PARAM oder SQL_DATA_ AT_EXEC, oder kleiner oder gleich SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Length-Parameterwert gebunden wird, indem **SQLBindParameter** auf SQL_DATA_AT_EXEC festgelegt wurde, wurde des SQL-Typs, SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen des Datentyps sowie SQL_NEED_LONG_DATA_LEN Informationen Geben Sie in **SQLGetInfo** wurde von "Y".|  
|HY105|Ungültiger Parametertyp|Der Wert für das Argument angegebene *InputOutputType* in **SQLBindParameter** SQL_PARAM_OUTPUT und der Parameter wurde ein Eingabeparameter.|  
|HY109|Ungültige Cursorposition|Die vorbereitete Anweisung wurde eine positionierte Update- oder Delete-Anweisung und der Cursor positioniert wurde (durch **SQLSetPos** oder **SQLFetchScroll**) in einer Zeile, die gelöscht wurde oder konnte nicht abgerufen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
 **SQLExecute** zurückgeben kann eine beliebige SQLSTATE, die von zurückgegeben werden kann **SQLPrepare**basierend auf, wenn die Datenquelle für die SQL-Anweisung der Anweisung zugeordneten auswertet.  
  
## <a name="comments"></a>Kommentare  
 **SQLExecute** führt eine Anweisung vorbereitet, indem **SQLPrepare**. Nachdem die Anwendung verarbeitet oder die Ergebnisse eines Aufrufs verwirft **SQLExecute**, kann die Anwendung aufrufen **SQLExecute** erneut mit neuen Parameterwerte. Weitere Informationen über die vorbereitete Ausführung finden Sie unter [vorbereitete Ausführung](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
 Zum Ausführen einer **auswählen** -Anweisung mehr als einmal auf, die die Anwendung aufrufen muss **SQLCloseCursor** vor reexecuting der **auswählen** Anweisung.  
  
 Wenn die Datenquelle im Manualcommit-Modus (und erfordert explizite Transaktion Initiierung) und eine Transaktion nicht gestartet wurde wurde, initiiert der Treiber eine Transaktion vor dem Senden der SQL-Anweisung. Weitere Informationen finden Sie unter [Transaktionen](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Wenn eine Anwendung verwendet **SQLPrepare** vorbereiten und **SQLExecute** beim Übermitteln einer **COMMIT** oder **ROLLBACK** -Anweisung ist nicht möglich Interoperabilität zwischen DBMS-Produkte. Rufen Sie einen commit oder Rollback für eine Transaktion, **SQLEndTran**.  
  
 Wenn **SQLExecute** erkennt einen Data-at-Execution-Parameter, es wird SQL_NEED_DATA zurückgegeben. Die Anwendung sendet die Daten mit **SQLParamData** und **SQLPutData**. Finden Sie unter [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), und [Long-Daten senden](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Wenn **SQLExecute** führt ein gesuchtes Update, Insert oder Delete-Anweisung, die keine Zeilen in der Datenquelle, die den Aufruf von auswirkt **SQLExecute** gibt SQL_NO_DATA zurück.  
  
 Wenn der Wert des Attributs-Anweisung verweist SQL_ATTR_PARAMSET_SIZE größer als 1 ist und die SQL-Anweisung mindestens eine parametermarkierung enthält, **SQLExecute** führt die SQL-Anweisung einmal für jeden Satz von Parameterwerten in Arrays verweist die  *\*ParameterValuePtr* Argument in den Aufrufen **SQLBindParameter**. Weitere Informationen finden Sie unter [Arrays von Parameterwerten](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Wenn Lesezeichen aktiviert sind und eine Abfrage ausgeführt wird, kann nicht die Lesezeichen unterstützen, der Treiber sollten versuchen, von der Umgebung auf einen umgewandelt werden, die Lesezeichen unterstützt, indem Sie einen Attributwert und Rückgabe von SQLSTATE 01 s 02 (Optionswert wurde geändert). Wenn das Attribut kann nicht geändert werden, sollte der Treiber SQLSTATE HY024 zurück (Ungültiger Attributwert).  
  
> [!NOTE]  
>  Wenn Verbindungspooling verwenden, muss eine Anwendung keine SQL-Anweisungen, die die Datenbank oder im Kontext der Datenbank, wie z. B. ändern Ausführen der **verwenden** *Datenbank* -Anweisung in SQL Server, wodurch die ändert der Katalog, die von einer Datenquelle verwendet wird.  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), und [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Schließen des Cursors|[SQLCloseCursor-Funktion](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Ausführen eines Commit- oder Rollback-Vorgangs|[SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Das Abrufen mehrerer Datenzeilen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Freigeben eines Anweisungshandles|[SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Ein Cursorname zurückgeben|[SQLGetCursorName-Funktion](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Abrufen des Teils oder aller eine Spalte mit Daten|[SQLGetData-Funktion](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Den nächsten Parameter zum Senden von Daten für zurückgeben|[SQLParamData-Funktion](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Vorbereiten einer Anweisung für die Ausführung|[SQLPrepare-Funktion](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Senden der Parameterdaten zum Zeitpunkt der Ausführung|[SQLPutData-Funktion](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Ein Cursorname festlegen|[SQLSetCursorName-Funktion](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
