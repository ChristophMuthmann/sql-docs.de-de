---
title: SQLSetPos-Funktion | Microsoft Docs
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
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6140625da489bcb573b3beb4ca2be0838805f8d5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetpos-function"></a>SQLSetPos-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLSetPos** die Cursorposition in ein Rowset fest und ermöglicht es einer Anwendung, um Daten im Rowset zu aktualisieren oder zu aktualisieren oder Löschen von Daten im Resultset.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *' RowNumber '*  
 [Eingabe] Die Position der Zeile im Rowset für das Ausführen des Vorgangs angegeben wird, mit der *Vorgang* Argument. Wenn *RowNumber* gleich 0 ist, der Vorgang gilt für jede Zeile im Rowset.  
  
 Weitere Informationen finden Sie unter "Kommentare".  
  
 *Vorgang*  
 [Eingabe] Vorgang ausführen:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE AUF SQL_DELETE  
  
> [!NOTE]  
>  Der SQL_ADD-Wert für die *Vorgang* Argument wurde als veraltet klassifiziert für ODBC 3.*.x*. ODBC-3. *x* Treiber müssen SQL_ADD Gründen der Abwärtskompatibilität unterstützt. Diese Funktionalität wurde ersetzt durch einen Aufruf von **SQLBulkOperations** mit einem *Vorgang* von SQL_ADD. Wenn eine ODBC-3. *x* Anwendung arbeitet mit einer ODBC 2..* X* Treiber, der Treiber-Manager ordnet einen Aufruf von **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD auf **SQLSetPos** mit einer * Vorgang* von SQL_ADD.  
  
 Weitere Informationen finden Sie unter "Kommentare".  
  
 *LockType*  
 [Eingabe] Gibt an, wie die Zeile zu sperren, nach dem Ausführen des Vorgangs angegeben wird, der *Vorgang* Argument.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Weitere Informationen finden Sie unter "Kommentare".  
  
 **Gibt zurück**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetPos** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLSetPos** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
 Für alle diese SQLSTATEs, der SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurück (mit Ausnahme der 01xxx SQLSTATEs) zurückgeben kann, wird SQL_SUCCESS_WITH_INFO zurückgegeben, wenn ein Fehler, auf ein oder mehrere, aber nicht alle Zeilen einer Einfügung mehrerer Zeilen Operation auftritt, und SQL_ERROR zurückgegeben wird, wenn es sich bei Auftreten eines Fehlers in einer einzeiliges-Vorgang.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01001|Konflikt beim Cursorvorgang|Die *Vorgang* Argument war SQL_DELETE oder SQL_UPDATE und keine Zeilen oder mehr als eine Zeile gelöscht oder aktualisiert wurden. (Weitere Informationen über Updates auf mehr als eine Zeile, finden Sie unter der Beschreibung der SQL_ATTR_SIMULATE_CURSOR *Attribut* in **SQLSetStmtAttr**.) (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)<br /><br /> Die *Vorgang* Argument war SQL_DELETE oder SQL_UPDATE und Vorgangsfehler aufgrund einer Verletzung der vollständigen Parallelität. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Die *Vorgang* Argument war SQL_REFRESH und Zeichenfolgen- oder Binärdaten, die für eine Spalte oder Spalten mit einem Datentyp SQL_C_CHAR oder SQL_C_BINARY zurückgegeben, die in das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL geführt haben.|  
