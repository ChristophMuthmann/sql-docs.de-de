---
title: SQLBindParameter-Funktion | Microsoft Docs
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
- SQLBindParameter
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 299e4ced3e6047f7d3e205d384d3191d43e70ef1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLBindParameter** bindet einen Puffer an eine parametermarkierung in einer SQL­Anweisung. **SQLBindParameter** unterstützt die Bindung an eine Unicode-C-Datentyp, selbst wenn der zugrunde liegende Treiber Unicode-Daten nicht unterstützt.  
  
> [!NOTE]  
>  Diese Funktion ersetzt die Funktion ODBC 1.0 **SQLSetParam**. Weitere Informationen finden Sie unter "Kommentare".  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *ParameterNumber*  
 [Eingabe] Parameter, mit der Nummer sortiert sequenziell in der Reihenfolge der zunehmenden Parameter, beginnend mit 1.  
  
 *InputOutputType*  
 [Eingabe] Der Typ des Parameters. Weitere Informationen finden Sie unter "*InputOutputType* Argument" in "Kommentare".  
  
 *Werttyp*  
 [Eingabe] Der C-Datentyp des Parameters. Weitere Informationen finden Sie unter "*ValueType* Argument" in "Kommentare".  
  
 *ParameterType*  
 [Eingabe] Der SQL-Datentyp des Parameters. Weitere Informationen finden Sie unter "*ParameterType* Argument" in "Kommentare".  
  
 *ColumnSize*  
 [Eingabe] Die Größe der Spalte oder des Ausdrucks der entsprechenden parametermarkierung. Weitere Informationen finden Sie unter "*ColumnSize* Argument" in "Kommentare".  
  
 Wenn die Anwendung auf einem 64-Bit-Windows-Betriebssystem ausgeführt wird, finden Sie unter [ODBC-64-Bit-Informationen](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Eingabe] Die Dezimalstellen der Spalte oder des Ausdrucks der entsprechenden parametermarkierung. Weitere Informationen zur Spaltengröße finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Verzögerte Eingabe] Ein Zeiger auf einen Puffer für den Parameter-Daten. Weitere Informationen finden Sie unter "*ParameterValuePtr* Argument" in "Kommentare".  
  
 *Pufferlänge*  
 [Eingabe/Ausgabe] Länge der *ParameterValuePtr* Puffers in Bytes. Weitere Informationen finden Sie unter "*Pufferlänge* Argument" in "Kommentare".  
  
 Finden Sie unter [ODBC-64-Bit-Informationen](../../../odbc/reference/odbc-64-bit-information.md), wenn die Anwendung auf einem 64-Bit-Betriebssystem ausgeführt wird.  
  
 *StrLen_or_IndPtr*  
 [Verzögerte Eingabe] Ein Zeiger auf einen Puffer für die Länge des Parameters. Weitere Informationen finden Sie unter "*StrLen_or_IndPtr* Argument" in "Kommentare".  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLBindParameter** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLBindParameter** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datentyp von identifiziert die *ValueType* Argument kann nicht in den identifizierten Datentyp konvertiert werden die *ParameterType* Argument. Dieser Fehler zurückgegeben werden kann, durch **SQLExecDirect**, **SQLExecute**, oder **SQLPutData** zum Zeitpunkt der Ausführung anstatt von **SQLBindParameter**.|  
|07009|Ungültiger Deskriptorindex|(DM) der Wert für das Argument angegebene *ParameterNumber* war kleiner als 1.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der **MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY003|Ungültiger Anwendungspuffertyp|Der Wert, der durch das Argument angegebenen *ValueType* war keinem gültigen C-Datentyp oder SQL_C_DEFAULT.|  
|HY004|Ungültiger SQL-Datentyp|Der Wert für das Argument angegebene *ParameterType* war weder eine gültige ODBC SQL-Datentypbezeichner noch eine treiberspezifischen SQL Datentypbezeichner vom Treiber unterstützt werden.|  
|HY009|Ungültiger Argumentwert|(DM) das Argument *ParameterValuePtr* wurde ein null-Zeiger ist das Argument *StrLen_or_IndPtr* wurde ein null-Zeiger und das Argument *InputOutputType* war nicht SQL_PARAM_ DIE AUSGABE.<br /><br /> SQL_PARAM_OUTPUT (DM), wobei das Argument *ParameterValuePtr* wurde ein null-Zeiger wurde von der C-Typ Char oder Binary und die Pufferlänge (*CbValueMax*) war größer als 0.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn **SQLBindParameter** aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY021|Inkonsistente Deskriptorinformationen|Die Deskriptorinformationen während einer konsistenzprüfung aktiviert war nicht konsistent. (Siehe Abschnitt "Konsistenzprüfungen" in **SQLSetDescField**.)<br /><br /> Der Wert für das Argument angegebene *DecimalDigits* lag außerhalb des Bereichs von Werten, die von der Datenquelle für eine Spalte mit der angegebenen SQL-Datentyp unterstützt die *ParameterType* Argument.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) den Wert in *Pufferlänge* war kleiner als 0. (Siehe dazu die Beschreibung in das SQL_DESC_DATA_PTR-Feld **SQLSetDescField**.)|  
|HY104|Ungültiger Wert für Genauigkeit oder Dezimalstellen|Der Wert für das Argument angegebene *ColumnSize* oder *DecimalDigits* lag außerhalb des Bereichs von Werten, die von der Datenquelle für eine Spalte mit der angegebenen SQL-Datentyp unterstützt die  *ParameterType* Argument.|  
|HY105|Ungültiger Parametertyp|(DM) der Wert für das Argument angegebene *InputOutputType* war ungültig. (Siehe "Kommentare".)|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht die Konvertierung angegeben, durch die Kombination der Wert für das Argument angegebene *ValueType* und der treiberspezifischen-Wert, der für das Argument angegebene *ParameterType*.<br /><br /> Der Wert für das Argument angegebene *ParameterType* wurde eine gültige ODBC SQL-Datentypbezeichner, für den ODBC-Version vom Treiber unterstützt, jedoch wurde durch den Treiber oder die Datenquelle nicht unterstützt.<br /><br /> Der Treiber unterstützt nur ODBC 2. *x* und dem Argument *ValueType* war es eines der folgenden:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> und die Intervall-C-Datentypen in [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) in Anhang D:-Datentypen.<br /><br /> Der Treiber unterstützt nur die ODBC-Versionen vor 3.50 und dem Argument *ValueType* SQL_C_GUID wurde.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Ruft die Anwendung **SQLBindParameter** jede parametermarkierung in einer SQL-Anweisung zu binden. Bindungen bleiben wirksam, bis die Anwendung ruft **SQLBindParameter** wiederum ruft **SQLFreeStmt** mit der Option SQL_RESET_PARAMS oder Aufrufe **SQLSetDescField** an das Headerfeld SQL_DESC_COUNT APD auf 0 festgelegt.  
  
 Weitere Informationen zu Parametern finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md). Weitere Informationen zu Parameterdatentypen und parametermarkierungen, finden Sie unter [Parameterdatentypen](../../../odbc/reference/appendixes/parameter-data-types.md) und [Parametermarkierungen](../../../odbc/reference/appendixes/parameter-markers.md) in Anhang C: SQL-Grammatik.  
  
## <a name="parameternumber-argument"></a>ParameterNumber-Argument  
 Wenn *ParameterNumber* im Aufruf **SQLBindParameter** ist größer als der Wert der SQL_DESC_COUNT, **SQLSetDescField** wird aufgerufen, um den Wert der SQL_DESC_ erhöhen Anzahl der zu *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>InputOutputType-Argument  
 Die *InputOutputType* Argument gibt den Typ des Parameters. Dieses Argument legt die SQL_DESC_PARAMETER_TYPE Feld die IPD fest. Alle Parameter im SQL-Anweisungen, die keine Prozeduren, z. B. Aufrufen **einfügen** -Anweisungen sind *input**Parameter*. In Prozeduraufrufen können eingegeben werden, Eingabe/Ausgabe- oder Ausgabeparameter enthalten. (Eine Anwendung ruft **SQLProcedureColumns** zum Bestimmen des Typs eines Parameters in einem Prozeduraufruf; Parameter, dessen Typ kann nicht bestimmt, werden als Eingabeparameter angesehen.)  
  
 Die *InputOutputType* Argument ist einer der folgenden Werte:  
  
