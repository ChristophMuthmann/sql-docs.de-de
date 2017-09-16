---
title: SQLFetchScroll-Funktion | Microsoft Docs
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
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79224469fe1e6e4f0840eceb394b30cec63fcd2a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLFetchScroll** angegebene Rowset von Daten aus dem Resultset abruft, und gibt Daten für alle gebundenen Spalten zurück. Rowsets können eine absolute oder relative Position oder durch Lesezeichen angegeben werden.  
  
 Bei der Arbeit mit einem ODBC 2.x-Treiber ordnet der Treiber-Manager diese Funktion **SQLExtendedFetch**. Weitere Informationen finden Sie unter [Ersatz-Zuordnungsfunktionen für Backward Compatibility Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *FetchOrientation*  
 [Eingabe]  
  
 Der Typ des Abrufs:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Weitere Informationen finden Sie unter "Positionierung des Cursors" im Abschnitt "Kommentare".  
  
 *FetchOffset*  
 [Eingabe]  
  
 Die Nummer der Zeile abgerufen. Die Auslegung dieses Arguments hängt vom Wert von der *FetchOrientation* Argument. Weitere Informationen finden Sie unter "Positionierung des Cursors" im Abschnitt "Kommentare".  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLFetchScroll** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einer HandleType SQL_HANDLE_STMT auf, und ein Handle StatementHandle. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLFetchScroll** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben. Wenn es sich bei Auftreten eines Fehlers in einer einzelnen Spalte **SQLGetDiagField** kann mit einem DiagIdentifier SQL_DIAG_COLUMN_NUMBER um die Spalte zu bestimmen, der Fehler aufgetreten, andernfalls false ist, aufgerufen werden und **SQLGetDiagField** aufgerufen werden kann mit einem DiagIdentifier SQL_DIAG_ROW_NUMBER Bestimmen der Zeile, die diese Spalte enthält.  
  
 Für alle diese SQLSTATEs, der SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurück (mit Ausnahme der 01xxx SQLSTATEs) zurückgeben kann, wird SQL_SUCCESS_WITH_INFO zurückgegeben, wenn ein Fehler, auf ein oder mehrere, aber nicht alle Zeilen einer Einfügung mehrerer Zeilen Operation auftritt, und SQL_ERROR zurückgegeben wird, wenn es sich bei Auftreten eines Fehlers in einer einzeiliges-Vorgang.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL führte Zeichenfolgen- oder Binärdaten, die für eine Spalte zurückgegeben. Falls es sich um einen Zeichenfolgenwert handelt, wurde es rechts abgeschnitten.|  
|01 S 01|Fehler in Zeile|Fehler beim Abrufen von einer oder mehreren Zeilen.<br /><br /> (Wenn diese SQLSTATE zurückgegeben, wenn eine ODBC 3.*.x* Anwendung arbeitet mit einer ODBC 2.*.x* -Treiber verwenden, kann es ignoriert werden.)|  
|01S06|Es wurde versucht abzurufen, bevor das Resultset das erste Rowset zurückgab|Das angeforderte Rowset überlappenden am Anfang der Resultsets, die beim FetchOrientation SQL_FETCH_PRIOR wurde, die aktuelle Position länger als die erste Zeile wurde und die Anzahl der aktuellen Zeile kleiner als oder gleich der Rowsetgröße ist.<br /><br /> Das angeforderte Rowset überlappenden am Anfang der Resultsets, die beim FetchOrientation SQL_FETCH_PRIOR wurde, die aktuelle Position hinter dem Ende des Resultsets ausgewählt wurde und die Rowsetgröße größer war als die Größe des Resultsets.<br /><br /> Das angeforderte Rowset überlappenden am Anfang der Resultsets, die beim FetchOrientation SQL_FETCH_RELATIVE wurde FetchOffset negativ war und den absoluten Wert des FetchOffset kleiner oder gleich der Rowsetgröße war.<br /><br /> Das angeforderte Rowset überlappenden am Anfang das Resultset, wenn der Absolute Wert des FetchOffset größer war als die Größe des Resultsets FetchOffset negativ war und FetchOrientation SQL_FETCH_ABSOLUTE war, aber kleiner oder gleich der Größe des Rowsets.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S07|Teilbereiche wurden abgeschnitten.|Für eine Spalte zurückgegebenen Daten wurden abgeschnitten. Für numerische Datentypen und wurde die Nachkommastellen der Zahl gekürzt. Für die Zeit, Zeitstempel und Interval-Datentypen, die eine Komponente enthält wurde der Bruchteil der Zeit abgeschnitten.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert einer Spalte im Resultset konnte nicht an der angegebenen Datentyp konvertiert werden *TargetType* in **SQLBindCol**.<br /><br /> Spalte 0 wurde mit einem Datentyp von SQL_C_BOOKMARK gebunden, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde.<br /><br /> Spalte 0 wurde mit einem Datentyp von SQL_C_VARBOOKMARK gebunden, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE nicht festgelegt wurde.|  
|07009|Ungültiger Deskriptorindex|Der Treiber wurde von einer ODBC 2.*.x* Treiber, der nicht unterstützt **SQLExtendedFetch**, und eine Spaltennummer in der Bindung für eine Spalte angegeben wurde, 0.<br /><br /> Spalte 0 gebunden wurde, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22001|Zeichenfolgedaten wurden rechts abgeschnitten|Ein variabler Länge Lesezeichen für eine Spalte zurückgegeben wurde abgeschnitten.|  
|22002|Anzeigevariable erforderlich, aber nicht angegeben|NULL wurde abgerufene Daten in eine Spalte, deren *StrLen_or_IndPtr* festlegen, indem **SQLBindCol** (oder SQL_DESC_INDICATOR_PTR festlegen, indem **SQLSetDescField** oder ** SQLSetDescRec**) wurde ein null-Zeiger.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Den numerischen Wert (als numerisch oder Zeichenfolge) für eine oder mehrere gebundene Spalten zurückgeben würde die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird vorliegt.<br /><br /> Weitere Informationen finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) in [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Ungültiges Datetime-format|Eine Zeichenspalte im Resultset an ein Datum, Uhrzeit oder C-zeitstempelstruktur gebunden wurde, und ein Wert in der Spalte wurde, bzw. ein ungültiges Datum, Uhrzeit oder Zeitstempel.|  
|22012|Division durch 0 (null)|Ein Wert aus einem arithmetischen Ausdruck wurde von 0 (null) zurückgegeben Division geführt hat.|  
|22015|Überlauf der Intervall-Feld.|Intervalltyp C aus einer genauen numerischen oder Intervall SQL-Typ zuzuweisen, hat einen Datenverlust von signifikanten Stellen im Feld führende verursacht.<br /><br /> Beim Abrufen von Daten in ein C-Intervalltyp ist keine Darstellung des Werts des SQL-Datentyps in den Intervalltyp C.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Eine Zeichenspalte im Resultset an einen Zeichenpuffer C gebunden wurde, und die Spalte enthalten, ein Zeichen für die es keine Darstellung des Zeichensatzes des Puffers war.<br /><br /> Der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte wurde einem Zeichendatentyp; und kein Wert in der Spalte wurde ein gültiger Literal des gebundenen C-Typs.|  
|24000|Ungültiger Cursorstatus|Die *StatementHandle* in einem ausgeführten Zustand wurde jedoch kein Resultset zugeordnet wurde die *StatementHandle*.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion, in der der Abruf ausgeführt wurde, wurde beendet, um Deadlocks zu vermeiden.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLFetchScroll** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) dem angegebenen *StatementHandle* war nicht in einem ausgeführten Zustand. Die Funktion wurde aufgerufen, ohne zunächst **SQLExecDirect**, **SQLExecute** oder eine Katalogfunktion auf.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) **SQLFetch** wurde aufgerufen, die *StatementHandle* nach **SQLExtendedFetch** aufgerufen wurde und bevor **SQLFreeStmt** mit den SQL_ CLOSE-Option wurde aufgerufen.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Das SQL_ATTR_USE_BOOKMARK-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und Spalte 0 wurde auf einen Puffer, dessen Länge nicht gleich die maximale Länge für das Lesezeichen für dieses Resultset war, gebunden. (Diese Länge finden Sie im Feld SQL_DESC_OCTET_LENGTH vom IRD und abgerufen werden kann, durch den Aufruf **SQLDescribeCol**, **SQLColAttribute**, oder **SQLGetDescField**.)|  
|HY106|Der Fetchtyp außerhalb des gültigen Bereichs|DM) für das Argument FetchOrientation angegebene Wert war ungültig.<br /><br /> (DM) das Argument FetchOrientation war sql_fetch_bookmark auf, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.<br /><br /> Der Wert des Attributs SQL_ATTR_CURSOR_TYPE-Anweisung wurde SQL_CURSOR_FORWARD_ONLY und der Wert des Arguments FetchOrientation war nicht SQL_FETCH_NEXT.<br /><br /> Der Wert des Attributs SQL_ATTR_CURSOR_SCROLLABLE-Anweisung wurde SQL_NONSCROLLABLE und den Wert des Arguments FetchOrientation war nicht SQL_FETCH_NEXT.|  
|HY107|Zeilenwert außerhalb des gültigen Bereichs|Mit dem SQL_ATTR_CURSOR_TYPE-Attribut-Anweisung angegebene Wert war SQL_CURSOR_KEYSET_DRIVEN, jedoch mit SQL_ATTR_KEYSET_SIZE-Anweisungsattribut angegebene Wert größer als 0 und kleiner als der Wert, der mit der SQL_ATTR_ROW_ARRAY_ angegeben Anweisungsattribut Größe.|  
|HY111|Ungültige lesezeichenwerts|Das Argument FetchOrientation war sql_fetch_bookmark auf, und das Lesezeichen, um mit dem Wert in das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut auf war ungültig oder wurde ein null-Zeiger.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht die Konvertierung angegeben, durch die Kombination der *TargetType* in **SQLBindCol** und dem SQL-Datentyp der entsprechenden Spalte.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle, die das angeforderte Resultset zurückgegeben. Das Timeout wird durch SQLSetStmtAttr SQL_ATTR_QUERY_TIMEOUT festgelegt.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLFetchScroll** gibt eine angegebene Rowset aus dem Resultset zurück. Rowsets können anhand der absolute oder relative Position oder durch Lesezeichen angegeben werden. **SQLFetchScroll** kann nur verwendet werden, während ein Resultset vorhanden ist aufgerufen werden – d. h. nach einem Aufruf, der ein Resultset erstellt und vor dem Cursor Failover, das Resultset geschlossen wird. Wenn keine Spalten gebunden sind, werden die Daten in diesen Spalten zurückgegeben. Wenn die Anwendung einen Zeiger auf ein zeilenstatusarray oder auf einen Puffer, in dem die Anzahl der Zeilen abgerufen, zurückgegeben angegeben wurde **SQLFetchScroll** gibt diese Informationen auch zurück. Aufrufe von **SQLFetchScroll** können durch Aufrufe von gemischt werden **SQLFetch** jedoch durch Aufrufe von kombiniert werden, kann nicht **SQLExtendedFetch**.  
  
 Weitere Informationen finden Sie unter [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md) und [bildlauffähigen Cursor verwenden](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Positionieren den Cursor  
 Wenn das Resultset erstellt wird, befindet sich der Cursor vor dem Start des Resultsets. **SQLFetchScroll** der Cursor Block anhand der Werte von der *FetchOrientation* und *FetchOffset* Argumente wie in der folgenden Tabelle gezeigt. Im nächsten Abschnitt werden die genauen Regeln zur Bestimmung der am Anfang des neuen Rowsets angezeigt.  
  
|FetchOrientation|Bedeutung|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Zurückgeben des nächsten Rowsets. Dies entspricht dem Aufruf **SQLFetch**.<br /><br /> **SQLFetchScroll** ignoriert den Wert der *FetchOffset*.|  
|SQL_FETCH_PRIOR|Geben Sie das vorherige Rowset zurück.<br /><br /> **SQLFetchScroll** ignoriert den Wert der *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Zurückgeben des Rowsets *FetchOffset* vom Beginn des aktuellen Rowsets.|  
|SQL_FETCH_ABSOLUTE|Zurückgeben des Rowsets ab Zeile *FetchOffset*.|  
|SQL_FETCH_FIRST|Geben Sie im Resultset das erste Rowset zurück.<br /><br /> **SQLFetchScroll** ignoriert den Wert der *FetchOffset*.|  
|SQL_FETCH_LAST|Geben Sie in das Resultset auf die letzte vollständige Rowset zurück.<br /><br /> **SQLFetchScroll** ignoriert den Wert der *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Zurückgegeben Sie das Rowset FetchOffset Zeilen angegeben, die durch das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut Lesezeichen.|  
  
 Treiber sind nicht erforderlich, um alle Fetch-Ausrichtungen unterstützen. Ruft die Anwendung **SQLGetInfo** mit dem Datentyp Informationen SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 oder SQL_STATIC_CURSOR_ATTRIBUTES1 (je nach Typ des Cursors) um zu bestimmen, welche Fetch Ausrichtungen werden vom Treiber unterstützt. Die Anwendung sollte den SQL_CA1_NEXT, SQL_CA1_RELATIVE SQL_CA1_ABSOLUTE und WQL_CA1_BOOKMARK Bitmasken in diesen Typen von Informationen betrachten. Darüber hinaus, wenn der Cursor, nur vorwärts befindet und FetchOrientation nicht SQL_FETCH_NEXT, **SQLFetchScroll** SQLSTATE HY106 zurückgibt (Fetchtyp außerhalb des gültigen Bereichs).  
  
 Das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut gibt die Anzahl der Zeilen im Rowset an. Wenn das Rowset von abgerufen wird **SQLFetchScroll** überschneidet sich mit dem Ende des Resultsets, **SQLFetchScroll** gibt eine partielle Rowset zurück. D. h. wenn S + R – 1 ist größer als L, wobei S der ersten Zeile des Rowsets abgerufen wird, R ist die Rowsetgröße ist und L ist die letzte im Resultset, klicken Sie dann nur die ersten L – Zeile sind S + 1 Zeilen des Rowsets gültig. Die verbleibenden Zeilen sind leer und sein Status SQL_ROW_NOROW.  
  
 Nach dem **SQLFetchScroll** zurückgibt, die aktuelle Zeile ist die erste Zeile des Rowsets.  
  
## <a name="cursor-positioning-rules"></a>Cursorpositionierungsaufruf Regeln  
 In den folgenden Abschnitten werden die genauen Regeln für jeden Wert von FetchOrientation beschrieben. Diese Regeln verwenden, die folgende Notation wird.  
  
|Notation|Bedeutung|  
|--------------|-------------|  
|*Vor dem start*|Der Blockcursor wird vor dem Start des Resultsets positioniert. Wenn die erste Zeile des neuen Rowsets vor dem Start des Resultsets, ist **SQLFetchScroll** gibt SQL_NO_DATA zurück.|  
|*Nach dem Ende*|Die Blockcursor wird hinter das Ende des Resultsets festgelegt. Nach dem Ende des Resultsets, ist die erste Zeile des neuen Rowsets **SQLFetchScroll** gibt SQL_NO_DATA zurück.|  
|*CurrRowsetStart*|Die Anzahl der ersten Zeile im aktuellen Rowset.|  
|*LastResultRow*|Die Anzahl der letzten Zeile im Resultset.|  
|*RowsetSize*|Die Größe des Rowsets.|  
|*FetchOffset*|Der Wert, der die *FetchOffset* Argument.|  
|*BookmarkRow*|Die Zeile, die das Lesezeichen, das das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut gemäß entspricht.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*Vor dem start*|1|  
|*CurrRowsetStart + RowsetSize*[1] * \<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*Nach dem Ende*|  
|*Nach dem Ende*|*Nach dem Ende*|  
  
 [1] Wenn seit dem letzten Aufruf von Zeilen abzurufen, die Rowsetgröße geändert wurde, ist dies die Größe des Rowsets, die mit dem letzten Aufruf verwendet wurde.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*Vor dem start*|*Vor dem start*|  
|*CurrRowsetStart = 1*|*Vor dem start*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2] '.</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*Nach dem Ende und LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Nach dem Ende und LastResultRow > = RowsetSize* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2] '.</sup>|  
  
 [1] **SQLFetchScroll** SQLSTATE 01S06 zurückgibt (versucht abzurufen, bevor das Resultset das erste Rowset zurückgab) und SQL_SUCCESS_WITH_INFO zurückgegeben.  
  
 [2] Wenn seit dem letzten Aufruf von Zeilen abzurufen, die Rowsetgröße geändert wurde, ist dies die neue Rowsetgröße.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*(Vor dem start und FetchOffset > 0) ODER (nach dem Ende und FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart und FetchOffset < = 0*|*Vor dem start*|  
|*CurrRowsetStart = 1 und FetchOffset < 0*|*Vor dem start*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 und &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Vor dem start*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 und &#124; FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Nach dem Ende*|  
|*Nach dem Ende und FetchOffset > = 0*|*Nach dem Ende*|  
  
 [1] ***SQLFetchScroll*** gibt das gleiche Rowset zurück, als wäre es mit FetchOrientation SQL_FETCH_ABSOLUTE festgelegt aufgerufen wurde. Weitere Informationen finden Sie im Abschnitt "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** SQLSTATE 01S06 zurückgibt (versucht abzurufen, bevor das Resultset das erste Rowset zurückgab) und SQL_SUCCESS_WITH_INFO zurückgegeben.  
  
 [3] Wenn seit dem letzten Aufruf von Zeilen abzurufen, die Rowsetgröße geändert wurde, ist dies die neue Rowsetgröße.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*FetchOffset < 0 und &#124; FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 und &#124; FetchOffset &#124; > LastResultRow und &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Vor dem start*|  
|*FetchOffset < 0 und &#124; FetchOffset &#124; > LastResultRow und &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*Vor dem start*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Nach dem Ende*|  
  
 [1] **SQLFetchScroll** SQLSTATE 01S06 zurückgibt (versucht abzurufen, bevor das Resultset das erste Rowset zurückgab) und SQL_SUCCESS_WITH_INFO zurückgegeben.  
  
 [2] Wenn seit dem letzten Aufruf von Zeilen abzurufen, die Rowsetgröße geändert wurde, ist dies die neue Rowsetgröße.  
  
 Ein absoluter Abruf für einen dynamischen Cursor ausgeführt kann nicht das erforderliche Ergebnis bereitstellen, da Zeilenpositionen in einem dynamischen Cursor nicht festgelegt werden. Ein solcher Vorgang entspricht zuerst gefolgt von einem Fetch relative Fetch; Es ist keiner atomaren Operation, wie ein absoluter Abruf in einem statischen Cursor ist.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*Alle*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] Wenn seit dem letzten Aufruf von Zeilen abzurufen, die Rowsetgröße geändert wurde, ist dies die neue Rowsetgröße.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 Die folgenden Regeln gelten.  
  
