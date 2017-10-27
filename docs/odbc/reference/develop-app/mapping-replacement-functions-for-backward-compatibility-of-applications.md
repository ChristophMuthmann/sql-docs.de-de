---
title: "Zuordnungsfunktionen Ersatz für die Kompatibilität von Apps – ODBC | Microsoft Docs"
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
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 461f41eb5f8ae7481b65d293b0c3a619b59e7f9c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Zuordnungsfunktionen Ersatz für die Abwärtskompatibilität von Anwendungen
Eine ODBC 3.*.x* Anwendung arbeiten, über die ODBC 3.*.x* -Treiber-Manager funktioniert mit einer ODBC 2.* X* Treiber solange keine neuen Funktionen verwendet werden. Beide Funktionen dupliziert und verhaltensänderungen, allerdings wirken sich die Möglichkeit, die ODBC-3. *x* Anwendung funktioniert, in einer ODBC 2.* X* Treiber. Wenn Sie mit einer ODBC 2. arbeiten zu können. *x* -Treiber verwenden, wird der Treiber-Manager die folgenden ODBC 3. zugeordnet.* X* -Funktionen, die eine oder mehrere ODBC 2. ersetzt haben.* X* -Funktionen in der entsprechenden ODBC 2.* X* Funktionen.  
  
|ODBC-3. *x* Funktion|ODBC-2. *x* Funktion|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**, oder **SQLAllocStmt:**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**, oder **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] andere Aktionen möglicherweise vom jeweiligen Attribut, das angefordert wird auch ausgeführt werden.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLAllocEnv**, **SQLAllocConnect**, oder **SQLAllocStmt:**je nach Bedarf. Beim folgenden Aufruf **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 führt in der Treiber-Manager ausführen folgender (konzeptionelle, keine fehlerprüfung) Zuordnung:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLSetPos**. Beim folgenden Aufruf **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn die Operationsargument SQL_ADD ist, ruft der Treiber-Manager **SQLSetPos** wie folgt:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Wenn das Argument der Operation nicht SQL_ADD ist, gibt der Treiber SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner).  
  
3.  Wenn die Anwendung versucht, so ändern Sie die SQL_ATTR_ROW_STATUS_PTR zwischen den Aufrufen **SQLFetch** oder **SQLFetchScroll** und **SQLBulkOperations**, wird der Treiber-Manager Zurückgeben von SQLSTATE HY011 (Attribut kann nicht jetzt festgelegt werden).  
  
4.  Wenn die Operationsargument SQL_ADD ist, muss die Anwendung aufrufen **SQLBindCol** so binden Sie die Daten eingefügt werden. Es kann nicht aufgerufen werden **SQLSetDescField** oder **SQLSetDescRec** so binden Sie die Daten eingefügt werden.  
  
