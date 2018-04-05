---
title: SQLGetFunctions-Funktion | Microsoft Docs
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
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a38bc5d8e071efee286f726d75f6949243cbb77
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetFunctions** gibt Informationen dazu, ob ein Treiber eine bestimmte ODBC-Funktion unterstützt wird. Diese Funktion wird in der Treiber-Manager implementiert. Sie können auch im Treiber implementiert werden. Wenn ein Treiber implementiert **SQLGetFunctions**, der Treiber-Manager ruft die Funktion im Treiber. Andernfalls führt die Funktion selbst aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *FunctionId*  
 [Eingabe] Ein **#define** Wert ab, die ODBC-Funktion von Interesse; identifiziert. **SQL_API_ODBC3_ALL_FUNCTIONS OrSQL_API_ALL_FUNCTIONS**. **SQL_API_ODBC3_ALL_FUNCTIONS** werden von einer ODBC 3.*.x* Anwendung Unterstützung für ODBC 3. bestimmen*.x* und früheren Funktionen. **SQL_API_ALL_FUNCTIONS** wird von einer ODBC 2. verwendet*.x* Anwendung Unterstützung für ODBC 2. bestimmen*.x* und früheren Funktionen.  
  
 Eine Liste der **#define** Werte, die ODBC-Funktionen finden Sie unter den Tabellen in "Kommentare".  
  
 *SupportedPtr*  
 [Ausgabe]  Wenn *FunctionId* identifiziert eine ODBC-Funktion, *SupportedPtr* verweist auf ein einzelnes SQLUSMALLINT Wert, der SQL_TRUE, wenn die angegebene Funktion ist er nicht vom Treiber und SQL_FALSE unterstützt unterstützt.  
  
 Wenn *FunctionId* ist SQL_API_ODBC3_ALL_FUNCTIONS, *SupportedPtr* verweist auf ein SQLSMALLINT-Array mit einer Anzahl von Elementen SQL_API_ODBC3_ALL_FUNCTIONS_SIZE gleich. Dieses Array wird vom Treiber-Manager behandelt, als 4.000-Bit-Bitmap, die verwendet werden kann, um festzustellen, ob ein ODBC 3.*.x* oder earlier-Funktion unterstützt wird. Das Makro SQL_FUNC_EXISTS wird aufgerufen, um die funktionsunterstützung zu bestimmen. (Siehe "Kommentare".) Eine ODBC 3.*.x* Anwendung aufrufen kann **SQLGetFunctions** mit SQL_API_ODBC3_ALL_FUNCTIONS für eine ODBC-3.*.x* oder ODBC 2.*.x* Treiber.  
  
 Wenn *FunctionId* ist SQL_API_ALL_FUNCTIONS, *SupportedPtr* verweist auf ein Array SQLUSMALLINT von 100 Elementen. Das Array wird durch indiziert **#define** vom verwendeten Werten *FunctionId* identifizieren jede ODBC-Funktion; einige Elemente des Arrays sind, nicht verwendeter und für zukünftige Verwendung reserviert. Ein Element ist SQL_TRUE, wenn sie einer ODBC 2. identifiziert*.x* oder earlier-Funktion vom Treiber unterstützt werden. Es ist SQL_FALSE, wenn es eine ODBC-Funktion, die vom Treiber nicht unterstützt identifiziert oder eine ODBC-Funktion gibt nicht an.  
  
 Die Arrays, die **SupportedPtr* nullbasierte Indizierung verwendet.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetFunctions** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_DBC und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetFunctions** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------|-----|-----------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) **SQLGetFunctions** wurde aufgerufen, bevor **SQLConnect**, **SQLBrowseConnect**, oder **SQLDriverConnect**.<br /><br /> (DM) **SQLBrowseConnect** wurde aufgerufen, die *Verbindungshandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion aufgerufen wurde, bevor **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO oder SQL_SUCCESS zurückgegeben.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *Verbindungshandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY095|Funktionstyp außerhalb des gültigen Bereichs|(DM) eine ungültige *FunctionId* Wert angegeben wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
  
