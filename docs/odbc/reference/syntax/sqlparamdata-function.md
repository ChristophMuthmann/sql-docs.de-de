---
title: SQLParamData-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2debf8a85ad31533995613c5e06c17a6e4040d5a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlparamdata-function"></a>SQLParamData-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLParamData** dient zusammen mit **SQLPutData** Parameterdaten während der Ausführung der Anweisung, und klicken Sie mit angeben **SQLGetData** gestreamte ausgabeparameterdaten abgerufen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *ValuePtrPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Adresse des zurückzugebenden der *ParameterValuePtr* im angegebenen Puffer **SQLBindParameter** (für Parameterdaten) oder die Adresse des dem *TargetValuePtr* im angegebenen Puffer **SQLBindCol** (für Spaltendaten), wie in den Datensatz SQL_DESC_DATA_PTR Deskriptorfeld enthalten.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLParamData** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLParamData** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|Der Datenwert durch identifiziert die *ValueType* Argument in **SQLBindParameter** für der gebundene Parameter nicht in den identifizierten Datentyp konvertiert werden konnte die *ParameterType*Argument in **SQLBindParameter**.<br /><br /> Der Datenwert zurückgegeben, für einen Parameter gebunden werden, wie SQL_PARAM_INPUT_OUTPUT oder SQL_PARAM_OUTPUT nicht in der identifizierten Datentyp konvertiert werden konnte die *ValueType* Argument in **SQLBindParameter**.<br /><br /> (Wenn die Datenwerte für eine oder mehrere Zeilen nicht konvertiert werden konnte, aber eine oder mehrere Zeilen wurden erfolgreich zurückgegeben, diese Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22026|Zeichenfolgendaten, nicht übereinstimmende Länge|Der Typ der SQL_NEED_LONG_DATA_LEN Informationen in **SQLGetInfo** wurde von "Y", und weniger Daten für einen langen Parameter (der Datentyp war SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen-Datentyp) gesendet wurde, als angegeben wurde mit der *StrLen_or_IndPtr* Argument in **SQLBindParameter**.<br /><br /> Der Typ der SQL_NEED_LONG_DATA_LEN Informationen in **SQLGetInfo** wurde von "Y", und weniger Daten für eine lange Spalte (der Datentyp war SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen-Datentyp) gesendet wurde, als im angegebenen der Länge-Puffer für eine Spalte in eine Zeile mit Daten, die hinzugefügt oder aktualisiert wurde **SQLBulkOperations** oder mit aktualisierten **SQLSetPos**.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund einer Ressourcendeadlock mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*; die Funktion wurde dann erneut auf aufgerufen die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) der vorherigen Funktionsaufruf war keinen Aufruf von **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, oder **SQLSetPos** , in denen die Zurückgeben von Code war SQL_NEED_DATA oder der letzten Funktionsaufruf einen Aufruf von **SQLPutData**.<br /><br /> Die vorherigen Funktionsaufruf wurde ein Aufruf von **SQLParamData**.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLParamData** Funktion aufgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, die *StatementHandle* und zurückgegebene SQL_NEED_DATA zurück. **SQLCancel** wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber, die entspricht der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
 Wenn **SQLParamData** heißt beim Senden von Daten für einen Parameter in einer SQL­Anweisung, es können SQLSTATE, die von der Funktion aufgerufen, um die Ausführung der Anweisung zurückgegeben werden kann zurückgegeben (**SQLExecute** oder **SQLExecDirect**). Wenn sie, beim Senden von Daten für eine Spalte aufgerufen wird aktualisiert bzw. mit hinzugefügt **SQLBulkOperations** oder aktualisiert wird **SQLSetPos**, können sie alle SQLSTATE, die von zurückgegeben werden kann zurückgeben  **SQLBulkOperations** oder **SQLSetPos**.  
  
