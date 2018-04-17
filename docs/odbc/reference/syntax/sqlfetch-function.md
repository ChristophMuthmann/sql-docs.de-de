---
title: SQLFetch-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQLFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f1d87bc952852df3301d095203f6c94794de795d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfetch-function"></a>SQLFetch-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLFetch** des nächsten Rowsets von Daten aus dem Resultset abruft, und gibt Daten für alle gebundenen Spalten zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLFetch** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf [SQLGetDiagRec-Funktion](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) mit einem *HandleType*von SQL_HANDLE_STMT auf, und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLFetch** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben. Wenn es sich bei Auftreten eines Fehlers in einer einzelnen Spalte [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) kann aufgerufen werden, mit einer *DiagIdentifier* von SQL_DIAG_COLUMN_NUMBER, um die Spalte zu bestimmen, der Fehler aufgetreten, andernfalls false ist, und  **SQLGetDiagField** kann aufgerufen werden, mit einem *DiagIdentifier* von SQL_DIAG_ROW_NUMBER Bestimmen der Zeile, die Spalte enthält.  
  
 Für alle diese SQLSTATEs, der SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurück (mit Ausnahme der 01xxx SQLSTATEs) zurückgeben kann, wird SQL_SUCCESS_WITH_INFO zurückgegeben, wenn ein Fehler, auf ein oder mehrere, aber nicht alle Zeilen einer Einfügung mehrerer Zeilen Operation auftritt, und SQL_ERROR zurückgegeben wird, wenn es sich bei Auftreten eines Fehlers in einer einzeiliges-Vorgang.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL führte Zeichenfolgen- oder Binärdaten, die für eine Spalte zurückgegeben. Falls es sich um einen Zeichenfolgenwert handelt, wurde es rechts abgeschnitten.|  
