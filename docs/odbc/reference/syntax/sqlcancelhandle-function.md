---
title: SQLCancelHandle Funktion | Microsoft Docs
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
f1_keywords: SQLCancelHandle
helpviewer_keywords: SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3760400f23b558c27cd70a3ecd288171cbd56534
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.8  
  
 Einhaltung von Standards: keine  
  
 Es wird erwartet, dass die meisten ODBC 3.8 (und höher) Treiber dieser Funktion implementiert werden. Wenn ein Treiber einen Aufruf nicht **SQLCancelHandle** mit einer Verbindung zu behandeln, der *behandeln* Parameter SQL_ERROR mit SQLSTATE von IM001 und eine Nachricht zurück "Treiber diese Funktion nicht unterstützt" einen Aufruf um **SQLCancelHandle** mit einer Anweisung zu behandeln, als die *behandeln* Parameter wird zugeordnet zu einem Aufruf von **SQLCancel** vom Treiber-Manager und verarbeitet werden können, wenn der Treiber implementiert **SQLCancel**. Eine Anwendung kann mithilfe **SQLGetFunctions** zu bestimmen, ob ein Treiber unterstützt **SQLCancelHandle**.  
  
 **Zusammenfassung**  
 **SQLCancelHandle** bricht die Verarbeitung einer Verbindung oder einer Anweisung ab. Der Treiber-Manager zugeordnet ist, einen Aufruf von **SQLCancelHandle** zu einem Aufruf von **SQLCancel** Wenn *HandleType* SQL_HANDLE_STMT ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argumente  
 *HandleType*  
 [Eingabe] Der Typ des Handles auf dem Cacel-Verarbeitung. Gültige Werte sind SQL_HANDLE_DBC oder SQL_HANDLE_STMT auf.  
  
 *Handle*  
 [Eingabe] Das Handle für die Verarbeitung abzubrechen.  
  
 Wenn *behandeln* ist kein gültiges Handle von den vom angegebenen Typ *HandleType*, **SQLCancelHandle** gibt SQL_INVALID_HANDLE zurück.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLCancelHandle** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von Behandeln von SQL_HANDLE_STMT auf, und eine Anweisung *behandeln* oder ein *HandleType* SQL_HANDLE_DBC auf, und ein Verbindungshandle *behandeln*.  
  
 Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLCancelHandle** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) im Argument  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|Eine Funktion asynchron ausgeführte und die Anweisung für hieß eines Anweisungshandles, die zugeordnet der *behandeln*, und *HandleType* auf SQL_HANDLE_DBC festgelegt wurde. Die asynchrone-Funktion wurde noch ausgeführt, wenn **SQLCancelHandle** aufgerufen wurde.<br /><br /> (DM) die *HandleType* Argument war SQL_HANDLE_STMT auf, eine asynchron ausgeführte Funktion wurde für das zugeordnete Verbindungshandle; aufgerufen und die Funktion wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** für eines der zugeordneten Anweisungshandles hieß die *behandeln* und *HandleType* auf SQL_HANDLE_DBC festgelegt wird, und die SQL_PARAM_DATA_AVAILABLE zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> **SQLBrowseConnect** wurde aufgerufen, *Verbindungshandle*, und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde vor der Suche nach Prozess abgeschlossen wurde aufgerufen.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|*HandleType* SQL_HANDLE_ENV oder SQL_HANDLE_DESC festgelegt wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber zugeordnete der *behandeln* der Funktion nicht unterstützt.|  
  
 Wenn **SQLCancelHandle** aufgerufen wird und *HandleType* auf SQL_HANDLE_STMT festgelegt wird, können sie alle SQLSTATE, die von der Funktion zurückgegeben werden kann zurückgeben **SQLCancel**.  
  
