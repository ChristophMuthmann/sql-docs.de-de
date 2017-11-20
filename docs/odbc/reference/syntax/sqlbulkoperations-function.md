---
title: SQLBulkOperations-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea439a41a6a3d42c9266bbccfe53aace1c0f37f4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLBulkOperations** Bulk Einfüge- und Bulk Lesezeichen führt Vorgänge, einschließlich aktualisieren, löschen und Abrufen von Lesezeichen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Vorgang*  
 [Eingabe] Vorgang ausführen:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Weitere Informationen finden Sie unter "Kommentare".  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLBulkOperations** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLBulkOperations** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben . Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
 Für alle diese SQLSTATEs, der SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurück (mit Ausnahme der 01xxx SQLSTATEs) zurückgeben kann, wird SQL_SUCCESS_WITH_INFO zurückgegeben, wenn ein Fehler, auf ein oder mehrere, aber nicht alle Zeilen einer Einfügung mehrerer Zeilen Operation auftritt, und SQL_ERROR zurückgegeben wird, wenn es sich bei Auftreten eines Fehlers in einer einzeiliges-Vorgang.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Die *Vorgang* Argument war SQL_FETCH_BY_BOOKMARK und Zeichenfolgen- oder Binärdaten, die für eine Spalte oder Spalten mit einem Datentyp SQL_C_CHAR oder SQL_C_BINARY zurückgegeben, die in das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL geführt haben.|  