|01 S 01|Fehler in Zeile|Fehler beim Abrufen von einer oder mehreren Zeilen.<br /><br /> (Wenn diese SQLSTATE zurückgegeben, wenn eine ODBC 3.*.x* Anwendung arbeitet mit einer ODBC 2.*.x* -Treiber verwenden, kann es ignoriert werden.)|  
|01S07|Teilbereiche wurden abgeschnitten.|Für eine Spalte zurückgegebenen Daten wurden abgeschnitten. Für numerische Datentypen und wurde die Nachkommastellen der Zahl gekürzt. Für die Zeit, Zeitstempel und Interval-Datentypen, die eine Zeitkomponente enthalten, wurde der Bruchteil der Zeit abgeschnitten.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert einer Spalte im Resultset konnte nicht an der angegebenen Datentyp konvertiert werden *TargetType* in **SQLBindCol**.<br /><br /> Spalte 0 wurde mit einem Datentyp von SQL_C_BOOKMARK gebunden, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde.<br /><br /> Spalte 0 wurde mit einem Datentyp von SQL_C_VARBOOKMARK gebunden, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE nicht festgelegt wurde.|  
|07009|Ungültiger Deskriptorindex|Der Treiber wurde von einer ODBC 2.*.x* Treiber, der nicht unterstützt **SQLExtendedFetch**, und eine Spaltennummer in der Bindung für eine Spalte angegeben wurde, 0.<br /><br /> Spalte 0 gebunden wurde, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22001|Zeichenfolgedaten wurden rechts abgeschnitten|Ein variabler Länge Lesezeichen für eine Spalte zurückgegeben wurde abgeschnitten.|  
|22002|Anzeigevariable erforderlich, aber nicht angegeben|NULL wurde abgerufene Daten in eine Spalte, deren *StrLen_or_IndPtr* festlegen, indem **SQLBindCol** (oder SQL_DESC_INDICATOR_PTR festlegen, indem **SQLSetDescField** oder  **SQLSetDescRec**) wurde ein null-Zeiger.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Dem numerischen Wert als numerisch oder eine Zeichenfolge für eine oder mehrere gebundene Spalten zurückgeben würde die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird vorliegt.<br /><br /> Weitere Informationen finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) in Anhang D:-Datentypen.|  
|22007|Ungültiges Datetime-format|Eine Zeichenspalte im Resultset an ein Datum, Uhrzeit oder C-zeitstempelstruktur gebunden wurde, und ein Wert in der Spalte wurde, bzw. ein ungültiges Datum, Uhrzeit oder Zeitstempel.|  
|22012|Division durch 0 (null)|Ein Wert aus einem arithmetischen Ausdruck wurde von 0 (null) zurückgegeben Division geführt hat.|  
|22015|Überlauf der Intervall-Feld.|Intervalltyp C aus einer genauen numerischen oder Intervall SQL-Typ zuzuweisen, hat einen Datenverlust von signifikanten Stellen im Feld führende verursacht.<br /><br /> Beim Abrufen von Daten in ein C-Intervalltyp ist keine Darstellung des Werts des SQL-Datentyps in den Intervalltyp C.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Eine Zeichenspalte im Resultset an einen Zeichenpuffer C gebunden wurde, und die Spalte enthalten, ein Zeichen für die es keine Darstellung des Zeichensatzes des Puffers war.<br /><br /> Der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte wurde einem Zeichendatentyp; und kein Wert in der Spalte wurde ein gültiger Literal des gebundenen C-Typs.|  
|24000|Ungültiger Cursorstatus|Die *StatementHandle* in einem ausgeführten Zustand wurde jedoch kein Resultset zugeordnet wurde die *StatementHandle*.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion, in der der Abruf ausgeführt wurde, wurde beendet, um Deadlocks zu vermeiden.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die **SQLFetch** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Die **SQLFetch** Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Or **SQLFetch** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*  aus einem anderen Thread in einer multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLFetch** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) dem angegebenen *StatementHandle* war nicht in einem ausgeführten Zustand. Die Funktion wurde aufgerufen, ohne zunächst **SQLExecDirect**, **SQLExecute** oder eine Katalogfunktion auf.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) **SQLFetch** wurde aufgerufen, die *StatementHandle* nach **SQLExtendedFetch** aufgerufen wurde und bevor **SQLFreeStmt** mit den SQL_ CLOSE-Option wurde aufgerufen.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Das SQL_ATTR_USE_BOOKMARK-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und Spalte 0 wurde auf einen Puffer, dessen Länge nicht gleich die maximale Länge für das Lesezeichen für dieses Resultset war, gebunden. (Diese Länge finden Sie im Feld SQL_DESC_OCTET_LENGTH vom IRD und abgerufen werden kann, durch den Aufruf **SQLDescribeCol**, **SQLColAttribute**, oder **SQLGetDescField**.)|  
|HY107|Zeilenwert außerhalb des gültigen Bereichs|Mit dem SQL_ATTR_CURSOR_TYPE-Attribut-Anweisung angegebene Wert war SQL_CURSOR_KEYSET_DRIVEN, jedoch mit SQL_ATTR_KEYSET_SIZE-Anweisungsattribut angegebene Wert größer als 0 und kleiner als der Wert, der mit der SQL_ATTR_ROW_ARRAY_ angegeben Anweisungsattribut Größe.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht die Konvertierung angegeben, durch die Kombination der *TargetType* in **SQLBindCol** und dem SQL-Datentyp der entsprechenden Spalte.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle, die das angeforderte Resultset zurückgegeben. Das Timeout wird durch SQLSetStmtAttr SQL_ATTR_QUERY_TIMEOUT festgelegt.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLFetch** des nächsten Rowsets im Resultset zurückgegeben. Es kann nur verwendet werden, während ein Resultset vorhanden ist aufgerufen werden: d. h. nach einem Aufruf, der ein Resultset erstellt und vor dem Cursor Failover, das Resultset geschlossen wird. Wenn keine Spalten gebunden sind, werden die Daten in diesen Spalten zurückgegeben. Wenn die Anwendung einen Zeiger auf ein zeilenstatusarray oder auf einen Puffer, in dem die Anzahl der Zeilen abgerufen, zurückgegeben angegeben wurde **SQLFetch** gibt auch diese Informationen zurück. Aufrufe von **SQLFetch** können durch Aufrufe von gemischt werden **SQLFetchScroll** jedoch durch Aufrufe von kombiniert werden, kann nicht **SQLExtendedFetch**. Weitere Informationen finden Sie unter [Abrufen von Zeilendaten](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Wenn eine ODBC 3.*.x* Anwendung arbeitet mit einer ODBC 2.*.x* -Treiber verwenden, wird der Treiber-Manager zugeordnet **SQLFetch** Aufrufe von **SQLExtendedFetch** für ein ODBC 2.*.x* Treiber, unterstützt **SQLExtendedFetch**. Wenn die ODBC 2.*.x* -Treiber nicht unterstützt **SQLExtendedFetch**, ordnet der Treiber-Manager **SQLFetch** Aufrufe von **SQLFetch** in der ODBC-2 *.x* Treiber, der nur eine einzelne Zeile abrufen kann.  
  
 Weitere Informationen finden Sie unter [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
## <a name="positioning-the-cursor"></a>Positionieren den Cursor  
 Wenn das Resultset erstellt wird, befindet sich der Cursor vor dem Start des Resultsets. **SQLFetch** wird die nächste Rowset abgerufen. Dies entspricht dem Aufruf **SQLFetchScroll** mit *FetchOrientation* SQL_FETCH_NEXT festgelegt. Weitere Informationen zu Cursorn finden Sie unter [Cursor](../../../odbc/reference/develop-app/cursors.md) und [Blockcursor](../../../odbc/reference/develop-app/block-cursors.md).  
  
 Das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut gibt die Anzahl der Zeilen im Rowset an. Wenn das Rowset von abgerufen wird **SQLFetch** überschneidet sich mit dem Ende des Resultsets, **SQLFetch** gibt eine partielle Rowset zurück. D. h. wenn S + R – 1 ist größer als L, wobei S der ersten Zeile des Rowsets abgerufen wird, R ist die Rowsetgröße ist und L ist die letzte im Resultset, klicken Sie dann nur die ersten L – Zeile sind S + 1 Zeilen des Rowsets gültig. Die verbleibenden Zeilen sind leer und sein Status SQL_ROW_NOROW.  
  
 Nach dem **SQLFetch** zurückgibt, die aktuelle Zeile ist die erste Zeile des Rowsets.  
  
 Die in der folgenden Tabelle aufgeführten Regeln beschreiben cursorpositionierung nach einem Aufruf von **SQLFetch**basierend auf den in der zweiten Tabelle in diesem Abschnitt aufgeführten Bedingungen.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|Vor dem start|1|  
|*CurrRowsetStart* \< =  *LastResultRow – RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow – RowsetSize*[1]|Nach dem Ende|  
|Nach dem Ende|Nach dem Ende|  
  
 [1] Wenn zwischen Abrufvorgängen die Rowsetgröße geändert wird, ist dies die Größe des Rowsets, die mit der vorherigen Abruf verwendet wurde.  
  
 [2] Wenn zwischen Abrufvorgängen die Rowsetgröße geändert wird, ist dies die Größe des Rowsets, die mit der neuen Abrufoperation verwendet wurde.  
  
|Notation|Bedeutung|  
|--------------|-------------|  
|Vor dem start|Der Blockcursor wird vor dem Start des Resultsets positioniert. Wenn die erste Zeile des neuen Rowsets vor dem Start des Resultsets, ist **SQLFetch** gibt SQL_NO_DATA zurück.|  
|Nach dem Ende|Die Blockcursor wird hinter das Ende des Resultsets festgelegt. Nach dem Ende des Resultsets, ist die erste Zeile des neuen Rowsets **SQLFetch** gibt SQL_NO_DATA zurück.|  
|*CurrRowsetStart*|Die Anzahl der ersten Zeile im aktuellen Rowset.|  
|*LastResultRow*|Die Anzahl der letzten Zeile im Resultset.|  
|*RowsetSize*|Die Größe des Rowsets.|  
  
 Nehmen wir beispielsweise an ein Resultset hat 100 Zeilen und die Rowsetgröße ist 5. Die folgende Tabelle zeigt das zurückgegebene Rowset und der Rückgabewert Code **SQLFetch** für verschiedene Anfangspositionen.  
  
|Aktuelle rowset|Rückgabecode|Neue Schemarowsets|Anzahl der abgerufenen Zeilen|  
|--------------------|-----------------|----------------|------------------------|  
|Vor dem start|SQL_SUCCESS|1 bis 5|5|  
|1 bis 5|SQL_SUCCESS|6 bis 10|5|  
|52 bis 56|SQL_SUCCESS|57, 61|5|  
|91 bis 95|SQL_SUCCESS|96 bis 100|5|  
|93 auf 97|SQL_SUCCESS|98 bis 100. Zeilen, 4 und 5 den zeilenstatusarray werden auf SQL_ROW_NOROW festgelegt.|3|  
|96 bis 100|SQL_NO_DATA|Keine.|0|  
|99, 100|SQL_NO_DATA|Keine.|0|  
|Nach dem Ende|SQL_NO_DATA|Keine.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Zurückgeben von Daten im gebundenen Spalten  
 Als **SQLFetch** gibt jede Zeile, legt er die Daten für jede gebundene Spalte im Puffer, an diese Spalte gebunden. Wenn keine Spalten gebunden sind, **SQLFetch** keine Daten zurückgibt, aber die Blockcursor vorwärts bewegt. Die Daten können weiterhin mit abgerufen **SQLGetData**. Wenn der Cursor befindet sich eine mehrzeilige Cursor (d. h. SQL_ATTR_ROW_ARRAY_SIZE ist größer als 1), **SQLGetData** kann nur aufgerufen, wenn SQL_GD_BLOCK, wenn zurückgegeben wird **SQLGetInfo** aufgerufen wird und ein  *Infotyp* von SQL_GETDATA_EXTENSIONS. (Weitere Informationen finden Sie unter [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Für jede gebundene Spalte in einer Zeile **SQLFetch** bewirkt Folgendes:  
  
1.  Legt die Längen-/Indikatorpuffers auf SQL_NULL_DATA fest und zur nächsten Spalte fortgesetzt wird, wenn die Daten NULL sind. Wenn die Daten NULL ist, und es keine Längen-/Indikatorpuffers gebunden wurde, **SQLFetch** SQLSTATE 22002 (Indikatorvariable ist erforderlich, jedoch nicht angegeben) für die Zeile zurückgegeben und zur nächsten Zeile geht. Informationen dazu, wie Sie die Adresse eines Längen-/Indikatorpuffers zu bestimmen, finden Sie im "Puffer Adressen" [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Wenn die Daten für die Spalte ungleich NULL ist, **SQLFetch** fährt fort mit Schritt 2 fort.  
  
2.  Wenn das SQL_ATTR_MAX_LENGTH-Anweisungsattribut auf einen Wert ungleich NULL festgelegt ist, und die Spalte, Zeichen- oder Binärdaten darstellen enthält, werden die Daten auf SQL_ATTR_MAX_LENGTH Bytes abgeschnitten.  
  
    > [!NOTE]  
    >  Das SQL_ATTR_MAX_LENGTH-Anweisungsattribut soll den Netzwerkverkehr zu reduzieren. Es ist in der Regel von der Datenquelle implementiert, die die Daten abgeschnitten werden, bevor sie über das Netzwerk zurückgegeben wird. Treiber und Datenquellen werden nicht zu ihrer Unterstützung erforderlich. Aus diesem Grund um zu gewährleisten, dass die Daten auf eine bestimmte Größe abgeschnitten werden, eine Anwendung sollte ein Puffer der Größe und geben Sie die Größe in der *CbValueMax* Argument in **SQLBindCol**.  
  
3.  Konvertiert die Daten in den vom angegebenen Typ *TargetType* in **SQLBindCol**.  
  
4.  Wenn die Daten in einen Datentyp variabler Länge, z. B. Zeichen oder binär, konvertiert wurde **SQLFetch** überprüft, ob die Länge der Daten die Länge des Datenpuffers überschreitet. Die Länge der Zeichendaten (einschließlich der Null-Abschlusszeichen) überschreitet die Länge des Datenpuffers **SQLFetch** schneidet die Daten der Länge des Datenpuffers abzüglich der Länge von einer Null-Abschlusszeichen. Sie beendet Null-dann die Daten. Die Länge der binären Daten überschreitet die Länge des Datenpuffers **SQLFetch** verkürzt sie auf die Länge des Datenpuffers. Die Länge des Datenpuffers wird angegeben, mit *Pufferlänge* in **SQLBindCol**.  
  
     **SQLFetch** nie schneidet Daten in Daten fester Länge Typen konvertiert; es wird immer davon ausgegangen, dass die Länge des Datenpuffers die Größe des Datentyps.  
  
5.  Setzt die konvertierte (und möglicherweise abgeschnitten) Daten im Datenpuffer. Informationen dazu, wie Sie die Adresse des Datenpuffers zu bestimmen, finden Sie im "Puffer Adressen" [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Legt die Länge der Daten in die Längen-/Indikatorpuffers an. Wenn der Indikator Zeiger und den datenlängenzeigern auf den gleichen Puffer festgelegt wurden (wie ein Aufruf **SQLBindCol** ist), die Länge des Puffers für gültige Daten geschrieben und SQL_NULL_DATA wird in den Puffer für NULL-Daten geschrieben. Wenn keine Längen-/Indikatorpuffers gebunden wurde, **SQLFetch** gibt die Länge nicht zurück.  
  
    -   Für Zeichen- oder Binärdaten darstellen ist dies die Länge der Daten nach der Konvertierung und vor dem Abschneiden aufgrund der Datenpuffer zu klein ist. Wenn der Treiber die Länge der Daten nach der Konvertierung nicht ermitteln kann manchmal bei long-Daten der Fall ist, legt die Länge auf SQL_NO_TOTAL fest. Wenn Daten aufgrund der SQL_ATTR_MAX_LENGTH-Anweisungsattribut abgeschnitten wurde, wird der Wert dieses Attributs in der Längen-/Indikatorpuffers anstelle der tatsächlichen Länge eingefügt. Dies ist dieses Attribut ist darauf ausgelegt, Daten auf dem Server vor der Konvertierung, kürzen, damit der Treiber hat keine Möglichkeit zu ermitteln, welche die tatsächliche Länge ist.  
  
    -   Für alle anderen Datentypen ist dies die Länge der Daten nach der Konvertierung; d. h., ist es die Größe des Typs, der die Daten konvertiert wurde.  
  
     Informationen dazu, wie Sie die Adresse eines Längen-/Indikatorpuffers zu bestimmen, finden Sie im "Puffer Adressen" [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Wenn die Daten, während der Konvertierung ohne Verlust von signifikanten Stellen abgeschnitten werden (z. B. die reelle Zahl-1,234 auf die ganze Zahl 1, bei der Konvertierung abgeschnitten ist), **SQLFetch** SQLSTATE 01S07 zurückgibt (Sekundenbruchteile abgeschnitten) und SQL_ SUCCESS_WITH_INFO. Wenn die Daten abgeschnitten werden, da die Länge des Datenpuffers zu klein ist (z. B. die Zeichenfolge "Abcdef" in einem 4-Byte-Puffer abgelegt wird), **SQLFetch** SQLSTATE 01004 (Daten abgeschnitten) und SQL_SUCCESS_WITH_INFO zurückgegeben. Wenn Daten, aufgrund der SQL_ATTR_MAX_LENGTH-Anweisungsattribut abgeschnitten werden **SQLFetch** gibt SQL_SUCCESS zurück, und es wird keine SQLSTATE 01S07 zurückgegeben (Sekundenbruchteile abgeschnitten) oder SQLSTATE 01004 (Daten abgeschnitten). Wenn Daten abgeschnitten werden, während der Konvertierung mit einem Verlust von signifikanten Stellen (z. B., wenn ein SQL_INTEGER-Wert, der größer als 100.000 in eine SQL_C_TINYINT konvertiert wurden), **SQLFetch** gibt SQLSTATE 22003 (numerischen Wert außerhalb des gültigen Bereichs) und SQL_ERROR (wenn die Rowsetgröße 1 ist) oder SQL_SUCCESS_WITH_INFO (wenn die Rowsetgröße größer als 1 ist).  
  
 Den Inhalt der gebundenen Datenpuffer und Längen-/Indikatorpuffers sind nicht definiert, wenn **SQLFetch** oder **SQLFetchScroll** keinen SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgibt.  
  
## <a name="row-status-array"></a>Zeilenstatusarray  
 Die zeilenstatusarray wird verwendet, um den Status der einzelnen Zeilen im Rowset zurückgegeben. Die Adresse dieses Arrays ist mit der SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut festgelegt. Das Array muss wird von der Anwendung zugeordnet und so viele Elemente wie vom Attribut SQL_ATTR_ROW_ARRAY_SIZE-Anweisung angegeben werden. Seine Werte werden festgelegt, indem **SQLFetch**, **SQLFetchScroll**, und **SQLBulkOperations** oder **SQLSetPos** (außer wenn sie aufgerufen wurden Nachdem Sie von der Cursor erstellt wurde **SQLExtendedFetch**). Wenn der Wert des Attributs Anweisung SQL_ATTR_ROW_STATUS_PTR ein null-Zeiger ist, geben diese Funktionen nicht den Zeilenstatus zurück.  
  
 Der Inhalt des Array den Zeilenpuffer-Status ist nicht definiert, wenn **SQLFetch** oder **SQLFetchScroll** keinen SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgibt.  
  
 Die folgenden Werte werden in der zeilenstatusarray zurückgegeben.  
  
|Array-Statuswert Zeile|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|Die Zeile wurde erfolgreich abgerufen und seit dem letzten von diesem Resultset Abruf nicht geändert.|  
|SQL_ROW_SUCCESS_WITH_INFO|Die Zeile wurde erfolgreich abgerufen und seit dem letzten von diesem Resultset Abruf nicht geändert. Allerdings wurde eine Warnung zur Zeile zurückgegeben.|  
|SQL_ROW_ERROR|Fehler beim Abrufen einer Zeile.|  
|SQL_ROW_UPDATED [1], [2] und [3]|Die Zeile wurde erfolgreich abgerufen und geändert hat, seit dem letzten von diesem Resultset Abruf. Wenn die Zeile noch einmal von diesem Resultset abgerufen oder, durch aktualisiert wird **SQLSetPos**, der Status in den neuen Status der Zeile geändert wird.|  
|SQL_ROW_DELETED [3]|Die Zeile wurde seit dem letzten von diesem Resultset Abruf gelöscht.|  
|SQL_ROW_ADDED [4]|Die Zeile eingefügt wurde, indem **SQLBulkOperations**. Wenn die Zeile noch einmal von diesem Resultset abgerufen oder, durch aktualisiert wird **SQLSetPos**, ihr Status wird SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|Das Rowset überlappt, das Ende des Resultsets und, dass, die auf dieses Element des Arrays Status Zeile zugestimmt haben, wurde keine Zeile zurückgegeben.|  
  
 [1] Keyset, gemischte und dynamische Cursor, wenn ein Schlüssel-Wert aktualisiert wird, gilt die Datenzeile gelöscht wurden und eine neue Zeile hinzugefügt.  
  
 [2] einige Treiber können nicht Aktualisierungen an Daten erkennen und aus diesem Grund können dieser Wert zurückgeben. Um zu bestimmen, ob ein Treiber Updates von Zeilen erneut abgerufen erkannt werden kann, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** kann dieser Wert zurückgeben, nur mit gemischt wird er Aufrufe **SQLFetchScroll**. Grund hierfür ist, **SQLFetch** wird über das Resultset vorwärts verschoben, und wenn er exklusiv verwendet wird, nicht erneut Zeilen abzurufen. Da keine Zeilen erneut abgerufen werden, **SQLFetch** erkennt keine Änderungen an zuvor abgerufenen Zeilen. Jedoch wenn **SQLFetchScroll** platziert den Cursor vor einer zuvor Zeilen abgerufen und **SQLFetch** wird verwendet, um diese Zeilen abzurufen, **SQLFetch** erkennen alle Änderungen an die Zeilen.  
  
 [4] zurückgegeben nur von SQLBulkOperations. Nicht festlegen, indem **SQLFetch** oder **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Die Zeilen abgerufen, Puffer  
 Der Puffer abgerufenen Zeilen wird zum Zurückgeben der Anzahl der Zeilen abgerufen, z. B. die Zeilen, die für die keine Daten zurückgegeben wurden, weil ein Fehler aufgetreten, während sie wurden abgerufen werden. Das heißt, ist es die Anzahl der Zeilen, die für die der Wert in der zeilenstatusarray nicht SQL_ROW_NOROW ist. Die Adresse dieses Puffers wird mit der Anweisung SQL_ATTR_ROWS_FETCHED_PTR-Attribut angegeben. Der Puffer wird von der Anwendung zugeordnet. Es wird festgelegt, indem **SQLFetch** und **SQLFetchScroll**. Wenn der Wert des Attributs SQL_ATTR_ROWS_FETCHED_PTR-Anweisung ein null-Zeiger ist, geben diese Funktionen nicht die Anzahl der abgerufenen Zeilen zurück. Eine Anwendung kann zum Bestimmen der Anzahl der aktuellen Zeile im Resultset aufrufen **SQLGetStmtAttr** mit dem SQL_ATTR_ROW_NUMBER-Attribut.  
  
 Der Inhalt des Puffers abgerufenen Zeilen sind nicht definiert, wenn **SQLFetch** oder **SQLFetchScroll** keinen zurückgibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, außer wenn SQL_NO_DATA, in diesem Fall zurückgegeben wird die in den Puffer abgerufenen Zeilen ist auf 0 festgelegt.  
  
### <a name="error-handling"></a>Fehlerbehandlung  
 Fehler und Warnungen können auf einzelne Zeilen oder die gesamte Funktion gelten. Weitere Informationen zu DiagnoseDatensätze, finden Sie unter [Diagnose](../../../odbc/reference/develop-app/diagnostics.md) und [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Fehler und Warnungen für die gesamte Funktion  
 Wenn ein Fehler bezieht sich auf die gesamte Funktion, z. B. SQLSTATE HYT00 (Timeout ist abgelaufen) oder SQLSTATE 24000 (Ungültiger Cursorstatus), **SQLFetch** gibt SQL_ERROR zurück, und die entsprechenden SQLSTATE. Der Inhalt der Rowset-Puffer ist nicht definiert, und die Cursorposition bleibt unverändert.  
  
 Wenn eine Warnung für die gesamte Funktion gilt **SQLFetch** SQL_SUCCESS_WITH_INFO und SQLSTATE anwendbar. Die Status-Einträge für Warnungen, die für die gesamte Funktion gelten werden vor den statusdatensätzen zurückgegeben, die auf einzelne Zeilen angewendet.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Fehler und Warnungen in den einzelnen Zeilen  
 Wenn ein Fehler (z. B. SQLSTATE 22012 (Division durch 0 (null))) oder eine Warnung (z. B. SQLSTATE 01004 (Daten wurden abgeschnitten.)) für eine einzelne Zeile gilt **SQLFetch**bewirkt Folgendes:  
  
-   Legt das entsprechende Element des Arrays Status Zeile, SQL_ROW_ERROR auf Fehler oder SQL_ROW_SUCCESS_WITH_INFO für Warnungen fest.  
  
-   Fügt 0 (null) oder mehrere Statusdatensätze, die für den Fehler oder die Warnung SQLSTATEs enthalten.  
  
-   Legt die Zeilen- und Zahlenfelder in den statusdatensätzen fest. Wenn **SQLFetch** diverse Zeile oder Spalte kann nicht bestimmt werden. es legt diese Anzahl auf SQL_ROW_NUMBER_UNKNOWN oder SQL_COLUMN_NUMBER_UNKNOWN, bzw. Wenn der Status-Datensatz nicht für eine bestimmte Spalte gelten **SQLFetch** legt die Nummer der Spalte auf SQL_NO_COLUMN_NUMBER fest.  
  
 **SQLFetch** weiterhin das Abrufen von Zeilen, bis sie alle Zeilen im Rowset abgerufen hat. Es gibt SQL_SUCCESS_WITH_INFO zurück, es sei denn, die Fehler in jeder Zeile des Rowsets (nicht einschließlich Zeilen mit dem Status SQL_ROW_NOROW), wird in diesem Fall wird SQL_ERROR zurückgegeben. Insbesondere wenn die Rowsetgröße 1 und ein Fehler auftritt, in dieser Zeile **SQLFetch** gibt SQL_ERROR zurück.  
  
 **SQLFetch** die statusdatensätzen in Zeile Nummer Reihenfolge zurückgegeben. Wird zurückgegeben, also alle Statusdatensätze für unbekannte Zeilen (sofern vorhanden); als Nächstes alle Statusdatensätze für die erste Zeile (sofern vorhanden) zurückgegeben, und gibt dann alle Statusdatensätze für die zweite Zeile (sofern vorhanden) und So weiter zurück. Die Statusdatensätze für jede Zeile werden gemäß den normalen Regeln für die Anordnung von statusdatensätzen sortiert; Weitere Informationen finden Sie unter "Sequenz von Statusdatensätzen" in [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Deskriptoren und SQLFetch  
 In den folgenden Abschnitten wird beschrieben, wie **SQLFetch** interagiert mit Deskriptoren.  
  
#### <a name="argument-mappings"></a>Arguments-Zuordnungen  
 Der Treiber keine deskriptorfelder, die anhand der Argumente von fest **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Andere Deskriptorfelder  
 Die folgenden deskriptorfelder werden verwendet, indem **SQLFetch**.  
  
|Deskriptorfeld|"DESC".|Feld|Festgelegt durch|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|Header|SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|Header|SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|Header|SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut|  
|SQL_DESC_BIND_TYPE|ARD|Header|SQL_ATTR_ROW_BIND_TYPE-Anweisungsattribut|  
|SQL_DESC_COUNT|ARD|Header|*ColumnNumber* Argument **SQLBindCol**|  
|SQL_DESC_DATA_PTR|ARD|Datensätze|*TargetValuePtr* Argument **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|ARD|Datensätze|*StrLen_or_IndPtr* Argument in **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|ARD|Datensätze|*Pufferlänge* Argument in **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|Datensätze|*StrLen_or_IndPtr* Argument in **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|Header|SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut|  
|SQL_DESC_TYPE|ARD|Datensätze|*TargetType* Argument in **SQLBindCol**|  
  
 Alle deskriptorfelder können auch festgelegt werden, über **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Länge und Indikator Puffer trennen  
 Ein einzelner Puffer oder zwei separate Puffern, die zum Speichern Werte für Länge und der Indikator verwendet werden können, können Anwendungen binden. Wenn eine Anwendung ruft **SQLBindCol**, der Treiber setzt die SQL_DESC_OCTET_LENGTH_PTR und SQL_DESC_INDICATOR_PTR Felder von der ARD in die gleiche Adresse an, der übergeben wird, in der *StrLen_or_IndPtr* Argument. Wenn eine Anwendung ruft **SQLSetDescField** oder **SQLSetDescRec**, sie kann diese zwei Felder auf unterschiedlichen Adressen festgelegt.  
  
 **SQLFetch** bestimmt, ob die Anwendung separate Länge und der Indikator Puffer angegeben wurde. In diesem Fall, wenn die Daten nicht NULL ist, **SQLFetch** legt die Indikatorpuffers auf 0 fest und gibt die Länge des Puffers Länge zurück. Wenn die Daten NULL ist, werden **SQLFetch** die Indikatorpuffers auf SQL_NULL_DATA festgelegt und den Länge Puffer nicht geändert.  
  
### <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), und [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLDescribeCol-Funktion](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Schließen den Cursor in die Anweisung|[SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Abrufen des Teils oder aller eine Spalte mit Daten|[SQLGetData-Funktion](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Zurückgeben der Anzahl der Ergebnis Resultsetspalten|[SQLNumResultCols-Funktion](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Vorbereiten einer Anweisung für die Ausführung|[SQLPrepare-Funktion](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