## <a name="comments"></a>Kommentare  
 Diese Funktion ist vergleichbar mit **SQLCancel** jedoch möglicherweise eine Verbindung oder die Anweisung Handle als einen Parameter anstelle von nur einem Anweisungshandle dauern. Der Treiber-Manager zugeordnet ist, einen Aufruf von **SQLCancelHandle** zu einem Aufruf von **SQLCancel** Wenn *HandleType* SQL_HANDLE_STMT ist. Dadurch können Anwendungen mit **SQLCancelHandle** Anweisung Vorgänge Abbrechen, selbst wenn der Treiber nicht implementiert **SQLCancelHandle**.  
  
 Weitere Informationen zum Abbrechen einer Anweisung Vorgangs finden Sie unter [SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Wenn es sind keine Vorgänge in Bearbeitung auf *behandeln* der Aufruf von **SQLCancelHandle** hat keine Auswirkungen.  
  
 **SQLCancelHandle** für eine Verbindung Handle kann die folgenden Typen von Verarbeitung Abbrechen:  
  
-   Eine Funktion, die asynchron über die Verbindung ausgeführt wird.  
  
-   Eine Funktion, die auf dem Verbindungshandle in einem anderen Thread ausgeführt wird.  
  
 Wenn **SQLCancelHandle** aufgerufen, um eine Funktion, die asynchron ausgeführt, in einer Verbindung, veröffentlicht von Diagnosedatensätzen abzubrechen **SQLCancelHandle** , die zurückgegeben werden, dass Sie den Vorgang angefügt sind abgebrochen. **SQLCancelHandle** keinen zurückgibt DiagnoseDatensätze, allerdings beim Abbrechen einer Funktion, die über eine Verbindung in einem anderen Thread ausgeführt.  
  
 Mit **SQLCancelHandle** auf "Abbrechen" **SQLEndTran** kann die Verbindung im Zustand "angehalten" abgelegt. Weitere Informationen zum Zustand "angehalten", finden Sie unter [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Informationen zur Verwendung von **SQLCancelHandle** in einer Anwendung, die auf einem Windows-Betriebssystem, die älter als Windows 7 bereitgestellt werden, finden Sie unter [Kompatibilitätsmatrix](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Asynchronen Verarbeitung Verbindungsrelevante Abbrechen  
 Wenn eine Funktion SQL_STILL_EXECUTING zurückgibt, kann eine Anwendung aufrufen **SQLCancelHandle** um den Vorgang abzubrechen. Wenn die abbruchanforderung erfolgreich ist **SQLCancelHandle** gibt SQL_SUCCESS zurück. Dies bedeutet nicht, dass die ursprüngliche Funktion abgebrochen wurde. Er gibt an, dass beim Verarbeiten der Anforderung "Abbrechen". Der Treiber und die Datenquelle ermitteln, oder wenn der Vorgang abgebrochen wird. Die ursprüngliche Funktion aufrufen, bis der Rückgabecode nicht SQL_STILL_EXECUTING ist, muss die Anwendung weiterhin. Wenn die ursprüngliche Funktion abgebrochen wurde, ist der Rückgabecode SQL_ERROR und SQLSTATE HY008 (der Vorgang wurde abgebrochen). Wenn die ursprüngliche Funktion die normale Verarbeitung abgeschlossen (nicht abgebrochen wurde), der Rückgabecode wird SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR und ein SQLSTATE als HY008 (der Vorgang wurde abgebrochen), wenn die ursprüngliche Funktion fehlgeschlagen ist.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Abbrechen von Funktionen in einem anderen Thread ausführen  
 In einer multithread-Anwendung kann die Anwendung einen Vorgang abbrechen, der auf einem anderen Thread ausgeführt wird. Abbrechen des Vorgangs, der die Anwendung ruft **SQLCancelHandle** mit dem Handle von der Funktion, sondern in einem anderen Thread verwendet. Der Treiber und Betriebssystem bestimmen, wie der Vorgang abgebrochen wird. Die **SQLCancelHandle** Code gibt an, ob der Treiber die Anforderung verarbeitet, Rückgabe SQL_SUCCESS oder SQL_ERROR (keine Diagnoseinformationen wird zurückgegeben) zurückgeben. Wenn die Verarbeitung auf die ursprüngliche Funktion abgebrochen wird, gibt die ursprüngliche Funktion SQL_ERROR und SQLSTATE HY008 (abgebrochen).  
  
 Wenn eine Funktion wird ausgeführt, wenn **SQLCancelHandle** wird aufgerufen, in einem anderen Thread auf die Funktion "Abbrechen", ist es möglich, dass die Funktion erfolgreich ausgeführt werden und SQL_SUCCESS zurück, bevor der Abbruchvorgang wirksam werden kann. Ein Aufruf von **SQLCancelHandle** hat keine Auswirkung, wenn der Vorgang, bevor Sie abgeschlossen **SQLCancelHandle** konnte den Vorgang abzubrechen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abbrechen von einer Funktion, die asynchron ausgeführt, auf ein Anweisungshandle Abbrechen von einer Funktion in einer Anweisung, die Daten oder das Abbrechen einer Funktion, die auf eine Anweisung in einem anderen Thread ausgeführt wird.|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [Asynchrone Ausführung (Abrufmethode)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
