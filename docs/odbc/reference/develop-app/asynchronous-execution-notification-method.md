---
title: "Asynchrone Ausführung (Benachrichtigungsmethode) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b39bfb096e980106ecaef4e12ef9871f1a32452a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="asynchronous-execution-notification-method"></a>Asynchrone Ausführung (Benachrichtigungsmethode)
ODBC ermöglicht die asynchrone Ausführung der Verbindung und Anweisung Vorgänge. Ein Thread der Anwendung kann eine ODBC-Funktion aufrufen, im asynchronen Modus, und die Funktion zurückgeben kann, bevor der Vorgang abgeschlossen ist, wird der Thread der Anwendung zum Durchführen anderer Aufgaben ermöglichen ist. In Windows 7-SDK für asynchrone-Anweisung oder Verbindungsvorgängen sendet bestimmt eine Anwendung an, dass der asynchrone Vorgang abgeschlossen ist, verwenden der Abrufmethode war. Weitere Informationen finden Sie unter [asynchrone Ausführung (Methode abrufen)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Ab Windows 8-SDK, können Sie feststellen, dass ein asynchroner Vorgang abgeschlossen ist, verwenden die Benachrichtigungsmethode ist.  
  
 In der Abrufmethode müssen Anwendungen die asynchrone Funktion jedes Mal aufgerufen, er den Status des Vorgangs benötigt. Die Benachrichtigungsmethode ist vergleichbar mit dem Rückruf und warten in ADO.NET. Dagegen verwendet ODBC, Win32-Ereignissen als das Benachrichtigungsobjekt.  
  
 Die ODBC Cursor Library und ODBC asynchrone Benachrichtigung können nicht gleichzeitig verwendet werden. Beide Attribute festlegen, wird ein Fehler mit SQLSTATE S1119 zurückgegeben (Cursorbibliothek und asynchrone Benachrichtigung kann nicht gleichzeitig aktiviert sein).  
  
 Finden Sie unter [Benachrichtigung von asynchronen Funktion Abschluss](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) Informationen für Entwickler.  
  
> [!NOTE]  
>  Die Benachrichtigungsmethode wird mit der Cursorbibliothek nicht unterstützt. Eine Anwendung wird die Fehlermeldung angezeigt, wenn es versucht, die Cursorbibliothek über SQLSetConnectAttr, aktivieren, wenn die Benachrichtigungsmethode aktiviert ist.  
  
## <a name="overview"></a>Übersicht  
 Wenn eine ODBC-Funktion im asynchronen Modus aufgerufen wird, wird das Steuerelement an die aufrufende Anwendung sofort mit dem Rückgabecode SQL_STILL_EXECUTING zurückgegeben. Die Anwendung muss die Funktion wiederholt abrufen, bis sie einen anderen Wert als SQL_STILL_EXECUTING zurückgibt. Die Abrufschleife steigt die CPU-Auslastung, schlechten Leistung in vielen asynchronen Szenarios verursacht.  
  
 Sobald das Benachrichtigungsmodell verwendet wird, ist das Modell abrufen deaktiviert. Anwendungen sollten die ursprüngliche Funktion nicht erneut aufrufen. Rufen Sie [SQLCompleteAsync Funktion](../../../odbc/reference/syntax/sqlcompleteasync-function.md) auf den asynchronen Vorgang abzuschließen. Wenn eine Anwendung die ursprüngliche Funktion erneut aufgerufen wird, bevor der asynchrone Vorgang abgeschlossen ist, gibt der Aufruf SQL_ERROR mit SQLSTATE IM017 zurück (Abruf im Modus für asynchrone Benachrichtigung deaktiviert ist).  
  
 Wenn die Benachrichtigungsmodell verwenden, kann die Anwendung aufrufen **SQLCancel** oder **SQLCancelHandle** , einen Anweisung oder Verbindung Vorgang abzubrechen. Wenn die abbruchanforderung erfolgreich ist, gibt ODBC SQL_SUCCESS zurück. Diese Meldung, nicht dass die Funktion tatsächlich abgebrochen wurde; Er gibt an, dass beim Verarbeiten der Anforderung "Abbrechen". Gibt an, ob die Funktion tatsächlich abgebrochen wird, ist Treiber abhängiges und datenquellenabhängig. Wenn ein Vorgang abgebrochen wird, wird der Treiber-Manager weiterhin das Ereignis signalisiert. Der Treiber-Manager gibt SQL_ERROR zurück in den Rückgabecode Puffer und der Status ist SQLSTATE HY008 (der Vorgang wurde abgebrochen) an, dass der Abbruchvorgang ist erfolgreich. Wenn die Funktion die normale Verarbeitung abgeschlossen hat, gibt der Treiber-Manager SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurück.  
  
### <a name="downlevel-behavior"></a>Kompatible Verhalten  
 Die ODBC-Treiber-Manager-Version, die diese Benachrichtigung auf vollständige Unterstützung ist ODBC 3.81.  
  
|ODBC-Version der Anwendung|Treiber-Manager-Version|Treiberversion|Verhalten|  
|------------------------------|----------------------------|--------------------|--------------|  
|Neue Anwendung der ODBC-version|ODBC 3.81|ODBC 3.80 Treiber|Anwendung kann diese Funktion verwenden, wenn der Treiber diese Funktion unterstützt, andernfalls wird der Treiber-Manager Fehler ausgegeben.|  
|Neue Anwendung der ODBC-version|ODBC 3.81|3.80 Pre-ODBC-Treiber|Der Treiber-Manager werden Fehler ausgegeben, wenn der Treiber diese Funktion nicht unterstützt.|  
|Neue Anwendung der ODBC-version|Pre-ODBC-3.81|Any|Wenn die Anwendung diese Funktion verwendet, einen alten Treiber-Manager werden die neuen Attribute als treiberspezifischen Attribute betrachten, und der Treiber sollte den Fehler ausgegeben. Einen neuen Treiber-Manager werden diese Attribute nicht an den Treiber übergeben werden.|  
  
 Eine Anwendung sollte die Treiber-Manager-Version vor Verwendung dieses Features zu überprüfen. Andernfalls ist, wenn ein fehlerhaft geschriebene Treiber kein Fehler ist und der Treiber-Manager-Version vor ODBC 3.81, Verhalten nicht definiert.  
  
## <a name="use-cases"></a>Einsatzgebiete  
 In diesem Abschnitt wird gezeigt, Anwendungsfälle für asynchrone Ausführung und die Abrufmechanismus.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>Integrieren von Daten aus mehreren ODBC-Datenquellen  
 Eine Anwendung zur Integration werden asynchron Daten aus mehreren Datenquellen abgerufen. Einige Daten werden von Remotedatenquellen und einige Daten aus lokalen Dateien sind. Die Anwendung kann nicht fortgesetzt, bis die asynchronen Vorgänge abgeschlossen sind.  
  
 Anstatt wiederholt abzufragen einen Vorgang, um zu bestimmen, ob es vollständig ist, kann die Anwendung ein Ereignisobjekt erstellen und eine ODBC-Verbindungshandle oder ein ODBC-Anweisungshandle zuordnen. Die Anwendung ruft dann Betriebssystem Synchronisierung-APIs auf ein Ereignis oder mehrere viele Ereignisobjekte (ODBC-Ereignisse und andere Windows-Ereignisse) warten müssen. ODBC wird das Ereignisobjekt signalisieren, wenn der entsprechende asynchrone ODBC-Vorgang abgeschlossen ist.  
  
 Unter Windows Win32-Objekte verwendet werden, und, wird dem Benutzer ein einheitliches Programmiermodell bereitstellen. Treibermanager auf anderen Plattformen können die Implementierung der Ereignis-Objekt für diese Plattformen verwenden.  
  
 Das folgende Codebeispiel veranschaulicht die Verwendung der Verbindung und Anweisung asynchrone Benachrichtigung:  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>Bestimmen, ob ein Treiber unterstützt die asynchrone Benachrichtigung  
 Eine ODBC-Anwendung kann bestimmen, ob ein ODBC-Treiber die asynchrone Benachrichtigung durch den Aufruf unterstützt [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md). Der ODBC-Treiber-Manager wird daher rufen Sie die **SQLGetInfo** des Treibers SQL_ASYNC_NOTIFICATION.  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Ein ODBC-Handle zuordnen ein Win32-Ereignishandle  
 Anwendungen sind verantwortlich für das Erstellen von Win32-Ereignisobjekten, die über die entsprechenden Win32-Funktionen. Eine Anwendung kann eine Win32-Ereignishandle eine ODBC-Verbindungshandle oder eine ODBC-Anweisungshandle zuordnen.  
  
 Verbindungsattribute SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE und SQL_ATTR_ASYNC_DBC_EVENT bestimmen, ob ODBC im asynchronen Modus ausgeführt wird, und gibt an, ob ODBC Benachrichtigungsmodus für ein Verbindungshandle ermöglicht. Anweisungsattribute SQL_ATTR_ASYNC_ENABLE und SQL_ATTR_ASYNC_STMT_EVENT bestimmen, ob ODBC im asynchronen Modus ausgeführt wird, und gibt an, ob ODBC Benachrichtigungsmodus für ein Anweisungshandle ermöglicht.  
  
|SQL_ATTR_ASYNC_ENABLE oder SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT oder SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|Aktivieren|ungleich null|Asynchrone Benachrichtigung|  
|Aktivieren|NULL|Asynchronen Abruf|  
|Deaktivieren|any|Synchron|  
  
 Eine Anwendung kann asynchronen Betriebsmodus vorübergehend deaktivieren. ODBC ignoriert SQL_ATTR_ASYNC_DBC_EVENT Werte auf, wenn die Verbindung asynchrone Vorgang auf Systemebene deaktiviert ist. ODBC ignoriert SQL_ATTR_ASYNC_STMT_EVENT Werte auf, wenn die Anweisung asynchronen Vorgang auf Systemebene deaktiviert ist.  
  
 Synchroner Aufruf des **SQLSetStmtAttr** und **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** unterstützt asynchrone Vorgänge jedoch den Aufruf von **SQLSetConnectAttr** festzulegende SQL_ATTR_ASYNC_DBC_EVENT ist immer synchron.  
  
-   **SQLSetStmtAttr** asynchrone Ausführung nicht unterstützt.  
  
 Fehler beim Out-Szenario  
 Wenn **SQLSetConnectAttr** wird aufgerufen, bevor das Herstellen einer Verbindung kann nicht der Treiber-Manager den zu verwendenden Treiber zu bestimmen. Daher gibt der Treiber-Manager für Erfolg **SQLSetConnectAttr** jedoch das Attribut möglicherweise nicht im Treiber festlegen. Der Treiber-Manager wird diese Attribute festgelegt, wenn die Anwendung eine Verbindungsfunktion aufruft. Der Treiber-Manager können Fehler-Timeout auf, da Treiber asynchrone Vorgänge nicht unterstützt wird.  
  
 Vererbung von Verbindungsattribute  
 Die Anweisungen der Verbindung werden in der Regel die Verbindungsattribute erben. Allerdings wird das Attribut SQL_ATTR_ASYNC_DBC_EVENT kann nicht vererbt und wirkt sich nur auf die Verbindungsvorgänge.  
  
 Um eine ODBC-Verbindungshandle ein Ereignishandle zuzuordnen, eine ODBC-Anwendung die ODBC API-Aufrufe **SQLSetConnectAttr** und SQL_ATTR_ASYNC_DBC_EVENT gibt an, wie das Attribut und das Ereignis, als Wert des Attributs behandeln. Das neue ODBC-Attribut ist SQL_ATTR_ASYNC_DBC_EVENT vom Typ SQL_IS_POINTER.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 Erstellen Sie Anwendungen in der Regel AutoReset-Objekte. ODBC wird das Ereignisobjekt nicht zurückgesetzt werden. Anwendungen müssen sicherstellen, dass nicht das Objekt im Zustand "signalisiert" ist, bevor Sie eine asynchrone ODBC-Funktion aufrufen.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT ist ein nur-Treiber-Manager-Attribut, die nicht im Treiber festgelegt werden.  
  
 Der Standardwert von SQL_ATTR_ASYNC_DBC_EVENT ist NULL. Wenn der Treiber die asynchrone Benachrichtigung nicht unterstützt, Abrufen oder Festlegen der SQL_ATTR_ASYNC_DBC_EVENT zurück SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner).  
  
 Wenn der letzte SQL_ATTR_ASYNC_DBC_EVENT Wert festgelegt, ein ODBC-Verbindungshandle ist ungleich NULL, und die Anwendung aktiviert asynchronen Modus durch Festlegen des Attributs SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE mit SQL_ASYNC_DBC_ENABLE_ON, Aufrufen von ODBC-Verbindung Funktion, die asynchronen Modus unterstützt, wird eine abschlussbenachrichtigung abrufen. Wenn der letzte SQL_ATTR_ASYNC_DBC_EVENT-Wert, legen Sie für eine ODBC-Verbindungshandle NULL ist, wird ODBC nicht der Anwendung eine Benachrichtigung unabhängig davon gesendet, ob asynchroner Modus aktiviert ist.  
  
 Eine Anwendung kann SQL_ATTR_ASYNC_DBC_EVENT vor oder nach dem Festlegen des Attributs SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE festlegen.  
  
 Anwendungen können das SQL_ATTR_ASYNC_DBC_EVENT-Attribut auf eine ODBC-Verbindungshandle vor dem Aufrufen einer Verbindungsfunktion festlegen (**SQLConnect**, **SQLBrowseConnect**, oder ** SQLDriverConnect**). Da der ODBC-Treiber-Manager die ODBC-Treiber nicht wissen der Anwendung verwendet werden, wird SQL_SUCCESS zurückgegeben. Wenn die Anwendung eine Verbindungsfunktion aufruft, wird der ODBC-Treiber-Manager überprüfen Sie, ob der Treiber die asynchrone Benachrichtigung unterstützt. Wenn der Treiber die asynchrone Benachrichtigung nicht unterstützt, der ODBC-Treiber-Manager SQL_ERROR mit SQLSTATE S1_118 zurück (Treiber unterstützt keine asynchrone Benachrichtigung). Wenn der Treiber die asynchrone Benachrichtigung unterstützt, wird der ODBC-Treiber-Manager aufrufen den Treiber und legen Sie die entsprechenden Attribute SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK und SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT.  
  
 Ruft die Anwendung auf ähnliche Weise **SQLSetStmtAttr** für eine ODBC-Anweisung verarbeiten, und gibt das Attribut SQL_ATTR_ASYNC_STMT_EVENT zum Aktivieren oder deaktivieren die Anweisung auf die asynchrone Benachrichtigung. Da eine Anweisung-Funktion immer aufgerufen wird, nachdem die Verbindung hergestellt wurde, **SQLSetStmtAttr** SQL_ERROR mit SQLSTATE S1_118 zurück (Treiber unterstützt keine asynchrone Benachrichtigung) sofort, wenn das entsprechende Treiber bietet keine Unterstützung für asynchrone Vorgänge, oder der Treiber unterstützt asynchrone Vorgänge jedoch keine asynchrone Benachrichtigung.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT, der auf NULL festgelegt werden kann, wird ein nur-Treiber-Manager-Attribut, die nicht im Treiber festgelegt werden.  
  
 Der Standardwert von SQL_ATTR_ASYNC_STMT_EVENT ist NULL. Wenn der Treiber die asynchrone Benachrichtigung nicht unterstützt, Abrufen oder Festlegen des Attributs SQL_ATTR_ASYNC_ STMT_EVENT zurück SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner).  
  
 Eine Anwendung sollte dasselbe Ereignishandle nicht mehr als ein ODBC-Anweisungshandle zuordnen. Andernfalls wird eine Benachrichtigung verloren, wenn zwei asynchrone ODBC-Funktionsaufrufe auf zwei Handles abzuschließen, die das gleiche Ereignishandle freigeben. Um ein Anweisungshandle erben von der gleiche Ereignishandler von dem Verbindungshandle zu vermeiden, gibt ODBC SQL_ERROR mit SQLSTATE IM016 (kann nicht Anweisungsattribut in Verbindungshandle festgelegt) zurück, wenn eine Anwendung für ein Verbindungshandle SQL_ATTR_ASYNC_STMT_EVENT festlegt.  
  
