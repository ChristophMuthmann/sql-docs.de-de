---
title: SQLDescribeParam-Funktion | Microsoft Docs
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
apiname: SQLDescribeParam
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDescribeParam
helpviewer_keywords: SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df8d1653e158f19abf92eb1a650425213cbe393d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLDescribeParam** gibt die Beschreibung des eine parametermarkierung eine vorbereitete SQL­Anweisung zugeordnet. Diese Information ist auch in den Feldern von den IPD zur Verfügung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>Argument  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *ParameterNumber*  
 [Eingabe] Marker Parameternummer sortiert sequenziell in der Reihenfolge der zunehmenden Parameter, beginnend mit 1.  
  
 *DataTypePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem den SQL-Datentyp des Parameters zurückgegeben. Dieser Wert wird aus der SQL_DESC_CONCISE_TYPE-Datensatzfeld vom die IPD gelesen. Dadurch wird einer der Werte in der [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) Abschnitt Anhang D: Datentypen oder treiberspezifischen SQL-Datentyp.  
  
 In ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP im zurückgegeben  *\*DataTypePtr* für Datum, Uhrzeit oder Zeitstempeldaten bzw.; in ODBC 2.. *X*, SQL_DATE, SQL_TIME oder SQL_TIMESTAMP zurückgegeben. Der Treiber-Manager führt die erforderlichen Zuordnungen, wenn eine ODBC-2. *x* Anwendung arbeitet mit einer ODBC-3. *X* Treiber oder wenn eine ODBC 3.. *X* Anwendung arbeitet mit einer ODBC 2.. *X* Treiber.  
  
 Wenn *ColumnNumber* entspricht 0 (für eine Lesezeichenspalte), wird im SQL_BINARY zurückgegeben  *\*DataTypePtr* für Lesezeichen variabler Länge. (SQL_INTEGER wird zurückgegeben, wenn von einer ODBC 3. Lesezeichen verwendet werden. *x* Anwendung arbeiten mit einer ODBC 2.. *X* Treiber oder von einer ODBC 2.. *X* Anwendung arbeiten mit einem ODBC 3.. *X* Treiber.)  
  
 Weitere Informationen finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) in Anhang D:-Datentypen. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.  
  
 *ParameterSizePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Größe der Spalte oder des Ausdrucks der entsprechenden parametermarkierung in Zeichen zurückgegeben, wie von der Datenquelle definiert. Weitere Informationen zur Spaltengröße finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Anzahl der Dezimalstellen der Spalte oder einen Ausdruck mit dem entsprechenden Parameter zurückgegeben, wie von der Datenquelle definiert. Weitere Informationen über Dezimalstellen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem einen Wert zurückgegeben, der angibt, ob der Parameter NULL-Werte zulässt. Dieser Wert wird vom Feld SQL_DESC_NULLABLE die IPD gelesen. Einer der folgenden Typen:  
  
-   SQL_NO_NULLS: Der Parameter lässt keine NULL-Werte zu (Dies ist der Standardwert).  
  
-   SQL_NULLABLE: Der Parameter NULL-Werte zulässt.  
  
-   SQL_NULLABLE_UNKNOWN: Der Treiber kann nicht bestimmen, ob der Parameter NULL-Werte zulässt.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLDescribeParam** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLDescribeParam** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07009|Ungültiger Deskriptorindex|(DM) der Wert für das Argument angegebene *ParameterNumber* ist kleiner als 1.<br /><br /> Der Wert für das Argument angegebene *ParameterNumber* war größer als die Anzahl von Parametern in der zugeordneten SQL-Anweisung.<br /><br /> Die parametermarkierung ist Teil einer nicht-DML-Anweisung.<br /><br /> Die parametermarkierung war Bestandteil einer **wählen** Liste.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|21S01|Die Liste einzufügender Werte stimmt nicht mit Spaltenliste überein.|Die Anzahl von Parametern in der **einfügen** Anweisung entsprach nicht der Anzahl der Spalten in der Tabelle mit dem Namen in der Anweisung.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) die Funktion aufgerufen wurde vor dem Aufruf **SQLPrepare** oder **SQLExecDirect** für die *StatementHandle*.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLDescribeParam** Funktion aufgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Parametermarkierungen sind nummeriert, in der Reihenfolge der zunehmenden Parameter, beginnend mit 1, in der Reihenfolge, die sie in der SQL-Anweisung angezeigt werden.  
  
 **SQLDescribeParam** gibt nicht den Typ (Eingabe, Eingabe/Ausgabe- oder Ausgabeparameter) eines Parameters in einer SQL­Anweisung zurück. Ausgenommen sind alle Parameter im SQL-Anweisungen in Aufrufe von Prozeduren, Eingabeparameter. Um zu bestimmen, den Typ jedes Parameters in einem Aufruf an eine Prozedur, eine Anwendung ruft **SQLProcedureColumns**.  
  
 Weitere Informationen finden Sie unter [Parameter beschreiben](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel fordert den Benutzer für eine SQL-Anweisung, und klicken Sie dann die Anweisung vorbereitet. Als Nächstes ruft **SQLNumParams** zu bestimmen, ob die Anweisung keine Parameter enthält. Wenn die Anweisung Parameter enthält, ruft es **SQLDescribeParam** um diesen Parameter zu beschreiben und **SQLBindParameter** sie binden. Schließlich fordert den Benutzer für die Werte aller Parameter, und klicken Sie dann die Anweisung ausgeführt wird.  
  
```  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an einen parameter|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Vorbereiten einer Anweisung für die Ausführung|[SQLPrepare-Funktion](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
