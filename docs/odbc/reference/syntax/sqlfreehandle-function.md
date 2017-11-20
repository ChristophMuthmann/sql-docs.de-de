---
title: SQLFreeHandle-Funktion | Microsoft Docs
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
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd53996a8107a577cfae703a8f68f036e5ae0eb6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLFreeHandle** gibt eine bestimmte Umgebung, Verbindung, Anweisung oder Deskriptor Handle zugeordneten Ressourcen frei.  
  
> [!NOTE]  
>  Diese Funktion ist eine generische Funktion für die Freigabe des Handles. Er ersetzt die Funktionen der ODBC 2.0 **SQLFreeConnect** (für die Freigabe ein Verbindungshandle) und **SQLFreeEnv** (für die Freigabe ein Umgebungshandle). **SQLFreeConnect** und **SQLFreeEnv** sind in ODBC 3. veraltet*.x*. **SQLFreeHandle** ersetzt auch die ODBC 2.0-Funktion **SQLFreeStmt** (mit der SQL_DROP *Option*) für das Freigeben eines Anweisungshandles. Weitere Informationen finden Sie unter "Kommentare". Weitere Informationen, was der Treiber-Manager diese Funktion auf, wenn eine ODBC 3. ordnet*.x* Anwendung arbeitet mit einer ODBC 2.*.x* -Treiber verwenden, finden Sie unter [Ersatzfunktionen für rückwärts zuordnen Die Kompatibilität der Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>Argumente  
 *HandleType*  
 [Eingabe] Der Typ des Handles von freizugebenden **SQLFreeHandle**. Dabei muss es sich um einen der folgenden Werte sein:  
  
-   SQL_HANDLE_DBC AUF  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV AUF  
  
-   SQL_HANDLE_STMT AUF  
  
 SQL_HANDLE_DBC_INFO_TOKEN Handle wird nur durch das Treiber-Manager und Treiber verwendet. Anwendungen sollten diese Handletyp nicht verwenden. Weitere Informationen zu SQL_HANDLE_DBC_INFO_TOKEN, finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 Wenn *HandleType* ist nicht mit einer dieser Werte **SQLFreeHandle** gibt SQL_INVALID_HANDLE zurück.  
  
 *Handle*  
 [Eingabe] Das Handle freigegeben wird.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
 Wenn **SQLFreeHandle** gibt SQL_ERROR zurück, das Handle ist noch gültig.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLFreeHandle** gibt SQL_ERROR zurück, die einen zugeordneten SQLSTATE-Wert aus der Struktur diagnostische Daten für das Handle abgerufen werden können, **SQLFreeHandle** hat versucht, die frei, jedoch nicht. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLFreeHandle** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY010|Fehler bei Funktionssequenz|(DM) die *HandleType* Argument SQL_HANDLE_ENV und mindestens eine Verbindung wurde in einem reservierten und nicht verbundenen Zustand. **SQLDisconnect** und **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, muss für jede Verbindung vor dem Aufruf aufgerufen werden **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_ENV auf.<br /><br /> (DM) die *HandleType* Argument war SQL_HANDLE_DBC auf, und die Funktion aufgerufen wurde, vor dem Aufruf **SQLDisconnect** für die Verbindung.<br /><br /> (DM) die *HandleType* Argument war SQL_HANDLE_DBC auf. Eine asynchron ausgeführte Funktion aufgerufen wurde *behandeln* und die Funktion wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) die *HandleType* Argument war SQL_HANDLE_STMT auf. **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** mit das Anweisungshandle aufgerufen und SQL_NEED_DATA zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) die *HandleType* Argument war SQL_HANDLE_STMT auf. Eine asynchron ausgeführte Funktion wurde aufgerufen, auf das Anweisungshandle oder das zugeordnete Verbindungshandle, und die Funktion wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) die *HandleType* Argument war SQL_HANDLE_DESC. Eine asynchron ausgeführte Funktion wurde für das zugeordnete Verbindungshandle aufgerufen wird. und die Funktion wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) alle Produktpaket Handles und andere Ressourcen nicht freigegeben wurden vor dem **SQLFreeHandle** aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** für eines der zugeordneten Anweisungshandles hieß die *behandeln* und *HandleType* auf SQL_HANDLE_STMT festgelegt wurde oder SQL_HANDLE_DESC SQL_PARAM_DATA_AVAILABLE zurückgegeben wird. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Die *HandleType* Argument war SQL_HANDLE_STMT oder SQL_HANDLE_DESC und Aufruf der Funktion konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY017|Ungültige Verwendung eines automatisch zugeordneten Deskriptorhandles.|(DM) die *behandeln* Argument wurde an das Handle für einen automatisch zugewiesenen Deskriptor festgelegt.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) die *HandleType* Argument SQL_HANDLE_DESC und der Treiber wurde eine ODBC 2.*.x* Treiber.<br /><br /> (DM) die *HandleType* Argument SQL_HANDLE_STMT auf, und der Treiber nicht wurde eine gültige ODBC-Treiber.|  
  
