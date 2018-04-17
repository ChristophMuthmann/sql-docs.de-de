---
title: SQLCopyDesc Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8f857ee82ffb9d715e0e408715c9c56353687fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLCopyDesc** Deskriptorinformationen aus einem Deskriptorhandles in einen anderen kopiert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argumente  
 *SourceDescHandle*  
 [Eingabe] Quelle Deskriptorhandles.  
  
 *TargetDescHandle*  
 [Eingabe] Ziel-Deskriptorhandles. Die *TargetDescHandle* Argument ist ein Handle für einen Deskriptor für die Anwendung oder einem IPD möglich. *TargetDescHandle* kann nicht festgelegt werden, um ein Handle für ein IRD oder **SQLCopyDesc** SQLSTATE HY016 (ein eingebauter Zeilendeskriptor kann nicht geändert werden) zurück.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLCopyDesc** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_DESC und ein *behandeln* von *TargetDescHandle*. Wenn eine ungültige *SourceDescHandle* übergeben wurde in den Aufruf SQL_INVALID_HANDLE zurückgegeben werden, aber keine SQLSTATE zurückgegeben werden. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLCopyDesc** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
 Wenn ein Fehler zurückgegeben wird, wird den Aufruf von **SQLCopyDesc** sofort abgebrochen wird, und der Inhalt der Felder in der *TargetDescHandle* Deskriptor sind nicht definiert.  
  
 Da **SQLCopyDesc** implementiert werden kann, durch den Aufruf **SQLGetDescField** und **SQLSetDescField**, **SQLCopyDesc** gelegten Zurückgegebenes SQLSTATEs **SQLGetDescField** oder **SQLSetDescField**.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht zum Belegen des Speichers zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY007|Die zugeordnete Anweisung ist nicht vorbereitet.|*SourceDescHandle* ein IRD zugeordnet wurde, und der zugehörigen Anweisungshandle wies nicht den Status vorbereitete oder ausgeführte.|  