5.  Wenn die Operationsargument SQL_ADD und die Anzahl der einzufügenden Zeilen nicht identisch mit der aktuellen Rowsetgröße ist **SQLSetStmtAttr** aufgerufen werden, um das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der Zeilen werden festgelegt vor dem Aufruf eingefügt **SQLBulkOperations**. Um die vorherigen Rowsetgröße wiederherzustellen, muss die Anwendung SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut vor festgelegt **SQLFetch**, **SQLFetchScroll**, oder **SQLSetPos**aufgerufen wird.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLColAttributes**. Beim folgenden Aufruf **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn *FieldIdentifier* ist eines der folgenden:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX oder SQL_DESC_LOCAL_TYPE_NAME  
  
     der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY091 (Ungültiger Deskriptorfeldbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
2.  Der Treiber-Manager ordnet SQL_COLUMN_COUNT, SQL_COLUMN_NAME oder SQL_COLUMN_NULLABLE SQL_DESC_COUNT, SQL_DESC_NAME oder SQL_DESC_NULLABLE, bzw. (Einer ODBC 2*.x* Treiber nur SQL_COLUMN_COUNT, SQL_COLUMN_NAME, und SQL_COLUMN_NULLABLE nicht SQL_DESC_COUNT, SQL_DESC_NAME und SQL_DESC_NULLABLE Unterstützung benötigen.) Der Aufruf von SQLColAttribute zugeordnet ist:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Alle anderen *FieldIdentifier* Werte werden über den Treiber übergeben, mit **SQLColAttribute** zugeordnet **SQLColAttributes** wie vorher gezeigt.  
  
4.  Wenn *Pufferlänge* ist kleiner als 0 (null) der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY090 (ungültige Zeichenfolgen- oder Pufferlänge). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
5.  Wenn *FieldIdentifier* SQL_DESC_CONCISE_TYPE ist und der zurückgegebene Typ ist ein präziser Datetime-Datentyp, der Treiber-Manager-Zuordnungen, die das zurückgegebene für Datum, Uhrzeit und Timestamp-Codes Werte.  
  
6.  Der Treiber-Manager führt die erforderlichen geprüft, ob SQLSTATE HY010 (Funktionsreihenfolge) Anforderungen, die ausgelöst werden. Wenn also der Treiber-Manager SQL_ERROR und SQLSTATE HY010 zurückgibt (Sequenzfehler-Funktion). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLTransact**. Beim folgenden Aufruf **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 führt in der Treiber-Manager ausführen folgender (konzeptionelle, keine fehlerprüfung) Zuordnung:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLExtendedFetch** mit einem *FetchOrientation* Argument sql_fetch_next. Beim folgenden Aufruf **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 führt in der aufrufenden Treibermanager **SQLExtendedFetch**wie folgt:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 In diesem Aufruf der *PcRow* Argument wird festgelegt, auf den Wert, der die Anwendung das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut auf durch einen Aufruf von festlegt **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Wenn die Anwendung aufruft, **SQLSetStmtAttr** zum Festlegen der SQL_ATTR_ROW_STATUS_PTR auf ein Statusarray der Treiber-Manager speichert die Zeiger. *RowStatusArray* kann ein null-Zeiger gleich sein.  
  
 Wenn der Treiber nicht unterstützt **SQLExtendedFetch** und die Cursorbibliothek geladen wird, wird der Treiber-Manager verwendet der Cursorbibliothek **SQLExtendedFetch** abzubildenden **SQLFetch** an **SQLExtendedFetch**. Wenn der Treiber nicht unterstützt **SQLExtendedFetch** und die Cursorbibliothek nicht geladen wird, wird der Treiber-Manager übergibt den Aufruf von **SQLFetch** über den Treiber. Wenn die Anwendung aufruft, **SQLSetStmtAttr** zum Festlegen der SQL_ATTR_ROW_STATUS_PTR der Treiber-Manager wird sichergestellt, dass das Array aufgefüllt wird. Wenn die Anwendung aufruft, **SQLSetStmtAttr** um SQL_ATTR_ROWS_FETCHED_PTR festzulegen, legt der Treiber-Manager dieses Feld auf 1 fest.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLExtendedFetch**. Beim folgenden Aufruf **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn die Anwendung aufruft, **SQLSetStmtAttr** um lassen Sie SQL_ATTR_ROW_STATUS_PTR (wodurch das Feld SQL_DESC_ARRAY_STATUS_PTR in IRD versetzt wird), zeigen Sie in ein Statusarray von, speichert der Treiber-Manager this-Zeiger. Lassen Sie diesen Zeiger werden *RowStatusArray*können, andernfalls *RowStatusArray* gleich einem null-Zeiger sein. Wenn die *RowStatusArray* -Argument ein null-Zeiger festgelegt wird, die der Treiber-Manager wird eine Zeile Statusarray generiert.  
  
2.  Wenn *FetchOrientation* ist keiner der SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST oder sql_fetch_bookmark auf, der Treiber-Manager gibt SQL_ERROR mit SQLSTATE zurück. HY106 (Fetchtyp außerhalb des gültigen Bereichs). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
3.  Fall:  
  
-   Wenn *FetchOrientation* SQL_FETCH_BOOKMARK, gleich ist:  
  
    -   Wenn **SQLSetStmtAttr** hieß früher legen Sie den Wert der SQL_ATTR_FETCH_BOOKMARK_PTR, Sie können *bak* der Wert, der durch die Dereferenzierung des Zeigers SQL_DESC_FETCH_BOOKMARK_PTR abgerufen werden.  
  
    -   Andernfalls Rückgabe von SQL_ERROR mit SQLSTATE HY111 (Ungültiger lesezeichenwerts). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
     Der Treiber-Manager ruft **SQLExtendedFetch**wie folgt:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   Andernfalls ruft der Treiber-Managers **SQLExtendedFetch**wie folgt:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     In diesen Aufrufen der *PcRow* Argument wird festgelegt, auf den Wert, der die Anwendung das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut auf durch einen Aufruf von festlegt **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE ist SQL_ROWSET_SIZE setzen zugeordnet.  
  
-   Wenn *rc* ist gleich SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, und wenn *FetchOrientation* gleich SQL_FETCH_BOOKMARK und *FetchOffset* ist nicht 0 ist, klicken Sie dann den Treiber gleich Manager sendet eine Warnung, SQLSTATE 01S10 (Versuch zum Abrufen von einem Lesezeichen Offset Offsetwert ignoriert), und gibt SQL_SUCCESS_WITH_INFO zurück.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLFreeEnv**, **SQLFreeConnect**, oder **SQLFreeStmt** je nach Bedarf. Beim folgenden Aufruf **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 führt in der Treiber-Manager ausführen folgender (konzeptionelle, keine fehlerprüfung) Zuordnung:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLGetConnectOption**. Beim folgenden Aufruf **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn *Attribut* ist kein treiberdefinierten Verbindung oder Anweisung Attribut und ist kein Attribut in ODBC 2. definiert.* X*, der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
2.  Wenn *Attribut* SQL_ATTR_AUTO_IPD oder SQL_ATTR_METADATA_ID der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 gleich (Ungültiger Attribut-/Optionsbezeichner).  
  
3.  Der Treiber-Manager führt die erforderlichen überprüft, ob SQLSTATE 08003 (Verbindung nicht geöffnet) oder SQLSTATE HY010 (Funktionsreihenfolge) ausgelöst werden muss. Wenn dies der Fall ist, wird der Treiber-Manager gibt SQL_ERROR zurück, und sendet die entsprechende Fehlermeldung. Keine weiteren Regeln in diesem Abschnitt gelten.  
  
4.  Der Treiber-Manager ruft **SQLGetConnectOption** wie folgt:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Beachten Sie, dass die *Pufferlänge* und *StringLengthPtr* werden ignoriert.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Wenn eine ODBC-3.*x* Anwendung arbeiten mit einer ODBC 2*.x* Treiber ruft **SQLGetData** mit der *ColumnNumber* Argument gleich 0, die ODBC 3*.x* -Treiber-Manager wird dies zugeordnet zu einem Aufruf von **SQLGetStmtOption** mit der *Option* -Attributsatz zur SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>'SQLGetStmtAttr'  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLGetStmtOption**. Beim folgenden Aufruf **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn *Attribut* ist kein treiberdefinierten Verbindung oder Anweisung Attribut und ist kein Attribut in ODBC 2. definiert.* X*, der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
2.  Wenn *Attribut* ist eines der folgenden:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
3.  Der Treiber-Manager führt die erforderlichen geprüft, ob SQLSTATE HY010 (Funktionsreihenfolge) Anforderungen, die ausgelöst werden. Wenn also der Treiber-Manager SQL_ERROR und SQLSTATE HY010 zurückgibt (Sequenzfehler-Funktion). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
4.  Wenn *Attribut* gleich SQL_ATTR_ROWS_FETCHED_PTR fest, der Treiber-Manager gibt ein Zeiger auf die interne Treibermanager-Variable *cRow*, die es verwendet wurde oder in einem Aufruf verwendet ** SQLExtendedFetch**. Keine weiteren Regeln in diesem Abschnitt gelten.  
  
5.  Wenn *Attribut* entspricht, SQL_DESC_FETCH_BOOKMARK_PTR, gibt der Treiber-Manager den entsprechenden Zeiger, die während eines Aufrufs zwischengespeichert wurde **SQLSetStmtAttr**.  
  
6.  Wenn *Attribut* entspricht, SQL_ATTR_ROW_STATUS_PTR, gibt der Treiber-Manager den entsprechenden Zeiger, die während eines Aufrufs zwischengespeichert wurde **SQLSetStmtAttr**.  
  
7.  Der Treiber-Manager ruft **SQLGetStmtOption** wie folgt:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     wobei *Befehls beschäftigt*, *fOption*, und *PvParam* wird mit den Werten der festgelegt werden *StatementHandle*, *Attribut*, und *ValuePtr*zugeordnet. Die *Pufferlänge* und *StringLengthPtr* werden ignoriert.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLSetConnectOption**. Beim folgenden Aufruf **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn *Attribut* ist kein treiberdefinierten Verbindung oder Anweisung Attribut und ist kein Attribut in ODBC 2. definiert.* X*, der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
2.  Wenn *Attribut* gleich SQL_ATTR_AUTO_IPD der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner).  
  