|01 S 01|Fehler in Zeile|Die *RowNumber* Argument war 0 und Fehler in einer oder mehreren Zeilen beim Ausführen des Vorgangs angegeben wird, mit der *Vorgang* Argument.<br /><br /> (SQL_SUCCESS_WITH_INFO wird zurückgegeben, wenn ein Fehler, auf ein oder mehrere, aber nicht alle Zeilen einer Einfügung mehrerer Zeilen Operation auftritt, und SQL_ERROR zurückgegeben wird, wenn auf einer einzelnen Zeile Vorgang ein Fehler auftritt.)<br /><br /> (Diese SQLSTATE wird nur zurückgegeben, wenn **SQLSetPos** wird aufgerufen, nachdem **SQLExtendedFetch**, wenn der Treiber einer ODBC 2..* X* Treiber und die Cursorbibliothek wird nicht verwendet.)|  
|01S07|Teilbereiche wurden abgeschnitten.|Die *Vorgang* Argument war SQL_REFRESH, der Datentyp des Puffers Anwendung war nicht SQL_C_CHAR oder sql_c_binary angegeben und die Daten an die Anwendungspuffer für eine oder mehrere Spalten zurückgegeben wurden abgeschnitten. Für numerische Datentypen und wurde die Nachkommastellen der Zahl gekürzt. Für die Zeit, Zeitstempel und Interval-Datentypen, die eine Komponente enthält wurde der Bruchteil der Zeit abgeschnitten.<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert einer Spalte im Resultset konnte nicht an der angegebenen Datentyp konvertiert werden *TargetType* im Aufruf **SQLBindCol**.|  
|07009|Ungültiger Deskriptorindex|Das Argument *Vorgang* SQL_REFRESH oder SQL_UPDATE war, und eine Spalte mit der eine Spaltennummer, die größer als die Anzahl der Spalten im Resultset gebunden wurde.|  
|21S02|Die Spaltenzahl der abgeleiteten Tabelle stimmt nicht mit Spaltenliste überein.|Das Argument *Vorgang* SQL_UPDATE wurde und keine Spalten aktualisiert wurden, da alle Spalten, entweder ungebundenen schreibgeschützt wurden, oder der Wert in der gebundenen Längen-/Indikatorpuffers SQL_COLUMN_IGNORE war.|  
|22001|Die Zeichenfolgedaten rechts abgeschnitten.|Die *Vorgang* Argument war SQL_UPDATE auf, und die Zuweisung von einem Zeichen- oder binären Wert einer Spalte führt das Abschneiden von NichtLeer (für Zeichen) oder ungleich Null (für binär)-Zeichen oder Bytes.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Das Argument *Vorgang* wurde SQL_UPDATE auf, und die Zuweisung eines numerischen Werts einer Spalte im Resultset die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird.<br /><br /> Das Argument *Vorgang* SQL_REFRESH wurde und das Zurückgeben des numerischen Werts für eine oder mehrere gebundene Spalten hätte ein Verlust signifikanter Ziffern.|  
|22007|Ungültiges Datetime-format|Das Argument *Vorgang* wurde SQL_UPDATE auf, und die Zuweisung eines Date- oder Timestamp-Werts an eine Spalte im Resultset Jahr, Monat oder Tagesfeld außerhalb des gültigen Bereichs.<br /><br /> Das Argument *Vorgang* SQL_REFRESH war und zurückgeben den Date- oder Timestamp-Wert für eine oder mehrere gebundene Spalten hätte Jahr, Monat oder Tagesfeld außerhalb des gültigen Bereichs.|  
|22008|Überlauf für Datum/Uhrzeit-Feld.|Die *Vorgang* Argument war SQL_UPDATE auf, und die Leistung von "DateTime" arithmetische auf Daten an eine Spalte im Resultset gesendet werden in einem Datetime-Feld (Jahr, Monat, Tag, Stunde, Minute oder zweiten Feld) des umzuwandelnden Ergebnis geführt hat außerhalb anhand des gregorianischen Kalenders natürlichen Regeln für datetimes-Werte des zulässigen Bereichs von Werten für das Feld oder ungültig.<br /><br /> Die *Vorgang* Argument war SQL_REFRESH und die Leistung von "DateTime" arithmetische auf Daten aus dem Resultset abgerufen werden in einem Datetime-Feld (Jahr, Monat, Tag, Stunde, Minute oder zweiten Feld) des umzuwandelnden Ergebnis geführt hat außerhalb anhand des gregorianischen Kalenders natürlichen Regeln für datetimes-Werte des zulässigen Bereichs von Werten für das Feld oder ungültig.|  
|22015|Überlauf der Intervall-Feld.|Die *Vorgang* Argument wurde SQL_UPDATE auf, und die Zuweisung von einem genauen numerischen oder C Intervalltyp auf ein Intervall SQL-Datentyp einen Verlust signifikanter Ziffern.<br /><br /> Die *Vorgang* Argument war SQL_UPDATE; Wenn Sie ein Intervall SQL-Typ zuweisen, gab es keine Darstellung des Werts der C-Typ im Intervall SQL-Typ.<br /><br /> Die *Vorgang* Argument war SQL_REFRESH und Intervalltyp C zuweisen aus einer genauen numerischen oder Intervall SQL-Typ hat einen Datenverlust von signifikanten Stellen im Feld führende verursacht.<br /><br /> Die *Vorgang* Argument war SQL_ Aktualisieren; beim Zuweisen zu Intervalltyp C gab es keine Darstellung des Werts des SQL-Datentyps in den Intervalltyp C.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Die *Vorgang* Argument war SQL_REFRESH; der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte eines Zeichendatentyps; und der Wert in der Spalte nicht wurde ein gültiger Literal vom den C-Typ gebunden.<br /><br /> Das Argument *Vorgang* SQL_UPDATE wurde; der SQL-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der C-Typ SQL_C_CHAR; und der Wert in der Spalte nicht wurde ein gültiger Literal des gebundenen SQL-Typs.|  
|23000|Einschränkungsverletzung Integrität|Das Argument *Vorgang* SQL_DELETE oder SQL_UPDATE wurde und eine Einschränkung der Integrität verletzt wurde.|  
|24000|Ungültiger Cursorstatus|Die *StatementHandle* wurde in einem ausgeführten Zustand, aber kein Resultset zugeordnet wurde die *StatementHandle*.<br /><br /> (DM) ein Cursor geöffnet wurde die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.<br /><br /> Ein Cursor geöffnet wurde die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde, aber der Cursor wurde vor dem Start des Resultsets oder nach das Ende des Resultsets.<br /><br /> Das Argument *Vorgang* SQL_DELETE, SQL_REFRESH oder SQL_UPDATE wurde und der Cursor vor dem Start des Resultsets oder nach dem Ende des Resultsets positioniert wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|42000|Syntaxfehler oder zugriffsverletzung|Der Treiber konnte die Zeilensperre bei Bedarf zum Ausführen des Vorgangs angefordert, die im Argument *Vorgang*.<br /><br /> Der Treiber konnte die Zeile zu sperren, wie im Argument angefordert *LockType*.|  
|44000|WITH CHECK OPTION-Verstoß|Die *Vorgang* Argument war SQL_UPDATE auf, und das Update wurde für eine Tabelle ausgeführt oder eine Tabelle aus der Tabelle durch Angabe erstellten abgeleitet **WITH CHECK OPTION**, sodass eine oder mehrere Zeilen betroffen das Update wird nicht mehr in der Tabelle vorhanden sein.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*, und klicken Sie dann die Funktion aufgerufen wurde erneut auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde noch ausgeführt werden, wenn die SQLSetPos-Funktion aufgerufen wurde.<br /><br /> (DM) dem angegebenen *StatementHandle* war nicht in einem ausgeführten Zustand. Die Funktion wurde aufgerufen, ohne zunächst **SQLExecDirect**, **SQLExecute**, oder eine Katalogfunktion auf.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) der Treiber wurde eine ODBC-2. *x* -Treiber und **SQLSetPos** wurde aufgerufen, eine *StatementHandle* nach **SQLFetch** aufgerufen wurde.|  
|HY011|Attribut kann jetzt nicht festgelegt werden|(DM) der Treiber wurde eine ODBC-2. *x* Treiber; die SQL_ATTR_ROW_STATUS_PTR Anweisungsattribut festgelegt wurde, klicken Sie dann **SQLSetPos** wurde aufgerufen, bevor **SQLFetch**, **SQLFetchScroll**, oder **SQLExtendedFetch** aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Die *Vorgang* Argument SQL_UPDATE, ein Datenwert wurde ein null-Zeiger, und der Spaltenwert für die Länge nicht wurde SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA, 0 oder kleiner oder gleich SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Die *Vorgang* Argument war SQL_UPDATE; ein Datenwert war nicht null-Zeiger; wurde von der C-Datentyp SQL_C_BINARY oder SQL_C_CHAR; und der Spaltenwert für die Länge ist kleiner als 0, aber ungleich auf SQL_DATA_AT_EXEC SQL_COLUMN_IGNORE , SQL_NTS oder SQL_NULL_DATA oder kleiner oder gleich SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Der Wert in ein Längen-/Indikatorpuffers wurde SQL_DATA_AT_EXEC; der SQL-Typ wurde entweder SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen Datentyp; und welche Informationen SQL_NEED_LONG_DATA_LEN in **SQLGetInfo** wurde von "Y".|  
|HY092|Ungültiges Attribut-ID|(DM) der angegebene Wert für die *Vorgang* Argument war ungültig.<br /><br /> (DM) der angegebene Wert für die *LockType* Argument war ungültig.<br /><br /> Die *Vorgang* Argument SQL_UPDATE oder SQL_DELETE und das SQL_ATTR_CONCURRENCY-Anweisungsattribut wurde SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Zeilenwert außerhalb des gültigen Bereichs|Der Wert für das Argument angegebene *RowNumber* war größer als die Anzahl der Zeilen im Rowset.|  
|HY109|Ungültige Cursorposition|Der Cursor zugeordnet der *StatementHandle* wurde als Vorwärtscursor, definiert, damit der Cursor innerhalb des Rowsets nicht positioniert werden kann. Siehe die Beschreibung für das SQL_ATTR_CURSOR_TYPE-Attribut in **SQLSetStmtAttr**.<br /><br /> Die *Vorgang* Argument war SQL_UPDATE, SQL_DELETE oder SQL_REFRESH und die Zeile durch die *RowNumber* Argument wurde gelöscht oder nicht abgerufen wurde.<br /><br /> (DM) die *RowNumber* -Argument lautete 0 (null) und die *Vorgang* Argument war SQL_POSITION.<br /><br /> **SQLSetPos** wurde aufgerufen, nachdem **SQLBulkOperations** aufgerufen wurde und bevor **SQLFetchScroll** oder **SQLFetch** aufgerufen wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht den in der angeforderte Vorgang der *Vorgang* Argument oder die *LockType* Argument.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr** mit einer *Attribut* des SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
  
