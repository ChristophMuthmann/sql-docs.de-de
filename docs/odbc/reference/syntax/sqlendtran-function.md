---
title: SQLEndTran-Funktion | Microsoft Docs
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
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea99ca26105d3c31330108979a5b182329aa6ba5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlendtran-function"></a>SQLEndTran-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLEndTran** fordert einen Commit- oder Rollback-Vorgang für alle aktiven Vorgänge für alle Anweisungen, die eine Verbindung zugeordnet. **SQLEndTran** können auch anfordern, dass ein Commit oder Rollback-Vorgang für alle Verbindungen, die verknüpft sind mit einer Umgebung ausgeführt werden.  
  
> [!NOTE]  
>  Weitere Informationen zu welcher der Treiber-Manager ordnet diese Funktion auf, wenn eine ODBC 3. *x* Anwendung arbeitet mit einer ODBC 2. *X* -Treiber verwenden, finden Sie unter [Ersatz-Zuordnungsfunktionen für Backward Compatibility Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumente  
 *HandleType*  
 [Eingabe] Typ-ID zu behandeln. Enthält entweder SQL_HANDLE_ENV auf (Wenn *behandeln* ist ein Umgebungshandle) oder SQL_HANDLE_DBC auf (Wenn *behandeln* ist ein Verbindungshandle).  
  
 *Handle*  
 [Eingabe] Das Handle, der vom angegebenen Typ *HandleType*, des Bereichs der Transaktion angibt. Weitere Informationen finden Sie unter "Kommentare".  
  
 *' CompletionType '*  
 [Eingabe] Einer der beiden folgenden Werte:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLEndTran** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit dem entsprechenden *HandleType*und *behandeln*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLEndTran** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08003|Verbindung nicht geöffnet|(DM) die *HandleType* wurde SQL_HANDLE_DBC auf, und die *behandeln* war nicht verbunden.|  
|08007|Verbindungsfehler während der Transaktion|Die *HandleType* SQL_HANDLE_DBC wurde und die Verbindung zugeordnet ist die *behandeln* Fehler während der Ausführung der Funktion, und er darf nicht bestimmt, ob der angeforderte  **COMMIT** oder **ROLLBACK** vor Auftreten des Fehlers aufgetreten sind.|  
|25 S 01|Transaktionsstatus unbekannt|Eine oder mehrere Verbindungen im *behandeln* konnte die Transaktion mit dem angegebenen Ergebnis abgeschlossen wird, und das Ergebnis ist unbekannt.|  
|25S02|Transaktion ist noch aktiv|Der Treiber konnte nicht aus, um sicherzustellen, dass die gesamte Arbeit in der globalen Transaktion automatisch abgeschlossen werden konnte, und die Transaktion ist noch aktiv.|  
|25S03|Transaktion wird ein Rollback ausgeführt.|Der Treiber konnte nicht garantieren, dass alle Arbeiten in der globalen Transaktion automatisch abgeschlossen werden konnte und die gesamte in der Transaktion, die in aktiv Arbeit *behandeln* zurückgesetzt wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund eines Deadlocks Ressource mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40002|Einschränkungsverletzung Integrität|Die *' CompletionType '* wurde SQL_COMMIT, und zwar die Verpflichtung Änderungen einschränkungsverletzung Integrität. Daher wurde die Transaktion ein Rollback ausgeführt.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*SzMessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *Verbindungshandle*. Die Funktion aufgerufen wurde und bevor sie die Ausführung beendet [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md) aufgerufen wurde, auf die *Verbindungshandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *Verbindungshandle*.<br /><br /> Die Funktion aufgerufen wurde und bevor sie die Ausführung beendet **SQLCancelHandle** aufgerufen wurde, auf die *Verbindungshandle* aus einem anderen Thread in einer multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion ein Anweisungshandle zugeordneten hieß die *Verbindungshandle* und wurde noch ausgeführt, wenn **SQLEndTran** aufgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *Verbindungshandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** für ein Anweisungshandle zugeordneten hieß die *Verbindungshandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *behandeln* mit *HandleType* auf SQL_HANDLE_DBC festgelegt und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** hieß für eines der zugeordneten Anweisungshandles *behandeln* und zurückgegebene SQL_PARAM_DATA_AVAILABLE. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY012|Ungültiger Transaktionsvorgangscode|(DM) der Wert für das Argument angegebene *' CompletionType '* war weder SQL_COMMIT noch SQL_ROLLBACK.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|(DM) der Wert für das Argument angegebene *HandleType* war weder SQL_HANDLE_ENV noch SQL_HANDLE_DBC auf.|  
|HY115|SQLEndTran ist für eine Umgebung, die eine Verbindung mit der asynchronen Ausführung aktiviert enthält, nicht zulässig|(DM) *HandleType* kann nicht auf SQL_HANDLE_ENV festgelegt werden, wenn die asynchrone Ausführung Verbindungsfunktionen für eine Verbindung in der Umgebung aktiviert ist.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten", in der in diesem Thema im Abschnitt "Kommentare".|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht die **ROLLBACK** Vorgang.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *Verbindungshandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Für einen ODBC-3. *x* -Treiber verwenden, wenn *HandleType* ist SQL_HANDLE_ENV und *behandeln* der Treiber-Manager aufruft, ist eine gültige Umgebungshandle **SQLEndTran**in jeder Umgebung zugeordneten Treibers untersuchen. Die *behandeln* Argument für den Aufruf von einem Treiber werden Umgebungshandle des Treibers. Für einen ODBC-2. *x* -Treiber verwenden, wenn *HandleType* ist SQL_HANDLE_ENV und *behandeln* ist ein gültiger Umgebungsname-Handle, und es gibt mehrere Verbindungen in dieser Umgebung verbunden der Treiber-Manager aufrufen wird **SQLTransact** im Treiber einmal für jede Verbindung in einem verbundenen Zustand in der Umgebung. Die *behandeln* Argument bei jedem Aufruf werden die Verbindungs-Handle. In beiden Fällen versucht, einen commit oder Rollback für Transaktionen, abhängig vom Wert der Treiber *' CompletionType '*, für alle Verbindungen, die für diese Umgebung verbunden sind. Verbindungen, die nicht aktiv sind, beeinflussen die Transaktion nicht.  
  
> [!NOTE]  
>  **SQLEndTran** kann nicht verwendet werden, um einen commit oder Rollback für Transaktionen auf einer freigegebenen Umgebung. SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner) wird zurückgegeben, wenn **SQLEndTran** aufgerufen wird und *behandeln* entweder das Handle einer freigegebenen Umgebung oder das Handle für eine Verbindung mit einer freigegebenen festlegen Umgebung.  
  
 Der Treiber-Manager gibt SQL_SUCCESS zurück, nur dann, wenn er für jede Verbindung SQL_SUCCESS empfängt. Wenn der Treiber-Manager auf eine oder mehrere Verbindungen SQL_ERROR empfängt, wird SQL_ERROR zurückgegeben, an die Anwendung und die Diagnoseinformationen befindet sich in der Struktur Diagnosedaten der Umgebung. Um zu bestimmen, welche Verbindung oder Verbindungen während der Commit- oder Rollback-Vorgang ist fehlgeschlagen, kann die Anwendung aufrufen **SQLGetDiagRec** für jede Verbindung.  
  
