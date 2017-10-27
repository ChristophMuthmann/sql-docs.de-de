---
title: "Asynchrone Ausführung (Abrufmethode) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d4237eddad4847840d16440fbd4cb0940a61d40
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="asynchronous-execution-polling-method"></a>Asynchrone Ausführung (Abrufmethode)
Vor der ODBC 3.8 und Windows 7-SDK wurden asynchrone Vorgänge nur auf Anweisung Funktionen zulässig. Weitere Informationen finden Sie unter der **Anweisung-Vorgänge asynchron ausführen**weiter unten in diesem Thema.  
  
 ODBC 3.8 im SDK für Windows 7 eingeführt asynchrone Ausführung von Vorgängen mit Verbindungen. Weitere Informationen finden Sie unter der **Verbindung-Vorgänge asynchron ausführen** weiter unten in diesem Thema.  
  
 In Windows 7-SDK für asynchrone-Anweisung oder Verbindungsvorgängen sendet bestimmt eine Anwendung an, dass der asynchrone Vorgang abgeschlossen ist, verwenden der Abrufmethode war. Ab Windows 8-SDK, können Sie feststellen, dass ein asynchroner Vorgang abgeschlossen ist, verwenden die Benachrichtigungsmethode ist. Weitere Informationen finden Sie unter [asynchrone Ausführung (Benachrichtigungsmethode)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 Standardmäßig werden ODBC-Funktionen von Treibern synchron ausgeführt; d. h. die Anwendung ruft eine Funktion, und der Treiber keinen erst nach Abschluss der Funktion Steuerelement an die Anwendung zurückgibt. Allerdings können einige Funktionen asynchron ausgeführt werden. d. h. die Anwendung ruft die Funktion, und die Treiber nach der minimalen Verarbeitung Steuerelement an die Anwendung zurückgegeben. Die Anwendung kann dann andere Funktionen aufrufen, während die erste Funktion noch ausgeführt wird.  
  
 Asynchrone Ausführung wird unterstützt, für die meisten Funktionen, die größtenteils auf die Datenquelle ausgeführt werden, z. B. die Funktionen zum Herstellen von Verbindungen, Vorbereiten und Ausführen von SQL-Anweisungen, Abrufen von Metadaten, Daten abzurufen und Transaktionen übernommen. Es ist besonders hilfreich, wenn das Task ausgeführt wird, für die Datenquelle sehr lange, wie z. B. einen Anmeldeprozess oder eine komplexe Abfrage an eine große Datenbank durchführt.  
  
 Wenn die Anwendung ausgeführt, eine Funktion mit einer Anweisung oder die Verbindung, die für die asynchrone Verarbeitung aktiviert ist wird, der Treiber führt eine minimale Menge an Verarbeitungstyp (z. B. überprüfen die Argumente für Fehler), übergibt der Verarbeitung an die Datenquelle und gibt die Steuerung an die Anwendung mit dem Rückgabecode SQL_STILL_EXECUTING. Die Anwendung führt anschließend andere Aufgaben. Um zu bestimmen, wenn die asynchrone Funktion abgeschlossen ist, fragt die Anwendung den Treiber in regelmäßigen Abständen durch Aufrufen der Funktion mit den gleichen Argumenten, wie er ursprünglich verwendet. Wenn die Funktion noch ausgeführt wird, gibt sie SQL_STILL_EXECUTING zurück. Wenn sie die Ausführung beendet hat, wird den Code zurückgegebene haben würden synchron, z. B. SQL_SUCCESS oder SQL_ERROR SQL_NEED_DATA ausgeführt wurde zurückgegeben.  
  
 Gibt an, ob eine Funktion synchron oder asynchron ausgeführt wird, treiberspezifisch. Nehmen wir beispielsweise an die resultsetmetadaten im Treiber zwischengespeichert wird. In diesem Fall es kaum Zeit in Anspruch nimmt **SQLDescribeCol** und der Treiber sollte führen Sie einfach die Funktion aus, sondern künstlich Ausführung verzögern. Andererseits, wenn der Treiber zum Abrufen der Metadaten aus der Datenquelle benötigt, sollte es zurückgeben Steuerelement an die Anwendung während dieser Bereinigungstasks. Die Anwendung muss daher einen anderen Rückgabecode als SQL_STILL_EXECUTING verarbeiten, wenn sie zunächst eine Funktion asynchron ausgeführt wird.  
  
## <a name="executing-statement-operations-asynchronously"></a>Anweisung Vorgänge asynchron ausführen  
 Die folgenden Funktionen für die Anweisung für eine Datenquelle verwendet werden und asynchron ausgeführt werden können:  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 Asynchrone anweisungsausführung wird auf einer pro-Anweisung oder Verbindungsbasis, abhängig von der Datenquelle gesteuert. D. h., gibt die Anwendung nicht, dass eine bestimmte Funktion ist, die asynchron ausgeführt werden, aber jede Funktion, die für eine bestimmte Anweisung ausgeführt wird, die asynchron ausgeführt werden. Mithilfe der Softwareoption Out, welcher Schlüssel unterstützt wird, eine Anwendung ruft [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) mit einer Option SQL_ASYNC_MODE. SQL_AM_CONNECTION wird zurückgegeben, wenn Verbindungsebene asynchrone Ausführung (für ein Anweisungshandle) unterstützt wird. SQL_AM_STATEMENT, wenn auf Anweisungsebene asynchrone Ausführung unterstützt wird.  
  
 Um anzugeben, dass Funktionen, die mit einer bestimmten Anweisung ausgeführt werden, werden asynchron ausgeführt, die Anwendung ruft **SQLSetStmtAttr** mit der SQL_ATTR_ASYNC_ENABLE mit Attributen versehen und legt es auf SQL_ASYNC_ENABLE_ON. Wenn Verbindungsebene asynchroner Verarbeitung unterstützt wird, das Anweisungsattribut SQL_ATTR_ASYNC_ENABLE ist schreibgeschützt und seinen Wert unterscheidet sich das Verbindungsattribut für die Verbindung auf der die Anweisung zugewiesen wurde. Es ist treiberspezifische gibt an, ob der Wert des Attributs Anweisung über verkürzt Anweisung oder höher festgelegt ist. Beim Festlegen SQL_ERROR und SQLSTATE HYC00 zurück (optionales Feature nicht implementiert).  
  
 Um anzugeben, dass Funktionen, die mit einer bestimmten Verbindung ausgeführt werden, werden asynchron ausgeführt, die Anwendung ruft **SQLSetConnectAttr** mit der SQL_ATTR_ASYNC_ENABLE mit Attributen versehen und legt es auf SQL_ASYNC_ENABLE_ON. Alle zukünftigen Anweisungshandle zugeordnet, die für die Verbindung werden für die asynchrone Ausführung aktiviert sein. Es ist treiberdefinierten, gibt an, ob vorhandene Anweisungshandles von dieser Aktion aktiviert werden. Wenn SQL_ATTR_ASYNC_ENABLE auf SQL_ASYNC_ENABLE_OFF festgelegt ist, werden alle Anweisungen für die Verbindung im synchronen Modus. Wenn die asynchrone Ausführung aktiviert ist, wird eine aktive Anweisung für die Verbindung ein Fehler zurückgegeben.  
  
 Um die maximale Anzahl gleichzeitiger aktiver-Anweisungen im asynchronen Modus zu bestimmen, die der Treiber für eine gegebene Verbindung unterstützen kann, ruft die Anwendung **SQLGetInfo** mit der Option SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 Der folgende Code zeigt die Funktionsweise des Modells abrufen:  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 Während eine Funktion asynchron ausgeführt wird, kann die Anwendung Funktionen für alle anderen Anweisungen aufrufen. Die Anwendung kann auch Funktionen über eine Verbindung mit Ausnahme des asynchronen Anweisung zugeordneten aufrufen. Die Anwendung kann nur rufen jedoch die ursprüngliche Funktion und die folgenden Funktionen (mit das Anweisungshandle oder die zugehörige Verbindung, Umgebungshandle) nach einer Anweisung gibt SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (über das Anweisungshandle)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 Wenn die Anwendung jede andere Funktion mit der asynchronen-Anweisung oder die Verbindung mit dieser Anweisung verknüpfte aufruft, gibt die Funktion SQLSTATE HY010 (Funktion Sequenzfehler), zum Beispiel.  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 Wenn eine Anwendung eine Funktion ruft, um zu bestimmen, ob er immer noch asynchron ausgeführt wird, muss das ursprüngliche Anweisungshandle verwendet werden. Dies ist, da die asynchrone Ausführung regelmäßig pro Anweisung nachverfolgt wird. Die Anwendung muss darüber hinaus gültige Werte für die anderen Argumente bereitgestellt – die ursprüngliche Argumente führen – nach fehlerüberprüfung im Treiber-Manager abgerufen. Nachdem der Treiber das Anweisungshandle überprüft und feststellt, dass die Anweisung asynchron ausgeführt wird, ignoriert jedoch alle anderen Argumente.  
  
 Während eine Funktion asynchron ausgeführt wird – das heißt, nachdem sie SQL_STILL_EXECUTING zurückgegeben wurde und bevor die Rückgabe eines anderen Codes – die Anwendung durch den Aufruf abzubrechen **SQLCancel** oder **SQLCancelHandle** mit dem gleichen Anweisungshandle. Dies ist nicht garantiert Ausführung Abbrechen. Beispielsweise die Funktion möglicherweise bereits abgeschlossen haben. Darüber hinaus der Code zurückgegebenes **SQLCancel** oder **SQLCancelHandle** gibt nur an, ob der Versuch, die Funktion "Abbrechen" erfolgreich war, nicht, ob es sich tatsächlich um die Funktion abgebrochen. Um zu bestimmen, ob die Funktion abgebrochen wurde, ruft die Anwendung die Funktion erneut aus. Wenn die Funktion abgebrochen wurde, wird SQL_ERROR und SQLSTATE HY008 (der Vorgang wurde abgebrochen). Wenn die Funktion nicht abgebrochen wurde, wird einem anderen Code, z. B. SQL_SUCCESS, SQL_STILL_EXECUTING oder mit einem anderen SQLSTATE SQL_ERROR zurückgegeben.  
  
 Deaktivieren Sie asynchrone Ausführung einer bestimmten Anweisung aus, wenn der Treiber auf Anweisungsebene asynchronen Verarbeitung, ruft die Anwendung unterstützt **SQLSetStmtAttr** mit der SQL_ATTR_ASYNC_ENABLE mit Attributen versehen und legt es auf SQL_ ASYNC_ENABLE_OFF. Wenn der Treiber Verbindungsebene asynchronen Verarbeitung unterstützt, die Anwendung aufruft, **SQLSetConnectAttr** , SQL_ATTR_ASYNC_ENABLE auf SQL_ASYNC_ENABLE_OFF, festzulegen, die asynchrone Ausführung alle Anweisungen auf deaktiviert die Verbindung.  
  
 Die Anwendung sollte in der sich wiederholenden Schleife der ursprünglichen Funktion DiagnoseDatensätze verarbeiten. Wenn **SQLGetDiagField** oder **SQLGetDiagRec** wird aufgerufen, wenn eine asynchrone Funktion ausgeführt wird, wird die aktuelle Liste der DiagnoseDatensätze zurückgegeben. Jedes Mal, wenn der ursprüngliche Funktionsaufruf wiederholt wird, löscht er die vorherigen DiagnoseDatensätze.  
  
## <a name="executing-connection-operations-asynchronously"></a>Verbindungsvorgänge asynchron ausführen  
 Zugelassen Sie vor der ODBC 3.8 asynchrone Ausführung wurde, für die Anweisung bezogenen Vorgänge wie z. B. vorbereiten, führen Sie aus und abzurufen Sie, als auch für Vorgänge mit Metadaten Katalog. ODBC 3.8 ab, ist asynchron auch möglich, dass die Verbindung bezogene Vorgänge, die z. b. wenn eine Verbindung herstellt, trennen, Commit- und Rollback.  
  
 Weitere Informationen zu ODBC 3.8, finden Sie unter [Neuigkeiten in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 Verbindungsvorgängen sendet, der asynchron ausgeführt wird, in den folgenden Szenarien nützlich:  
  
-   Wenn eine kleine Anzahl von Threads eine große Anzahl von Geräten mit sehr hohen Datenraten verwaltet. Um die Reaktionsfähigkeit und Skalierbarkeit Ihres Systems maximieren ist es wünschenswert, dass alle Vorgänge asynchron ist.  
  
-   Wenn Sie Datenbankvorgängen über mehrere Verbindungen zu verstrichene Übertragung Zeiten zu minimieren, überlappen möchten.  
  
-   Effiziente asynchrone ODBC-Aufrufe und die Möglichkeit, Verbindungsvorgänge "Abbrechen" aktivieren eine Anwendung, die der Benutzer auf alle langsamen Vorgang "Abbrechen", ohne dass Timeouts warten.  
  
 Die folgenden Funktionen, die über Verbindungshandles ausgeführt werden, können nun asynchron ausgeführt werden:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 Um zu bestimmen, ob ein Treiber asynchrone Vorgänge zu diesen Funktionen unterstützt, eine Anwendung ruft **SQLGetInfo** mit SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE wird zurückgegeben, wenn asynchrone Vorgänge unterstützt werden. SQL_ASYNC_DBC_NOT_CAPABLE wird zurückgegeben, wenn asynchrone Vorgänge werden nicht unterstützt.  
  
 Um anzugeben, dass Funktionen, die mit einer bestimmten Verbindung ausgeführt werden, werden asynchron ausgeführt, die Anwendung ruft **SQLSetConnectAttr** und legt das Attribut SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE auf SQL_ASYNC_DBC_ENABLE fest _AUF. Festlegen von Verbindungsattribut vor dem Herstellen einer Verbindung immer wird synchron ausgeführt. Darüber hinaus der Vorgang, der die Verbindung festlegen-Attribut SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE mit **SQLSetConnectAttr** immer synchron ausgeführt wird.  
  
 Eine Anwendung kann asynchrone Vorgang vor dem Herstellen einer Verbindung. Da der Treiber-Manager den Treiber zu verwenden, bevor das Herstellen einer Verbindung nicht ermitteln kann, wird der Treiber-Manager immer Erfolg in zurückgegeben **SQLSetConnectAttr**. Es kann jedoch fehlschlagen herstellen, wenn der ODBC-Treiber keine asynchrone Vorgänge unterstützt.  
  
 Im Allgemeinen kann gibt es höchstens eine asynchron ausführen-Funktion mit einem bestimmten Verbindungshandle oder ein Anweisungshandle zugeordnet ist. Ein Verbindungshandle kann jedoch mehr als ein Anweisungshandle zugeordnet haben. Ist kein asynchroner Vorgang, der auf dem Verbindungshandle ausführen, kann ein Handle für die zugehörige Anweisung einen asynchronen Vorgang ausführen. Auf ähnliche Weise können Sie einen asynchronen Vorgang für ein Verbindungshandle lassen, wenn es keine asynchrone Vorgänge in Bearbeitung auf alle zugeordneten Anweisungshandle sind. Versuch, führen Sie einen asynchronen Vorgang, der mithilfe eines Handles, das gerade einen asynchronen Vorgang ausführt, gibt HY010 "Funktionsreihenfolge" zurück.  
  
 Wenn ein Verbindungsvorgang SQL_STILL_EXECUTING zurückgibt, kann eine Anwendung nur aufrufen die ursprüngliche Funktion und die folgenden Funktionen für diese Verbindungshandle:  
  
-   **SQLCancelHandle** (auf dem Verbindungshandle)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (Zuordnen von ENV/Datenbank)  
  
-   **SQLAllocHandleStd** (Zuordnen von ENV/Datenbank)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 Die Anwendung sollte in der sich wiederholenden Schleife der ursprünglichen Funktion DiagnoseDatensätze verarbeiten. Wenn SQLGetDiagField oder SQLGetDiagRec aufgerufen wird, wenn eine asynchrone Funktion ausgeführt wird, wird die aktuelle Liste der DiagnoseDatensätze zurückgegeben. Jedes Mal, wenn der ursprüngliche Funktionsaufruf wiederholt wird, löscht er die vorherigen DiagnoseDatensätze.  
  
 Wenn eine Verbindung wird geöffnet oder geschlossen asynchron, der Vorgang ist abgeschlossen, wenn die Anwendung im ursprünglichen Funktionsaufruf SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO empfängt.  
  
 Eine neue Funktion wurde um ODBC 3.8, **SQLCancelHandle**. Diese Funktion bricht ab, der sechs Verbindungsfunktionen (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**, und **SQLSetConnectAttr**). Eine Anwendung sollte Aufrufen **SQLGetFunctions** zu bestimmen, ob der Treiber unterstützt **SQLCancelHandle**. Wie bei **SQLCancel**, wenn **SQLCancelHandle** gibt Erfolg, heißt das nicht der Vorgang wurde abgebrochen. Eine Anwendung sollte die ursprüngliche Funktion erneut aus, um zu bestimmen, ob der Vorgang abgebrochen wurde, aufrufen. **SQLCancelHandle** können Sie asynchrone Operationen für Verbindungshandles oder Anweisungshandles "Abbrechen". Mit **SQLCancelHandle** Handle zum Abbrechen eines Vorgangs für eine Anweisung ist die gleiche wie das Aufrufen **SQLCancel**.  
  
 Es ist nicht notwendig, beide unterstützen das **SQLCancelHandle** und asynchronverbindung Vorgänge zur gleichen Zeit. Ein Treiber kann asynchrone Verbindungsvorgänge unterstützen, aber nicht **SQLCancelHandle**, oder umgekehrt.  
  
 Asynchrone Verbindungsvorgänge und **SQLCancelHandle** kann auch verwendet werden, die von ODBC 3.x und ODBC 2.x-Anwendungen mit einem ODBC 3.8-Treiber und der ODBC 3.8-Treiber-Manager. Informationen zum Aktivieren von einer älteren Anwendung um neue Funktionen in höheren ODBC-Version verwenden, finden Sie unter [Kompatibilitätsmatrix](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Verbindungspooling  
 Wenn Verbindungspooling aktiviert ist, werden asynchrone Vorgänge nur minimal zum Herstellen einer Verbindung unterstützt (mit **SQLConnect** und **SQLDriverConnect**) und schließen eine Verbindung mit **SQLDisconnect**. Eine Anwendung sollte jedoch immer noch den Rückgabewert SQL_STILL_EXECUTING behandeln **SQLConnect**, **SQLDriverConnect**, und **SQLDisconnect**.  
  
 Wenn Verbindungspooling aktiviert ist, **SQLEndTran** und **SQLSetConnectAttr** für asynchrone Vorgänge unterstützt werden.  
  
## <a name="example"></a>Beispiel  
  
### <a name="description"></a>Description  
 Das folgende Beispiel zeigt, wie Sie **SQLSetConnectAttr** asynchrone Ausführung für Funktionen im Zusammenhang mit Verbindung zu aktivieren.  
  
### <a name="code"></a>Code  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>Beispiel  
  
### <a name="description"></a>Description  
 Dieses Beispiel zeigt die asynchronen Commit-Vorgängen. Rollback-Operationen können auch auf diese Weise erfolgen.  
  
### <a name="code"></a>Code  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von ODBC-Anweisungen](../../../odbc/reference/develop-app/executing-statements-odbc.md)