|HY010|Fehler bei Funktionssequenz|(DM) in der Deskriptor behandelt *SourceDescHandle* oder *TargetDescHandle* zugeordnet wurde eine *StatementHandle* für die eine asynchrone (nicht-Funktion eine) wurde aufgerufen, und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) in der Deskriptor behandelt *SourceDescHandle* oder *TargetDescHandle* zugeordnet wurde eine *StatementHandle* für die **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** aufgerufen und SQL_NEED_DATA zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *SourceDescHandle* oder *TargetDescHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLCopyDesc** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** für eines der zugeordneten Anweisungshandles hieß die *SourceDescHandle* oder *TargetDescHandle* und SQL_PARAM_DATA_AVAILABLE zurückgegeben. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY016|Ein Implementierungszeilendeskriptor kann nicht geändert werden.|*TargetDescHandle* ein IRD zugeordnet wurde.|  
|HY021|Inkonsistente Deskriptorinformationen|Die Deskriptorinformationen während einer konsistenzprüfung aktiviert war nicht konsistent. Weitere Informationen finden Sie unter "Konsistenzprüfungen" in **SQLSetDescField**.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|Der Aufruf von **SQLCopyDesc** aufgefordert, einen Aufruf von **SQLSetDescField**, aber  *\*ValuePtr* war nicht gültig für die *FieldIdentifier* Argument auf *TargetDescHandle*.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *SourceDescHandle* oder *TargetDescHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Ein Aufruf von **SQLCopyDesc** Kopien, die die Felder des Deskriptors Quelle zum Ziel-Deskriptorhandles behandeln. Felder können nur für einen Deskriptor für die Anwendung oder einem IPD, jedoch nicht zu einer IRD kopiert werden. Felder können von einer Anwendung oder einen Deskriptor Implementierung kopiert werden.  
  
 Felder können aus einer IRD kopiert werden, nur dann, wenn das Anweisungshandle im Status vorbereitet oder ausgeführt wird; andernfalls gibt die Funktion SQLSTATE HY007 (zugeordnete Anweisung ist nicht vorbereitet sind).  
  
 Felder können aus einem IPD kopiert werden, unabhängig davon, ob eine Anweisung vorbereitet wurde. Wenn eine SQL-Anweisung mit dynamischen Parametern vorbereitet wurde und automatischer Auffüllung der die IPD unterstützt und aktiviert ist, wird die IPD vom Treiber aufgefüllt. Wenn **SQLCopyDesc** aufgerufen wird und die IPD als die *SourceDescHandle*, ausgefüllter Felder beim Übertragungsvorgang kopiert werden. Wenn die IPD vom Treiber nicht aufgefüllt wird, werden die Inhalte der Felder in den IPD ursprünglich kopiert.  
  
 Alle Felder des Deskriptors, mit Ausnahme von SQL_DESC_ALLOC_TYPE (die angibt, ob die Deskriptorhandles, automatisch oder explizit zugeordnet wurde), kopiert werden, und zwar unabhängig davon, ob das Feld für den Deskriptor Ziel definiert wird. Kopierte Felder überschreiben vorhandene Felder.  
  
 Der Treiber alle deskriptorfelder kopiert, wenn die *SourceDescHandle* und *TargetDescHandle* Argumente denselben Treiber zugeordnet sind, auch wenn die Treiber auf zwei unterschiedliche Verbindungen werden oder Umgebungen. Wenn die *SourceDescHandle* und *TargetDescHandle* Argumente verschiedenen Treiber zugeordnet sind, werden der Treiber-Manager kopiert ODBC-definierten Felder, sondern kopiert keine treiberdefinierten Felder oder Felder nicht von ODBC für den Typ des Deskriptors definiert sind.  
  
 Der Aufruf von **SQLCopyDesc** sofort abgebrochen wird, wenn ein Fehler auftritt.  
  
 Wenn das SQL_DESC_DATA_PTR-Feld kopiert wird, erfolgt eine konsistenzprüfung auf dem Ziel-Deskriptor. Wenn die konsistenzprüfung fehlschlägt, SQLSTATE HY021 (inkonsistente Deskriptorinformationen) wird zurückgegeben, und der Aufruf von **SQLCopyDesc** sofort abgebrochen wird. Weitere Informationen zu konsistenzprüfungen, finden Sie unter "Konsistenzprüfungen" in [SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Deskriptorhandles können über Verbindungen kopiert werden, selbst wenn die Verbindungen unter verschiedenen Umgebungen sind. Wenn der Treiber-Manager erkennt, dass die Quelle und Ziel Deskriptors Handles nicht zu derselben Verbindung und die beiden Verbindungen gehören gehören, um Treiber zu trennen, implementiert **SQLCopyDesc** durch Ausführen einer feldspezifischen Kopieren Sie mithilfe von **SQLGetDescField** und **SQLSetDescField**.  
  
 Wenn **SQLCopyDesc** aufgerufen wird und eine *SourceDescHandle* auf einen Treiber und eine *TargetDescHandle* auf eine andere Treiber, die Fehlerwarteschlange in der die  *SourceDescHandle* deaktiviert ist. Dies geschieht, weil **SQLCopyDesc** wird in diesem Fall durch Aufrufe von implementiert **SQLGetDescField** und **SQLSetDescField**.  
  
> [!NOTE]  
>  Eine Anwendung kann in der Lage, eine explizit zugeordneten Deskriptorhandles mit Zuordnen einer *StatementHandle*, anstatt Aufrufen **SQLCopyDesc** Felder aus einen Deskriptor in einen anderen kopieren. Ein explizit zugewiesenen Deskriptor kann eine andere zugeordnet werden *StatementHandle* auf dem gleichen *Verbindungshandle* durch Festlegen der SQL_ATTR_APP_ROW_DESC oder SQL_ATTR_APP_PARAM_DESC-Anweisung um das Handle des Deskriptors explizit zugewiesene Attribut. Nachdem dies geschehen ist, **SQLCopyDesc** muss nicht aufgerufen werden, um deskriptorfeldwerte aus einen Deskriptor auf einen anderen kopieren. Ein Deskriptor-Handle kann nicht zugeordnet werden eine *StatementHandle* auf einem anderen *Verbindungshandle*, jedoch mit der gleichen deskriptorfeldwerte auf *StatementHandles*auf verschiedenen *ConnectionHandles*, **SQLCopyDesc** aufgerufen werden muss.  
  
 Eine Beschreibung der Felder in einem Deskriptor Header oder Datensatz, finden Sie unter [SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Weitere Informationen zu Deskriptoren, finden Sie unter [Deskriptoren](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Kopieren die Zeilen zwischen Tabellen  
 Eine Anwendung kann Daten aus einer Tabelle in eine andere kopieren ohne die Daten auf Anwendungsebene zu kopieren. Zu diesem Zweck bindet die Anwendung die gleichen Datenpuffer und Deskriptorinformationen eine Anweisung, die die Daten abruft und die Anweisung, die die Daten in eine Kopie einfügt. Dies kann erreicht werden, durch die gemeinsame Nutzung einer Anwendungsdiensts (Binden einen explizit zugewiesenen Deskriptor als die ARD für eine Anweisung und in einer anderen APD) oder mithilfe von **SQLCopyDesc** So kopieren Sie die Bindungen zwischen den ARD und die APD der beiden Anweisungen. Wenn Sie die Anweisungen auf anderen Verbindungen sind **SQLCopyDesc** muss verwendet werden. Darüber hinaus **SQLCopyDesc** muss aufgerufen werden, um die Bindungen zwischen IRD und die IPD der beiden Anweisungen zu kopieren. Über die Anweisungen für die gleiche Verbindung zum Kopieren der Informationstyp SQL_ACTIVE_STATEMENTS vom Treiber für einen Aufruf zurückgegebene **SQLGetInfo** muss größer als 1 ist für diesen Vorgang erfolgreich ausgeführt werden kann. (Dies ist nicht die Groß-/Kleinschreibung beim Kopieren von Verbindungen.)  
  
### <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel werden Deskriptor Vorgänge verwendet, kopieren Sie die Felder der Tabelle PartsSource in der PartsCopy-Tabelle. Der Inhalt der Tabelle PartsSource werden abgerufen, in Rowsets Puffer in *hstmt0*. Diese Werte werden als Parameter eine INSERT-Anweisung verwendet, auf *hstmt1* zu den Spalten der Tabelle PartsCopy aufgefüllt. Die Felder des IRD der dazu *hstmt0* werden kopiert, auf die Felder der IPD von *hstmt1*, und die Felder von der ARD von *hstmt0* werden in die Felder der APD von kopiert*hstmt1*. Verwendung **SQLSetDescField** , legen Sie die IPD-SQL_DESC_PARAMETER_TYPE-Attribut auf SQL_PARAM_INPUT an, wenn IRD-Feldern von einer Anweisung mit der Output-Parameter in IPD-Feldern kopieren, die Eingabeparameter werden müssen.  
  
```  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abrufen von mehreren deskriptorfelder|[SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Festlegen einer einzelnen Deskriptorfeld|[SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Mehrere deskriptorfelder festlegen|[SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