|Bedingung|Erste Zeile der neuen Rowsets|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Vor dem start*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Nach dem Ende*|  
  
 Weitere Informationen zu Lesezeichen finden Sie unter [Lesezeichen (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Auswirkungen der gelöschten, hinzugefügt und Fehlerzeilen auf Bewegung des Cursors  
 Statische und keysetgesteuerte Cursor erkennen manchmal Zeilen hinzugefügt, um das Ergebnis festgelegt, und Entfernen von Zeilen, die aus dem Resultset gelöscht. Durch Aufrufen von **SQLGetInfo** mit dem SQL_STATIC_CURSOR_ATTRIBUTES2 und SQL_KEYSET_CURSOR_ATTRIBUTES2 Optionen und die SQL_CA2_SENSITIVITY_ADDITIONS SQL_CA2_SENSITIVITY_DELETIONS und SQL_CA2_SENSITIVITY_ ansehen UPDATES Bitmasken, eine Anwendung bestimmt, ob hierzu die Cursor, die durch einen bestimmten Treiber implementiert. In den folgenden Abschnitten beschrieben Treiber, die gelöschte Zeilen zu erkennen und entfernen können, die Auswirkungen dieses Verhaltens. Treiber, die gelöschte Zeilen erkennen können, aber nicht entfernt werden, Löschvorgänge wirken sich nicht auf Cursor Bewegungen und in den folgenden Abschnitten werden nicht angewendet.  
  
 Wenn der Cursor Zeilen zum Resultset hinzugefügt erkennt oder Zeilen aus dem Resultset gelöscht entfernt, wird es angezeigt, als ob er diese Änderungen erkennt nur dann, wenn es Daten abruft. Dies schließt die Groß-/Kleinschreibung bei **SQLFetchScroll** mit FetchOrientation SQL_FETCH_RELATIVE und FetchOffset auf 0 festgelegt wird, auf das gleiche Rowset erneut abrufen festgelegt aufgerufen wird, jedoch nicht die Groß-/Kleinschreibung Wenn SQLSetPos mit fOption auf SQL_ aufgerufen wird AKTUALISIEREN. Im letzteren Fall werden die Daten in den Puffern Rowset aktualisiert, aber nicht erneut abgerufen und gelöschte Zeilen werden nicht aus dem Resultset entfernt. Daher werden, wenn eine Zeile gelöscht oder das aktuelle Rowset eingefügt, in der Cursor nicht die Rowset-Puffer geändert. Stattdessen erkannt die Änderung, wenn alle Rowset abruft zuvor enthalten die gelöschte Zeile oder enthält jetzt die eingefügte Zeile.  
  
 Beispiel:  
  
```  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 Wenn **SQLFetchScroll** gibt ein neues Rowset, das eine Position relativ zum aktuellen Rowset wurde – FetchOrientation ist SQL_FETCH_NEXT, SQL_FETCH_PRIOR oder SQL_FETCH_RELATIVE – Änderungen auf das aktuelle Rowset sind nicht enthalten Wenn die Anfangsposition des neuen Rowsets zu berechnen. Allerdings ist diese Änderung außerhalb der aktuellen Rowset enthalten, ist er kann sie ermitteln. Darüber hinaus, wenn **SQLFetchScroll** gibt ein neues Rowset, das eine Position, die unabhängig von der das aktuelle Rowset wurde – FetchOrientation also SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE oder SQL_FETCH_BOOKMARK – es enthält alle Änderungen sie kann ermitteln, selbst wenn sie das aktuelle Rowset enthält.  
  
 Beim bestimmen, ob die neu hinzugefügte Zeilen innerhalb oder außerhalb der aktuellen Rowsets sind, gilt eine partielle Rowset auf die letzte gültige Zeile enden; d. h. die letzte Zeile die Zeilenstatus nicht SQL_ROW_NOROW ist. Nehmen wir beispielsweise an der Cursor ist der neu hinzugefügte Zeilen erkennen kann, das aktuelle Rowset ist eine partielle Rowset, die Anwendung fügt neue Zeilen und der Cursor fügt diese Zeilen bis zum Ende des Resultsets. Wenn die Anwendung aufruft, **SQLFetchScroll** mit FetchOrientation festgelegt SQL_FETCH_NEXT, **SQLFetchScroll** gibt das Rowset, beginnend mit der ersten neu hinzugefügte Zeile zurück.  
  
 Nehmen wir beispielsweise an das aktuelle Rowset besteht aus Zeilen 21 bis 30, die Rowsetgröße ist 10, der Cursor entfernt Zeilen aus dem Resultset gelöscht und der Cursor erkennt Zeilen zum Resultset hinzugefügt. Die folgende Tabelle zeigt die Zeilen **SQLFetchScroll** in verschiedenen Situationen zurückgegeben.  
  
|Ändern|FETCH-Typ|FetchOffset|Neue Schemarowsets [1]|  
|------------|----------------|-----------------|---------------------|  
|Löschen der Zeile 21|NEXT|0|31 bis 40|  
|Löschen der Zeile 31|NEXT|0|32 bis 41|  
|Einfügen einer Zeile zwischen Zeilen 21 und 22|NEXT|0|31 bis 40|  
|Einfügen einer Zeile zwischen Zeilen 30 und 31|NEXT|0|Eingefügte Zeile, 31 bis 39|  
|Löschen der Zeile 21|PRIOR|0|11 bis 20|  
|Löschen der Zeile 20|PRIOR|0|10 bis 19|  
|Einfügen einer Zeile zwischen Zeilen 21 und 22|PRIOR|0|11 bis 20|  
|Einfügen einer Zeile zwischen Zeilen 20 und 21|PRIOR|0|eingefügte Zeile 12 bis 20|  
|Löschen der Zeile 21|RELATIVE|0|22 bis 31<sup>[2]</sup>|  
|Löschen der Zeile 21|RELATIVE|1|22 bis 31|  
|Einfügen einer Zeile zwischen Zeilen 21 und 22|RELATIVE|0|21, eingefügte Zeile, 22 bis 29|  
|Einfügen einer Zeile zwischen Zeilen 21 und 22|RELATIVE|1|22 bis 31|  
|Löschen der Zeile 21|ABSOLUTE|21|22 bis 31<sup>[2]</sup>|  
|Löschen der Zeile 22|ABSOLUTE|21|21, 23 und 31 liegen|  
|Einfügen einer Zeile zwischen Zeilen 21 und 22|ABSOLUTE|22|Eingefügte Zeile, 22 bis 29|  
  
 [1] diese Spalte verwendet die Zeilennummern, bevor Zeilen eingefügt oder gelöscht wurden.  
  
 [2] In diesem Fall versucht der Cursor ab Zeile 21 Zeilen zurückgeben. Da Zeile 21 gelöscht wurde, ist die erste Zeile zurückgegebene Zeile 22.  
  
 Fehlerzeilen (d. h. Zeilen mit dem Status des SQL_ROW_ERROR) wirken sich nicht auf Bewegung des Cursors aus. Wenn das aktuelle Rowset mit Zeile 11 und den Status der beginnt, ist Zeile 11 SQL_ROW_ERROR, Aufrufen von **SQLFetchScroll** mit FetchOrientation SQL_FETCH_RELATIVE und FetchOffset festgelegt auf 5 festgelegt beginnend mit Zeile 16, Rowset zurückgegeben Ebenso wie dies der Fall wäre, wenn der Status für Zeile 11 SQL_SUCCESS wurde.  
  
## <a name="returning-data-in-bound-columns"></a>Zurückgeben von Daten im gebundenen Spalten  
 **SQLFetchScroll** Daten in gebundenen Spalten zurückgegeben, auf die gleiche Weise wie **SQLFetch**. Weitere Informationen finden Sie unter "Zurückgeben von Daten im gebundenen Spalten" in [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Wenn keine Spalten gebunden sind, **SQLFetchScroll** keine Daten zurückgibt, jedoch werden die Blockcursor an die angegebene Position verschoben. Gibt an, ob Daten von ungebundenen Spalten eines Cursors Block mit abgerufen werden können **SQLGetData** hängt vom Treiber. Diese Funktion wird unterstützt, wenn ein Aufruf von **SQLGetInfo** das bit für den Informationstyp SQL_GETDATA_EXTENSIONS SQL_GD_BLOCK zurückgibt.  
  
## <a name="buffer-addresses"></a>Puffer-Adressen  
 **SQLFetchScroll** die gleiche Formel verwendet, um zu bestimmen, die Adresse der Daten und Längenindikator/Puffer als **SQLFetch**. Weitere Informationen finden Sie im "Puffer Adressen" [SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Zeilenstatusarray  
 **SQLFetchScroll** legt die Werte in der zeilenstatusarray auf die gleiche Weise wie SQLFetch fest. Weitere Informationen finden Sie unter "Zeilenstatusarray" in [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Die Zeilen abgerufen, Puffer  
 **SQLFetchScroll** gibt die Anzahl der Zeilen im Puffer abgerufenen Zeilen abgerufen, auf die gleiche Weise wie **SQLFetch**. Weitere Informationen finden Sie unter "Zeilen abgerufen Puffer" im [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn eine Anwendung ruft **SQLFetchScroll** in einem ODBC 3.x-Treiber ruft der Treiber-Manager **SQLFetchScroll** im Treiber. Wenn eine Anwendung ruft **SQLFetchScroll** in einem ODBC 2.x-Treiber ruft der Treiber-Manager SQLExtendedFetch im Treiber. Da **SQLFetchScroll** und SQLExtendedFetch Behandeln von Fehlern in eine etwas andere Art und Weise, sieht die Anwendung geringfügig Fehlerverhalten beim Aufrufen von **SQLFetchScroll** in ODBC 2.x und ODBC 3.x-Treiber.  
  
 **SQLFetchScroll** Fehler und Warnungen zurückgegeben, auf die gleiche Weise wie **SQLFetch**; Weitere Informationen finden Sie unter "Fehlerbehandlung" in **SQLFetch**. **SQLExtendedFetch** gibt Fehler zurück, auf die gleiche Weise wie **SQLFetch**, mit folgenden Ausnahmen:  
  
 Beim Auftreten einer Warnung, die für eine bestimmte Zeile im Rowset gilt, legt SQLExtendedFetch den zugehörigen Eintrag in der zeilenstatusarray auf SQL_ROW_SUCCESS nicht SQL_ROW_SUCCESS_WITH_INFO fest.  
  
 Bei Fehlern in jeder Zeile im Rowset gibt SQLExtendedFetch SQL_SUCCESS_WITH_INFO nicht SQL_ERROR zurück.  
  
 In jeder Gruppe von statusdatensätzen, die auf eine einzelne Zeile angewendet wird, muss der erste Status Datensatz SQLExtendedFetch zurückgegebenes SQLSTATE 01 s 01 enthalten (Fehler in Zeile); **SQLFetchScroll** keinen SQLSTATE zurückgibt. Wenn SQLExtendedFetch zusätzliche SQLSTATEs zurückgeben kann, muss sie weiterhin SQLSTATE zurückgeben.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll und vollständige Parallelität  
 Wenn ein Cursor durch vollständige Parallelität verwendet –, also das SQL_ATTR_CONCURRENCY-Anweisungsattribut den Wert SQL_CONCUR_VALUES oder SQL_CONCUR_ROWVER hat – **SQLFetchScroll** aktualisiert die vollständige Parallelität-Werte, die durch die Daten verwendet wird die Quelle zu ermitteln, ob eine Zeile geändert wurde. Dies geschieht bei jedem **SQLFetchScroll** ein neues Rowsets, einschließlich dann, wenn es das aktuelle Rowset refetches abruft. (Es heißt mit FetchOrientation SQL_FETCH_RELATIVE und FetchOffset festlegen auf 0 festgelegt.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll und ODBC 2.x-Treiber  
 Wenn eine Anwendung ruft **SQLFetchScroll** in einem ODBC 2.x-Treiber ordnet der Treiber-Manager diesen Aufruf an **SQLExtendedFetch**. Übergibt die folgenden Werte für die Argumente der **SQLExtendedFetch**.  
  
|SQLExtendedFetch-argument|Wert|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle in **SQLFetchScroll**.|  
|FetchOrientation|FetchOrientation in **SQLFetchScroll**.|  
|FetchOffset|Wenn FetchOrientation nicht SQL_FETCH_BOOKMARK, den Wert der FetchOffset-Argument in ist **SQLFetchScroll** verwendet wird.<br /><br /> Wenn FetchOrientation SQL_FETCH_BOOKMARK ist, wird bei der Adresse, die durch das SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisungsattribut angegebene gespeicherte Wert verwendet.|  
|RowCountPtr|Die Adresse, die durch das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut angegeben wird.|  
|RowStatusArray|Die Adresse, die durch das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR angegeben.|  
  
 Weitere Informationen finden Sie unter [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Deskriptoren und SQLFetchScroll  
 **SQLFetchScroll** interagiert mit Deskriptoren auf die gleiche Weise wie **SQLFetch**. Weitere Informationen finden Sie im Abschnitt "Deskriptoren und SQLFetchScroll" [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [spaltenbezogene Bindungen](../../../odbc/reference/develop-app/column-wise-binding.md), [zeilenbezogene Bindungen](../../../odbc/reference/develop-app/row-wise-binding.md), [positioniert, Update- und Delete-Anweisungen](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), und [Aktualisieren von Zeilen im Rowset mit SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ausführen von Bulk Insert, Update oder Delete-Vorgänge|[SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLDescribeCol-Funktion](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Schließen den Cursor in die Anweisung|[SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Zurückgeben der Anzahl der Ergebnis Resultsetspalten|[SQLNumResultCols-Funktion](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Positionieren den Cursor, Aktualisieren von Daten im Rowset aktualisieren oder Löschen von Daten im Resultset|[SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