### <a name="calling-asynchronous-odbc-functions"></a>Aufrufen asynchroner ODBC-Funktionen  
 Nach dem Aktivieren der asynchrone Benachrichtigung und einen asynchronen Vorgang starten, kann die Anwendung eine ODBC-Funktion aufrufen. Wenn die Funktion auf den Satz von Funktionen, die asynchrone Operation zu unterstützen gehört, erhalten die Anwendung eine abschlussbenachrichtigung bei Abschluss des Vorgangs, unabhängig davon, ob Fehler bei der Funktion oder war erfolgreich.  Die einzige Ausnahme ist, dass die Anwendung eine ODBC-Funktion mit einem ungültigen Handle der Verbindung oder Anweisung aufruft. In diesem Fall ODBC nicht das Ereignis-Handle abrufen und legen Sie sie auf den signalisierten Zustand aufweisen.  
  
 Die Anwendung muss sicherstellen, dass das zugeordnete Ereignis-Objekt in einen nicht signalisierten Zustand vor dem Starten eines asynchronen Vorgangs für die entsprechende ODBC-Handle. ODBC wird das Ereignisobjekt nicht zurückgesetzt werden.  
  
### <a name="getting-notification-from-odbc"></a>Abrufen von Benachrichtigungen aus ODBC  
 Ein Thread der Anwendung aufrufen kann **WaitForSingleObject** , auf ein Ereignishandle oder deren Aufruf warten **WaitForMultipleObjects** zum Warten auf ein Array von Ereignishandles, und werden angehalten, bis eine oder alle der Ereignisobjekte signalisiert oder das Timeoutintervall verstreicht.  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```