## <a name="comments"></a>Kommentare  
 **SQLParamData** aufgerufen werden, um Data-at-Execution-Daten für zwei Zwecke bereitstellen: Parameterdaten, die in einem Aufruf verwendet werden, **SQLExecute** oder **SQLExecDirect**, oder Spaltendaten, die werden verwendet, wenn eine Zeile aktualisiert oder durch einen Aufruf von hinzugefügt **SQLBulkOperations** oder durch einen Aufruf von aktualisiert **SQLSetPos**. Zum Zeitpunkt der Ausführung **SQLParamData** zurück an die Anwendung, die ein Indikator für die Daten der Treiber erforderlich ist.  
  
 Wenn eine Anwendung ruft **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos**, gibt der Treiber SQL_NEED_ Daten bei Bedarf Data-at-Execution-Daten. Eine Anwendung ruft dann **SQLParamData** bestimmen, welche Daten senden. Wenn der Treiber die Parameterdaten erforderlich ist, gibt der Treiber der  *\*ValuePtrPtr* den Wert, der die Anwendung im Rowset Puffer nehmen die Ausgabe puffert. Die Anwendung kann diesen Wert verwenden, um zu bestimmen, welche Parameterdaten der Treiber anfordert. Wenn der Treiber die Spaltendaten erforderlich ist, gibt der Treiber der  *\*ValuePtrPtr* Puffern Sie die Adresse, die die Spalte ursprünglich wie folgt, gebunden wurde:  
  
 *Adresse gebunden* + *binden Offset* + ((*Zeilennummer* – 1) X *Elementgröße*)  
  
 auf die Variablen definiert werden, wie in der folgenden Tabelle angegeben.  
  
|Variable|Description|  
|--------------|-----------------|  
|*Adresse gebunden*|Die Adresse angegeben, mit der *TargetValuePtr* Argument in **SQLBindCol**.|  
|*Binden von Offset*|Der Wert, der mit der SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut angegebenen Adresse gespeichert.|  
|*Zeilennummer*|Die 1-basierten Nummer der Zeile im Rowset. Einzeiliges Abrufe, die standardmäßig, die werden zu können, ist dies 1.|  
|*Elementgröße*|Der Wert des Attributs SQL_ATTR_ROW_BIND_TYPE-Anweisung für die Daten und Längenindikator/Puffer.|  
  
 Sie gibt überdies SQL_NEED_DATA zurück, der ein Indikator für die Anwendung, die sie aufrufen sollte **SQLPutData** zum Senden der Daten.  
  
 Ruft die Anwendung **SQLPutData** so oft wie nötig, um die Data-at-Execution-Daten für die Spalte oder Parameter zu senden. Nachdem alle Daten für die Spalte oder Parameter gesendet wurde, ruft die Anwendung **SQLParamData** erneut aus. Wenn **SQLParamData** erneut wird SQL_NEED_DATA zurückgegeben, für eine andere Spalte oder die Daten gesendet werden müssen. Daher ruft die Anwendung erneut **SQLPutData**. Wenn alle Data-at-Execution-Daten wurde gesendet für alle Parameter oder Spalten, klicken Sie dann **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, den Wert in  *\*ValuePtrPtr* ist nicht definiert ist, und die SQL-Anweisung ausgeführt werden kann oder der **SQLBulkOperations** oder **SQLSetPos** Aufruf verarbeitet werden kann.  
  
 Wenn **SQLParamData** stellt Parameterdaten für eine gesuchte update oder delete-Anweisung, die keine Zeilen in der Datenquelle, die den Aufruf von auswirkt **SQLParamData** gibt SQL_NO_DATA zurück.  
  
 Weitere Informationen zu wie Data-at-Execution-Parameterdaten zur Ausführungszeit für die Anweisung übergeben wird, finden Sie unter "Übergeben von Parameterwerten" in [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) und [Long-Daten senden](../../../odbc/reference/develop-app/sending-long-data.md). Weitere Informationen zu Spaltendaten, wie Data-at-Execution-aktualisiert oder hinzugefügt wird, finden Sie im Abschnitt "Verwenden von SQLSetPos" in [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Ausführen von Massenladen Updates mithilfe von Lesezeichen" in [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), und [Long-Daten und SQLSetPos und SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
 **SQLParamData** kann zum Abrufen von gestreamte Ausgabeparameter aufgerufen werden. Wenn **SQLMoreResults**, **SQLExecute**, **SQLGetData**, oder **SQLExecDirect** gibt SQL_PARAM_DATA_AVAILABLE, rufen Sie **SQLParamData** um zu bestimmen, welche Parameter einen Wert zur Verfügung hat. Weitere Informationen zu SQL_PARAM_DATA_AVAILABLE und gestreamte Output-Parameter, finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an einen parameter|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen über einen Parameter in einer Anweisung|[SQLDescribeParam-Funktion](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Senden der Parameterdaten zum Zeitpunkt der Ausführung|[SQLPutData-Funktion](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [Abrufen von Ausgabeparametern mithilfe von SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
