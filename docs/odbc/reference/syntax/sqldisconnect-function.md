---
title: SQLDisconnect-Funktion | Microsoft Docs
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
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d210614a32c2dd8190c37777d3ac06a99756156
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqldisconnect-function"></a>SQLDisconnect-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLDisconnect** schließt die Verbindung eines bestimmten Verbindungshandles zugeordnet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLDisconnect** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_DBC und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLDisconnect** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01002|Fehler beim Trennen|Während die Trennung der Verbindung ist ein Fehler aufgetreten. Allerdings war erfolgreich die Trennung der Verbindung ein. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08003|Verbindung nicht geöffnet|(DM) die Verbindung im Argument angegebene *Verbindungshandle* konnte nicht geöffnet werden.|  
|25000|Ungültiger Transaktionsstatus|Es wurde eine Transaktion wird ausgeführt, für die Verbindung, die durch das Argument angegebenen *Verbindungshandle*. Die Transaktion bleibt aktiv.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *Verbindungshandle*. Die Funktion aufgerufen wurde, und vor dem Ausführen von Finshed [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md) aufgerufen wurde, auf die *Verbindungshandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *Verbindungshandle*.<br /><br /> Die Funktion aufgerufen wurde und bevor sie die Ausführung beendet **SQLCancelHandle** aufgerufen wurde, auf die *Verbindungshandle* aus einem anderen Thread in einer multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) hieß eine asynchron ausgeführte Funktion für eine *StatementHandle* zugeordneten der *Verbindungshandle* und wurde noch ausgeführt, wenn **SQLDisconnect** wurde wird aufgerufen.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *Verbindungshandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, eine *StatementHandle*  zugeordneten der *Verbindungshandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle, die auf die Anforderung geantwortet hat, und die Verbindung immer noch aktiv ist. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *Verbindungshandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Wenn eine Anwendung ruft **SQLDisconnect** nach **SQLBrowseConnect** wird SQL_NEED_DATA zurückgegeben und bevor sie einen anderen Rückgabecode zurückgibt, wird der Treiber bricht die Verbindung mit dem Durchsuchen der Prozess ab und gibt zurück die Verbindung mit einem nicht verbundenen Zustand.  
  
 Wenn eine Anwendung ruft **SQLDisconnect** eine unvollständige Transaktion, die dem Verbindungshandle zugeordnet ist, gibt der Treiber SQLSTATE 25000 (Ungültiger Transaktionsstatus), gibt an, dass die Transaktion nicht geändert wurden. und die Verbindung geöffnet ist. Eine unvollständige Transaktion ist eine, die kein Commit oder Rollback mit **SQLEndTran**.  
  
 Wenn eine Anwendung ruft **SQLDisconnect** , bevor sie alle Anweisungen der Verbindung zugeordnete freigegeben hat, der Treiber, nachdem sie erfolgreich eine Verbindung mit der Datenquelle trennt freigegeben diese Anweisungen und alle Deskriptoren, die wurden für die Verbindung explizit zugewiesen. Jedoch, wenn eine oder mehrere der die Anweisungen der Verbindung zugeordnet noch ausgeführt werden asynchron ausgeführt wird, **SQLDisconnect** gibt SQL_ERROR zurück, mit dem Wert SQLSTATE HY010 (Sequenzfehler-Funktion). Darüber hinaus **SQLDisconnect** wird freizugeben, alle zugeordneten Anweisungen und alle Deskriptoren, der explizit für die Verbindung zugewiesen wurde, wenn die Verbindung in einem angehaltenen Zustand ist oder wenn **SQLDisconnect** wurde wurde erfolgreich vom abgebrochen **SQLCancelHandle**.  
  
 Informationen darüber, wie eine Anwendung verwendet **SQLDisconnect**, finden Sie unter [Trennen von einer Datenquelle oder Treiber](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Eine gepoolte Verbindung trennen  
 Wenn Verbindungspooling, für die einer freigegebenen Umgebung aktiviert ist und eine Anwendung ruft **SQLDisconnect** für eine Verbindung in der Umgebung, die Verbindung an den Verbindungspool zurückgegeben und ist weiterhin verfügbar, mit anderen Komponenten verwenden die gleichen freigegebenen Umgebung.  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [Beispiel-ODBC-Anwendung](../../../odbc/reference/sample-odbc-program.md), [SQLBrowseConnect-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), und [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle|[SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle mit einer Zeichenfolge oder ein Dialogfeld Verbindungsdialogfeld|[SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Ausführen eines Commit- oder Rollback-Vorgangs|[SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Freigeben eines Verbindungshandles|[SQLFreeConnect-Funktion](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
