---
title: SQLCancel-Funktion | Microsoft Docs
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
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 262622d1131bab843375794f383a39f9ac5e017a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcancel-function"></a>SQLCancel-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLCancel** bricht die Verarbeitung in einer Anweisung ab.  
  
 Verwenden Sie zum Abbrechen der Verarbeitung einer Verbindung oder einer Anweisung [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLCancel** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLCancel** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) im Argument  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLCancel** Funktion aufgerufen wurde.<br /><br /> (DM) aufgrund ein asynchrones Vorgangs auf ein Verbindungshandle ausgeführt wird, die mit zugeordnetem Abbruchvorgang *StatementHandle*.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY018|"Abbrechen"-Anforderung wurde vom Server abgelehnt|Der Server abgelehnt, die Anforderung "Abbrechen".|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 **SQLCancel** können die folgenden Typen von Verarbeitung in einer Anweisung Abbrechen:  
  
-   Eine Funktion, die asynchron ausgeführt, bei der Anweisung an.  
  
-   Eine Funktion in einer Anweisung, die Daten benötigt.  
  
-   Eine Funktion, die bei der Anweisung in einem anderen Thread ausgeführt wird.  
  
 In ODBC 2. *x*, wenn eine Anwendung ruft **SQLCancel** Wenn bei der Anweisung, keine Verarbeitung erfolgt **SQLCancel** hat dieselbe Wirkung wie das **SQLFreeStmt** mit der Option SQL_CLOSE; Dieses Verhalten wird nur der Vollständigkeit halber definiert und Anwendungen sollten Aufrufen **SQLFreeStmt** oder **SQLCloseCursor** um Cursor zu schließen.  
  
 Wenn **SQLCancel** wird aufgerufen, um eine Funktion, die asynchrone Ausführung in einer Anweisung oder eine Funktion in einer Anweisung, dass Anforderungen Daten DiagnoseDatensätze veröffentlicht, die von der Funktion, die abgebrochen wird, deaktiviert sind, Abbrechen und **SQLCancel**  sendet einen eigenen DiagnoseDatensätze; Wenn **SQLCancel** wird aufgerufen, um eine Funktion, die auf eine Anweisung in einem anderen Thread ausgeführt wird "Abbrechen", ist jedoch nicht die Diagnose deaktivieren Datensätze des umzuwandelnden abgebrochen-Funktion, jedoch nicht Senden Sie eine eigene DiagnoseDatensätze.  
  
## <a name="canceling-asynchronous-processing"></a>Asynchronen Verarbeitung Abbrechen  
 Nachdem eine Anwendung asynchron eine Funktion aufruft, ruft er die Funktion wiederholt ausführen, um zu bestimmen, ob die Verarbeitung abgeschlossen wurde. Wenn die Funktion noch verarbeitet wird, gibt es SQL_STILL_EXECUTING zurück. Wenn die Funktion verarbeitet wurde, wird einen anderen Code zurückgegeben.  
  
 Nach dem Aufrufen der Funktion, die SQL_STILL_EXECUTING zurückgibt, kann eine Anwendung aufrufen **SQLCancel** an die Funktion "Abbrechen". Der Treiber gibt SQL_SUCCESS zurück, wenn die abbruchanforderung erfolgreich ist, befindet. Diese Meldung, nicht dass die Funktion tatsächlich abgebrochen wurde; Er gibt an, dass beim Verarbeiten der Anforderung "Abbrechen". Ist Treiber abhängiges und datenquellenabhängig, wann bzw. ob die Funktion tatsächlich abgebrochen wird. Die ursprüngliche Funktion aufrufen, bis der Rückgabecode nicht SQL_STILL_EXECUTING ist, muss die Anwendung weiterhin. Wenn die Funktion erfolgreich abgebrochen wurde, ist der Rückgabecode SQL_ERROR und SQLSTATE HY008 (der Vorgang wurde abgebrochen). Wenn die Funktion die normale Verarbeitung abgeschlossen hat, ist der Rückgabecode SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, wenn die Funktion erfolgreich ausgeführt wurde, SQL_ERROR und ein SQLSTATE als HY008 (der Vorgang wurde abgebrochen.) Wenn der Fehler bei der Funktion.  
  