> [!CAUTION]  
>  Für Informationen zu der Anweisung, die besagt **SQLSetPos** in aufgerufen werden kann und er muss für die Kompatibilität mit ODBC 2. führen*.x* -Anwendungen finden Sie unter [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md).  
  
## <a name="rownumber-argument"></a>RowNumber-Argument  
 Die *RowNumber* -Argument gibt die Nummer der Zeile im Rowset für das Ausführen des Vorgangs gemäß den *Vorgang* Argument. Wenn *RowNumber* gleich 0 ist, der Vorgang gilt für jede Zeile im Rowset. *RowNumber* muss ein Wert zwischen 0 und die Anzahl der Zeilen im Rowset.  
  
> [!NOTE]  
>  In der Programmiersprache C Arrays sind 0-basiert und die *RowNumber* Argument ist 1-basiert. Angenommen, um die fünfte Zeile des Rowsets zu aktualisieren, eine Anwendung ändert die Rowset-Puffer Arrayindex 4 gibt jedoch eine *RowNumber* 5.  
  
 Alle Vorgänge positionieren Sie den Cursor in der Zeile, die vom angegebenen *RowNumber*. Die folgenden Vorgänge erfordern eine Cursorposition:  
  
-   Positioniert Update und delete-Anweisungen.  
  
-   Aufrufe von **SQLGetData**.  
  
-   Aufrufe von **SQLSetPos** mit den Optionen SQL_DELETE SQL_REFRESH und SQL_UPDATE auf.  
  
 Z. B. wenn *RowNumber* ist 2 für einen Aufruf **SQLSetPos** mit einer *Vorgang* von SQL_DELETE, befindet sich des Cursors auf der zweiten Zeile des Rowsets und diese Zeile wird gelöscht. Der Eintrag in der Implementierung zeilenstatusarray (verweist das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR) für die zweite Zeile wird in SQL_ROW_DELETED geändert.  
  
 Einer Anwendung angegeben beim Aufrufen eine Cursorposition **SQLSetPos**. Im Allgemeinen, ruft er **SQLSetPos** mit dem Vorgang SQL_POSITION oder SQL_REFRESH zur Positionierung des Cursors vor der Ausführung einer positionierte update oder delete-Anweisung oder Aufrufen **SQLGetData**.  
  
## <a name="operation-argument"></a>Vorgangsargument  
 Die *Vorgang* Argument unterstützt die folgenden Vorgänge. Um zu bestimmen, welche Optionen von einer Datenquelle unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit der SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 oder SQL_STATIC_ CURSOR_ATTRIBUTES1 Informationstyp (je nach Typ des Cursors).  
  
