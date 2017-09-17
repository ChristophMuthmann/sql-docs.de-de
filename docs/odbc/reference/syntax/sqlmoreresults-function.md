---
title: SQLMoreResults-Funktion | Microsoft Docs
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
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 772bfd3d05d620840ea43c9f1313b4d94add10de
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlmoreresults-function"></a>SQLMoreResults-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLMoreResults** bestimmt, ob weitere Ergebnisse auf eine Anweisung mit verfügbaren **wählen**, **UPDATE**, **einfügen**, oder ** Löschen Sie** Anweisungen und, wenn dies der Fall ist, initialisiert verarbeiten, um diese Ergebnisse zu erzielen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE ODER SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLMoreResults** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* SQL _HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLMoreResults** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Optionswert wurde geändert.|Der Wert eines Attributs Anweisung als Batch geändert wurde verarbeitet. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Fehler bei der zugeordnete Verbindung während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die **SQLMoreResults** Funktion aufgerufen wurde und bevor er abgeschlossen Ausführung **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle *. Die **SQLMoreResults** Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die **SQLMoreResults** Funktion aufgerufen wurde und bevor er abgeschlossen Ausführung **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle * aus einem anderen Thread in einer multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLMoreResults** Funktion aufgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **Wählen Sie** Anweisungen Resultsets zurückgegeben. **UPDATE**, **einfügen**, und **löschen** Anweisungen geben die Anzahl der betroffenen Zeilen zurück. Wenn eine dieser Anweisungen als Batch mit Arrays von Parametern verarbeitet werden (nummeriert in aufsteigender Reihenfolge der Parameter in der Reihenfolge, die sie in den Batch angezeigt werden) oder in Prozeduren übermittelt, können sie mehrere Resultsets zurückgeben oder Zeilenanzahl. Informationen zu Batches von Anweisungen und Arrays von Parametern finden Sie unter [Batches von SQL-Anweisungen](../../../odbc/reference/develop-app/batches-of-sql-statements.md) und [Arrays von Parameterwerten](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Nach dem Ausführen des Batches, wird die Anwendung auf das erste Resultset positioniert. Die Anwendung kann Aufrufen **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll **, **SQLSetPos**, sowie alle Metadatenfunktionen, auf das erste oder alle nachfolgenden Resultset mit Vorwärtscursor, ebenso wie dies der Fall wäre es wäre nur ein einzelnes Resultset. Nachdem sie das erste Resultset abgeschlossen ist, ruft die Anwendung **SQLMoreResults** auf das nächste Resultset verschieben. Wenn ein anderes Resultset oder Count verfügbar ist, wird **SQLMoreResults** gibt SQL_SUCCESS zurück, und das Resultset oder Count-zur weiteren Verarbeitung initialisiert. Wenn Zeile Count – Generieren von Anweisungen in der Zwischenzeit angezeigt führen Anweisungen Set – generieren, können sie der Tabulatortaste aufrufen abgestuft werden **SQLMoreResults**. Nach dem Aufruf **SQLMoreResults** für **UPDATE**, **einfügen**, oder **löschen** -Anweisungen, die eine Anwendung kann eine Aufrufen **SQLRowCount**.  
  
 Wenn es eine aktuelle Resultset mit nicht abgerufenen Zeilen wurde **SQLMoreResults** verwirft dieses Resultset und das nächste Resultset oder Anzahl verfügbar macht. Wenn alle Ergebnisse verarbeitet wurden, **SQLMoreResults** gibt SQL_NO_DATA zurück. Für einige Treiber sind Output-Parameter und Rückgabewerte nicht verfügbar, bis alle Resultsets und Zeilenanzahl verarbeitet wurden. Für solche Treiber Ausgabeparameter und Rückgabewerte verfügbar wenn **SQLMoreResults** gibt SQL_NO_DATA zurück.  
  
 Alle Bindungen, die eingerichtet wurden, für das vorherige Resultset immer noch bleiben gültig. Wenn die spaltenstrukturen für dieses Resultset unterschiedlich sind, klicken Sie dann aufrufen **SQLFetch** oder **SQLFetchScroll** kann zu einem Fehler oder Abschneiden führen. Um dies zu verhindern, muss die Anwendung aufrufen **SQLBindCol** explizit nach Bedarf erneut binden (oder dazu deskriptorfelder). Alternativ können Sie die Anwendung aufrufen kann **SQLFreeStmt** mit einem *Option* SQL_UNBIND alle Spaltenpuffer aufzuheben.  
  
 Die Werte der Anweisungsattribute, z. B. Cursortyp, Cursorparallelität, Keysetgröße oder maximale Länge möglicherweise ändern, wie die Anwendung über den Batch durch Aufrufe von navigiert **SQLMoreResults**. In diesem Fall **SQLMoreResults** SQL_SUCCESS_WITH_INFO und SQLSTATE 01 s 02 zurück (Optionswert wurde geändert).  
  
 Aufrufen von **SQLCloseCursor**, oder **SQLFreeStmt** mit einem *Option* von SQL_CLOSE, verwirft alle Resultsets und Zeilenanzahl, die als Ergebnis der Ausführung von verfügbar waren der Batch. Das Anweisungshandle gibt die zugeordneten oder "vorbereitet". Aufrufen von **SQLCancel** eine asynchron ausgeführte Funktion abgebrochen, wenn ein Batch ausgeführt wurde und das Anweisungshandle in der ausgeführten Cursor positioniert ist, oder asynchroner Zustand alle Ergebnisse Mengen führt und Zeilenanzahl generiert vom Batch verworfen werden, wenn der Aufruf von "Abbrechen" erfolgreich war. Klicken Sie dann die Anweisung wird in den vorbereiteten oder zugeordneten versetzt.  
  
 Wenn ein Batch von Anweisungen oder eine Prozedur mit anderen SQL-Anweisungen enthält **wählen**, **UPDATE**, **einfügen**, und **löschen** -Anweisungen Diese anderen Anweisungen wirken sich nicht **SQLMoreResults**.  
  
 Weitere Informationen finden Sie unter [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Wenn eine gesuchte aktualisieren, insert oder-Anweisung in DELETE ein Batch von Anweisungen wirkt sich keine Zeilen in der Datenquelle **SQLMoreResults** gibt SQL_SUCCESS zurück. Dies unterscheidet sich von der Groß-/Kleinschreibung ein gesuchtes Update, insert oder delete-Anweisung, die über ausgeführt wird **SQLExecDirect**, **SQLExecute**, oder **SQLParamData**, welche Gibt SQL_NO_DATA zurück, wenn es keine Zeilen in der Datenquelle nicht beeinträchtigt wird. Wenn eine Anwendung ruft **SQLRowCount** zum Abrufen der Anzahl der Zeilen nach einem Aufruf von **SQLMoreResults** hat keine Zeilen betroffen **SQLRowCount** SQL_NO_DATA zurückgegeben wird.  
  
 Weitere Informationen zu den gültigen Sequenzierung ergebnisverarbeitung Funktionsreihe, finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Weitere Informationen zu SQL_PARAM_DATA_AVAILABLE und gestreamte Output-Parameter, finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Verfügbarkeit der Zeilenanzahl  
 Wenn ein Batch mehrere aufeinander folgende Zeile Count – Generieren von Anweisungen enthält, ist es möglich, dass diese Zeilenanzahl in nur einem Zeilenanzahl Rollup enthalten sind. Beispielsweise verfügt ein Batch einfügen fünf Anweisungen aus, und dann bestimmte Datenquellen von fünf einzelne Zeilenanzahl zurückgegeben werden. Bestimmte andere Datenquellen zurückgeben, nur eine Zeilenanzahl, die die Summe aus den fünf einzelnen Zeilenanzahl darstellt.  
  
 Wenn ein Batch eine Kombination von Ergebnis Satz – generieren und Zeile Count – Generieren von Anweisungen enthält, Zeilenanzahl oder möglicherweise nicht zur Verfügung überhaupt. Das Verhalten des Treibers in Bezug auf die Verfügbarkeit der Zeilenanzahl wird aufgelistet, in der Informationstyp SQL_BATCH_ROW_COUNT verfügbar durch einen Aufruf von **SQLGetInfo**. Nehmen wir beispielsweise an, dass der Batch enthält eine **wählen**, gefolgt von zwei **einfügen**s und ein anderes **wählen**. Klicken Sie dann sind die folgenden Fälle möglich:  
  
-   Die Zeilenanzahl auf die beiden entsprechenden **einfügen** Anweisungen sind überhaupt nicht verfügbar. Der erste Aufruf von **SQLMoreResults** positionieren Sie für das Resultset der zweiten **wählen** Anweisung.  
  
-   Die Zeilenanzahl auf die beiden entsprechenden **einfügen** Anweisungen einzeln verfügbar sind. (Ein Aufruf von **SQLGetInfo** gibt nicht das SQL_BRC_ROLLED_UP Bit für den Typ der SQL_BATCH_ROW_COUNT Informationen zurück.) Der erste Aufruf von **SQLMoreResults** positionieren Sie auf der Anzahl der Zeilen des ersten **einfügen**, und der zweite Aufruf positionieren Sie auf der Anzahl der Zeilen des zweiten **einfügen**. Der dritte Aufruf von **SQLMoreResults** positionieren Sie für das Resultset der zweiten **wählen** Anweisung.  
  
-   Die Zeilenanzahl auf die beiden entsprechenden **fügt** werden als Rollup in ein einzelnes Zeilenanzahl, die verfügbar ist. (Ein Aufruf von **SQLGetInfo** gibt das bit für den Informationstyp SQL_BATCH_ROW_COUNT SQL_BRC_ROLLED_UP.) Der erste Aufruf von **SQLMoreResults** positionieren Sie die Rollup-Zeilenanzahl und der zweite Aufruf von **SQLMoreResults** positionieren Sie für das Resultset der zweiten **wählen**.  
  
 Bestimmten Treiber stellen die Zeilenanzahl nur für explizite Batches und gespeicherte Prozeduren nicht verfügbar.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen des Teils oder aller eine Spalte mit Daten|[SQLGetData-Funktion](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