> [!NOTE]  
>  In ODBC 3.5 verwendet wird, einen Aufruf von **SQLCancel** Wenn keine Verarbeitung auf die Anweisung ausgeführt wird als nicht behandelt wird **SQLFreeStmt** mit der Option SQL_CLOSE, enthält jedoch keine Auswirkung auf allen ist. Um einen Cursor zu schließen, eine Anwendung aufrufen sollte **SQLCloseCursor**, nicht **SQLCancel**.  
  
 Weitere Informationen über die asynchrone Verarbeitung finden Sie unter [asynchrone Ausführung](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Abbrechen von Funktionen, die Daten benötigen.  
 Nach dem **SQLExecute** oder **SQLExecDirect** wird SQL_NEED_DATA zurückgegeben und vor dem Senden von Daten für alle Data-at-Execution-Parameter kann eine Anwendung aufrufen **SQLCancel** um die Ausführung der Anweisung "Abbrechen". Nachdem die Anweisung abgebrochen wurde, kann die Anwendung aufrufen **SQLExecute** oder **SQLExecDirect** erneut aus. Weitere Informationen finden Sie unter [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Nach dem **SQLBulkOperations** oder **SQLSetPos** wird SQL_NEED_DATA zurückgegeben und vor dem Senden von Daten für alle Data-at-Execution-Spalten kann eine Anwendung aufrufen **SQLCancel** um den Vorgang abzubrechen. Nachdem der Vorgang abgebrochen wurde, kann die Anwendung aufrufen **SQLBulkOperations** oder **SQLSetPos** erneut Abbrechen hat keine Auswirkungen auf die Cursor-Status oder der aktuellen Cursorposition. Weitere Informationen finden Sie unter [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) oder [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Abbrechen von Funktionen in einem anderen Thread ausführen  
 In einer multithread-Anwendung kann die Anwendung eine Funktion "Abbrechen", die auf einem anderen Thread ausgeführt wird. Die Funktion, ruft die Anwendung Abbrechen **SQLCancel** mit der gleichen Anweisungshandle, die von der Zielfunktion, aber in einem anderen Thread verwendet. Wie die Funktion abgebrochen wird, hängt von der Treiber und Betriebssystem. Wie durch das Abbrechen einer Funktion, die asynchron ausgeführt wird, den Rückgabecode des ausgeführt der **SQLCancel** gibt nur an, ob der Treiber die Anforderung erfolgreich verarbeitet. Nur SQL_SUCCESS oder SQL_ERROR zurückgegeben werden können. Es wird keine Diagnoseinformationen zurückgegeben. Wenn die ursprüngliche Funktion abgebrochen wird, wird SQL_ERROR und SQLSTATE HY008 (der Vorgang wurde abgebrochen).  
  
 Wenn eine SQL-Anweisung wird ausgeführt, wenn **SQLCancel** aufgerufen wird, in einem anderen Thread zum Abbrechen der anweisungsausführung, es ist möglich, für die Ausführung erfolgreich ausgeführt werden kann und return SQL_SUCCESS zurück, während die "Abbrechen" ist auch erfolgreich ist. In diesem Fall wird der Treiber-Manager davon ausgegangen, dass der Cursor geöffnet wird, durch die anweisungsausführung durch die "Abbrechen", geschlossen wird, damit die Anwendung nicht den Cursor verwenden kann.  
  
 Weitere Informationen zu threading, finden Sie unter [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an einen parameter|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Leistungsfähige Bulk Einfüge- oder Aktualisierungsvorgänge|[SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Bricht eine Funktion, die asynchrone Ausführung für ein Verbindungshandle darüber hinaus an der Funktionalität der **SQLCancel**.|[SQLCancelHandle-Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Freigeben eines Anweisungshandles|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Abrufen von einem Feld ein Diagnosedatensatz oder ein Feld des Diagnose-Headers|[SQLGetDiagField-Funktion](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Abrufen von mehreren Feldern einer Diagnosedaten-Struktur|[SQLGetDiagRec-Funktion](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Den nächsten Parameter zum Senden von Daten für zurückgeben|[SQLParamData-Funktion](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Senden der Parameterdaten zum Zeitpunkt der Ausführung|[SQLPutData-Funktion](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Positionieren den Cursor in einem Rowset, das Aktualisieren von Daten im Rowset aktualisieren oder Löschen von Daten im Resultset|[SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