-   SQL_PARAM_INPUT. Der Parameter kennzeichnet einen Parameter in einer SQL­Anweisung, die keine Prozedur z. B. aufruft ein **einfügen** -Anweisung, oder kennzeichnet einen Eingabeparameter in einer Prozedur. Beispielsweise die Parameter in **INSERT in Mitarbeiter VALUES (?,?,?)**  Eingabeparameter zulässig; Sie sind, während die Parameter in **{AddEmp aufrufen (?,?,?)}**  ist möglich, jedoch nicht notwendigerweise, Eingabeparameter.  
  
     Wenn die Anweisung ausgeführt wird, sendet der Treiber Daten für den Parameter an die Datenquelle an. die \* *ParameterValuePtr* Puffer muss einen gültigen Eingabewert enthalten oder **StrLen_or_IndPtr* Puffer enthalten muss, SQL_NULL_DATA, SQL_DATA_AT_EXEC oder das Ergebnis der SQL_LEN_DATA_AT _EXEC-Makro.  
  
     Wenn eine Anwendung den Typ eines Parameters in einem Prozeduraufruf bestimmen kann, legt *InputOutputType* auf SQL_PARAM_INPUT; Wenn die Datenquelle gibt einen Wert für den Parameter zurück, verwirft der Treiber es.  
  
-   SQL_PARAM_INPUT_OUTPUT AN. Der Parameter kennzeichnet ein Eingabe-/Ausgabeparameter in einer Prozedur. Z. B. der Parameter im **{aufrufen GetEmpDept(?)}**  ist ein e/a-Parameter, der den Namen eines Mitarbeiters akzeptiert und gibt den Namen des Mitarbeiters Abteilung zurück.  
  
     Wenn die Anweisung ausgeführt wird, sendet der Treiber Daten für den Parameter an die Datenquelle an. die \* *ParameterValuePtr* Puffer muss einen gültigen Eingabewert enthalten oder die \* *StrLen_or_IndPtr* SQL_NULL_DATA, SQL_DATA_AT_EXEC oder das Ergebnis des Puffers darf das Makro SQL_LEN_DATA_AT_EXEC. Nachdem die Anweisung ausgeführt wird, gibt der Treiber Daten für den Parameter an die Anwendung zurück. Wenn die Datenquelle nicht für eine Eingabe/Ausgabe-Parameter einen Wert zurückgibt, wird der Treiber setzt die **StrLen_or_IndPtr* Puffer auf SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Wenn eine Anwendung ODBC 1.0 aufruft **SQLSetParam** in ODBC 2.0-Treiber, der Treiber-Manager konvertiert diese zu einem Aufruf von **SQLBindParameter** in dem die *InputOutputType* Argument ist auf SQL_PARAM_INPUT_OUTPUT festgelegt.  
  
-   SQL_PARAM_OUTPUT. Der Parameter kennzeichnet den Rückgabewert einer Prozedur oder ein Output-Parameter in einer Prozedur; in beiden Fällen werden diese als bezeichnet *Ausgabeparameter*. Z. B. der Parameter im **{? = aufrufen GetNextEmpID}** ist ein Ausgabeparameter, der die nächste Mitarbeiter-ID zurückgibt.  
  
     Nachdem die Anweisung ausgeführt wird, gibt der Treiber Daten für den Parameter an die Anwendung, es sei denn, die *ParameterValuePtr* und *StrLen_or_IndPtr* Argumente sind beide null-Zeiger in diesem Fall die Treiber verwirft den Ausgabewert. Wenn die Datenquelle, die nicht über einen Wert für ein Output-Parameter zurückgibt, wird der Treiber setzt die **StrLen_or_IndPtr* Puffer auf SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Gibt an, dass ein Eingabe-/Ausgabeparameter gestreamt werden sollen. **SQLGetData** Parameterwerte in Teilen lesen können. *Pufferlänge* wird ignoriert, da die Länge des Puffers beim Aufruf von bestimmt wird **SQLGetData**. Der Wert von der *StrLen_or_IndPtr* Puffer muss SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC oder das Ergebnis des SQL_LEN_DATA_AT_EXEC Makros enthalten. Wenn es an der Ausgabe gestreamt wird, muss ein Parameter als Data-at-Execution (DAE) Parameter an der Eingabe gebunden werden. *ParameterValuePtr* kann jeder nicht-Null-Zeiger-Wert, der zurückgegebenen **SQLParamData** wie, dessen Wert die benutzerdefinierten token-übergebene mit *ParameterValuePtr* für beide Eingaben und die Ausgabe. Weitere Informationen finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Identisch mit SQL_PARAM_INPUT_OUTPUT_STREAM, für ein Output-Parameter. **StrLen_or_IndPtr* wird an der Eingabe ignoriert.  
  
 Die folgende Tabelle enthält verschiedene Kombinationen von *InputOutputType* und **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Ergebnis|Deaktivieren Sie auf ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*Len*) oder SQL_DATA_AT_EXEC|Eingabe in Teilen|*ParameterValuePtr* kann ausnahmslos Zeiger zurückgegebenen **SQLParamData** wie, dessen Wert die benutzerdefinierten token-übergebene mit *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Nicht SQL_LEN_DATA_AT_EXEC (*Len*) oder SQL_DATA_AT_EXEC|Eingabe gebunden Puffer|*ParameterValuePtr* ist die Adresse des Eingabepuffers.|  
|SQL_PARAM_OUTPUT|An der Eingabe ignoriert.|Gebundene Ausgabepuffer|*ParameterValuePtr* ist die Adresse des Ausgabepuffers.|  
|SQL_PARAM_OUTPUT_STREAM|An der Eingabe ignoriert.|Ausgabestream|*ParameterValuePtr* kann keinem Zeigerwert, der zurückgegebenen **SQLParamData** wie, dessen Wert die benutzerdefinierten token-übergebene mit *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT AN|SQL_LEN_DATA_AT_EXEC (*Len*) oder SQL_DATA_AT_EXEC|Eingabe in Teilen und gebundene Ausgabepuffer|*ParameterValuePtr* ist die Adresse des Ausgabepuffers, die auch von zurückgegeben werden **SQLParamData** wie, dessen Wert die benutzerdefinierten token-übergebene mit *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT AN|Nicht SQL_LEN_DATA_AT_EXEC (*Len*) oder SQL_DATA_AT_EXEC|Eingabe gebunden, Puffer und gebundene Ausgabepuffer|*ParameterValuePtr* ist die Adresse des freigegebenen e/a-Puffers.|  
L_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*Len*) oder SQL_DATA_AT_EXEC|Eingabe in Teilen und gestreamte Ausgabe|*ParameterValuePtr* kann beliebiger Zeigerwert ungleich Null-, die von zurückgegeben werden sein **SQLParamData** wie, dessen Wert die benutzerdefinierten token-übergebene mit *ParameterValuePtr* für beide Eingabe und Ausgabe.|  
  
> [!NOTE]  
>  Der Treiber muss entscheiden, welche SQL-Typen zulässig sind, wenn eine Anwendung eines Ausgabe- oder i / o-Parameter gebunden, wie gestreamt. Der Treiber-Manager generiert keinen Fehler für eine ungültige SQL-Typ.  
  
