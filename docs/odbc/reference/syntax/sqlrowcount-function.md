---
title: SQLRowCount-Funktion | Microsoft Docs
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
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04a4e5061a80fec51361e82c57102df8e3fa34c8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlrowcount-function"></a>SQLRowCount-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLRowCount** gibt die Anzahl der betroffenen Zeilen ein **UPDATE**, **einfügen**, oder **löschen** Anweisung; eine SQL_ADD SQL_UPDATE_BY_BOOKMARK oder SQL_ Vorgang DELETE_BY_BOOKMARK **SQLBulkOperations**; oder eines Vorgangs SQL_UPDATE oder SQL_DELETE in **SQLSetPos**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *RowCountPtr*  
 [Ausgabe] Zeigt auf einen Puffer, in dem die Zeilenanzahl zurückgegeben. Für **UPDATE**, **einfügen**, und **löschen** -Anweisungen für die SQL_ADD SQL_UPDATE_BY_BOOKMARK und SQL_DELETE_BY_BOOKMARK Vorgänge in  **SQLBulkOperations**, und für Vorgänge SQL_UPDATE oder SQL_DELETE im **SQLSetPos**, zurückgegebene Wert in **RowCountPtr* ist entweder die Anzahl von betroffenen Zeilen die Anforderung oder – 1, wenn die Anzahl der betroffenen Zeilen nicht verfügbar ist.  
  
 Wenn **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos oder SQLMoreResults** aufgerufen wird, wird die SQL_DIAG_ROW_COUNT -Feld der Struktur Diagnosedaten auf der Anzahl der Zeilen festgelegt ist, und die Anzahl der Zeilen in der Implementierung abhängiges Weise zwischengespeichert ist. **SQLRowCount** gibt den zwischengespeicherten Zeilenanzahlwert zurück. Die zwischengespeicherte Zeilenanzahlwert ist gültig, bis das Anweisungshandle wieder auf den vorbereiteten oder zugeordneten Status festgelegt wird, wird die Anweisung erneut ausgeführt, oder **SQLCloseCursor** aufgerufen wird. Beachten Sie, dass eine Funktion aufgerufen wurde, da das Feld SQL_DIAG_ROW_COUNT festgelegt wurde, der Wert von zurückgegeben **SQLRowCount** möglicherweise ungleich dem Wert im Feld SQL_DIAG_ROW_COUNT Feld SQL_DIAG_ROW_COUNT auf zurückgesetzt wird 0 von einem beliebigen Funktionsaufruf.  
  
 Für andere Anweisungen und Funktionen, kann der Treiber den zurückgegebenen Wert definieren \* *RowCountPtr*. Z. B. möglicherweise einige Datenquellen kann die Anzahl von zurückgegebenen Zeilen zurückgeben einer **wählen** -Anweisung oder eine Katalogfunktion vor dem Abrufen der Zeilen.  
  
> [!NOTE]  
>  Viele Datenquellen können nicht in einem Resultset vor dem Abrufen der sie die Anzahl der Zeilen zurückgegeben. für eine optimale Interoperabilität sollte der Anwendungen nicht auf diesem Verhalten basieren.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLRowCount** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLRowCount** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLRowCount** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß die Funktion vor dem Aufruf **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** für die  *StatementHandle*.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Wenn die letzte SQL-Anweisung, die über das Anweisungshandle ausgeführt, nicht wurde eine **UPDATE**, **einfügen**, oder **löschen** Anweisung oder, wenn die *Vorgang* Argument in den vorhergehenden Aufruf von **SQLBulkOperations** war nicht SQL_ADD, SQL_UPDATE_BY_BOOKMARK oder SQL_DELETE_BY_BOOKMARK, oder wenn die *Vorgang* Argument in den vorhergehenden Aufruf von  **SQLSetPos** war kein SQL_UPDATE und SQL_DELETE, den Wert der **RowCountPtr* Treiber definiert ist. Weitere Informationen finden Sie unter [bestimmen die Anzahl der betroffenen Zeilen](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