## <a name="comments"></a>Kommentare  
 **SQLGetFunctions** zurückgibt, die immer **SQLGetFunctions**, **SQLDataSources**, und **SQLDrivers** werden unterstützt. Es liegt daran, dass diese Funktionen in der Treiber-Manager implementiert werden. Der Treiber-Manager wird das entsprechende Unicode-Funktion eine ANSI-Funktion zuordnen, wenn Unicode-Funktion vorhanden ist und eine Unicode-Funktion an die entsprechende ANSI-Funktion zugeordnet werden, werden Wenn die ANSI-Funktion vorhanden ist. Informationen zur Verwendung von Anwendungen **SQLGetFunctions**, finden Sie unter [Übereinstimmungsebenen Schnittstelle](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 Im folgenden werden eine Liste der gültigen Werte für *FunctionId* für Funktionen, die der ISO-92-Ebene – die Einhaltung von Standards entsprechen:  
  
|FunctionId Wert|FunctionId Wert|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 Im folgenden werden eine Liste der gültigen Werte für *FunctionId* für Funktionen, die die Open Group-Ebene – die Einhaltung von Standards entsprechen:  
  
|FunctionId Wert|FunctionId Wert|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 Im folgenden werden eine Liste der gültigen Werte für *FunctionId* für Funktionen, die die ODBC-Ebene – die Einhaltung von Standards entsprechen.  
  
|FunctionId Wert|FunctionId Wert|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS [1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] bei der Arbeit mit einer ODBC 2.*.x* -Treiber **SQLBulkOperations** wird zurückgegeben, als nur unterstützt, wenn beide folgenden Bedingungen erfüllt sind: die ODBC 2.*.x* -Treiber unterstützt  **SQLSetPos**, und der Typ der Informationen SQL_POS_OPERATIONS gibt das SQL_POS_ADD Bit festgelegt.  
  
 Im folgenden werden eine Liste der gültigen Werte für *FunctionId* für Funktionen, die in ODBC 3.8 oder höher eingeführt:  
  
|FunctionId Wert|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** wird zurückgegeben, als nur unterstützt, wenn der Treiber sowohl unterstützt **SQLCancel** und **SQLCancelHandle**. Wenn **SQLCancel** wird unterstützt, aber **SQLCancelHandle** jedoch nicht, die Anwendung kann immer noch Aufrufen **SQLCancelHandle** für ein Anweisungshandle, da er zur zugeordnetwerdensollen **SQLCancel**.  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS-Makro  
 Die SQL_FUNC_EXISTS (*SupportedPtr*, *FunctionID*) Makro wird verwendet, um zu bestimmen, die Unterstützung von ODBC 3.*.x* oder Funktionen, die nach dem früheren **SQLGetFunctions**  aufgerufen wurde mit einem *FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS Argument. Ruft die Anwendung SQL_FUNC_EXISTS mit der *SupportedPtr* Argument festgelegt wird, um die *SupportedPtr* übergebene *SQLGetFunctions*, und mit der  *FunctionID* Argument festgelegt wird, um die **#define** für die Funktion. SQL_FUNC_EXISTS gibt SQL_TRUE, wenn die Funktion unterstützt wird und SQL_FALSE andernfalls zurück.  
  
> [!NOTE]  
>  Bei der Arbeit mit einer ODBC 2.*.x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Managers zurück SQL_TRUE für **SQLAllocHandle** und **SQLFreeHandle**da **SQLAllocHandle** zugeordnet **SQLAllocEnv**, **SQLAllocConnect**, oder **SQLAllocStmt:**, und Da **SQLFreeHandle** zugeordnet **SQLFreeEnv**, **SQLFreeConnect**, oder **SQLFreeStmt**. **SQLAllocHandle** oder **SQLFreeHandle** mit einem *HandleType* Argument SQL_HANDLE_DESC wird nicht unterstützt, allerdings, obwohl SQL_TRUE für die Funktionen, die zurückgegeben wird, denn es gibt keine ODBC 2.*.x* Funktion in diesem Fall zuzuordnen.  
  
## <a name="code-example"></a>Codebeispiel  
 Die folgenden drei Beispiele zeigen, wie eine Anwendung verwendet **SQLGetFunctions** zu bestimmen, ob ein Treiber unterstützt **SQLTables**, **SQLColumns**, und  **SQLStatistics**. Wenn der Treiber diese Funktionen nicht unterstützt, trennt die Anwendung aus dem Treiber. Im ersten Beispiel wird **SQLGetFunctions** einmal für jede Funktion.  
  
```  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 Im zweiten Beispiel ruft die Anwendung ODBC 3.x **SQLGetFunctions** und übergibt ein Array in der **SQLGetFunctions** gibt Informationen über alle ODBC 3.x und früheren Funktionen.  
  
```  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 Im dritte Beispiel wird eine ODBC 2.x-Anwendung ruft **SQLGetFunctions** und übergibt ein Array von 100 Elementen in der **SQLGetFunctions** gibt Informationen über alle ODBC 2.x und früheren Funktionen.  
  
```  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Zurückgeben von Informationen zu einer Datenquelle oder Treiber|[SQLGetInfo-Funktion](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Die Einstellung eines Attributs Anweisung zurückgeben|[SQLGetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
