---
title: SQLPutData-Funktion | Microsoft Docs
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
apiname: SQLPutData
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLPutData
helpviewer_keywords: SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d1a3d60c2a6cd5ed19f0183ba51a5a016ccfc36
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlputdata-function"></a>SQLPutData-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLPutData** ermöglicht es einer Anwendung zum Senden von Daten für einen Parameter oder eine Spalte an den Treiber während der Ausführung der Anweisung. Diese Funktion kann verwendet werden, um Zeichen- oder Binärdatenwerte in Teilen auf eine Spalte mit einem Zeichen, Binary oder Daten datenquellenspezifischen-Datentyp (z. B. Parameter SQL_LONGVARBINARY oder SQL_LONGVARCHAR Typen) zu senden. **SQLPutData** unterstützt die Bindung an eine Unicode-C-Datentyp, selbst wenn der zugrunde liegende Treiber Unicode-Daten nicht unterstützt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *DataPtr*  
 [Eingabe] Ein Zeiger auf einen Puffer, der die tatsächlichen Daten für den Parameter oder eine Spalte enthält. Müssen die Daten in der C-Datentyp angegeben werden, der *ValueType* Argument **SQLBindParameter** (für Parameterdaten) oder die *TargetType* Argument des  **SQLBindCol** (für Spaltendaten).  
  
 *StrLen_or_Ind*  
 [Eingabe] Länge des \* *DataPtr*. Gibt die Menge der Daten in einem Aufruf gesendeten **SQLPutData**. Die Menge der Daten kann mit jedem Aufruf für einen bestimmten Parameter oder die Spalte variieren. *StrLen_or_Ind* wird ignoriert, es sei denn, sie eine der folgenden Bedingungen erfüllt:  
  
-   *StrLen_or_Ind* SQL_NTS, SQL_NULL_DATA oder SQL_DEFAULT_PARAM ist.  
  
-   Die C-Datentyp, der im angegebenen **SQLBindParameter** oder **SQLBindCol** SQL_C_CHAR oder sql_c_binary angegeben ist.  
  
-   Der C-Datentyp ist SQL_C_DEFAULT, und die Standard-C-Datentyp für den angegebenen SQL-Datentyp ist SQL_C_CHAR oder sql_c_binary angegeben.  
  
 Für alle anderen Typen von C-Daten Wenn *StrLen_or_Ind* ist kein SQL_NULL_DATA oder SQL_DEFAULT_PARAM der Treiber setzt voraus, dass die Größe des der \* *DataPtr* Puffer ist die Größe des angegebenen C-Datentyp mit *ValueType* oder *TargetType* und sendet den gesamten Datenwert. Weitere Informationen finden Sie unter [Konvertieren von Daten von C-in SQL-Datentypen](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) in Anhang D:-Datentypen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLPutData** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLPutData** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Das Abschneiden von nicht leeren Zeichen oder Binärdaten ungleich NULL führte Zeichenfolgen- oder Binärdaten für ein Output-Parameter zurückgegeben. Falls es sich um einen Zeichenfolgenwert handelt, wurde es rechts abgeschnitten. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert durch identifiziert die *ValueType* Argument in **SQLBindParameter** für der gebundene Parameter nicht in den identifizierten Datentyp konvertiert werden konnte die *ParameterType*Argument in **SQLBindParameter**.|  