3.  Der Treiber-Manager führt die erforderlichen geprüft, ob SQLSTATE 08003 (Verbindung nicht geöffnet) oder SQLSTATE HY010 (Funktionsreihenfolge) erforderlich, die ausgelöst werden. Wenn einer dieser Fehler ausgelöst werden muss, wird der Treiber-Manager gibt SQL_ERROR zurück, und sendet die entsprechende Fehlermeldung. Keine weiteren Regeln in diesem Abschnitt gelten.  
  
4.  Der Treiber-Manager ruft **SQLSetConnectOption** wie folgt:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     wobei *Hdbc*, *fOption*, und *vParam* wird mit den Werten der festgelegt werden *Verbindungshandle*, *Attribut*, und *ValuePtr*zugeordnet. *StringLengthPtr* wird ignoriert.  
  
> [!NOTE]  
>  Die Fähigkeit zum Festlegen von Anweisungsattribute auf Verbindungsebene wurde als veraltet markiert. Anweisungsattribute sollte nie auf der Verbindungsebene durch ein ODBC-3 festgelegt werden. *x* Anwendung.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Der Treiber-Manager zugeordnet, diese Option, um **SQLSetStmtOption**. Beim folgenden Aufruf **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 führt die folgende Sequenz von Schritten:  
  