## <a name="valuetype-argument"></a>ValueType-Argument  
 Die *ValueType* Argument gibt den C-Datentyp des Parameters. Dieses Argument legt die SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE Felder der APD fest. Diese Angabe muss einen der Werte in der [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) Abschnitt Anhang D:-Datentypen.  
  
 Wenn die *ValueType* -Argument ist eines der Intervalldatentypen das SQL_DESC_TYPE-Feld der der *ParameterNumber* Datensatz APD SQL_INTERVAL festgelegt ist, Feld SQL_DESC_CONCISE_TYPE in APD auf festgelegt ist präzise Intervall-Datentyp und die SQL_DESC_DATETIME_INTERVAL_CODE Felder die *ParameterNumber* Datensatz auf eine Subcode für den bestimmten Intervall-Datentyp festgelegt ist. (Siehe [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).) Das Standardintervall führende Genauigkeit (2) und Intervall Sekunden standardgenauigkeit (6), wie in den Feldern SQL_DESC_DATETIME_INTERVAL_PRECISION und SQL_DESC_PRECISION der APD, festgelegt, werden für die Daten verwendet. Wenn entweder standardgenauigkeit nicht geeignet ist, die Anwendung sollten explizit festlegen das Deskriptorfeld durch einen Aufruf von **SQLSetDescField** oder **SQLSetDescRec**.  
  
 Wenn die *ValueType* -Argument ist eines der Datentypen "DateTime", das SQL_DESC_TYPE-Feld der der *ParameterNumber* Datensatz APD auf SQL_DATETIME Feld SQL_DESC_CONCISE_TYPE der festgelegt*ParameterNumber* Datensatz APD präzise "DateTime" C-Datentyp und Feld SQL_DESC_DATETIME_INTERVAL_CODE festgelegt ist die *ParameterNumber* Datensatz auf eine Subcode für den bestimmten "DateTime" festgelegt ist -Datentyp. (Siehe [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Wenn die *ValueType* Argument ist ein SQL_C_NUMERIC-Datentyp, der die standardgenauigkeit (also treiberdefinierten) und der Standardwert für die Dezimalstellen (0), wie in den Feldern SQL_DESC_PRECISION und SQL_DESC_SCALE der APD, festgelegt werden für die Daten verwendet. Wenn die Standardwerte für die Genauigkeit oder Skala nicht geeignet ist, die Anwendung sollten explizit festlegen das Deskriptorfeld durch einen Aufruf von **SQLSetDescField** oder **SQLSetDescRec**.  
  
 SQL_C_DEFAULT gibt an, dass der Wert des Parameters vom Standard-C-Datentyp übertragen werden, für der SQL-Datentyp mit angegebenen *ParameterType*.  
  
 Sie können auch einen erweiterte C-Datentyp angeben. Weitere Informationen finden Sie unter [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Weitere Informationen finden Sie unter [C-Standarddatentypen](../../../odbc/reference/appendixes/default-c-data-types.md), [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), und [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) in Anhang D:-Datentypen.  
  
## <a name="parametertype-argument"></a>ParameterType-Argument  
 Diese Angabe muss einen der Werte aufgeführt, die der [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) Abschnitt Anhang D:-Datentypen, oder es muss es sich um eine treiberspezifische-Wert. Dieses Argument legt die SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE Felder von der IPD fest.  
  
 Wenn die *ParameterType* Argument ist einer der Bezeichner "DateTime", das SQL_DESC_TYPE-Feld der IPD auf SQL_DATETIME festgelegt ist, die präzise "DateTime" SQL-Datentyp und die SQL_DESC_ Feld SQL_DESC_CONCISE_TYPE die IPD festgelegt ist DATETIME_INTERVAL_CODE Feld ist auf den entsprechenden "DateTime" subcodewert festgelegt.  
  
 Wenn *ParameterType* ist ein Bezeichner Intervall das SQL_DESC_TYPE-Feld der IPD auf SQL_INTERVAL festgelegt ist, das SQL_DESC_CONCISE_TYPE-Feld, der die IPD präzise SQL Intervall-Datentyp und die SQL_DESC_DATETIME_ festgelegt ist Die IPD INTERVAL_CODE Feld wird auf dem Subcode angemessenen Abständen festgelegt. Feld SQL_DESC_DATETIME_INTERVAL_PRECISION die IPD der führenden Intervall-Genauigkeit festgelegt ist, und Feld SQL_DESC_PRECISION der Intervall Sekunden Genauigkeit festgelegt ist, falls zutreffend. Wenn der Wert von SQL_DESC_DATETIME_INTERVAL_PRECISION oder SQL_DESC_PRECISION nicht geeignet ist, die Anwendung sollten explizit festlegen es durch den Aufruf **SQLSetDescField**. Weitere Informationen zu diesen Feldern finden Sie unter [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Wenn die *ValueType* Argument ist ein SQL_NUMERIC-Datentyp, der die standardgenauigkeit (also treiberdefinierten) und der Standardwert für die Dezimalstellen (0) als Gruppe in den Feldern SQL_DESC_PRECISION und SQL_DESC_SCALE, der die IPD sind für die Daten verwendet. Wenn die Standardwerte für die Genauigkeit oder Skala nicht geeignet ist, die Anwendung sollten explizit festlegen das Deskriptorfeld durch einen Aufruf von **SQLSetDescField** oder **SQLSetDescRec**.  
  
 Weitere Informationen dazu, wie die Daten konvertiert werden, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) und [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) in Anhang D:-Datentypen.  
  
## <a name="columnsize-argument"></a>ColumnSize-Argument  
 Die *ColumnSize* Argument gibt die Größe der Spalte oder des Ausdrucks, der an die parametermarkierung, die Länge der Daten oder beides entspricht. Dieses Argument legt verschiedene Felder eines IPD, abhängig von der SQL-Datentyp (der *ParameterType* Argument). Die folgenden Regeln gelten für diese Zuordnung:  
  
-   Wenn *ParameterType* SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, oder einem der präzisen SQL "DateTime" oder ein Zeitintervall Datentypen, Feld SQL_DESC_LENGTH die IPD festgelegt ist auf den Wert des  *ColumnSize*. (Weitere Informationen finden Sie unter der [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) Abschnitt im Anhang D:-Datentypen.)  
  
-   Wenn *ParameterType* ist SQL_DECIMAL SQL_NUMERIC, SQL_FLOAT SQL_REAL oder SQL_DOUBLE, Feld SQL_DESC_PRECISION die IPD festgelegt ist, auf den Wert der *ColumnSize*.  
  
-   Für andere Datentypen die *ColumnSize* Argument wird ignoriert.  
  
 Weitere Informationen finden Sie unter "Übergeben von Parameterwerten" und SQL_DATA_AT_EXEC in "*StrLen_or_IndPtr* Argument."  
  
## <a name="decimaldigits-argument"></a>DecimalDigits-Argument  
 Wenn *ParameterType* SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND oder SQL_INTERVAL_MINUTE_TO_SECOND, ist das SQL_DESC_PRECISION-Feld, der die IPD festgelegt ist um *DecimalDigits*. Wenn *ParameterType* ist SQL_NUMERIC oder SQL_DECIMAL, Feld SQL_DESC_SCALE die IPD festgelegt ist, um *DecimalDigits*. Für alle anderen Datentypen die *DecimalDigits* Argument wird ignoriert.  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr-Argument  
 Die *ParameterValuePtr* Argument verweist auf einen Puffer, wenn **SQLExecute** oder **SQLExecDirect** aufgerufen wird, enthält die eigentlichen Daten für den Parameter. Die Daten in Form von angegeben werden müssen die *ValueType* Argument. Dieses Argument legt das SQL_DESC_DATA_PTR-Feld des APD fest. Eine Anwendung kann festlegen, die *ParameterValuePtr* Argument für ein null-Zeiger, solange  *\*StrLen_or_IndPtr* SQL_NULL_DATA oder SQL_DATA_AT_EXEC ist. (Dies trifft nur zu Eingabe-oder e/a).  
  
 Wenn \* *StrLen_or_IndPtr* ist das Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*)-Makro oder SQL_DATA_AT_EXEC, klicken Sie dann *ParameterValuePtr* ist ein anwendungsdefinierte Zeigerwert, der mit dem Parameter zugeordnet ist. Es wird zurückgegeben, um die Anwendung über **SQLParamData**. Beispielsweise *ParameterValuePtr* ein Token nicht 0 (null), z. B. einen Parameter mit der Nummer, die einen Zeiger auf Daten oder ein Zeiger auf eine Struktur, die die Anwendung mit dem Eingabeparameter gebunden werden kann. Beachten Sie jedoch, auch wenn der Parameter ist ein Eingabe-/Ausgabeparameter *ParameterValuePtr* muss ein Zeiger auf einen Puffer, in dem der Ausgabewert gespeichert, sein. Wenn der Wert in das Anweisungsattribut SQL_ATTR_PARAMSET_SIZE größer als 1 ist, können die Anwendung den Wert verweist das SQL_ATTR_PARAMS_PROCESSED_PTR-Anweisungsattribut zusammen mit den *ParameterValuePtr* Argument. Beispielsweise *ParameterValuePtr* möglicherweise zeigen Sie auf ein Array von Werten und die Anwendung möglicherweise verwenden Sie den Wert SQL_ATTR_PARAMS_PROCESSED_PTR verweist auf den richtigen Wert aus dem Array abzurufen. Weitere Informationen finden Sie unter "Übergeben von Parameterwerte" weiter unten in diesem Abschnitt.  
  
 Wenn die *InputOutputType* Argument ist SQL_PARAM_INPUT_OUTPUT oder SQL_PARAM_OUTPUT, *ParameterValuePtr* verweist auf einen Puffer, in dem der Treiber den Ausgabewert zurückgibt. Wenn die Prozedur eine oder mehrere Resultsets zurückgibt, die \* *ParameterValuePtr* Puffer ist garantiert nicht festgelegt werden, bis alle Ergebnis legt/Zeilenanzahl verarbeitet wurden. Wenn der Puffer nicht festgelegt ist, bis die Verarbeitung abgeschlossen ist, sind die Output-Parameter und Rückgabewerte nicht verfügbar, bis **SQLMoreResults** gibt SQL_NO_DATA zurück. Aufrufen von **SQLCloseCursor** oder **SQLFreeStmt** mit einer Option SQL_CLOSE führt dazu, dass diese Werte verworfen werden.  
  
 Wenn der Wert in das Anweisungsattribut SQL_ATTR_PARAMSET_SIZE größer als 1 ist, ist *ParameterValuePtr* verweist auf ein Array. Eine einzelne SQL-Anweisung verarbeitet die vollständige Array der Eingabewerte für einen Eingabe- oder e/a-Parameter und gibt ein Array von Ausgabewerte für eine Eingabe/Ausgabe- oder Output-Parameter.  
  
## <a name="bufferlength-argument"></a>Pufferlänge-Argument  
 Für Zeichen- und Binärdaten C die *Pufferlänge* Argument gibt die Länge des der \* *ParameterValuePtr* Puffer (wenn es sich um ein einzelnes Element ist) oder die Länge eines Elements in der \* *ParameterValuePtr* array (wenn der Wert in das Anweisungsattribut SQL_ATTR_PARAMSET_SIZE größer als 1 ist). Dieses Argument legt die SQL_DESC_OCTET_LENGTH-Datensatzfeld vom APD fest. Wenn die Anwendung mehrere Werte gibt *Pufferlänge* wird verwendet, um zu bestimmen, den Speicherort der Werte in der **ParameterValuePtr* array, bei der Eingabe und Ausgabe. Eingabe/Ausgabe- und Ausgabeparameter-Parameter wird es verwendet, zu bestimmen, ob zum Abschneiden von Zeichen- und Binärdaten von C in der Ausgabe:  
  
-   Für C Zeichendaten, wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *Pufferlänge*, die Daten in \* *ParameterValuePtr* auf abgeschnitten  *Pufferlänge* abzüglich der Länge von einer Null-Abschlusszeichen und wird vom Treiber Null-terminiert.  
  
-   Für C Binärdaten, wenn die Anzahl der zurückzugebenden verfügbaren Bytes überschreitet *Pufferlänge*, die Daten in \* *ParameterValuePtr* auf abgeschnitten *Pufferlänge*Bytes.  
  
 Für alle anderen Typen von C-Daten die *Pufferlänge* Argument wird ignoriert. Die Länge des der \* *ParameterValuePtr* Puffer (wenn es sich um ein einzelnes Element ist) oder die Länge eines Elements in der \* *ParameterValuePtr* array (wenn die Anwendung, aufruft **SQLSetStmtAttr** mit einem *Attribut* Argument SQL_ATTR_PARAMSET_SIZE auf mehrere Werte für jeden Parameter angeben) wird davon ausgegangen, dass die Länge der C-Datentyp.  
  
 Für die gestreamte Ausgabe- oder gestreamte Eingabe-/Ausgabeparameter der *Pufferlänge* Argument wird ignoriert, da die Länge des Puffers in angegeben sind **SQLGetData**.  
  
> [!NOTE]  
>  Wenn eine Anwendung ODBC 1.0 aufruft **SQLSetParam** in einer ODBC-3. *X* Treiber, der Treiber-Manager konvertiert diese zu einem Aufruf von **SQLBindParameter** in dem die *Pufferlänge* Argument weist immer SQL_SETPARAM_VALUE_MAX. Da der Treiber-Manager einen Fehler Wenn eine ODBC 3. zurückgibt. *x* setzt *Pufferlänge* zu SQL_SETPARAM_VALUE_MAX, eine ODBC 3. *X* Treiber kann Hiermit können Sie bestimmen, wann sie von einer ODBC-1.0-Anwendung aufgerufen wird.  
  
> [!NOTE]  
>  In **SQLSetParam**die Möglichkeit, in dem eine Anwendung die Länge des gibt, der **ParameterValuePtr* zu Puffern, damit der Treiber zurückkehren kann, Zeichen- oder Binärdaten und die Möglichkeit, in dem eine Anwendung sendet, eine Array von Zeichen oder binäre Parameterwerte an den Treiber sind treiberdefinierten.  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr-Argument  
 Die *StrLen_or_IndPtr* Argument verweist auf einen Puffer, wenn **SQLExecute** oder **SQLExecDirect** aufgerufen wird, enthält mindestens eine der folgenden. (Dieses Argument stellt die SQL_DESC_OCTET_LENGTH_PTR und SQL_DESC_INDICATOR_PTR Datensatzfelder der Anwendung Parameter Zeiger.)  
  
-   Die Länge des Parameterwerts im gespeicherten **ParameterValuePtr*. Dies wird mit Ausnahme von Zeichen- oder Binärdaten C ignoriert.  
  
-   SQL_NTS. Der Wert des Parameters ist eine Null-terminierte Zeichenfolge.  
  
-   SQL_NULL_DATA. Der Parameterwert ist NULL.  
  
-   SQL_DEFAULT_PARAM. Eine Prozedur ist die Verwendung den Standardwert eines Parameters, statt eines Werts aus der Anwendung abgerufen. Dieser Wert gilt nur in einer Prozedur, die aufgerufen wird, in der kanonischen ODBC-Syntax, und klicken Sie dann nur, wenn die *InputOutputType* Argument ist SQL_PARAM_INPUT oder SQL_PARAM_INPUT_OUTPUT SQL_PARAM_INPUT_OUTPUT_STREAM. Wenn \* *StrLen_or_IndPtr* SQL_DEFAULT_PARAM, ist die *ValueType*, *ParameterType*, *ColumnSize*,  *DecimalDigits*, *Pufferlänge*, und *ParameterValuePtr* Argumente für Eingabeparameter ignoriert werden und werden verwendet, um den Wert des Ausgabeparameters für die Eingabe zu definieren / Output-Parameter.  
  
-   Das Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro. Die Daten für den Parameter mit gesendet werden, **SQLPutData**. Wenn die *ParameterType* Argument ist SQL_LONGVARBINARY, SQL_LONGVARCHAR oder einen langen Daten datenquellenspezifischen-Datentyp, und gibt "Y" für den Typ der SQL_NEED_LONG_DATA_LEN-Informationen in der Treiber **SQLGetInfo**, *Länge* ist die Anzahl der Bytes der Daten für den Parameter; gesendet werden sollen, andernfalls *Länge* muss ein nicht negativen Wert und wird ignoriert. Weitere Informationen finden Sie unter "Übergeben Parameterwerte" weiter unten in diesem Abschnitt.  
  
     Um beispielsweise anzugeben, dass mit 10.000 Datenbytes gesendet wird **SQLPutData** in einen oder mehrere Aufrufe für einen Parameter SQL_LONGVARCHAR eine Anwendung festlegt **StrLen_or_IndPtr* auf SQL_LEN_DATA_AT_EXEC ( 10000).  
  
-   SQL_DATA_AT_EXEC. Die Daten für den Parameter mit gesendet werden, **SQLPutData**. Dieser Wert wird von ODBC 1.0-Anwendungen, die beim Aufruf von ODBC 3. *x* Treiber. Weitere Informationen finden Sie unter "Übergeben Parameterwerte" weiter unten in diesem Abschnitt.  
  
 Wenn *StrLen_or_IndPtr* ist ein null-Zeiger der Treiber wird davon ausgegangen, dass alle Werte der Eingabeparameter ungleich NULL sind und-Zeichen und Binärdatentypen Null-terminiert ist. Wenn *InputOutputType* ist SQL_PARAM_OUTPUT oder SQL_PARAM_OUTPUT_STREAM und *ParameterValuePtr* und *StrLen_or_IndPtr* sind beide null-Zeiger, der Treiber verwirft der Ausgabewert.  
  
> [!NOTE]  
>  Anwendungsentwickler sind dringend davon abgeraten, von der Angabe von null-Zeiger für *StrLen_or_IndPtr* Wenn der Datentyp des Parameters SQL_C_BINARY ist. Um sicherzustellen, dass ein Treiber nicht unerwartet SQL_C_BINARY-Daten abgeschnitten *StrLen_or_IndPtr* muss einen Zeiger auf eine gültige Länge-Wert enthalten.  
  
 Wenn die *InputOutputType* Argument ist SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM oder SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* verweist auf einen Puffer, in dem die Treiber zurückgibt, SQL_NULL_DATA, die Anzahl der zurückzugebenden in verfügbaren Bytes \* *ParameterValuePtr* (ausgenommen die Null-Terminierung Byte Zeichendaten,) oder SQL_NO_TOTAL (wenn die Anzahl der Bytes, die zur Verfügung Return kann nicht ermittelt werden). Wenn die Prozedur eine oder mehrere Resultsets zurückgibt, den **StrLen_or_IndPtr* Puffer ist garantiert nicht festgelegt werden, bis alle Ergebnisse abgerufen wurden.  
  
 Wenn der Wert in das Anweisungsattribut SQL_ATTR_PARAMSET_SIZE größer als 1 ist, ist *StrLen_or_IndPtr* verweist auf ein Array von Werten SQLLEN. Diese können beliebige Werte, die weiter oben in diesem Abschnitt aufgeführten und verarbeitet werden, werden mit einer einzigen SQL­Anweisung.  
  
## <a name="passing-parameter-values"></a>Übergeben von Parameterwerten  
 Eine Anwendung kann den Wert für einen Parameter übergeben, entweder in der \* *ParameterValuePtr* Puffer oder durch eine oder mehrere Aufrufe von **SQLPutData**. Parameter, deren Daten mit übergeben werden **SQLPutData** als bekanntermaßen *Data-at-Execution-* Parameter. Diese werden in der Regel zum Senden von Daten für Parameter SQL_LONGVARBINARY und SQL_LONGVARCHAR verwendet und können mit anderen Parametern kombiniert werden.  
  
 Um Parameterwerte zu übergeben, führt eine Anwendung die folgende Sequenz von Schritten aus:  
  
1.  Aufrufe **SQLBindParameter** für jeden Parameter, um Puffer für den Wert des Parameters zu binden (*ParameterValuePtr* Argument) und Längenindikator / (*StrLen_or_IndPtr* Argument). Bei Data-at-Execution-Parametern *ParameterValuePtr* ist ein anwendungsdefinierte Zeigerwert, z. B. einen Parameter mit der Nummer oder ein Zeiger auf Daten. Der Wert wird später zurückgegeben werden und kann verwendet werden, um den Parameter zu identifizieren.  
  
2.  Legt Werte für Eingabe- und Eingabe-/Ausgabeparameter Parameter in der \* *ParameterValuePtr* und **StrLen_or_IndPtr* Puffer:  
  
    -   Für die normalen Parameter setzt die Anwendung den Wert des Parameters in der \* *ParameterValuePtr* Puffer und die Länge des Werts in der **StrLen_or_IndPtr* Puffer. Weitere Informationen finden Sie unter [Einstellung Parameterwerte](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Für Data-at-Execution-Parameter, die Anwendung legt das Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro (beim Aufrufen von ODBC 2.0-Treiber) in der **StrLen_or_IndPtr* Puffer.  
  
3.  Aufrufe **SQLExecute** oder **SQLExecDirect** zum Ausführen der SQL-Anweisung.  
  
    -   Wenn keine Data-at-Execution-Parameter vorhanden sind, ist der Prozess abgeschlossen.  
  
    -   Wenn Data-at-Execution-Parameter vorhanden sind, gibt die Funktion SQL_NEED_DATA zurück.  
  
4.  Aufrufe **SQLParamData** zum Abrufen des Anwendung definierten Werts im angegebenen der *ParameterValuePtr* Argument **SQLBindParameter** für den ersten Data-at-Execution-Parameter verarbeitet werden. **SQLParamData** wird SQL_NEED_DATA zurückgegeben.  
  
    > [!NOTE]  
    >  Obwohl Data-at-Execution-Parameter Data-at-Execution-Spalten ähneln, der Rückgabewert von **SQLParamData** für jedes unterschiedlich ist. Data-at-Execution-Parameter sind Parameter in einer SQL­Anweisung für die Daten werden mit gesendet **SQLPutData** Wenn die Anweisung ausgeführt wird, mit **SQLExecDirect** oder **SQLExecute**. Sie sind mit gebunden **SQLBindParameter**. Der Rückgabewert von **SQLParamData** ein Zeigerwert wird übergeben werden, um **SQLBindParameter** in der *ParameterValuePtr* Argument. Data-at-Execution-Spalten in einem Rowset für die Daten mit gesendet werden, sind **SQLPutData** Wenn eine Zeile aktualisiert oder mit hinzugefügt **SQLBulkOperations** oder mit aktualisierten **SQLSetPos**. Sie sind mit gebunden **SQLBindCol**. Den Rückgabewert von **SQLParamData** ist die Adresse der Zeile in der **TargetValuePtr* Puffer (festgelegt durch einen Aufruf von **SQLBindCol**), die verarbeitet wird.  
  
5.  Aufrufe **SQLPutData** ein- oder mehrmals zum Senden von Daten für den Parameter. Mehr als ein Aufruf ist erforderlich, wenn der Wert größer ist die \* *ParameterValuePtr* im angegebenen Puffer **SQLPutData**; mehrere Aufrufe **SQLPutData**für denselben Parameter dürfen nur, wenn auf eine Spalte mit einem Zeichen, Binary oder Daten datenquellenspezifischen Datentyp Zeichendaten C senden, oder beim Senden von Binärdaten C an eine Spalte mit einem Zeichen, binary, oder geben Sie die Datenquelle spezifischen Daten.  
  
6.  Aufrufe **SQLParamData** erneut aus, um zu signalisieren, dass alle Daten für den Parameter gesendet wurde.  
  
    -   Wenn weitere Data-at-Execution-Parameter sind **SQLParamData** gibt SQL_NEED_DATA zurück, und der Anwendung definierte Wert für den nächsten Data-at-Execution-Parameter verarbeitet werden. Die Anwendung wiederholt die Schritte 4 und 5.  
  
    -   Wenn keine weiteren Data-at-Execution-Parameter vorhanden sind, ist der Prozess abgeschlossen. Wenn die Anweisung erfolgreich ausgeführt wurde, **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO; Wenn Fehler bei der Ausführung gibt SQL_ERROR zurück. An diesem Punkt **SQLParamData** können alle SQLSTATE, die von der Funktion zurückgegeben werden kann, die verwendet wird, zum Ausführen der Anweisung zurückgeben (**SQLExecDirect** oder **SQLExecute**).  
  
         Ausgabewerte für alle Parameter Eingabe/Ausgabe- oder Ausgabeparameter stehen in der \* *ParameterValuePtr* und **StrLen_or_IndPtr* puffert, nachdem die Anwendung alle Resultsets abruft. durch die Anweisung generiert.  
  
 Aufrufen von **SQLExecute** oder **SQLExecDirect** setzt die Anweisung in einem Zustand SQL_NEED_DATA zurück. Die Anwendung kann zu diesem Zeitpunkt nur aufrufen **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, oder **SQLPutData** mit der Anweisung oder der *Verbindungshandle* der Anweisung zugeordnet. Wenn eine andere Funktion mit der Anweisung oder die Verbindung mit der Anweisung verknüpfte aufgerufen wird, gibt die Funktion SQLSTATE HY010 (Sequenzfehler-Funktion). Die Anweisung bewirkt, dass die SQL_NEED_DATA Zustand über, wenn **SQLParamData** oder **SQLPutData** einen Fehler zurückgibt, **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, oder die Anweisung abgebrochen.  
  
 Wenn die Anwendung aufruft, **SQLCancel** während der Treiber noch Daten für Data-at-Execution-Parameter benötigt, verwirft des Treibers anweisungsausführung; die Anwendung kann dann aufrufen **SQLExecute** oder  **SQLExecDirect** erneut aus.  
  
## <a name="retrieving-streamed-output-parameters"></a>Abrufen von gestreamte Output-Parameter  
 Wenn eine Anwendung festlegt *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM oder SQL_PARAM_OUTPUT_STREAM, den Wert des Ausgabeparameters abgerufen werden muss, durch eine oder mehrere Aufrufe von **SQLGetData**. Wenn der Treiber einen Ausgabestream Parameterwert zur Rückgabe an die Anwendung verfügt, wird es SQL_PARAM_DATA_AVAILABLE zurückgegeben, als Antwort auf einen Aufruf für die folgenden Funktionen: **SQLMoreResults**, **SQLExecute**, und **SQLExecDirect**. Ruft die Anwendung **SQLParamData** um zu bestimmen, welcher Parameterwert verfügbar ist.  
  
 Weitere Informationen zu SQL_PARAM_DATA_AVAILABLE und gestreamte Output-Parameter, finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Verwenden von Arrays von Parametern  
 Wenn eine Anwendung eine Anweisung mit parametermarkierungen auf und übergibt ein Array von Parametern vorbereitet hat, gibt es zwei Möglichkeiten, die dies ausgeführt werden kann. Eine Möglichkeit ist für den Treiber auf die Array-verarbeitungsmöglichkeiten des Back-End abhängig, in dem Fall die gesamte Anweisung mit dem Array der Parameter als eine unteilbare Einheit behandelt wird. Oracle ist ein Beispiel für eine Datenquelle, die verarbeitungsmöglichkeiten des Arrays unterstützt. Eine weitere Möglichkeit zum Implementieren dieses Feature ist für den Treiber zum Generieren eines Batches von SQL-Anweisungen, eine SQL-Anweisung für jeden Satz von Parametern in das Parameterarray und der Batch ausgeführt. Arrays von Parametern können nicht verwendet werden, mit einer **UPDATE WHERE CURRENT OF** Anweisung.  
  
 Wenn ein Array von Parametern verarbeitet wird, einzelne Ergebnis legt/Zeilenanzahl (eine für jeden Parametersatz) können verfügbar sein, oder Anzahlen für Mengen/Zeilen können in einem Rollup. Die SQL_PARAM_ARRAY_ROW_COUNTS option **SQLGetInfo** gibt an, ob die Zeilenanzahl für jeden Satz von Parametern (SQL_PARC_BATCH) verfügbar sind oder nur eine Zeilenanzahl ist verfügbar (SQL_PARC_NO_BATCH).  
  
 Die SQL_PARAM_ARRAY_SELECTS option **SQLGetInfo** gibt an, ob ein Resultset verfügbar für jeden Satz von Parametern (SQL_PAS_BATCH ist) oder nur ein Resultset verfügbar (SQL_PAS_NO_BATCH). Wenn der Treiber eine Ergebnis Satz – generieren mit einem Array von Parametern auszuführenden Anweisung nicht zulässig ist, gibt SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT zurück.  
  
 Weitere Informationen finden Sie unter [SQLGetInfo-Funktion](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Unterstützung von Arrays von Parametern, ist verweist SQL_ATTR_PARAMSET_SIZE-Anweisungsattribut festgelegt, um die Anzahl der Werte für jeden Parameter anzugeben. Wenn das Feld größer als 1 ist, müssen Feld SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR in APD auf Arrays verweisen. Die Kardinalität jedes Arrays ist gleich dem Wert des SQL_ATTR_PARAMSET_SIZE.  
  
 Feld SQL_DESC_ROWS_PROCESSED_PTR APD verweist auf einen Puffer, der die Anzahl der Sätze von Parametern, die verarbeitet worden sind enthält, einschließlich Fehler. Während jeder Satz von Parametern verarbeitet wird, speichert der Treiber einen neuen Wert im Puffer. Wenn dies ein null-Zeiger ist, wird keine Anzahl zurückgegeben. Wenn Arrays von Parametern verwendet werden, wird der Wert, der durch das Feld SQL_DESC_ROWS_PROCESSED_PTR APD gezeigt wird aufgefüllt, selbst wenn von der Einstellung Funktion SQL_ERROR zurückgegeben wird. Wird SQL_NEED_DATA zurückgegeben, wird der Wert, der durch das Feld SQL_DESC_ROWS_PROCESSED_PTR APD verweist auf den Satz der Parameter festgelegt, die verarbeitet wird.  
  
 Was geschieht, wenn ein Array von Parametern gebunden ist und ein **UPDATE WHERE CURRENT OF** -Anweisung ausgeführt wird-Treiber definiert ist.  
  
## <a name="column-wise-parameter-binding"></a>Spaltenweisen Parameterbindung  
 In spaltenbezogene Bindungen bindet die Anwendung separaten Parameter und Längenindikator/Arrays auf jeden Parameter an.  
  
 Um spaltenbezogene Bindungen zu verwenden, wird die Anwendung zuerst SQL_ATTR_PARAM_BIND_TYPE-Anweisungsattribut auf SQL_PARAM_BIND_BY_COLUMN. (Dies ist die Standardeinstellung.) Für jede Spalte gebunden ist führt die Anwendung die folgenden Schritte aus:  
  
1.  Ordnet eine Parameterpufferarray an.  
  
2.  Ordnet ein Array von Längenindikator/Puffer.  
  
    > [!NOTE]  
    >  Wenn die Anwendung direkt in Deskriptoren geschrieben, wenn spaltenbezogene Bindung verwendet wird, können die separaten Arrays für Länge und der Indikator Daten verwendet werden.  
  
3.  Aufrufe **SQLBindParameter** mit den folgenden Argumenten:  
  
    -   *ValueType* ist der C#-Typ, der ein einzelnes Element in der Parameterpufferarray.  
  
    -   *ParameterType* ist die SQL-Typ des Parameters.  
  
    -   *ParameterValuePtr* ist die Adresse der Parameterpufferarray.  
  
    -   *Pufferlänge* ist die Größe der ein einzelnes Element in der Parameterpufferarray. Die *Pufferlänge* Argument wird ignoriert, wenn die Daten Daten fester Länge ist.  
  
    -   *StrLen_or_IndPtr* ist die Adresse des Längenindikator/Arrays.  
  
 Weitere Informationen, wie diese Informationen verwendet werden finden Sie unter "ParameterValuePtr Argument" in "Kommentare" weiter unten in diesem Abschnitt. Weitere Informationen zur spaltenbezogene Bindung von Parametern finden Sie unter [Arrays Bindungsparameter](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>Parameterbindung  
 Die zeilenweise Bindung definiert die Anwendung eine Struktur, die Parameter und Längenindikator/Puffer für jeden Parameter gebunden werden.  
  
 Um die zeilenweise Bindung zu verwenden, führt die Anwendung die folgenden Schritte aus:  
  
1.  Definiert eine Struktur zum Speichern von eines einzelnen Satz von Parametern (einschließlich der Parameter und Längenindikator/Puffer) und weist ein Array dieser Strukturen.  
  
    > [!NOTE]  
    >  Wenn die Anwendung direkt in Deskriptoren geschrieben, wenn die zeilenweise Bindung verwendet wird, können separate Felder für Länge und der Indikator Daten verwendet werden.  
  
2.  Legt das Anweisungsattribut SQL_ATTR_PARAM_BIND_TYPE fest, auf die Größe der Struktur, die einen einzelnen Satz von Parametern enthält, oder auf die Größe einer Instanz eines Puffers in die die Parameter gebunden werden. Die Länge muss Platz für die gebundenen Parameter und möglicherweise vorhandene Auffüllzeichen der Struktur bzw. des Puffers, um sicherzustellen, dass bei der die Adresse des gebundenen Parameter mit der angegebenen Länge erhöht wird, wird das Ergebnis auf den Anfang des denselben Parameter im zeigen enthalten die nächste Zeile. Bei Verwendung der *"sizeof"* -Operator in ANSI C, wird dieses Verhalten garantiert.  
  
3.  Aufrufe **SQLBindParameter** mit den folgenden Argumenten für jeden Parameter gebunden werden:  
  
    -   *ValueType* ist der Typ des Elements Puffer Parameter an die Spalte gebunden ist.  
  
    -   *ParameterType* ist die SQL-Typ des Parameters.  
  
    -   *ParameterValuePtr* ist die Adresse des Elements Parameter Puffer in das erste Arrayelement.  
  
    -   *Pufferlänge* ist die Größe des Elements Puffer Parameter.  
  
    -   *StrLen_or_IndPtr* ist die Adresse des Elements Längenindikator/gebunden werden.  
  
 Weitere Informationen, wie diese Informationen verwendet werden, finden Sie unter "*ParameterValuePtr* Argument" weiter unten in diesem Abschnitt. Weitere Informationen über das zeilenbezogene Binden von Parametern finden Sie unter der [Arrays Bindungsparameter](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Fehlerinformationen  
 Wenn ein Treiber nicht Parameterarrays als Batches implementiert wird (die Option SQL_PARAM_ARRAY_ROW_COUNTS entspricht SQL_PARC_NO_BATCH), werden Fehlersituationen behandelt, als wäre eine Anweisung ausgeführt wurden. Wenn der Treiber Parameterarrays als Batches implementiert werden, kann eine Anwendung das Headerfeld SQL_DESC_ARRAY_STATUS_PTR die IPD verwenden, um zu bestimmen, welche Parameter für eine SQL-Anweisung oder die Parameter in einem Array von Parametern verursacht  **SQLExecDirect** oder **SQLExecute** auf einen Fehler zurück. Dieses Feld enthält Statusinformationen für jede Zeile von Parameterwerten. Wenn das Feld zeigt an, dass ein Fehler aufgetreten ist, werden Felder in der Struktur Diagnosedaten der Zeilen- und Parameter Nummer des Parameters an, die nicht. Durch das Headerfeld SQL_DESC_ARRAY_SIZE im APD, die durch das SQL_ATTR_PARAMSET_SIZE-Anweisungsattribut festgelegt werden kann, wird die Anzahl der Elemente im Array definiert werden.  
  
> [!NOTE]  
>  Das Headerfeld SQL_DESC_ARRAY_STATUS_PTR im APD wird verwendet, um Parameter zu ignorieren. Weitere Informationen zu Parameter werden ignoriert finden Sie im nächsten Abschnitt, "Einen Satz von Parametern wird ignoriert."  
  
 Wenn **SQLExecute** oder **SQLExecDirect** gibt SQL_ERROR zurück, die Elemente im Array verweist das SQL_DESC_ARRAY_STATUS_PTR-Feld in den IPD SQL_PARAM_ERROR SQL_PARAM_SUCCESS, SQL_ enthält PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED oder SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Für jedes Element im Array enthält die Diagnosedaten Struktur eine oder mehrere Statusdatensätze. Die SQL_DIAG_ROW_NUMBER-Feld der Struktur gibt die Zeilennummer der Parameterwerte, die den Fehler verursacht hat. Wenn es möglich ist, des entsprechenden Parameters in einer Zeile von Parametern zu ermitteln, die den Fehler verursacht hat, wird der Parameter mit der Nummer im Feld SQL_DIAG_COLUMN_NUMBER eingegeben werden.  
  
 SQL_PARAM_UNUSED eingegeben wird, wenn ein Parameter nicht verwendet wurde, da in einem früheren-Parameter ist ein Fehler aufgetreten, die erzwungen **SQLExecute** oder **SQLExecDirect** abgebrochen. Z. B. wenn 50 Parameter vorhanden sind und ein Fehler beim Ausführen des Fortieth Satz an Parametern, die verursacht **SQLExecute** oder **SQLExecDirect** abgebrochen, und klicken Sie dann im SQL_PARAM_UNUSED eingegeben wird, die Statusarray für Parameter 41 bis 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE eingegeben, wenn der Treiber Arrays von Parametern als eine Einheit, die aufgrund eines monolithischen, behandelt, damit sie keine derartige einzelne Parameter Fehlerinformationen nicht generiert.  
  
 Einige Fehler bei der Verarbeitung einer einzelnen Satz von Parametern dazu führen, dass die Verarbeitung der nachfolgenden Sätze von Parametern im Array zu beenden. Andere Fehler wirken sich nicht auf die Verarbeitung der nachfolgenden Parameter aus. Welche Fehler Verarbeitung angehalten werden, ist die treiberdefinierten. Wenn die Verarbeitung wird nicht beendet, alle Parameter im Array werden verarbeitet, aufgrund des Fehlers SQL_SUCCESS_WITH_INFO zurückgegeben und der Puffer von SQL_ATTR_PARAMS_PROCESSED_PTR definiert und der maximalen Anzahl von Parametersätzen verarbeitet festgelegt ist (gemäß der SQL_ATTR_PARAMSET_SIZE-Anweisungsattribut) inklusive Fehler Sätze.  
  
> [!CAUTION]  
>  Tritt ein Fehler bei der Verarbeitung eines Arrays von Parametern des ODBC-Verhalten unterscheidet sich in ODBC 3. *x* als ODBC 2. vorlag. *X*. In ODBC 2. *x*, der Funktion zurückgegebene endete, Verarbeitung und SQL_ERROR zurück. Der Puffer verweist die *Pirow* Argument **SQLParamOptions** enthalten die Anzahl der Fehlerzeile. In ODBC 3. *x*, die Funktion gibt SQL_SUCCESS_WITH_INFO zurück und Verarbeiten von Mai entweder beendet oder fortgesetzt werden. Wenn es weiterhin auftritt, wird das SQL_ATTR_PARAMS_PROCESSED_PTR angegebene Puffer festgelegt werden, auf den Wert aller Parameter verarbeitet, einschließlich derer, die zu einem Fehler führten. Diese Änderung im Verhalten kann für vorhandene Anwendungen beeinträchtigen.  
  
 Wenn **SQLExecute** oder **SQLExecDirect** gibt vor dem Abschluss der Verarbeitung von alle Parametersätze, die in einem Parameterarray, z. B. wenn SQL_ERROR oder SQL_NEED_DATA zurückgegeben wird, enthält das Statusarray Status für diesen Parameter, die bereits verarbeitet wurden. Der Speicherort, auf das Feld SQL_DESC_ROWS_PROCESSED_PTR in den IPD enthält die Nummer der Zeile in das Parameterarray an, das den Fehlercode SQL_ERROR oder SQL_NEED_DATA verursacht hat. Wenn ein Array von Parametern an eine SELECT-Anweisung gesendet wird, wird die Verfügbarkeit des Status Arraywerte treiberdefinierten; Diese möglicherweise zur Verfügung, nachdem die Anweisung ausgeführt wurde, oder als Ergebnis legt abgerufen werden.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorieren eine Reihe von Parametern  
 Feld SQL_DESC_ARRAY_STATUS_PTR APD (wie durch das SQL_ATTR_PARAM_STATUS_PTR-Anweisungsattribut festgelegt) kann verwendet werden, um anzugeben, dass eine Reihe von gebundenen Parametern in einer SQL­Anweisung ignoriert werden sollen. Zum Weiterleiten von des Treibers, um eine oder mehrere Sätze von Parametern während der Ausführung ignorieren soll eine Anwendung folgende Schritte ausführen:  
  
1.  Rufen Sie **SQLSetDescField** , legen Sie das Headerfeld SQL_DESC_ARRAY_STATUS_PTR APD, zeigen Sie auf ein Array von SQLUSMALLINT Werte Statusinformationen enthält. Dieses Feld kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit einem *Attribut* des SQL_ATTR_PARAM_OPERATION_PTR, dem eine Anwendung für das Feld festgelegt werden, ohne eine Deskriptorhandles abrufen können.  
  
2.  Legen Sie jedes Element des Arrays definiert, die durch das Feld SQL_DESC_ARRAY_STATUS_PTR APD auf einen der zwei Werte an:  
  
    -   SQL_PARAM_IGNORE, um anzugeben, dass die Ausführung der Anweisung die Zeile ausgeschlossen wird.  
  
    -   SQL_PARAM_PROCEED, um anzugeben, dass die Zeile in der Ausführung der Anweisung enthalten ist.  
  
3.  Rufen Sie **SQLExecDirect** oder **SQLExecute** zum Ausführen der vorbereiteten Anweisung.  
  
 Die folgenden Regeln gelten für das Array, das durch das Feld SQL_DESC_ARRAY_STATUS_PTR APD definiert:  
  
-   Der Zeiger festgelegt ist standardmäßig auf null.  
  
-   Wenn der Zeiger null ist, werden alle Sätze von Parametern verwendet, als ob alle Elemente auf SQL_ROW_PROCEED festgelegt wurden.  
  
-   Wenn ein Element auf SQL_PARAM_PROCEED garantiert nicht, dass der Vorgang dieses bestimmten Satz von Parametern verwendet.  
  
-   SQL_PARAM_PROCEED ist als 0 in der Headerdatei definiert.  
  
 Eine Anwendung kann die SQL_DESC_ARRAY_STATUS_PTR Feld im APD auf desselben Arrays als verweisen, auf das durch das SQL_DESC_ARRAY_STATUS_PTR in IRD festgelegt. Dies ist hilfreich beim Binden von Parametern an Zeilendaten. Parameter können dann nach dem Status des Zeilendaten ignoriert werden. Zusätzlich zu den SQL_PARAM_IGNORE, der folgende Code dazu führen, dass einen Parameter in einer SQL­Anweisung ignoriert werden soll: SQL_ROW_DELETED, SQL_ROW_UPDATED und SQL_ROW_ERROR. Zusätzlich zu den SQL_PARAM_PROCEED, verursacht der folgende Code eine SQL-Anweisung, um den Vorgang fortzusetzen: SQL_ROW_SUCCESS SQL_ROW_SUCCESS_WITH_INFO und SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Erneutes Binden von Parametern  
 Eine Anwendung kann eine der beiden Vorgänge so ändern Sie eine Bindung durchführen:  
  
-   Rufen Sie **SQLBindParameter** an eine neue Bindung für eine Spalte, die bereits gebunden ist. Der Treiber wird die alte Bindung mit den neuen Wert überschrieben.  
  
-   Geben Sie einen Offset Pufferadresse hinzugefügt werden, die von der Bindung Aufruf angegeben wurde **SQLBindParameter**. Weitere Informationen finden Sie im nächsten Abschnitt, "Erneute Zuordnung mit Offsets."  
  
## <a name="rebinding-with-offsets"></a>Das erneute Binden mit Offsets  
 Erneutes Binden von Parametern ist besonders nützlich, wenn eine Anwendung einen Puffer Bereich Setup verfügt, die viele Parameter jedoch einen Aufruf enthalten können **SQLExecDirect** oder **SQLExecute** nur einige der Parameter verwendet. Der restliche Speicherplatz in Pufferbereichs kann für den nächsten Satz von Parametern durch Ändern der vorhandenen Bindung mit einem Offset verwendet werden.  
  
 Das Headerfeld SQL_DESC_BIND_OFFSET_PTR im APD verweist auf den Offset für die Bindung. Wenn das Feld nicht Null ist, der Treiber dereferenziert den Zeiger und, wenn keiner der Werte in den Feldern SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR ein null-Zeiger ist fügt den verweislosen Wert für diese Felder in den Deskriptor Datensätze zum Zeitpunkt der Ausführung. Die neuen Zeigerwerte werden verwendet, wenn die SQL-Anweisungen ausgeführt werden. Der Offset bleibt gültig, nachdem die erneute Zuordnung. Da SQL_DESC_BIND_OFFSET_PTR ein Zeiger auf den Offset selbst, sondern der Offset ist, eine Anwendung kann den Offset direkt ändern, ohne Aufruf [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) oder [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) an Ändern Sie das Deskriptorfeld. Der Zeiger festgelegt ist standardmäßig auf null. Feld SQL_DESC_BIND_OFFSET_PTR der ARD kann festgelegt werden, durch den Aufruf von [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) oder durch einen Aufruf von [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)mit einem *fAttribute* von SQL_ATTR_PARAM_BIND_ OFFSET_PTR.  
  
 Die Bindung Offset wird immer direkt auf die Werte in den Feldern SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR hinzugefügt. Wenn der Offset in einen anderen Wert geändert wird, wird der neue Wert direkt auf den Wert in jedem Deskriptorfeld weiterhin hinzugefügt. Der neue Offset ist die Summe aus der Wert des Felds und alle früheren Offsets nicht hinzugefügt.  
  
## <a name="descriptors"></a>Deskriptoren  
 Wie ein Parameter gebunden ist, wird nach Feldern der APDs und Descriptor, IPD bestimmt. Die Argumente in **SQLBindParameter** werden verwendet, um diese deskriptorfelder festgelegt. Die Felder können auch festgelegt werden, indem Sie die **SQLSetDescField** Funktionen, obwohl **SQLBindParameter** ist effizienter, die verwendet werden, da die Anwendung nicht unbedingt eine Deskriptorhandles zum Aufrufen von erhalten**SQLBindParameter**.  
  
> [!CAUTION]  
>  Aufrufen von **SQLBindParameter** für eine Anweisung auf andere Anweisungen auswirken kann. Dieser Fehler tritt bei der der Anweisung zugeordneten ARD explizit zugeordnet, und auch andere Anweisungen zugeordnet ist. Da **SQLBindParameter** ändert die Felder des APD, die Änderungen zu übernehmen, um alle Anweisungen, denen dieses Deskriptors zugeordnet ist. Wenn dies nicht das erforderliche Verhalten ist, die Anwendung sollte trennen dieses Deskriptors aus den anderen Anweisungen vor **SQLBindParameter**.  
  
 Im Prinzip **SQLBindParameter** führt Sie nacheinander die folgenden Schritte aus:  
  
1.  Aufrufe [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) um APD-Handle abzurufen.  
  
2.  Aufrufe [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) zum Abrufen der APD SQL_DESC_COUNT-Felds, und, wenn der Wert des der *ColumnNumber* Arguments überschreitet den Wert von SQL_DESC_COUNT Aufrufe **SQLSetDescField**erhöhen den Wert der SQL_DESC_COUNT auf *ColumnNumber*.  
  
3.  Aufrufe [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) mehrere Male auf, um die folgenden Felder der APD Werte zuzuweisen:  
  
    -   Legt SQL_DESC_TYPE und SQL_DESC_CONCISE_TYPE auf den Wert der *ValueType*, außer wenn *ValueType* ist eine präzise Bezeichner eines Untertyps "DateTime" oder ein Zeitintervall, SQL_DESC_TYPE auf SQL_ festgelegt "DateTime" oder SQL_INTERVAL, bzw. legt SQL_DESC_CONCISE_TYPE präzise Bezeichner und SQL_DESC_DATETIME_INTERVAL_CODE an den entsprechenden "DateTime" oder das Intervall Subcode.  
  
    -   Legt das Feld SQL_DESC_OCTET_LENGTH auf den Wert der *Pufferlänge*.  
  
    -   Legt das SQL_DESC_DATA_PTR-Feld auf den Wert der *%ParameterValue*.  
  
    -   Legt das Feld SQL_DESC_OCTET_LENGTH_PTR auf den Wert der *StrLen_or_Ind*.  
  
    -   Legt das Feld SQL_DESC_INDICATOR_PTR auch auf den Wert der *StrLen_or_Ind*.  
  
     Die *StrLen_or_Ind* Parameter gibt an, die Informationen für die Anzeige und die Länge für den Parameterwert.  
  
4.  Aufrufe [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) um IPD-Handle abzurufen.  
  
5.  Aufrufe [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) die IPD SQL_DESC_COUNT Feld abgerufen und, wenn der Wert des der *ColumnNumber* Arguments überschreitet den Wert von SQL_DESC_COUNT Aufrufe **SQLSetDescField**erhöhen den Wert der SQL_DESC_COUNT auf *ColumnNumber*.  
  
6.  Aufrufe [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) mehrere Male auf, um die folgenden Felder von der IPD Werte zuzuweisen:  
  
    -   Legt SQL_DESC_TYPE und SQL_DESC_CONCISE_TYPE auf den Wert des *ParameterType*, außer wenn *ParameterType* ist eine präzise Bezeichner eines Untertyps "DateTime" oder ein Zeitintervall, SQL_DESC_TYPE wird zum SQL_DATETIME oder SQL_INTERVAL Sicherungssätze, SQL_DESC_CONCISE_TYPE die präzise Bezeichner, und stellt SQL_DESC_DATETIME_INTERVAL_CODE an den entsprechenden "DateTime" oder das Intervall Subcode.  
  
    -   Legt eine oder mehrere der SQL_DESC_LENGTH SQL_DESC_PRECISION und SQL_DESC_DATETIME_INTERVAL_PRECISION, je nach *ParameterType*.  
  
    -   Legt SQL_DESC_SCALE auf den Wert der *DecimalDigits*.  
  
 Wenn der Aufruf von **SQLBindParameter** ein Fehler auftritt, der Inhalt der deskriptorfelder, die im APD festgelegt haben, würden sind nicht definiert und Feld SQL_DESC_COUNT APD bleibt unverändert. Darüber hinaus die SQL_DESC_LENGTH, SQL_DESC_PRECISION SQL_DESC_SCALE und SQL_DESC_TYPE Felder des entsprechenden Datensatzes in den IPD sind nicht definiert, und das SQL_DESC_COUNT-Feld, der die IPD bleibt unverändert.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Konvertierung von Aufrufen an und von SQLSetParam  
 Wenn eine Anwendung ODBC 1.0 aufruft **SQLSetParam** in einer ODBC-3. *X* -Treiber verwenden, die ODBC 3. *X* Treibermanager ordnet den Aufruf aus, wie in der folgenden Tabelle gezeigt.  
  
|Aufrufen von ODBC 1.0-Anwendung|Rufen Sie ODBC-3. *x* Treiber|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle ParameterNumber "," SQL_PARAM_INPUT_OUTPUT "," ValueType "," ParameterType, *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel wird eine Anwendung eine SQL-Anweisung zum Einfügen von Daten in die Tabelle ORDERS vorbereitet. Für jeden Parameter in der Anweisung, die Anwendung aufruft, **SQLBindParameter** an die ODBC-C-Datentyp und der SQL-Datentyp des Parameters und einen Puffer zu jedem Parameter zu binden. Für jede Zeile der Daten, weist die Anwendung Datenwerte für jeden Parameter und Aufrufe **SQLExecute** zum Ausführen der Anweisung.  
  
 Im folgende Beispiel wird davon ausgegangen, dass Sie eine ODBC-Datenquelle verfügen, auf dem Computer namens Northwind herzustellen, die den Northwind-Datenbank zugeordnet ist.  
  
 Weitere Codebeispiele finden Sie unter [SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLProcedures-Funktion](../../../odbc/reference/syntax/sqlprocedures-function.md), [SQLPutData-Funktion](../../../odbc/reference/syntax/sqlputdata-function.md), und [SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel führt eine Anwendung eine gespeicherte SQL Server-Prozedur, die einen benannten Parameter verwenden.  
  
```  
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Zurückgeben von Informationen über einen Parameter in einer Anweisung|[SQLDescribeParam-Funktion](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Freigeben von Parameterpuffern bei der Anweisung an|[SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Zurückgeben der Anzahl der Parameter|[SQLNumParams-Funktion](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Den nächsten Parameter zum Senden von Daten für zurückgeben|[SQLParamData-Funktion](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Angeben mehrerer Parameterwerte|[SQLParamOptions-Funktion](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Senden der Parameterdaten zum Zeitpunkt der Ausführung|[SQLPutData-Funktion](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [Abrufen von Ausgabeparametern mithilfe von SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