|*Vorgang*<br /><br /> Argument|Vorgang|  
|------------------------------|---------------|  
|SQL_POSITION|Der Treiber setzt den Cursor in der Zeile, angegeben *RowNumber*.<br /><br /> Der Inhalt der zeilenstatusarray verweist das Anweisungsattribut SQL_ATTR_ROW_OPERATION_PTR für die SQL_POSITION ignoriert *Vorgang*.|  
|SQL_REFRESH|Der Treiber setzt den Cursor in der Zeile, angegeben *RowNumber* und aktualisiert Daten in den Puffern Rowset für diese Zeile. Weitere Informationen dazu, wie der Treiber die Daten in den Puffern Rowset zurückgibt, finden Sie in den Beschreibungen, spaltenweise und zeilenweise binden in **SQLBindCol**.<br /><br /> **SQLSetPos** mit einem *Vorgang* von SQL_REFRESH aktualisiert den Status und die Inhalte der Zeilen innerhalb des aktuellen abgerufenen Rowsets. Dies schließt das Lesezeichen zu aktualisieren. Da die Daten in den Puffern aktualisiert jedoch nicht erneut abgerufen wird, ist die Mitgliedschaft des Rowsets fest. Dies unterscheidet sich von der Aktualisierung durchgeführt, die durch einen Aufruf von **SQLFetchScroll** mit eine *FetchOrientation* von SQL_FETCH_RELATIVE und ein *RowNumber* gleich 0 (null) und refetches Das Rowset aus dem Resultset, damit sie zusätzliche Daten anzeigen und entfernen kann gelöschte Daten, wenn diese Vorgänge von der Treiber und der Cursor unterstützt werden.<br /><br /> Eine erfolgreiche Aktualisierung mit **SQLSetPos** ändert sich nicht auf die Zeilenstatus SQL_ROW_DELETED. Gelöschte Zeilen innerhalb des Rowsets werden weiterhin als bis zum nächsten Abrufvorgang gelöscht markiert werden. Die Zeilen werden an den nächsten Abrufvorgang ausgeblendet, wenn der Cursor eine Komprimierung unterstützt (in dem eine nachfolgende **SQLFetch** oder **SQLFetchScroll** keinen gelöschte Zeilen zurückgibt).<br /><br /> Zeilen werden nicht angezeigt, wenn eine Aktualisierung mit hinzugefügt **SQLSetPos** erfolgt. Dieses Verhalten unterscheidet sich von **SQLFetchScroll** mit einem *FetchType* von SQL_FETCH_RELATIVE und ein *RowNumber* gleich 0 (null) und das aktuelle Rowset wird jedoch auch aktualisiert hinzugefügte Datensätze anzeigen oder gelöschte Datensätze pack, falls diese Vorgänge werden vom Cursor unterstützt.<br /><br /> Eine erfolgreiche Aktualisierung mit **SQLSetPos** ändert sich Zeilenstatus SQL_ROW_ADDED auf SQL_ROW_SUCCESS (sofern die zeilenstatusarray vorhanden ist).<br /><br /> Eine erfolgreiche Aktualisierung mit **SQLSetPos** ändert sich Zeilenstatus SQL_ROW_UPDATED in den neuen Status der Zeile (sofern die zeilenstatusarray vorhanden ist).<br /><br /> Im Falle ein Fehlers eine **SQLSetPos** -Operation für eine Zeile, der Zeilenstatus festgelegt, SQL_ROW_ERROR (wenn die zeilenstatusarray vorhanden ist).<br /><br /> Für einen Cursor geöffnet, mit einer SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_ROWVER oder SQL_CONCUR_VALUES, eine Aktualisierung mit **SQLSetPos** möglicherweise aktualisieren Sie die vollständige Parallelität-Werte, die von der Datenquelle verwendet, um zu erkennen, die die Zeile hat sich geändert. In diesem Fall werden die Zeilenversionen oder Werte, die verwendet werden, um sicherzustellen, dass Cursorparallelität aktualisiert, sobald die Rowset-Puffer vom Server aktualisiert werden. Dies tritt auf, für jede Zeile, die aktualisiert werden.<br /><br /> Der Inhalt der zeilenstatusarray verweist das Anweisungsattribut SQL_ATTR_ROW_OPERATION_PTR für die SQL_REFRESH ignoriert *Vorgang*.|  
|SQL_UPDATE|Der Treiber setzt den Cursor in der Zeile, angegeben *RowNumber* und aktualisiert die zugrunde liegenden Zeile der Daten mit den Werten in den Puffern Rowset (das *TargetValuePtr* Argument in ** SQLBindCol**). Ruft die Länge der Daten aus den Längenindikator/Puffern ab (der *StrLen_or_IndPtr* Argument in **SQLBindCol**). Wenn die Länge einer beliebigen Spalte SQL_COLUMN_IGNORE ist, wird die Spalte nicht aktualisiert werden. Nach dem Aktualisieren der Zeile, ändert der Treiber das entsprechende Element des Arrays Status Zeile SQL_ROW_UPDATED oder SQL_ROW_SUCCESS_WITH_INFO an (sofern die zeilenstatusarray vorhanden ist).<br /><br /> Es ist treiberdefinierten, welches Verhalten wird Wenn **SQLSetPos** mit einer *Vorgang* SQL_UPDATE Argument für einen Cursor, enthält doppelte Spalten, aufgerufen wird. Der Treiber kann ein SQLSTATE treiberdefinierten zurückgeben, können aktualisieren Sie die erste Spalte, die im Resultset angezeigt wird oder andere treiberdefinierten Verhalten führen.<br /><br /> Die Zeile Operation-Array verweist das Anweisungsattribut SQL_ATTR_ROW_OPERATION_PTR kann verwendet werden, um anzugeben, dass eine Zeile im aktuellen Rowset während eines Massenupdates ignoriert werden sollen. Weitere Informationen finden Sie unter "Status und Vorgang Arrays" weiter unten in diesem Funktionsverweis.|  
|SQL_DELETE|Der Treiber setzt den Cursor in der Zeile, angegeben *RowNumber* und löscht die zugrunde liegenden Zeile der Daten. Das entsprechende Element des Arrays Zeile Status SQL_ROW_DELETED geändert. Nachdem die Zeile gelöscht wurde, sind die folgenden nicht gültig für die Zeile: positioniert Update und delete-Anweisungen, Aufrufe von **SQLGetData**, und Aufrufe von **SQLSetPos** mit *Vorgang* gruppenfilterausdrücken SQL_POSITION festgelegt. Treiber, die eine Komprimierung zu unterstützen, wird die Zeile aus dem Cursor gelöscht, wenn neue Daten aus der Datenquelle abgerufen werden.<br /><br /> Gibt an, ob die Zeile sichtbar bleibt, hängt von den Cursortyp ab. Beispielsweise sind die gelöschte Zeilen für statische und keysetgesteuerte Cursor sichtbar, aber für dynamische Cursor nicht sichtbar.<br /><br /> Die Zeile Operation-Array verweist das Anweisungsattribut SQL_ATTR_ROW_OPERATION_PTR kann verwendet werden, um anzugeben, dass eine Zeile im aktuellen Rowset während einer massenlöschung ignoriert werden sollen. Weitere Informationen finden Sie unter "Status und Vorgang Arrays" weiter unten in diesem Funktionsverweis.|  
  