1.  Wenn *Attribut* ist kein treiberdefinierten Verbindung oder Anweisung Attribut und ist kein Attribut in ODBC 2. definiert.* X*, der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
2.  Wenn *Attribut* ist eines der folgenden:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     der Treiber-Manager gibt SQL_ERROR mit SQLSTATE HY092 (Ungültiger Attribut-/Optionsbezeichner). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
3.  Der Treiber-Manager führt die erforderlichen überprüft, ob SQLSTATE HY010 (Funktionsreihenfolge) erforderlich, die ausgelöst werden. Wenn also der Treiber-Manager SQL_ERROR und SQLSTATE HY010 zurückgibt (Sequenzfehler-Funktion). Keine weiteren Regeln in diesem Abschnitt gelten.  
  
4.  Wenn *Attribut* ist gleich SQL_ATTR_PARAMSET_SIZE oder SQL_ATTR_PARAMS_PROCESSED_PTR finden Sie im Abschnitt "Zuordnungen für die Behandlung von Parameterarrays," weiter unten in diesem Thema. Keine weiteren Regeln in diesem Abschnitt gelten.  
  
5.  Wenn *Attribut* gleich SQL_ATTR_ROWS_FETCHED_PTR fest, der Zeiger für die spätere Verwendung mit Wert, Treibermanager-Caches **SQLFetchScroll**.  
  
6.  Wenn *Attribut* gleich SQL_ATTR_ROW_STATUS_PTR, der Zeiger für die spätere Verwendung mit Wert, Treibermanager-Caches **SQLFetchScroll** oder **SQLSetPos**. Keine weiteren Regeln in diesem Abschnitt gelten.  
  
7.  Wenn *Attribut* gleich SQL_ATTR_FETCH_BOOKMARK_PTR-Treiber-Managers Caches *ValuePtr* und den zwischengespeicherten Wert weiter unten in einem Aufruf von **SQLFetchScroll**. Keine weiteren Regeln in diesem Abschnitt gelten.  
  