|07S01|Ungültige Verwendung des Standardparameters|Legen Sie ein Parameterwert mit **SQLBindParameter**SQL_DEFAULT_PARAM wurde und der entsprechende Parameter verfügte nicht über einen Standardwert.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22001|Die Zeichenfolgedaten rechts abgeschnitten.|Die Zuweisung von einem Zeichen- oder binären Wert einer Spalte führte zu NichtLeer (Zeichen) oder ungleich Null (binären) Zeichen oder Bytes wird abgeschnitten.<br /><br /> Der Typ der SQL_NEED_LONG_DATA_LEN Informationen in **SQLGetInfo** wurde von "Y", und weitere Daten für einen langen Parameter (der Datentyp war SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen-Datentyp) gesendet wurden, als angegeben wurde mit der *StrLen_or_IndPtr* Argument in **SQLBindParameter**.<br /><br /> Der Typ der SQL_NEED_LONG_DATA_LEN Informationen in **SQLGetInfo** wurde von "Y", und weitere Daten für eine lange Spalte (der Datentyp war SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen-Datentyp) gesendet wurden, als im angegebenen der Länge-Puffer für eine Spalte in eine Zeile mit Daten, die hinzugefügt oder aktualisiert wurde **SQLBulkOperations** oder mit aktualisierten **SQLSetPos**.|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|Die Daten für einen numerischen gebundene Parameter gesendet oder Spalte verursacht die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abgeschnitten wird, wenn die zugehörigen Tabellenspalte zugewiesen.<br /><br /> Einen numerischen Wert (als numerisch oder Zeichenfolge) für einen oder mehrere Parameter für Eingabe/Ausgabe- oder Ausgabeparameter zurückgeben würde die gesamten (im Gegensatz zu Sekundenbruchteile) Teil der Zahl abzuschneidende vorliegt.|  
|22007|Ungültiges Datetime-format|Die Daten für einen Parameter oder eine Spalte, die an einem Datum, Uhrzeit oder Timestamp-Struktur gebunden wurde gesendet wurde, ein ungültiges Datum, Uhrzeit oder Zeitstempel.<br /><br /> Ein Eingabe/Ausgabe- oder Ausgabe-Parameter an ein Datum, Uhrzeit oder C-zeitstempelstruktur gebunden wurde, und ein Wert im Parameters zurückgegeben wurde, bzw. ein ungültiges Datum, Uhrzeit oder Zeitstempel. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|22008|Überlauf der DateTime-Feld.|Ein Datetime-Ausdruck für eine Eingabe/Ausgabe berechnet oder Ausgabeparameter Verzeichnisdiensts ist ein Datum, Uhrzeit oder C-zeitstempelstruktur, die ungültig war.|  
|22012|Division durch 0 (null)|Ein arithmetischer Ausdruck für eine Eingabe/Ausgabe berechnet oder Ausgabeparameter Verzeichnisdiensts Division durch 0 (null).|  
|22015|Überlauf der Intervall-Feld.|Die Daten für eine genaue numerische oder Intervall gesendet oder Parameter in einem Intervall SQL-Datentyp hat einen Datenverlust von signifikanten Stellen verursacht.<br /><br /> Daten für eine Spalte Intervall oder einen Parameter mit mehr als ein Feld gesendet wurde, wurde in einen numerischen Datentyp konvertiert und hatte keine Darstellung in den numeric-Datentyp.<br /><br /> Die Daten gesendet werden, für die Spalte oder Parameter auf ein Intervall SQL-Typ zugewiesen wurde, und es wurde keine Darstellung des Werts der C-Typ im Intervall SQL-Typ.<br /><br /> Die Daten für einen genauen numerischen oder Intervall C-Spalte oder Parameter für den Intervalltyp C gesendet hat einen Datenverlust von signifikanten Stellen verursacht.<br /><br /> Die Daten gesendet werden, für die Spalte oder Parameter auf ein Intervall C-Struktur zugewiesen wurde, und es wurde keine Darstellung der Daten in der Datenstruktur Intervall.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|Der C-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der SQL-Typ der Spalte wurde einem Zeichendatentyp; und kein Wert in der Spalte oder Parameter wurde ein gültiger Literal des gebundenen C-Typs.<br /><br /> Der SQL-Typ wurde eine genaue oder ungefähre numerische, einen datetime-Wert oder ein Intervall-Datentyp; der C-Typ wurde SQL_C_CHAR; und kein Wert in der Spalte oder Parameter wurde ein gültiger Literal des gebundenen SQL-Typs.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) das Argument *DataPtr* wurde ein null-Zeiger und das Argument *StrLen_or_Ind* war nicht 0 (null) SQL_DEFAULT_PARAM oder SQL_NULL_DATA.|  
|HY010|Fehler bei Funktionssequenz|(DM) der vorherigen Funktionsaufruf war keinen Aufruf von **SQLPutData** oder **SQLParamData**.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde noch ausgeführt werden, wenn die SQLPutData-Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY019|Die gesendeten Daten sind nicht-Zeichen oder Binärdaten|**SQLPutData** aufgerufene mehr als einmal für einen Parameter oder eine Spalte wurde und es wurde nicht verwendet wird, zum Senden von Zeichendaten C auf eine Spalte mit einem Zeichen, Binary oder Daten datenquellenspezifischen Datentyp oder zum Senden von Binärdaten C auf eine Spalte mit einem Zeichen , Binär- oder Data datenquellenspezifischen-Datentyp.|  
|HY020|Bei dem Versuch, einen null-Wert zu verketten.|**SQLPutData** mehr als einmal aufgerufen wurde, seit dem Aufruf, der SQL_NEED_DATA zurückgegeben, und klicken Sie in einem dieser Aufrufe der *StrLen_or_Ind* Argument SQL_NULL_DATA oder SQL_DEFAULT_PARAM enthalten sind.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Das Argument *DataPtr* war ein null-Zeiger und das Argument *StrLen_or_Ind* war kleiner als 0, aber nicht SQL_NTS oder SQL_NULL_DATA gleich.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
 Wenn **SQLPutData** heißt beim Senden von Daten für einen Parameter in einer SQL­Anweisung, es können SQLSTATE, die von der Funktion aufgerufen, um die Ausführung der Anweisung zurückgegeben werden kann zurückgegeben (**SQLExecute** oder **SQLExecDirect**). Wenn sie, beim Senden von Daten für eine Spalte aufgerufen wird aktualisiert bzw. mit hinzugefügt **SQLBulkOperations** oder aktualisiert wird **SQLSetPos**, können sie alle SQLSTATE, die von zurückgegeben werden kann zurückgeben  **SQLBulkOperations** oder **SQLSetPos**.  
  