## <a name="locktype-argument"></a>LockType-Argument  
 Die *LockType* Argument bietet eine Möglichkeit für Anwendungen, um die Parallelität zu steuern. In den meisten Fällen unterstützt Datenquellen, Parallelitätsstufen und Transaktionen unterstützen, nur den SQL_LOCK_NO_CHANGE-Wert, der die *LockType* Argument. Die *LockType* Argument wird im Allgemeinen nur für die Unterstützung dateibasierter verwendet.  
  
 Die *LockType* -Argument gibt die Lock-Zustand der Zeile nach **SQLSetPos** ausgeführt wurde. Wenn der Treiber konnte nicht gesperrt werden die Zeile, die zum Ausführen des angeforderten Vorgangs oder zum Erfüllen der *LockType* Argument SQL_ERROR und SQLSTATE 42000 (Syntaxfehler oder zugriffsverletzung) zurückgegeben.  
  
 Obwohl die *LockType* Argument für eine einzelne Anweisung angegeben wird, die Sperre berechtigt, die gleichen Berechtigungen für alle Anweisungen für die Verbindung. Insbesondere kann eine Sperre, die von einer Anweisung für eine Verbindung abgerufen wurde durch eine andere Anweisung auf die gleiche Verbindung entsperrt werden.  
  
 Eine Zeile gesperrt, bis **SQLSetPos** bleibt gesperrt, bis die Anwendung ruft **SQLSetPos** für die Zeile mit *LockType* SQL_LOCK_UNLOCK oder bis die Anwendung festlegen Aufrufe **SQLFreeHandle** für die Anweisung oder **SQLFreeStmt** mit der Option SQL_CLOSE. Für einen Treiber, die Transaktionen unterstützt, wird eine Zeile durch gesperrt **SQLSetPos** entsperrt wird, wenn die Anwendung aufruft, **SQLEndTran** , einen commit oder Rollback für eine Transaktion für die Verbindung (falls ein Cursor geschlossen wird Wenn eine Transaktion wird ein Commit oder Rollback, durch die zurückgegebene SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR Informationstypen **SQLGetInfo**).  
  
 Die *LockType* Argument unterstützt die folgenden Typen von Sperren. Um zu bestimmen, welche Sperren von einer Datenquelle unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit der SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 oder SQL_STATIC_ CURSOR_ATTRIBUTES1 Informationstyp (je nach Typ des Cursors).  
  
|*LockType* Argument|Sperrtyp|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|Der Treiber oder die Datenquelle wird sichergestellt, dass die Zeile in dem Zustand gesperrt oder entsperrt ist, vor dem **SQLSetPos** aufgerufen wurde. Dieser Wert der *LockType* können Datenquellen, die keine explizite Sperren auf Zeilenebene durch die Verwendung der Sperren erforderlich ist, den aktuellen parallelitätseinstellung Isolationsstufen unterstützen.|  
|SQL_LOCK_EXCLUSIVE|Der Treiber oder die Datenquelle sperrt die Zeile ausschließlich aus. Eine Anweisung auf eine andere Verbindung oder in einer anderen Anwendung kann nicht zum Abrufen von Sperren auf die Zeile verwendet werden.|  
|SQL_LOCK_UNLOCK|Der Treiber oder die Datenquelle entsperrt die Zeile an.|  
  
 Wenn ein Treiber SQL_LOCK_EXCLUSIVE unterstützt jedoch keine SQL_LOCK_UNLOCK, bleibt eine Zeile, die gesperrt wird gesperrt, bis zum Auftreten eines der Funktionsaufrufe, die im vorherigen Absatz beschrieben.  
  
 Wenn ein Treiber SQL_LOCK_EXCLUSIVE unterstützt jedoch keine SQL_LOCK_UNLOCK, eine Zeile, die gesperrt wird bleibt gesperrt bis die Anwendung ruft **SQLFreeHandle** für die Anweisung oder **SQLFreeStmt** mit die SQL_CLOSE-Option. Wenn der Treiber Transaktionen unterstützt, und des Cursors schließen nach Commit oder Rollback der Transaktion, ruft die Anwendung **SQLEndTran**.  
  
 Für Update- und Delete-Vorgänge im **SQLSetPos**, die Anwendung verwendet die *LockType* Argument wie folgt:  
  
-   Um zu gewährleisten, dass eine Zeile nicht ändert, nachdem sie abgerufen wurden, ruft die Anwendung **SQLSetPos** mit *Vorgang* SQL_REFRESH festgelegt und *LockType* SQL_LOCK_ festgelegt EXKLUSIVE.  
  
-   Wenn die Anwendung legt *LockType* zu SQL_LOCK_NO_CHANGE, der Treiber wird sichergestellt, dass ein Update- oder Delete-Vorgang erfolgreich ist, nur dann, wenn die Anwendung für das SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_LOCK angegeben.  
  
-   Wenn die Anwendung für das SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_ROWVER oder SQL_CONCUR_VALUES angegeben ist, wird der Treiber Zeilenversionen oder Werte vergleicht, und lehnt den Vorgang ab, wenn die Zeile geändert wurde, seit die Anwendung die Zeile abgerufen.  
  