8.  Der Treiber-Manager ruft **SQLSetStmtOption** wie folgt:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     wobei *Befehls beschäftigt*, *fOption*, und *vParam* wird mit den Werten der festgelegt werden *StatementHandle*, *Attribut*, und *ValuePtr*zugeordnet. Die *StringLength* Argument wird ignoriert.  
  
     Wenn ein ODBC-2. *x* -Treiber unterstützt-Zeichenfolge, die treiberspezifische-Anweisungsoptionen können nur eine ODBC 3.* X* Anwendung aufrufen sollte **SQLSetStmtOption** zum Festlegen dieser Optionen.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Zuordnungen für die Behandlung von Parameterarrays  
 Wenn die Anwendung aufruft:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 der Treiber-Manager aufruft:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 Der Treiber-Manager gibt einen Zeiger später auf diese Variable, wenn die Anwendung aufruft, **SQLGetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR abgerufen. Der Treiber-Manager kann nicht diese interne Variable geändert werden, bis das Anweisungshandle auf den vorbereiteten oder zugeordneten Zustand zurückgegeben wird.  
  
 Eine ODBC-3. *x* Anwendung aufrufen kann **SQLGetStmtAttr** um den Wert der SQL_ATTR_PARAMS_PROCESSED_PTR abzurufen, obwohl sie nicht explizit Feld SQL_DESC_ARRAY_SIZE im APD festgelegt wurde. Diese Situation kann z. B. auftreten, wenn die Anwendung eine generische Routine verfügt, die prüft, ob die aktuelle "Zeile" von Parametern bei verarbeiteten **SQLExecute** wird SQL_NEED_DATA zurückgegeben. Diese Routine wird aufgerufen, und zwar unabhängig davon, ob die SQL_DESC_ARRAY_SIZE 1 beträgt oder größer als 1 ist. Um dies zu berücksichtigen, der Treiber-Manager müssen diese internen Variablen definieren, und zwar unabhängig davon, ob die Anwendung aufgerufen hat **SQLSetStmtAttr** Feld SQL_DESC_ARRAY_SIZE im APD festlegen. Wenn SQL_DESC_ARRAY_SIZE nicht festgelegt wurde, wird der Treiber-Manager hat, um sicherzustellen, dass diese Variable den Wert "1" vor der Rückgabe von enthält **SQLExecDirect** oder **SQLExecute**.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 In ODBC 3. *x*Aufrufen **SQLFetch** oder **SQLFetchScroll** füllt die SQL_DESC_ARRAY_STATUS_PTR in IRD und das SQL_DIAG_ROW_NUMBER-Feld eines angegebenen Diagnose-Datensatzes enthält die Nummer der Zeile im Rowset, dem auf diesen Datensatz beziehen. Verwenden Sie diese, kann die Anwendung eine Fehlermeldung mit einer bestimmten Zeilenposition korrelieren.  
  
 Eine ODBC-2. *x* Treiber wird in der Lage, diese Funktionalität bereit. Er bietet jedoch Abgrenzung der Fehler mit SQLSTATE 01 s 01 (Fehler in Zeile). Eine ODBC-3. *x* Anwendung, die **SQLFetch** oder **SQLFetchScroll** beim gegen einer ODBC 2.* X* Treiber benötigt, um diese Tatsache bewusst sein. Beachten Sie außerdem, dass eine solche Anwendung kann nicht aufgerufen werden **SQLGetDiagField** tatsächlich Feld SQL_DIAG_ROW_NUMBER trotzdem abgerufen. Eine ODBC-3. *x* Anwendung arbeiten mit einer ODBC 2.* X* Treiber wird in der Lage, rufen Sie **SQLGetDiagField** nur mit einem *DiagIdentifier* Argument SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE oder SQL_DIAG_ SQLSTATE. Die ODBC 3.*.x* -Treiber-Manager verwaltet die Diagnosedaten-Struktur, bei der Arbeit mit einer ODBC 2.* X* Treiber, aber die ODBC 2.* X* Treiber gibt nur diese vier Felder zurück.  
  
 Wenn eine ODBC-2.*x* Anwendung arbeitet mit einer ODBC 2.* X* -Treiber verwenden, wenn mehrere Fehler vom Treiber-Manager zurückgegeben werden bei einer Operation führen kann verschiedene Fehler können zurückgegeben werden, indem die ODBC 3.*.x* Treiber-Manager als von der ODBC 2.* X* -Treiber-Manager.  
  