|01 S 01|Fehler in Zeile|Die *Vorgang* Argument war SQL_ADD, und beim Ausführen des Vorgangs ist in einer oder mehreren Zeilen ein Fehler aufgetreten, aber mindestens eine Zeile wurde erfolgreich hinzugefügt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)<br /><br /> (Dieser Fehler wird nur ausgelöst, wenn eine Anwendung mit einer ODBC 2 arbeitet. *x* Treiber.)|  
|01S07|Teilbereiche wurden abgeschnitten.|Die *Vorgang* Argument war SQL_FETCH_BY_BOOKMARK, der Datentyp des Puffers Anwendung war nicht SQL_C_CHAR oder sql_c_binary angegeben und die Daten an die Anwendungspuffer für eine oder mehrere Spalten zurückgegeben wurden abgeschnitten. (Für numerische C-Datentypen, wurden die Nachkommastellen der Zahl abgeschnitten. Für die Zeit, Zeitstempel und Intervall C-Datentypen, die eine Zeitkomponente enthalten, wurde der Bruchteil der Zeit gekürzt.)<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Die *Vorgang* Argument wurde SQL_FETCH_BY_BOOKMARK und der Datenwert einer Spalte im Resultset konnte nicht an der angegebenen Datentyp konvertiert werden die *TargetType* Argument im Aufruf von **SQLBindCol**.<br /><br /> Die *Vorgang* Argument war SQL_UPDATE_BY_BOOKMARK oder SQL_ADD und der Datenwert in die Anwendungspuffer konnte nicht in den Datentyp einer Spalte im Resultset konvertiert werden.|  
|07009|Ungültiger Deskriptorindex|Das Argument *Vorgang* SQL_ADD wurde und eine Spalte mit der eine Spaltennummer, die größer als die Anzahl der Spalten im Resultset gebunden wurde.|  
|21S02|Die Spaltenzahl der abgeleiteten Tabelle stimmt nicht mit Spaltenliste überein.|Das Argument *Vorgang* SQL_UPDATE_BY_BOOKMARK; wurde und keine Spalten aktualisiert wurden, da alle Spalten haben, entweder ungebundenen oder nur-Lese wurden- oder der Wert in der gebundenen Längen-/Indikatorpuffers SQL_COLUMN_IGNORE wurde.|  
|22001|Zeichenfolgedaten wurden rechts abgeschnitten|Die Zuweisung von einem Zeichen- oder binären Wert einer Spalte im Resultset Verzeichnisdiensts NichtLeer (für Zeichen) oder ungleich Null (für binär)-Zeichen oder Bytes wird abgeschnitten.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Die *Vorgang* Argument wurde SQL_ADD oder SQL_UPDATE_BY_BOOKMARK, und die Zuweisung eines numerischen Werts einer Spalte im Resultset die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird.<br /><br /> Das Argument *Vorgang* SQL_FETCH_BY_BOOKMARK wurde und das Zurückgeben des numerischen Werts für eine oder mehrere gebundene Spalten hätte ein Verlust signifikanter Ziffern.|  
|22007|Ungültiges Datetime-format|Die *Vorgang* Argument wurde SQL_ADD oder SQL_UPDATE_BY_BOOKMARK, und die Zuweisung eines Date- oder Timestamp-Werts an eine Spalte im Resultset Jahr, Monat oder Tagesfeld außerhalb des gültigen Bereichs.<br /><br /> Das Argument *Vorgang* SQL_FETCH_BY_BOOKMARK war und zurückgeben den Date- oder Timestamp-Wert für eine oder mehrere gebundene Spalten hätte Jahr, Monat oder Tagesfeld außerhalb des gültigen Bereichs.|  
|22008|Überlauf für Datum/Uhrzeit-Feld.|Die *Vorgang* Argument war SQL_ADD oder SQL_UPDATE_BY_BOOKMARK, und die Leistung von "DateTime" arithmetische auf Daten gesendet werden, um eine Spalte im Resultset führt ein Datetime-Feld (Jahr, Monat, Tag, Stunde, Minute oder Sekunde Feld) des Ergebnisses fallen außerhalb des zulässigen Bereichs von Werten für das Feld oder ungültiger Daten basierend auf dem gregorianischen Kalender natürlichen Regeln für datetimes verstrichen ist.<br /><br /> Die *Vorgang* Argument war SQL_FETCH_BY_BOOKMARK, und die Leistung von arithmetischen auf Daten aus dem Resultset abgerufen werden "DateTime" führt ein Datetime-Feld (Jahr, Monat, Tag, Stunde, Minute oder zweiten Feld) von der Ergebnis fallen außerhalb des zulässigen Bereichs von Werten für das Feld oder ungültiger Daten basierend auf dem gregorianischen Kalender natürlichen Regeln für datetimes verstrichen ist.|  
|22015|Überlauf der Intervall-Feld.|Die *Vorgang* Argument wurde SQL_ADD oder SQL_UPDATE_BY_BOOKMARK, und die Zuweisung von einem genauen numerischen oder C Intervalltyp auf ein Intervall SQL-Datentyp einen Verlust signifikanter Ziffern.<br /><br /> Die *Vorgang* Argument war SQL_ADD oder SQL_UPDATE_BY_BOOKMARK; Wenn Sie ein Intervall SQL-Typ zuweisen, gab es keine Darstellung des Werts der C-Typ im Intervall SQL-Typ.<br /><br /> Die *Vorgang* Argument war SQL_FETCH_BY_BOOKMARK und Intervalltyp C zuweisen aus einer genauen numerischen oder Intervall SQL-Typ hat einen Datenverlust von signifikanten Stellen im Feld führende verursacht.<br /><br /> Die *Vorgang* Argument war SQL_FETCH_BY_BOOKMARK; beim Zuweisen zu Intervalltyp C gab es keine Darstellung des Werts des SQL-Datentyps in den Intervalltyp C.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Die *Vorgang* Argument war SQL_FETCH_BY_BOOKMARK; der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte wurde einem Zeichendatentyp; und der Wert in der Spalte war keine gültige Literale des gebundenen C-Typ.<br /><br /> Das Argument *Vorgang* SQL_ADD oder SQL_UPDATE_BY_BOOKMARK wurde; der SQL-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der C-Typ SQL_C_CHAR; und der Wert in der Spalte nicht wurde ein gültiger Literal vom den SQL-Typ gebunden.|  
|23000|Einschränkungsverletzung Integrität|Die *Vorgang* Argument war SQL_ADD, SQL_DELETE_BY_BOOKMARK oder SQL_UPDATE_BY_BOOKMARK und eine Einschränkung der Integrität verletzt wurde.<br /><br /> Die *Vorgang* Argument war SQL_ADD und eine Spalte, die nicht gebunden wurde als NOT NULL und keinen Standard besitzt definiert ist.<br /><br /> Die *Vorgang* Argument war SQL_ADD, in die gebundenen angegebene Länge *StrLen_or_IndPtr* SQL_COLUMN_IGNORE war und die Spalte nicht über einen Standardwert verfügen.|  
|24000|Ungültiger Cursorstatus|Die *StatementHandle* wurde in einem ausgeführten Zustand, aber kein Resultset zugeordnet wurde die *StatementHandle*.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund einer Ressourcendeadlock mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|42000|Syntaxfehler oder zugriffsverletzung|Der Treiber konnte Zeilensperre Bedarf zum Ausführen des Vorgangs angefordert die *Vorgang* Argument.|  
|44000|WITH CHECK OPTION-Verstoß|Die *Vorgang* Argument war SQL_ADD oder SQL_UPDATE_BY_BOOKMARK und die Einfügung oder Updatevorgang für eine Tabelle ausgeführt wurde (oder eine Tabelle aus der angezeigten Tabelle abgeleitet), die erstellt wurde, indem **WITH CHECK OPTION**, so, dass eine oder mehrere Zeilen Insert betroffen oder Update wird nicht mehr in der Tabelle vorhanden sein.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLBulkOperations** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) dem angegebenen *StatementHandle* war nicht in einem ausgeführten Zustand. Die Funktion wurde aufgerufen, ohne zunächst **SQLExecDirect**, **SQLExecute**, oder eine Katalogfunktion auf.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLSetPos** wurde aufgerufen, die *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) der Treiber wurde eine ODBC-2. *x* -Treiber und **SQLBulkOperations** wurde aufgerufen, eine *StatementHandle* vor **SQLFetchScroll** oder **SQLFetch ** aufgerufen wurde.<br /><br /> (DM) **SQLBulkOperations** wurde aufgerufen, nachdem **SQLExtendedFetch** aufgerufen wurde, auf die *StatementHandle*.|  
|HY011|Attribut kann jetzt nicht festgelegt werden|(DM) der Treiber wurde eine ODBC-2. *x* Treiber und das SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut festgelegt wurde, zwischen den Aufrufen **SQLFetch** oder **SQLFetchScroll** und **SQLBulkOperations **.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Die *Vorgang* Argument war SQL_ADD oder SQL_UPDATE_BY_BOOKMARK; ein Datenwert war nicht null-Zeiger; wurde von der C-Datentyp SQL_C_BINARY oder SQL_C_CHAR; und der Spaltenwert für die Länge ist kleiner als 0, aber ungleich-SQL_DATA_AT_EXEC , SQL_COLUMN_IGNORE, SQL_NTS oder SQL_NULL_DATA oder kleiner oder gleich SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Der Wert in ein Längen-/Indikatorpuffers wurde SQL_DATA_AT_EXEC; der SQL-Typ wurde entweder SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen Datentyp; und welche Informationen SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** wurde von "Y".<br /><br /> Die *Vorgang* Argument war SQL_ADD SQL_ATTR_USE_BOOKMARK-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde und Spalte 0 in einen Puffer mit einer Länge nicht die maximale Länge für das Lesezeichen für dieses Resultset gleich war gebunden wurde. (Diese Länge finden Sie im Feld SQL_DESC_OCTET_LENGTH vom IRD und abgerufen werden kann, durch den Aufruf **SQLDescribeCol**, **SQLColAttribute**, oder **SQLGetDescField**.)|  
|HY092|Ungültiges Attribut-ID|(DM) der angegebene Wert für die *Vorgang* Argument war ungültig.<br /><br /> Die *Vorgang* Argument war SQL_ADD, SQL_UPDATE_BY_BOOKMARK oder SQL_DELETE_BY_BOOKMARK und das SQL_ATTR_CONCURRENCY-Anweisungsattribut auf SQL_CONCUR_READ_ONLY festgelegt wurde.<br /><br /> Die *Vorgang* Argument war SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK oder SQL_UPDATE_BY_BOOKMARK, und die Lesezeichenspalte wurde nicht gebunden oder das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht den in der angeforderte Vorgang der *Vorgang* Argument.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr** mit einer *Attribut* Argument SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
  