> [!NOTE]  
>  Der Treiber-Manager eine globale Transaktion nicht über alle Verbindungen simulieren und daher nicht Zweiphasen-Commit-Protokolle verwenden.  
  
 Wenn *' CompletionType '* ist SQL_COMMIT, **SQLEndTran** gibt die Anforderung für ein Commit für alle aktiven Vorgänge für jede Anweisung mit einer betroffenen Verbindung verknüpft sind. Wenn *' CompletionType '* ist SQL_ROLLBACK, **SQLEndTran** gibt eine Rollback-Anforderung für alle aktiven Vorgänge für jede Anweisung mit einer betroffenen Verbindung verknüpft sind. Wenn es aktiv ist, keine Transaktionen sind **SQLEndTran** gibt SQL_SUCCESS zurück, hat keine Auswirkungen auf alle Datenquellen. Weitere Informationen finden Sie unter [Committing und parallele Transaktionen](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Wenn der Treiber im Manualcommit Modus (durch Aufrufen **SQLSetConnectAttr** mit der SQL_ATTR_AUTOCOMMIT Attributgruppe auf SQL_AUTOCOMMIT_OFF festlegen), eine neue Transaktion wird implizit gestartet, wenn eine SQL-Anweisung, die im enthalten sein kann eine Transaktion ist für die aktuelle Datenquelle ausgeführt. Weitere Informationen finden Sie unter [Commit-Modus](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Um zu bestimmen, wie Transaktionsvorgänge Cursor auswirken, eine Anwendung ruft **SQLGetInfo** mit den Optionen SQL_CURSOR_ROLLBACK_BEHAVIOR und SQL_CURSOR_COMMIT_BEHAVIOR. Weitere Informationen finden Sie unter den folgenden Abschnitten sowie unter [Auswirkungen von Transaktionen für Cursor und vorbereitete Anweisungen](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Wenn der SQL_CURSOR_ROLLBACK_BEHAVIOR oder SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_DELETE, Wert **SQLEndTran** schließt und löscht alle geöffneten Cursor für alle Anweisungen, die der Verbindung zugeordnet und verwirft alle ausstehenden Ergebnisse. **SQLEndTran** einer beliebigen Anweisung in einem zugeordneten (Vorbereitung) Status; vorhanden bleibt die Anwendung die berichtsteile können sie für nachfolgende SQL-Abfragen oder durch Aufrufen **SQLFreeStmt** oder **SQLFreeHandle** mit eine *HandleType* von SQL_HANDLE_STMT auf, um sie freizugeben.  
  
 Wenn der SQL_CURSOR_ROLLBACK_BEHAVIOR oder SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_CLOSE, Wert **SQLEndTran** schließt alle geöffneten Cursor für alle Anweisungen, die der Verbindung zugeordnet. **SQLEndTran** einer beliebigen Anweisung in einem Status ' vorbereitet '; vorhanden bleibt die Anwendung aufrufen kann **SQLExecute** für eine Anweisung, die die Verbindung erst nach Aufrufen von zugeordnet **SQLPrepare**.  
  
 Wenn der SQL_CURSOR_ROLLBACK_BEHAVIOR oder SQL_CURSOR_COMMIT_BEHAVIOR SQL_CB_PRESERVE, Wert **SQLEndTran** wirkt sich nicht auf die geöffnete Cursor, die der Verbindung zugeordnet. Cursor bleiben in der Zeile, die sie vor dem Aufruf von verweist **SQLEndTran**.  
  
 Für die Treiber und Datenquellen, die Unterstützung von Transaktionen, Aufrufen von **SQLEndTran** mit entweder auf SQL_COMMIT oder SQL_ROLLBACK Wenn keine Transaktion aktiv ist gibt SQL_SUCCESS zurück (bedeutet, dass keine Arbeit ein Commit oder Rollback) und hat keine Auswirkung auf die Datenquelle.  
  
 Wenn ein Treiber im Autocommit-Modus befindet, wird der Treiber-Manager nicht aufrufen **SQLEndTran** im Treiber. **SQLEndTran** immer gibt SQL_SUCCESS zurück, unabhängig davon, ob beim Aufruf einer *' CompletionType '* der SQL_COMMIT oder SQL_ROLLBACK fest.  
  
 Treiber oder Datenquellen, die keine Transaktionen unterstützen (**SQLGetInfo** *Option* SQL_TXN_CAPABLE ist SQL_TC_NONE) effektiv immer im Autocommit-Modus sind und daher stets SQL_SUCCESS für **SQLEndTran** fest, ob sie aufgerufen werden, mit einem *' CompletionType '* der SQL_COMMIT oder SQL_ROLLBACK fest. Solche Treiber und die Datenquellen werden nicht tatsächlich Transaktionen beim dazu zurückgesetzt.  
  
## <a name="suspended-state"></a>Zustand "angehalten"  
 Im Treiber-Manager, die vor Windows 7 veröffentlicht wurden, eine Transaktion aktiv war Wenn **SQLEndTran** SQL_ERROR zurückgegeben, aus dem Treiber. Allerdings war es möglich, dass die Transaktion wurde erfolgreich auf dem Server ausgeführt, aber der Treiber auf dem Client nicht benachrichtigt wurde, (z. B., weil ein Netzwerkfehler aufgetreten ist). Somit gäbe es die Verbindung in einem fehlerhaften Zustand. Ab Windows 7, wenn **SQLEndTran** gibt SQL_ERROR zurück, die Verbindung ist möglicherweise im Zustand "angehalten". In einem angehaltenen Zustand ist es möglich, nur-Lese Funktionen aufrufen. Schließlich wird die Anwendung sollte Aufrufen **SQLDisconnect** auf eine unterbrochene Verbindung mit Ressourcen freizugeben.  
  
 Wenn alle der folgenden Bedingungen erfüllt sind, wird die Verbindung in einem angehaltenen Zustand versetzen:  
  
-   Der Treiber gibt SQL_ERROR aus **SQLEndTran**.  
  
-   Der Treiber ist ODBC 3.8 oder höher.  
  
-   Die Version der Anwendung ist 3.8 oder höher. oder die neu kompilierten ODBC 2.x oder 3.x-Anwendung wurde erfolgreich abgebrochen der **SQLEndTran** Funktion über **SQLCancelHandle**.  
  
-   Der Treiber nicht eine der folgenden Meldungen zurück, die bestätigen, dass die Transaktion nicht abgeschlossen wurde:  
  
    -   25S03: Transaktion ein Rollback  
  
    -   40001: Serialisierungsfehler aufgetreten  
  
    -   40002: integritätseinschränkung  
  
    -   HYC00: Optionales Feature nicht implementiert  
  
 Wenn **SQLEndTran** hieß in einer Umgebung Handle- und seine Verbindungen die oben genannten Bedingungen erfüllt, alle Verbindungen herstellen einer Verbindung mit der gleichen Treiber werden in den Zustand "angehalten" versetzt.  
  
 Nachdem eine Anwendung ruft **SQLDisconnect** auf eine unterbrochene Verbindung die Verbindung verwendet werden kann, eine Verbindung mit einer anderen Datenquelle oder die gleiche Datenquelle herzustellen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abbrechen von einer Funktion, die auf ein Verbindungshandle asynchron ausgeführt wird.|[SQLCancelHandle-Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Zurückgeben von Informationen zu einer Datenquelle oder Treiber|[SQLGetInfo-Funktion](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Ein Handle freigeben|[SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Freigeben eines Anweisungshandles|[SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [Asynchrone Ausführung (Abrufmethode)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