-   Wenn die Anwendung für das SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_READ_ONLY angegeben ist, wird der Treiber ein Update abgelehnt oder Löschvorgang.  
  
 Weitere Informationen über das SQL_ATTR_CONCURRENCY-Anweisungsattribut finden Sie unter [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Status und Vorgang Arrays  
 Die folgenden Status und den Betrieb Arrays werden verwendet, wenn Aufrufen **SQLSetPos**:  
  
-   Die zeilenstatusarray (wie das Feld SQL_DESC_ARRAY_STATUS_PTR in IRD und SQL_ATTR_ROW_STATUS_ARRAY-Anweisungsattribut auf verweist) enthält die Statuswerte für jede Zeile der Daten im Rowset. Der Treiber setzt die Statuswerte in diesem Array nach einem Aufruf von **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, oder **SQLSetPos** . Dieses Array wird durch das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR verwiesen.  
  
-   Das Array der Zeile-Vorgang (wie das SQL_DESC_ARRAY_STATUS_PTR-Feld in der ARD und SQL_ATTR_ROW_OPERATION_ARRAY-Anweisungsattribut auf verweist) enthält einen Wert für jede Zeile im Rowset, der angibt, ob ein Aufruf von **SQLSetPos**für ein Massenvorgang ignoriert oder ausgeführt wird. Jedes Element im Array wird auf SQL_ROW_PROCEED (Standard) oder SQL_ROW_IGNORE festgelegt. Dieses Array wird durch das Anweisungsattribut SQL_ATTR_ROW_OPERATION_PTR verwiesen.  
  
 Die Anzahl der Elemente in den Arrays Status und der Vorgang muss die Anzahl der Zeilen im Rowset (gemäß dem SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut) gleich.  
  
 Informationen zu den zeilenstatusarray finden Sie unter [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Informationen zu der Zeile Operation-Array finden Sie unter "Wird ignoriert, eine Zeile in einer Massenvorgänge" weiter unten in diesem Abschnitt.  
  
## <a name="using-sqlsetpos"></a>SQLSetPos verwenden  
 Bevor eine Anwendung ruft **SQLSetPos**, müssen sie die folgende Sequenz von Schritten ausführen:  
  
1.  Wenn die Anwendung aufruft **SQLSetPos** mit *Vorgang* SQL_UPDATE Aufruf festgelegt **SQLBindCol** (oder **SQLSetDescRec**) für die einzelnen Spalte, geben Sie die Angabe des Datentyps und Puffer für Daten- und die Länge der Spaltenwerts zu binden.  
  
2.  Wenn die Anwendung aufruft **SQLSetPos** mit *Vorgang* auf SQL_DELETE oder SQL_UPDATE Aufruf festgelegt **SQLColAttribute** sicherstellen, dass die Spalten, gelöscht oder aktualisiert werden soll können aktualisiert werden.  
  
3.  Rufen Sie **SQLExecDirect**, **SQLExecute**, oder eine Katalogfunktion auf ein Resultset zu erstellen.  
  
4.  Rufen Sie **SQLFetch** oder **SQLFetchScroll** zum Abrufen der Daten.  
  
 Weitere Informationen zur Verwendung von **SQLSetPos**, finden Sie unter [Aktualisieren von Daten mit SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Löschen von Daten mit SQLSetPos  
 Zum Löschen von Daten mit **SQLSetPos**, eine Anwendung ruft **SQLSetPos** mit *RowNumber* auf die Nummer der Zeile festgelegt, um das Löschen und *Vorgang*auf SQL_DELETE festgelegt.  
  
 Nachdem die Daten gelöscht wurde, ändert der Treiber den Wert in der Implementierung zeilenstatusarray für die entsprechende Zeile in SQL_ROW_DELETED (oder SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Aktualisieren von Daten mit SQLSetPos  
 Eine Anwendung kann den Wert für eine Spalte übergeben, in den gebundenen Datenpuffer oder durch eine oder mehrere Aufrufe von **SQLPutData**. Spalten, deren Daten mit übergeben werden **SQLPutData** als bekanntermaßen *Data-at-Execution-* *Spalten*. Diese werden häufig zum Senden von Daten für Spalten SQL_LONGVARBINARY und SQL_LONGVARCHAR verwendet und können mit anderen Spalten kombiniert werden.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Um Daten mit SQLSetPos, eine Anwendung zu aktualisieren:  
  
1.  Stellen Werte in den Daten und Längenindikator/Puffern mit gebundenen **SQLBindCol**:  
  
    -   Für normale Spalten platziert die Anwendung den neue Spaltenwert in der * \*TargetValuePtr* Puffer und die Länge des Werts in der * \*StrLen_or_IndPtr* Puffer. Wenn die Zeile nicht aktualisiert werden sollen, wird die Anwendung SQL_ROW_IGNORE in dieser Zeile relevant-Element des Arrays Vorgang Zeile an.  
  
    -   Für Data-at-Execution-Spalten wird die Anwendung einen anwendungsdefinierten Wert, z. B. die Spaltennummer in der * \*TargetValuePtr* Puffer. Der Wert kann später verwendet werden, um die Spalte zu identifizieren.  
  
         Die Anwendung gibt das Ergebnis von der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro in den **StrLen_or_IndPtr* Puffer. Wenn der SQL-Datentyp der Spalte SQL_LONGVARBINARY, SQL_LONGVARCHAR oder einem long-Daten datenquellenspezifischen-Datentyp und der Treiber "Y" für den Informationstyp SQL_NEED_LONG_DATA_LEN in gibt **SQLGetInfo**, *Länge * ist die Anzahl der Bytes der Daten für den Parameter; gesendet werden sollen, andernfalls muss er einen nicht negativen Wert und wird ignoriert.  
  
2.  Aufrufe **SQLSetPos** mit der *Vorgang* Argument, die auf SQL_UPDATE auf festgelegt ist, um die Zeile der Daten zu aktualisieren.  
  
    -   Wenn keine Data-at-Execution-Spalten vorhanden sind, ist der Prozess abgeschlossen.  
  
    -   Wenn Data-at-Execution-Spalten vorhanden sind, wird die Funktion wird SQL_NEED_DATA zurückgegeben, und mit Schritt 3 fortgesetzt wird.  
  
3.  Aufrufe **SQLParamData** die Adresse des abzurufenden der * \*TargetValuePtr* Puffer für die erste Data-at-Execution-Spalte verarbeitet werden. **SQLParamData** wird SQL_NEED_DATA zurückgegeben. Die Anwendung ruft den anwendungsdefinierten Wert aus der * \*TargetValuePtr* Puffer.  
  
    > [!NOTE]  
    >  Obwohl Data-at-Execution-Parametern mit Data-at-Execution-Spalten vergleichbar sind, wird der Wert zurückgegeben, durch **SQLParamData** für jedes unterschiedlich ist.  
  
    > [!NOTE]  
    >  Data-at-Execution-Parameter sind Parameter in einer SQL­Anweisung für die Daten werden mit gesendet **SQLPutData** Wenn die Anweisung ausgeführt wird, mit **SQLExecDirect** oder **SQLExecute**. Sie sind mit gebunden **SQLBindParameter** oder durch Festlegen der Deskriptoren mit **SQLSetDescRec**. Der Rückgabewert von **SQLParamData** ist eine 32-Bit-Wert, der an übergebene **SQLBindParameter** in der *ParameterValuePtr* Argument.  
  
    > [!NOTE]  
    >  Data-at-Execution-Spalten in einem Rowset für die Daten mit gesendet werden, sind **SQLPutData** beim Aktualisieren einer Zeile mit **SQLSetPos**. Sie sind mit gebunden **SQLBindCol**. Der Rückgabewert von **SQLParamData** ist die Adresse der Zeile in der **TargetValuePtr* Puffer, die verarbeitet wird.  
  
4.  Aufrufe **SQLPutData** ein- oder mehrmals zum Senden von Daten für die Spalte. Mehr als ein Aufruf ist erforderlich, wenn alle Datenwerte in zurückgegeben werden, können die * \*TargetValuePtr* im angegebenen Puffer **SQLPutData**; mehrere Aufrufe **SQLPutData** für dieselbe Spalte dürfen nur, wenn auf eine Spalte mit einem Zeichen, Binary oder Daten datenquellenspezifischen Datentyp Zeichendaten C senden, oder beim Senden von Binärdaten C an eine Spalte mit einem Zeichen, binary, oder geben Sie die Datenquelle spezifischen Daten.  
  
5.  Aufrufe **SQLParamData** erneut aus, um zu signalisieren, dass alle Daten für die Spalte gesendet wurde.  
  
    -   Wenn weitere Data-at-Execution-Spalten vorhanden sind **SQLParamData** gibt SQL_NEED_DATA sowie die Adresse der *TargetValuePtr* Puffer für die nächste Data-at-Execution-Spalte verarbeitet werden. Die Anwendung wiederholt die Schritte 4 und 5.  
  
    -   Wenn keine weiteren Data-at-Execution-Spalten vorhanden sind, ist der Prozess abgeschlossen. Wenn die Anweisung erfolgreich ausgeführt wurde **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO; Wenn Fehler bei der Ausführung gibt SQL_ERROR zurück. An diesem Punkt **SQLParamData** zurückgeben kann eine beliebige SQLSTATE, die von zurückgegeben werden kann **SQLSetPos**.  
  
 Wenn Daten aktualisiert wurde, ändert der Treiber den Wert in der Implementierung zeilenstatusarray für die entsprechende Zeile in SQL_ROW_UPDATED an.  
  
 Wenn der Vorgang abgebrochen wird oder ein Fehler, in auftritt **SQLParamData** oder **SQLPutData**nach **SQLSetPos** wird SQL_NEED_DATA zurückgegeben und vor dem Senden von Daten für alle Data-at-Execution-Spalten, die Anwendung kann aufrufen nur **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions **, **SQLParamData**, oder **SQLPutData** für die Anweisung oder die Verbindung mit der Anweisung verknüpft sind. Wenn für die Anweisung oder die Verbindung mit der Anweisung verknüpfte jede andere Funktion aufgerufen wird, gibt die Funktion SQL_ERROR und SQLSTATE HY010 (Sequenzfehler-Funktion).  
  
 Wenn die Anwendung aufruft, **SQLCancel** während der Treiber für Data-at-Execution-Spalten weiterhin Daten benötigt, bricht der Treiber den Vorgang ab. Die Anwendung kann dann aufrufen **SQLSetPos** erneut Abbrechen hat keine Auswirkungen auf die Cursor-Status oder der aktuellen Cursorposition.  
  
 Wenn die SELECT-Liste der Query-Spezifikation, die dem Cursor zugeordnet mehr als einen Verweis auf die gleiche Spalte enthält, ob ein Fehler generiert wird, oder der Treiber die doppelte Verweise ignoriert, und führt die angeforderten Vorgänge ist Treiber definiert ist.  
  
## <a name="performing-bulk-operations"></a>Massenimport  
 Wenn die *RowNumber* Argument gleich 0 ist, der Treiber führt den Vorgang angegeben sein, der *Vorgang* Argument für jede Zeile im Rowset, das einen Wert SQL_ROW_PROCEED im Feld "" in der Zeile Vorgang Array verweist SQL_ATTR_ROW_OPERATION_PTR-Anweisungsattribut. Dies ist ein gültiger Wert von der *RowNumber* Argument für ein *Vorgang* Argument SQL_DELETE, SQL_REFRESH, oder SQL_UPDATE, aber nicht SQL_POSITION. **SQLSetPos** mit einer *Vorgang* von SQL_POSITION und ein *RowNumber* SQLSTATE HY109 gleich 0 zurück (ungültige Cursorposition).  
  
 Wenn ein Fehler auftritt, bezieht sich auf das gesamte Rowset, z. B. SQLSTATE HYT00 (Timeout ist abgelaufen), gibt der Treiber SQL_ERROR zurück, und die entsprechenden SQLSTATE-Code. Der Inhalt der Rowset-Puffer ist nicht definiert, und die Cursorposition bleibt unverändert.  
  
 Wenn ein Fehler auftritt, bezieht sich auf eine einzelne Zeile und den Treiber ein:  
  
-   Legt das Element für die Zeile in der zeilenstatusarray verweist das SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut auf SQL_ROW_ERROR fest.  
  
-   Sendet eine oder mehrere zusätzliche SQLSTATEs für den Fehler in der Fehlerwarteschlange und setzt das SQL_DIAG_ROW_NUMBER-Feld in der Struktur diagnostische Daten.  
  
 Nachdem sie the erroder oder Warning, verarbeitet, wenn der Treiber den Vorgang für die verbleibenden Zeilen im Rowset abgeschlossen wird, wird SQL_SUCCESS_WITH_INFO zurückgegeben. Daher enthält die Fehlerwarteschlange für jede Zeile, die einen Fehler zurückgegeben, NULL oder mehr zusätzliche SQLSTATEs. Wenn der Treiber den Vorgang beendet, nachdem sie den Fehler oder die Warnung verarbeitet wurde, wird SQL_ERROR zurückgegeben.  
  
 Wenn der Treiber alle Warnungen, z. B. SQLSTATE 01004 (Daten abgeschnitten) zurückgibt, wird der Warnungen, die auf das gesamte Rowset oder unbekannten Zeilen im Rowset anwenden, bevor die Fehlerinformationen zurückgegeben, die für bestimmte Zeilen gilt zurückgegeben. Warnungen für bestimmte Zeilen zusammen mit allen anderen Fehlerinformationen über die Zeilen zurückgegeben.  
  
 Wenn *RowNumber* gleich 0 und *Vorgang* SQL_UPDATE, SQL_REFRESH oder SQL_DELETE, ist die Anzahl von Zeilen, die **SQLSetPos** arbeitet auf verweist das SQL_ATTR_ROWS _FETCHED_PTR-Anweisungsattribut.  
  
 Wenn *RowNumber* gleich 0 und *Vorgang* ist SQL_DELETE, SQL_REFRESH oder SQL_UPDATE auf, die aktuelle Zeile, wenn der Vorgang identisch mit der aktuellen Zeile, bevor Sie den Vorgang ist.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Eine Zeile in einem Massenvorgang ignoriert  
 Die Zeile Operation-Array kann verwendet werden, um anzugeben, dass eine Zeile im aktuellen Rowset bei einem Vorgang mithilfe ignoriert werden sollen **SQLSetPos**. Um den Treiber, um eine oder mehrere Zeilen zu ignorieren, während eines Massenvorgangs zu leiten, sollte eine Anwendung die folgenden Schritte ausführen:  
  
1.  Rufen Sie **SQLSetStmtAttr** beim Festlegen des Attributs SQL_ATTR_ROW_OPERATION_PTR-Anweisung, um auf ein Array von SQLUSMALLINTs zu verweisen. Dieses Feld kann auch festgelegt werden, durch den Aufruf **SQLSetDescField** festzulegende das Headerfeld SQL_DESC_ARRAY_STATUS_PTR ARD, der erfordert, dass eine Anwendung die Deskriptorhandles erhält.  
  
2.  Jedes Element des Arrays Vorgang Zeile auf einen von zwei Werten festgelegt:  
  
    -   SQL_ROW_IGNORE, um anzugeben, dass die Zeile für Massenvorgänge ausgeschlossen ist.  
  
    -   SQL_ROW_PROCEED, um anzugeben, dass die Zeile in der Massenvorgang enthalten ist. (Dies ist der Standardwert.)  
  
3.  Rufen Sie **SQLSetPos** Massenvorgangs ausführen.  
  
 Die folgenden Regeln gelten für die Zeile Operation-Array:  
  
-   SQL_ROW_IGNORE und SQL_ROW_PROCEED beeinflussen nur mithilfe von Massenvorgängen **SQLSetPos** mit einem *Vorgang* SQL_DELETE oder SQL_UPDATE auf. Sie haben keine Auswirkungen auf Aufrufe **SQLSetPos** mit einer *Vorgang* SQL_REFRESH oder SQL_POSITION.  
  
-   Der Zeiger festgelegt ist standardmäßig auf null.  
  
-   Wenn der Zeiger null ist, werden alle Zeilen aktualisiert, als ob alle Elemente auf SQL_ROW_PROCEED festgelegt wurden.  
  
-   Wenn ein Element auf SQL_ROW_PROCEED garantiert nicht, dass der Vorgang in einer bestimmten Zeile wiederholt werden soll. Z. B. wenn eine bestimmte Zeile im Rowset den Status SQL_ROW_ERROR hat, der Treiber möglicherweise nicht zum Aktualisieren dieser Zeile unabhängig davon, ob die Anwendung SQL_ROW_PROCEED angegeben. Eine Anwendung muss überprüfen Sie immer die zeilenstatusarray, um festzustellen, ob der Vorgang erfolgreich war.  
  
-   SQL_ROW_PROCEED ist als 0 in der Headerdatei definiert. Eine Anwendung kann die Zeile Operation-Array auf 0 initialisiert werden, um alle Zeilen zu verarbeiten.  
  
-   Wenn das Element Anzahl "n" in der Zeile Operation-Array SQL_ROW_IGNORE festgelegt ist und **SQLSetPos** wird aufgerufen, um das Ausführen eines Massenupdates oder Löschvorgang, der n-te Zeile in das Rowset bleibt unverändert, nach dem Aufruf von **SQLSetPos**.  
  
-   Eine Anwendung sollte automatisch eine schreibgeschützte Spalte auf SQL_ROW_IGNORE festgelegt.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Eine Spalte in einem Massenvorgang ignorieren  
 Um dies führte zu unnötigem-Diagnose generiert durch versuchten Updates auf eine oder mehrere schreibgeschützte Spalten zu vermeiden, kann eine Anwendung den Wert in der gebundenen Längen-/Indikatorpuffers auf SQL_COLUMN_IGNORE festlegen. Weitere Informationen finden Sie unter [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel ermöglicht einer Anwendung einen Benutzer die ORDERS-Tabelle durchsuchen und Aktualisieren des Auftragsstatus. Der Cursor wird mit einer Rowsetgröße von 20 keysetgesteuerte und Steuerung durch vollständige Parallelität, die Zeilenversionen Vergleich verwendet. Nach jedem Rowset abgerufen wird, wird die Anwendung wird ausgegeben, und ermöglicht es dem Benutzer auswählen und aktualisieren den Status eines Auftrags. Die Anwendung verwendet **SQLSetPos** zur Positionierung des Cursors auf die ausgewählte Zeile und führt ein positioniertes Update der Zeile. (Die Fehlerbehandlung wird aus Gründen der Übersichtlichkeit weggelassen.)  
  
```  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 Weitere Beispiele finden Sie unter [positioniert Update- und Delete-Anweisungen](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) und [Aktualisieren von Zeilen im Rowset mit SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ausführen von Massenvorgängen, die nicht auf die Cursorposition Block beziehen|[SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Ein einzelnes Datenfeld ein Deskriptor abrufen|[SQLGetDescField-Funktion](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Abrufen von mehreren Feldern einen Deskriptor|[SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Ein Deskriptor, der ein einzelnes Datenfeld festlegen|[SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Ein Deskriptor, der mehrere Felder festlegen|[SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