## <a name="comments"></a>Kommentare  
 **SQLFreeHandle** dient zum Freigeben des Handles für Umgebungen, Verbindungen, Anweisungen und Deskriptoren, wie in den folgenden Abschnitten beschrieben. Allgemeine Informationen zu Handles finden Sie unter [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Ein Handle sollte von einer Anwendung nicht verwendet werden, nachdem dieser freigegeben wurde. der Treiber-Manager überprüft nicht die Gültigkeit eines Handles in einem Funktionsaufruf.  
  
## <a name="freeing-an-environment-handle"></a>Ein Umgebungshandle freigeben  
 Vor dem Aufrufen **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, muss eine Anwendung aufrufen **SQLFreeHandle** mit einem *HandleType*SQL_HANDLE_DBC auf, für alle Verbindungen, die unter der Umgebung zugeordnet. Andernfalls, den Aufruf von **SQLFreeHandle** gibt SQL_ERROR und die Umgebung und alle aktiven Verbindungen bleibt gültig. Weitere Informationen finden Sie unter [Umgebung behandelt](../../../odbc/reference/develop-app/environment-handles.md) und [Reservieren der Umgebung behandelt](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Wenn die Umgebung auf einer freigegebenen Umgebung ist, ruft die Anwendung, die **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, nicht mehr hat Zugriff auf die Umgebung nach dem Aufruf, sondern der Umgebung Ressourcen sind nicht unbedingt freigegeben. Der Aufruf von **SQLFreeHandle** dekrementiert den Verweiszähler der Umgebung. Der Verweiszähler wird vom Treiber-Manager verwaltet. Wenn es nicht 0 (null) erreicht, wird die freigegebene Umgebung nicht freigegeben, da er noch von einer anderen Komponente verwendet wird. Wenn der Verweiszähler auf 0 (null) erreicht, werden die Ressourcen der freigegebenen Umgebung freigegeben.  
  
## <a name="freeing-a-connection-handle"></a>Freigeben eines Verbindungshandles  
 Vor dem Aufrufen **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, muss eine Anwendung aufrufen **SQLDisconnect** für die Verbindung, wenn eine Verbindung zu diesem vorhanden ist behandeln*.* Andernfalls, den Aufruf von **SQLFreeHandle** gibt SQL_ERROR zurück, und die Verbindung bleibt gültig.  
  
 Weitere Informationen finden Sie unter [Verbindungshandles](../../../odbc/reference/develop-app/connection-handles.md) und [Trennen von einer Datenquelle oder Treiber](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="freeing-a-statement-handle"></a>Freigeben eines Anweisungshandles  
 Ein Aufruf von **SQLFreeHandle** mit einer *HandleType* von SQL_HANDLE_STMT auf alle Ressourcen, die durch einen Aufruf von zugewiesen wurden freigegeben **SQLAllocHandle** mit einer  *HandleType* von SQL_HANDLE_STMT auf. Wenn eine Anwendung ruft **SQLFreeHandle** um eine Anweisung freizugeben, die Ergebnisse ausstehen, die ausstehende Ergebnisse gelöscht werden. Wenn eine Anwendung ein Anweisungshandle frei, gibt der Treiber die vier automatisch zugeordneten Deskriptoren dieser Handle zugeordneten frei. Weitere Informationen finden Sie unter [Anweisung verarbeitet](../../../odbc/reference/develop-app/statement-handles.md) und [Freigabe ein Anweisungshandle](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 Beachten Sie, dass **SQLDisconnect** löscht automatisch alle Anweisungen und Deskriptoren öffnen, für die Verbindung.  
  
## <a name="freeing-a-descriptor-handle"></a>Ein Deskriptor-Handle freigeben  
 Ein Aufruf von **SQLFreeHandle** mit einer *HandleType* der SQL_HANDLE_DESC freigegeben die Deskriptorhandles in *behandeln*. Der Aufruf von **SQLFreeHandle** aufgehoben wird von der Anwendung, die kein Zeigerfeld (einschließlich SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR) verwiesen werden möglicherweise zugewiesener Speicher eines beliebigen anwendungsparameterdeskriptor-Datensatz des *behandeln*. Vom Treiber für Felder, die keine Zeiger Felder sind zugewiesene Arbeitsspeicher wird freigegeben, wenn das Handle freigegeben wird. Wenn ein Benutzer zugeordneten Deskriptorhandles freigegeben wird, werden alle Anweisungen, denen das Handle freigegebene mit zugeordnet war, ihre jeweiligen automatisch zugeordneten Deskriptorhandles wieder.  
  
> [!NOTE]  
>  ODBC 2.*.x* Treiber unterstützen keine freigebenden Deskriptorhandles, wie sie beim Zuordnen von Deskriptorhandles nicht unterstützen.  
  
 Beachten Sie, dass **SQLDisconnect** löscht automatisch alle Anweisungen und Deskriptoren öffnen, für die Verbindung. Wenn eine Anwendung ein Anweisungshandle frei, gibt der Treiber alle automatisch generierten Deskriptoren dieser Handle zugeordneten frei.  
  
 Weitere Informationen zu Deskriptoren, finden Sie unter [Deskriptoren](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Weitere Codebeispiele finden Sie unter [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) und [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
### <a name="code"></a>Code  
  
```  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ein Cursorname festlegen|[SQLSetCursorName-Funktion](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC-Beispielprogramm](../../../odbc/reference/sample-odbc-program.md)