## <a name="comments"></a>Kommentare  
 **SQLPutData** aufgerufen werden, um Data-at-Execution-Daten für zwei Zwecke angeben: Parameterdaten in einem Aufruf verwendet werden **SQLExecute** oder **SQLExecDirect**, oder die Spaltendaten verwendet werden, wenn eine Zeile aktualisiert oder durch einen Aufruf von hinzugefügt **SQLBulkOperations** oder aktualisiert wird, durch den Aufruf von **SQLSetPos**.  
  
 Wenn eine Anwendung ruft **SQLParamData** bestimmen, welche Daten es sollte zu senden, gibt der Treiber einen Indikator, der die Anwendung kann verwenden, um zu bestimmen, welche, der zu sendenden Parameterdaten oder, in dem Spaltendaten gefunden werden können. Sie gibt überdies SQL_NEED_DATA zurück, der ein Indikator für die Anwendung, die sie aufrufen sollte **SQLPutData** zum Senden der Daten. In der *DataPtr* Argument **SQLPutData**, die Anwendung übergibt einen Zeiger auf den Puffer, die die tatsächlichen Daten für den Parameter oder eine Spalte enthält.  
  
 Wenn der Treiber gibt SQL_SUCCESS zurück, für die **SQLPutData**, ruft die Anwendung **SQLParamData** erneut aus. **SQLParamData** gibt SQL_NEED_DATA zurück, wenn weitere Daten gesendet werden, müssen in diesem Fall ruft die Anwendung **SQLPutData** erneut aus. Es gibt SQL_SUCCESS zurück, wenn alle Data-at-Execution-Daten gesendet wurde. Die Anwendung ruft dann **SQLParamData** erneut aus. Wenn der Treiber SQL_NEED_DATA und ein anderer Indikator in zurückgibt  *\*ValuePtrPtr*, benötigt Daten für einen anderen Parameter oder die Spalte und **SQLPutData** erneut aufgerufen wird. Wenn der Treiber SQL_SUCCESS, klicken Sie dann alle Data-at-Execution-zurückgegeben Daten gesendet wurde, und die SQL-Anweisung kann ausgeführt werden oder die **SQLBulkOperations** oder **SQLSetPos** Aufruf verarbeitet werden kann.  
  
 Weitere Informationen zu wie Data-at-Execution-Parameterdaten zur Ausführungszeit für die Anweisung übergeben wird, finden Sie unter "Übergeben von Parameterwerten" in [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) und [Long-Daten senden](../../../odbc/reference/develop-app/sending-long-data.md). Weitere Informationen, wie Data-at-Execution-Spaltendaten aktualisiert oder hinzugefügt wird, finden Sie im Abschnitt "Verwenden von SQLSetPos" in [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Ausführen von Massenladen Updates mithilfe von Lesezeichen" in [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), und [Long-Daten und SQLSetPos und SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Eine Anwendung kann mithilfe **SQLPutData** zum Senden von Daten in Teilen nur, wenn auf eine Spalte mit einem Zeichen, Binary oder Daten datenquellenspezifischen Datentyp Zeichendaten C senden oder beim Senden von Binärdaten C auf eine Spalte mit einem Zeichen, Binär oder Daten Geben Sie die Datenquelle spezifischen Daten. Wenn **SQLPutData** wird aufgerufen, mehr als einmal unter anderen Bedingungen zurückgegeben SQL_ERROR und SQLSTATE HY019 (nicht-Zeichen oder Binärdaten gesendeten Daten sind).  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel wird angenommen, einen Datenquellennamen namens Test. Die zugeordnete Datenbank sollte es sich um eine Tabelle verfügen, die Sie, wie folgt erstellen können:  
  
```  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an einen parameter|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Den nächsten Parameter zum Senden von Daten für zurückgeben|[SQLParamData-Funktion](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