## <a name="mappings-for-bookmark-operations"></a>Zuordnungen für Vorgänge für Lesezeichen  
 Die ODBC 3.*.x* -Treiber-Manager führt die folgenden Zuordnungen, wenn eine ODBC 3.* X* Anwendung arbeiten mit einer ODBC 2.* X* Treiber Lesezeichen Vorgänge ausführt.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Wenn eine ODBC-3.*x* Anwendung arbeiten mit einer ODBC 2.* X* Treiber ruft **SQLBindCol** zum Binden an die Spalte 0 mit *fCType* SQL_C_VARBOOKMARK, die ODBC 3*.x* -Treiber-Manager überprüft, finden Sie unter ob die *Pufferlänge* Arguments ist kleiner als 4 oder größer als 4 und wenn dies der Fall ist, gibt SQLSTATE HY090 (ungültige Zeichenfolgen- oder Pufferlänge). Wenn die *Pufferlänge* Argument gleich 4 ist, ruft der Treiber-Manager **SQLBindCol** im Treiber nach dem Ersetzen *fCType* mit SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Wenn eine ODBC-3.*x* Anwendung arbeiten mit einer ODBC 2.* X* Treiber ruft **SQLColAttribute** mit der *ColumnNumber* Argument auf 0 festgelegt, der Treiber-Manager gibt den *FieldIdentifier* Werte in der folgenden Tabelle aufgeführt.  
  
|*FieldIdentifier*|Wert|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (leere Zeichenfolge)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|Der gleiche Wert zurückgegeben, indem **SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (leere Zeichenfolge)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (leere Zeichenfolge)|  
|SQL_DESC_LITERAL_SUFFIX|"" (leere Zeichenfolge)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (leere Zeichenfolge)|  
|SQL_DESC_NAME|"" (leere Zeichenfolge)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (leere Zeichenfolge)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (leere Zeichenfolge)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (leere Zeichenfolge)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Wenn eine ODBC-3.*x* Anwendung arbeiten mit einer ODBC 2.* X* Treiber ruft **SQLDescribeCol** mit der *ColumnNumber* Argument auf 0 festgelegt, gibt der Treiber-Manager in der folgenden Tabelle aufgeführten Werte zurück.  
  
|Puffer|Wert|  
|------------|-----------|  
|ColumnName|"" (leere Zeichenfolge)|  
|* NameLengthPtr|0|  
|* DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|* DecimalDigitsPtr|0|  
|* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Wenn eine ODBC-3.*x* Anwendung arbeiten mit einer ODBC 2.* X* Treiber macht die folgenden Aufruf von **SQLGetData** ein Lesezeichens abgerufen:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 der Aufruf zugeordnet ist **SQLGetStmtOption** mit einem *fOption* von SQL_GET_BOOKMARK, wie folgt:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 wobei *Befehls beschäftigt* und *PvParam* festgelegt sind, auf die Werte in *StatementHandle* und *TargetValuePtr*bzw. Das Lesezeichen wird zurückgegeben, in den Puffer, die durch die *PvParam* (*TargetValuePtr*) Argument. Der Wert in den Puffer verweist die *StrLen_or_IndPtr* Argument im Aufruf **SQLGetData** auf 4 festgelegt ist.  
  
 Diese Zuordnung ist notwendig, für den Fall, in dem Konto **SQLFetch** hieß vor dem Aufruf von **SQLGetData** und der ODBC 2.* X* Treiber wurde nicht unterstützt. **SQLExtendedFetch**. In diesem Fall **SQLFetch** würde an die ODBC 2. übergeben werden.* X* Treiber, in dem Abruf von Groß-/Kleinschreibung Lesezeichen wird nicht unterstützt.  
  
 **SQLGetData** kann nicht mehrmals aufgerufen werden, in einer ODBC 2.* X* Treiber zum Abrufen eines Lesezeichens in Teilen, deshalb wird beim Aufrufen **SQLGetData** mit der *Pufferlänge* Argument auf einen Wert kleiner als 4 festgelegt und die *ColumnNumber*Argument auf 0 festgelegt SQLSTATE HY090 zurück (ungültige Zeichenfolgen- oder Pufferlänge). **SQLGetData** , allerdings kann das gleiche Lesezeichen abzurufenden mehrmals aufgerufen.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Wenn eine ODBC-3. *x* Anwendung arbeiten mit einer ODBC 2.* X* Treiber ruft **SQLSetStmtAttr** Attributs SQL_ATTR_USE_BOOKMARKS auf SQL_UB_VARIABLE festlegen möchten, wird der Treiber-Manager das Attribut auf SQL_UB_ON in der zugrunde liegenden ODBC 2.* X* Treiber.

