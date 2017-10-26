---
title: SQLFreeStmt-Funktion | Microsoft Docs
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
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 929fc50091c914936b5bedfb58bd42c1d07d99ab
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLFreeStmt** beendet die Verarbeitung einer bestimmten Anweisung zugeordneten, schließt alle geöffneten Cursor verknüpft ist, mit der Anweisung, ausstehende Ergebnisse verworfen oder optional alle das Anweisungshandle zugeordnete Ressourcen frei.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle  
  
 *Option*  
 [Eingabe] Einer der folgenden Optionen:  
  
 SQL_ schließen: Schließt den Cursor zugeordnet *StatementHandle* (falls definiert) und verwirft alle ausstehenden Ergebnisse. Die Anwendung kann erneut öffnen dieses Cursors später durch Ausführen einer **wählen** Anweisung erneut mit der gleichen oder unterschiedliche Parameterwerte. Wenn keine Cursor geöffnet ist, wirkt sich diese Option nicht für die Anwendung. **SQLCloseCursor** kann auch aufgerufen werden, um einen Cursor zu schließen. Weitere Informationen finden Sie unter [Schließen des Cursors](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 SQL_DROP: Diese Option ist veraltet. Ein Aufruf von **SQLFreeStmt** mit einer *Option* der SQL_DROP zugeordnet wird, in der Treiber-Manager, um [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
 SQL_UNBIND: Legt das SQL_DESC_COUNT-Feld der ARD auf 0 (null), die Freigabe von Puffern für alle Spalten gebunden **SQLBindCol** für den angegebenen *StatementHandle*. Dies ist nicht die Lesezeichenspalte Bindung; zu diesem Zweck das SQL_DESC_DATA_PTR-Feld der ARD für die Lesezeichenspalte auf NULL festgelegt wird. Beachten Sie, dass wenn dieser Vorgang für einen explizit zugewiesenen Deskriptor ausgeführt wird, die von mehr als eine Anweisung gemeinsam verwendet wird, der Vorgang der Bindungen aller Anweisungen auswirkt, die den Deskriptor gemeinsam nutzen. Weitere Informationen finden Sie unter [Übersicht der Ergebnisse ' abrufen ' (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 SQL_RESET_PARAMS: Legt das SQL_DESC_COUNT-Feld der APD auf 0 festlegen, indem alle Parameter-Puffer freigeben **SQLBindParameter** für den angegebenen *StatementHandle*. Wenn Sie diesen Vorgang für einen explizit zugewiesenen Deskriptor ausgeführt wird, die von mehr als eine Anweisung gemeinsam verwendet wird, wirkt sich dieser Vorgang die Bindungen für alle Anweisungen, die den Deskriptor gemeinsam nutzen. Weitere Informationen finden Sie unter [Bindungsparameter](../../../odbc/reference/develop-app/binding-parameters-odbc.md).  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLFreeStmt** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLFreeStmt** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn **SQLFreeStmt** aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion aufgerufen wurde, mit *Option* auf SQL_RESET_PARAMS festgelegt, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY092|Optionstyp außerhalb des gültigen Bereichs|(DM) der Wert für das Argument angegebene *Option* war nicht:<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Aufrufen von **SQLFreeStmt** Option entspricht dem Aufruf mit der SQL_CLOSE **SQLCloseCursor**, außer dass **SQLFreeStmt** mit SQL_CLOSE hat keinen Einfluss auf die Anwendung Wenn kein Cursor für die Anweisung geöffnet ist. Wenn keine Cursor zu öffnen, einen Aufruf von **SQLCloseCursor** SQLSTATE 24000 (Ungültiger Cursorstatus) zurückgegeben.  
  
 Eine Anwendung sollte ein Anweisungshandle nicht verwenden, nachdem dieser freigegeben wurde; der Treiber-Manager überprüft nicht die Gültigkeit eines Handles in einem Funktionsaufruf.  
  
## <a name="example"></a>Beispiel  
 Es ist ein guter Programmierstil, Handles freizugeben. Allerdings enthält der Einfachheit halber im folgende Beispiel keine Code, der freigibt, Handles zugeordnet. Ein Beispiel zum Freigeben des Handles finden Sie unter [SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
```  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Schließen eines Cursors|[SQLCloseCursor-Funktion](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|Ein Handle freigeben|[SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Ein Cursorname festlegen|[SQLSetCursorName-Funktion](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