> [!CAUTION]  
>  Informationen zum Status der fehlerhaften Anweisung **SQLBulkOperations** in aufgerufen werden können und was sie tun muss, um die Kompatibilität mit ODBC 2.* X* -Anwendungen finden Sie unter der [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) Abschnitt in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
 Eine Anwendung verwendet **SQLBulkOperations** zum Ausführen der folgenden Vorgänge für die Basistabelle oder Sicht, die die aktuelle Abfrage entspricht:  
  
-   Fügen Sie neue Zeilen hinzu.  
  
-   Aktualisieren Sie einen Satz von Zeilen in der jede Zeile von einem Lesezeichen identifiziert wird.  
  
-   Löschen Sie einen Satz von Zeilen in der jede Zeile von einem Lesezeichen identifiziert wird.  
  
-   Rufen Sie eine Gruppe von Zeilen in der jede Zeile von einem Lesezeichen identifiziert wird.  
  
 Nach einem Aufruf von **SQLBulkOperations**, die Cursorposition Block ist nicht definiert. Rufen Sie die Anwendung muss **SQLFetchScroll** um die Cursorposition festzulegen. Eine Anwendung sollte Aufrufen **SQLFetchScroll** nur mit einer *FetchOrientation* Argument SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE oder sql_fetch_bookmark auf. Die Cursorposition ist nicht definiert, wenn die Anwendung aufruft, **SQLFetch** oder **SQLFetchScroll** mit einem *FetchOrientation* Argument SQL_FETCH_PRIOR, SQL_FETCH_NEXT, oder SQL_FETCH_RELATIVE.  
  
 Eine Spalte kann ignoriert werden, in der Bulk-Vorgänge durch einen Aufruf von **SQLBulkOperations** durch Festlegen der im Aufruf der angegebenen Spalte Längen-/Indikatorpuffers **SQLBindCol**, um SQL_COLUMN_IGNORE.  
  
 Es ist nicht notwendig, für die Anwendung das Anweisungsattribut SQL_ATTR_ROW_OPERATION_PTR festgelegt, wenn er ruft **SQLBulkOperations** da Zeilen beim Durchführen von Massenvorgängen mit dieser Funktion nicht ignoriert werden können.  
  
 Enthält der Puffer, der auf das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut zeigt die Anzahl der Zeilen, die durch einen Aufruf von betroffenen **SQLBulkOperations**.  
  
 Wenn die *Vorgang* -Argument SQL_ADD oder SQL_UPDATE_BY_BOOKMARK und die Select-Liste der Query-Spezifikation, die dem Cursor zugeordnet enthält mehr als einen Verweis auf die gleiche Spalte ist, es ist treiberdefinierten, ob ein Fehler wird generiert, oder der Treiber die doppelte Verweise ignoriert, und führt die angeforderten Vorgänge.  
  
 Weitere Informationen zur Verwendung von **SQLBulkOperations**, finden Sie unter [Aktualisieren von Daten mit SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Fügt Bulk ausführen  
 Zum Einfügen von Daten mit **SQLBulkOperations**, eine Anwendung führt die folgende Sequenz von Schritten:  
  
1.  Führt eine Abfrage, die ein Resultset zurückgibt.  
  
2.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der Zeilen, die sie einfügen möchte.  
  
3.  Aufrufe **SQLBindCol** um die Daten zu binden, die sie einfügen möchte. Die Daten werden in ein Array mit einer Größe, die gleich dem Wert des SQL_ATTR_ROW_ARRAY_SIZE gebunden.  
  
    > [!NOTE]  
    >  Die Größe des Arrays, verweist das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR muss entweder gleich SQL_ATTR_ROW_ARRAY_SIZE oder SQL_ATTR_ROW_STATUS_PTR sollte ein null-Zeiger sein.  
  
4.  Aufrufe **SQLBulkOperations**(*StatementHandle,* SQL_ADD), den Einfügevorgang auszuführen.  
  
5.  Wenn die Anwendung das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR festgelegt wurde, können sie dieses Array, um das Ergebnis des Vorgangs finden Sie unter überprüfen.  
  
 Wenn eine Anwendung bindet die Spalte 0 vor dem Aufrufen **SQLBulkOperations** mit einer *Vorgang* Argument SQL_ADD, der Treiber aktualisiert die Puffern mit gebundenen Spalten 0 mit den Werten der Lesezeichen für die neu eingefügte Zeile. Damit dies eintritt muss die Anwendung das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt haben vor der Ausführung der Anweisung. (Dies funktioniert nicht mit einer ODBC 2. *x* Treiber.)  
  
 Long-Daten können mithilfe von SQLParamData und SQLPutData Aufrufe in Teilen von SQLBulkOperations, hinzugefügt werden. Weitere Informationen finden Sie unter "Bereitstellen von langen Daten für Bulk Inserts und Updates" weiter unten in diesem Funktionsverweis.  
  
 Es ist nicht notwendig, für die Anwendung aufrufen **SQLFetch** oder **SQLFetchScroll** vor **SQLBulkOperations** (es sei denn, für eine ODBC-2 passiert.* X* Treiber; Siehe [Abwärtskompatibilität und zur Einhaltung von Standards](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 Das Verhalten ist treiberdefinierten Wenn **SQLBulkOperations**, mit einer *Vorgang* SQL_ADD, Argument für einen Cursor, enthält doppelte Spalten, aufgerufen wird. Der Treiber können ein SQLSTATE treiberdefinierten zurückgeben, zum Hinzufügen die Daten in die erste Spalte, die im Resultset angezeigt wird festgelegt oder andere treiberdefinierten Verhalten führen.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Ausführen von Massenaktualisierungen mithilfe von Lesezeichen  
 Um massenaktualisierungen auszuführen, mithilfe von Lesezeichen mit **SQLBulkOperations**, eine Anwendung führt die folgenden Schritte nacheinander:  
  
1.  Legt das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE fest.  
  
2.  Führt eine Abfrage, die ein Resultset zurückgibt.  
  
3.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der Zeilen, die sie aktualisieren möchte.  
  
4.  Aufrufe **SQLBindCol** um die Daten zu binden, die sie aktualisieren möchte. Die Daten werden in ein Array mit einer Größe, die gleich dem Wert des SQL_ATTR_ROW_ARRAY_SIZE gebunden. Ruft auch **SQLBindCol** Spalte 0 (die Lesezeichenspalte) binden.  
  
5.  Kopien gebunden Lesezeichen für die Zeilen an, die sie interessiert ist, aktualisieren Sie in das Array an die Spalte 0.  
  
6.  Aktualisiert die Daten in den Puffern mit gebundenen.  
  
    > [!NOTE]  
    >  Die Größe des Arrays, verweist das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR sollte gleich SQL_ATTR_ROW_ARRAY_SIZE oder SQL_ATTR_ROW_STATUS_PTR sollte ein null-Zeiger sein.  
  
7.  Aufrufe **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Wenn die Anwendung das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR festgelegt wurde, können sie dieses Array, um das Ergebnis des Vorgangs finden Sie unter überprüfen.  
  
8.  Ruft optional **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) zum Abrufen von Daten in die gebundenen Anwendungspuffer, um sicherzustellen, dass das Update aufgetreten ist.  
  
9. Wenn Daten aktualisiert wurde, ändert der Treiber den Wert in der zeilenstatusarray für die entsprechenden Zeilen in SQL_ROW_UPDATED an.  
  
 Massenupdates durchgeführte **SQLBulkOperations** zählen long-Daten über Aufrufe **SQLParamData** und **SQLPutData**. Weitere Informationen finden Sie unter "Bereitstellen von langen Daten für Bulk Inserts und Updates" weiter unten in diesem Funktionsverweis.  
  
 Wenn Cursor Lesezeichen beizubehalten, die Anwendung muss nicht aufrufen, **SQLFetch** oder **SQLFetchScroll** vor dem Aktualisieren von Lesezeichen. Sie können Lesezeichen verwenden, die sie von einem vorherigen Cursor gespeichert wurde. Wenn Lesezeichen, über den Cursor nicht beibehalten werden, muss die Anwendung aufrufen **SQLFetch** oder **SQLFetchScroll** Lesezeichen abgerufen.  
  
 Das Verhalten ist treiberdefinierten Wenn **SQLBulkOperations**, mit einer *Vorgang* SQL_UPDATE_BY_BOOKMARK, Argument für einen Cursor, enthält doppelte Spalten, aufgerufen wird. Der Treiber kann ein SQLSTATE treiberdefinierten zurückgeben, aktualisieren Sie die erste Spalte, die im Resultset angezeigt wird oder andere treiberdefinierten Verhalten führen.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Ausführen von Massenladen Ruft mithilfe von Lesezeichen  
 Zum Ausführen der Bulk-Abrufe mithilfe von Lesezeichen mit **SQLBulkOperations**, eine Anwendung führt die folgenden Schritte nacheinander:  
  
1.  Legt das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE fest.  
  
2.  Führt eine Abfrage, die ein Resultset zurückgibt.  
  
3.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der Zeilen, die abgerufen werden sollen.  
  
4.  Aufrufe **SQLBindCol** um die Daten zu binden, die abgerufen werden sollen. Die Daten werden in ein Array mit einer Größe, die gleich dem Wert des SQL_ATTR_ROW_ARRAY_SIZE gebunden. Ruft auch **SQLBindCol** Spalte 0 (die Lesezeichenspalte) binden.  
  
5.  Kopien gebunden Lesezeichen für die Zeilen an, die es in das Array abrufen möchte Spalte 0. (Dies setzt voraus, dass die Anwendung die Textmarken bereits separat erhalten hat.)  
  
    > [!NOTE]  
    >  Die Größe des Arrays, verweist das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR sollte gleich SQL_ATTR_ROW_ARRAY_SIZE oder SQL_ATTR_ROW_STATUS_PTR sollte ein null-Zeiger sein.  
  
6.  Aufrufe **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Wenn die Anwendung das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR festgelegt wurde, können sie dieses Array, um das Ergebnis des Vorgangs finden Sie unter überprüfen.  
  
 Wenn Cursor Lesezeichen beizubehalten, die Anwendung muss nicht aufrufen, **SQLFetch** oder **SQLFetchScroll** vor dem Abrufen von Lesezeichen. Sie können Lesezeichen verwenden, die sie von einem vorherigen Cursor gespeichert wurde. Wenn Lesezeichen, über den Cursor nicht beibehalten werden, muss die Anwendung aufrufen **SQLFetch** oder **SQLFetchScroll** einmal an die Lesezeichen abrufen.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Ausführen von Massenladen Löscht mithilfe von Lesezeichen  
 Zum Ausführen der Bulk-löscht, die mithilfe von Lesezeichen mit **SQLBulkOperations**, eine Anwendung führt die folgenden Schritte nacheinander:  
  
1.  Legt das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE fest.  
  
2.  Führt eine Abfrage, die ein Resultset zurückgibt.  
  
3.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der Zeilen, die gelöscht werden sollen.  
  
4.  Aufrufe **SQLBindCol** Spalte 0 (die Lesezeichenspalte) binden.  
  
5.  Kopien gebunden Lesezeichen für die Zeilen an, die sie interessiert ist, löschen Sie in das Array an die Spalte 0.  
  
    > [!NOTE]  
    >  Die Größe des Arrays, verweist das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR sollte gleich SQL_ATTR_ROW_ARRAY_SIZE oder SQL_ATTR_ROW_STATUS_PTR sollte ein null-Zeiger sein.  
  
6.  Aufrufe **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Wenn die Anwendung das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR festgelegt wurde, können sie dieses Array, um das Ergebnis des Vorgangs finden Sie unter überprüfen.  
  
 Wenn Cursor Lesezeichen beizubehalten, die Anwendung muss nicht aufrufen, **SQLFetch** oder **SQLFetchScroll** vor dem Löschen von Lesezeichen. Sie können Lesezeichen verwenden, die sie von einem vorherigen Cursor gespeichert wurde. Wenn Lesezeichen, über den Cursor nicht beibehalten werden, muss die Anwendung aufrufen **SQLFetch** oder **SQLFetchScroll** einmal an die Lesezeichen abrufen.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Long-Daten bereitstellen für Masseneinfügungen und-Updates  
 Long-Daten können angegeben werden, für masseneinfügungen und-Updates ausgeführt, die durch Aufrufe von **SQLBulkOperations**. Zum Einfügen oder Aktualisieren von long-Daten, führt eine Anwendung die folgenden Schritte aus, zusätzlich zu den Schritten, die in den Abschnitten "Masseneinfügung ausführen" und "Ausführen von Massenladen Updates mithilfe von Lesezeichen" weiter oben in diesem Thema beschrieben.  
  
1.  Wenn bindet die Daten mithilfe von **SQLBindCol**, die Anwendung wird einen anwendungsdefinierten Wert, z. B. die Nummer der Spalte, in der * \*TargetValuePtr* Puffer für die Data-at-Execution Spalten. Der Wert kann später verwendet werden, um die Spalte zu identifizieren.  
  
     Die Anwendung gibt das Ergebnis von der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro in den * \*StrLen_or_IndPtr* Puffer. Wenn der SQL-Datentyp der Spalte SQL_LONGVARBINARY, SQL_LONGVARCHAR oder einem long-Daten datenquellenspezifischen-Datentyp und der Treiber "Y" für den Informationstyp SQL_NEED_LONG_DATA_LEN in gibt **SQLGetInfo**, *Länge * ist die Anzahl der Bytes der Daten für den Parameter; gesendet werden sollen, andernfalls muss er einen nicht negativen Wert und wird ignoriert.  
  
2.  Wenn **SQLBulkOperations** aufgerufen wird, wenn Data-at-Execution-Spalten, die Funktion gibt SQL_NEED_DATA zurück und fährt mit Schritt 3 fort, das folgt vorhanden sind. (Wenn keine Data-at-Execution-Spalten vorhanden sind, ist der Prozess abgeschlossen.)  
  
3.  Ruft die Anwendung **SQLParamData** die Adresse des abzurufenden der * \*TargetValuePtr* Puffer für die erste Data-at-Execution-Spalte verarbeitet werden. **SQLParamData** wird SQL_NEED_DATA zurückgegeben. Die Anwendung ruft den anwendungsdefinierten Wert aus der * \*TargetValuePtr* Puffer.  
  
    > [!NOTE]  
    >  Obwohl Data-at-Execution-Parameter Data-at-Execution-Spalten ähneln, der Rückgabewert von **SQLParamData** für jedes unterschiedlich ist.  
  
     Data-at-Execution-Spalten in einem Rowset für die Daten mit gesendet werden, sind **SQLPutData** Wenn eine Zeile aktualisiert oder eingefügt mit **SQLBulkOperations**. Sie sind mit gebunden **SQLBindCol**. Der Rückgabewert von **SQLParamData** ist die Adresse der Zeile in der **TargetValuePtr* Puffer, die verarbeitet wird.  
  
4.  Ruft die Anwendung **SQLPutData** ein- oder mehrmals zum Senden von Daten für die Spalte. Mehr als ein Aufruf ist erforderlich, wenn der Datenwert in zurückgegeben werden, kann die * \*TargetValuePtr* im angegebenen Puffer **SQLPutData**; mehrere Aufrufe **SQLPutData** für dieselbe Spalte dürfen nur, wenn auf eine Spalte mit einem Zeichen, Binary oder Daten datenquellenspezifischen Datentyp Zeichendaten C senden, oder beim Senden von Binärdaten C an eine Spalte mit einem Zeichen, binary, oder geben Sie die Datenquelle spezifischen Daten.  
  
5.  Ruft die Anwendung **SQLParamData** erneut aus, um zu signalisieren, dass alle Daten für die Spalte gesendet wurde.  
  
    -   Wenn weitere Data-at-Execution-Spalten vorhanden sind **SQLParamData** gibt SQL_NEED_DATA sowie die Adresse der *TargetValuePtr* Puffer für die nächste Data-at-Execution-Spalte verarbeitet werden. Die Anwendung wiederholt die Schritte 4 und 5.  
  
    -   Wenn keine weiteren Data-at-Execution-Spalten vorhanden sind, ist der Prozess abgeschlossen. Wenn die Anweisung erfolgreich ausgeführt wurde **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO; Wenn Fehler bei der Ausführung gibt SQL_ERROR zurück. An diesem Punkt **SQLParamData** zurückgeben kann eine beliebige SQLSTATE, die von zurückgegeben werden kann **SQLBulkOperations**.  
  
 Wenn der Vorgang abgebrochen wird oder ein Fehler, in auftritt **SQLParamData** oder **SQLPutData** nach **SQLBulkOperations** wird SQL_NEED_DATA zurückgegeben und vor dem Senden von Daten für alle Data-at-Execution-Spalten, die Anwendung kann aufrufen nur **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions **, **SQLParamData**, oder **SQLPutData** für die Anweisung oder die Verbindung mit der Anweisung verknüpft sind. Wenn für die Anweisung oder die Verbindung mit der Anweisung verknüpfte jede andere Funktion aufgerufen wird, gibt die Funktion SQL_ERROR und SQLSTATE HY010 (Sequenzfehler-Funktion).  
  
 Wenn die Anwendung aufruft, **SQLCancel** während der Treiber für Data-at-Execution-Spalten weiterhin Daten benötigt, bricht der Treiber den Vorgang ab. Die Anwendung kann dann aufrufen **SQLBulkOperations** erneut Abbrechen hat keine Auswirkungen auf die Cursor-Status oder der aktuellen Cursorposition.  
  
## <a name="row-status-array"></a>Zeilenstatusarray  
 Die zeilenstatusarray Statuswerte für jede Zeile der Daten im Rowset enthält, nach einem Aufruf von **SQLBulkOperations**. Der Treiber setzt die Statuswerte in diesem Array nach einem Aufruf von **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, oder **SQLBulkOperations** . Dieses Array wird durch einen Aufruf von anfänglich aufgefüllt **SQLBulkOperations** Wenn **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde vor dem **SQLBulkOperations **. Dieses Array wird durch das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR verwiesen. Die Anzahl der Elemente in der Zeile Status Arrays, muss die Anzahl der Zeilen im Rowset (gemäß dem SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut) gleich. Informationen zu diesem zeilenstatusarray finden Sie unter [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgende Beispiel werden 10 Zeilen mit Daten zu einem Zeitpunkt aus der Customers-Tabelle abgerufen. Anschließend wird der Benutzer für eine Aktion dauern aufgefordert. Um den Netzwerkverkehr zu reduzieren, wird der Beispiel-Puffer updates, Löschvorgängen und und fügt lokal in den gebundenen Arrays, weist jedoch hinter der Rowsetdaten Offsets. Wenn der Benutzer entscheidet sich für das Senden von Updates, löschungen und auf die Datenquelle einfügungen, wird der Code legt die Bindung, die entsprechend offset fest und ruft **SQLBulkOperations**. Der Einfachheit halber kann nicht der Benutzer mehr als 10-Updates, löschungen oder einfügungen Puffer.  
  
```  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Ein einzelnes Datenfeld ein Deskriptor abrufen|[SQLGetDescField-Funktion](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Abrufen von mehreren Feldern einen Deskriptor|[SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Ein Deskriptor, der ein einzelnes Datenfeld festlegen|[SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Ein Deskriptor, der mehrere Felder festlegen|[SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Positionieren den Cursor, Aktualisieren von Daten im Rowset aktualisieren oder Löschen von Daten im rowset|[SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

