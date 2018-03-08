---
title: SQLSetDescRec-Funktion | Microsoft Docs
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
apiname: SQLSetDescRec
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetDescRec
helpviewer_keywords: SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c817bad04757820b7c8ee83905fbc0fad08b4e26
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 Die **SQLSetDescRec** Funktion legt mehrere deskriptorfelder, die den Datentyp auswirken und Puffer, der an eine Spalte oder Parameter Daten gebunden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *DescriptorHandle*  
 [Eingabe] Deskriptorhandles. Dies muss ein IRD-Handle.  
  
 *RecNumber*  
 [Eingabe] Gibt an, die Felder festzulegende enthält, Deskriptordatensatz. Deskriptordatensätze sind von 0 (null) mit Datensatznummer wird lesezeichendatensatzes 0 nummeriert. Dieses Argument muss gleich oder größer als 0 sein. Wenn *RecNumber* ist größer als der Wert der SQL_DESC_COUNT SQL_DESC_COUNTis geändert, um den Wert der *RecNumber*.  
  
 *Typ*  
 [Eingabe] Der Wert, auf das SQL_DESC_TYPE-Feld für den anwendungsparameterdeskriptor-Datensatz festgelegt.  
  
 *Untertyp*  
 [Eingabe] Für Datensätze, deren Typ SQL_DATETIME oder SQL_INTERVAL hat, ist dies der Wert, auf das Feld SQL_DESC_DATETIME_INTERVAL_CODE festgelegt.  
  
 *Länge*  
 [Eingabe] Der Wert, auf das Feld SQL_DESC_OCTET_LENGTH für den anwendungsparameterdeskriptor-Datensatz festgelegt.  
  
 *Genauigkeit*  
 [Eingabe] Der Wert, auf das Feld SQL_DESC_PRECISION für den anwendungsparameterdeskriptor-Datensatz festgelegt.  
  
 *Dezimalstellen*  
 [Eingabe] Der Wert, auf das Feld SQL_DESC_SCALE für den anwendungsparameterdeskriptor-Datensatz festgelegt.  
  
 *DataPtr*  
 [Verzögerte Eingabe oder Ausgabe] Der Wert, auf das SQL_DESC_DATA_PTR-Feld für den anwendungsparameterdeskriptor-Datensatz festgelegt. *DataPtr* kann auf ein null-Zeiger festgelegt werden.  
  
 Die *DataPtr* Argument kann auf ein null-Zeiger festgelegt werden, um das SQL_DESC_DATA_PTR-Feld auf einen null-Zeiger festgelegt. Wenn das Handle in die *DescriptorHandle* Argument ein ARD zugeordnet ist, dies hebt die Bindung der Spalte.  
  
 *StringLengthPtr*  
 [Verzögerte Eingabe oder Ausgabe] Der Wert, auf das Feld SQL_DESC_OCTET_LENGTH_PTR für den anwendungsparameterdeskriptor-Datensatz festgelegt. *StringLengthPtr* kann auf ein null-Zeiger festgelegt werden, um das Feld SQL_DESC_OCTET_LENGTH_PTR auf ein null-Zeiger festgelegt.  
  
 *IndicatorPtr*  
 [Verzögerte Eingabe oder Ausgabe] Der Wert, auf das Feld SQL_DESC_INDICATOR_PTR für den anwendungsparameterdeskriptor-Datensatz festgelegt. *IndicatorPtr* kann auf ein null-Zeiger festgelegt werden, um das SQL_DESC_INDICATOR_PTR-Feld auf einen null-Zeiger festgelegt.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetDescRec** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_DESC und ein *behandeln* von *DescriptorHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLSetDescRec** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07009|Ungültiger Deskriptorindex|Die *RecNumber* Argument wurde auf 0 festgelegt, und die *DescriptorHandle* bezeichnet ein IPD-Handle.<br /><br /> Die *RecNumber* Arguments ist kleiner als 0.<br /><br /> Die *RecNumber* Argument war größer als die maximale Anzahl von Spalten oder Parametern, die die Datenquelle unterstützt werden, und die *DescriptorHandle* Argument war ein APD, IPD oder ARD.<br /><br /> Die *RecNumber* Argument war gleich 0 (null) und die *DescriptorHandle* Argument ein implizit zugeordneten APD bezeichnet. (Dieser Fehler tritt nicht mit einer explizit zugewiesenen Anwendungsdiensts da nicht bekannt ist, ob eine explizit zugewiesene Anwendungsdiensts ein APD oder ARD bis Ausführung.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) die *DescriptorHandle* zugeordnet wurde eine *StatementHandle* für den eine asynchron ausgeführte Funktion (nicht beziehungsproblemen) aufgerufen wurde, und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* mit dem der *DescriptorHandle* verknüpft sind und SQL_NEED_DATA zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *DescriptorHandle*. Diese Funktion Aynchronous wurde weiterhin ausgeführt, wenn die **SQLSetDescRec** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** für eines der zugeordneten Anweisungshandles hieß die *DescriptorHandle* und SQL_PARAM_DATA_AVAILABLE zurückgegeben. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY016|Ein Implementierungszeilendeskriptor kann nicht geändert werden.|Die *DescriptorHandle* Argument ein IRD zugeordnet wurde.|  
|HY021|Inkonsistente Deskriptorinformationen|Die *Typ* Feld oder jedes andere Feld, das SQL_DESC_TYPE-Feld des Deskriptors zugeordnet war nicht gültig oder konsistent.<br /><br /> Während einer konsistenzprüfung überprüft Deskriptorinformationen war nicht konsistent. (Siehe "Konsistenzprüfungen," weiter unten in diesem Abschnitt.)|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Treiber wurde von einer ODBC 2.*.x* -Treiber der Deskriptor wurde ein ARD der *ColumnNumber* Argument wurde auf 0 festgelegt, sowie den Wert für das Argument angegebene *Pufferlänge* wurde nicht gleich 4.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *DescriptorHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Eine Anwendung kann Aufrufen **SQLSetDescRec** auf die folgenden Felder für eine einzelne Spalte oder Parameter festlegen:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (für Datensätze, deren Typ SQL_DATETIME oder SQL_INTERVAL wird)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Wenn ein Aufruf von **SQLSetDescRec** ein Fehler auftritt, wird der Inhalt des identifizierten Deskriptordatensatz der *RecNumber* Argument sind nicht definiert.  
  
 Wenn eine Spalte oder einen Parameter gebunden **SQLSetDescRec** können Sie mehrere Felder, die Auswirkungen auf die Bindung ohne Aufruf ändern **SQLBindCol** oder **SQLBindParameter** oder mehrere Serveraufrufe **SQLSetDescField**. **SQLSetDescRec** können auf ein Deskriptor, der derzeit nicht mit einer Anweisung verknüpfte Felder festlegen. Beachten Sie, dass **SQLBindParameter** legt mehr Felder als **SQLSetDescRec**, können Sie die Felder für eine APD und eine IPD in einem Aufruf festlegen und erfordert keine Deskriptorhandles.  
  
> [!NOTE]  
>  Das Anweisungsattribut SQL_ATTR_USE_BOOKMARKS sollte immer festgelegt werden, bevor **SQLSetDescRec** mit einem *RecNumber* Argument von 0 bis Lesezeichen Felder festlegen. Obwohl dies nicht erforderlich ist, wird dringend empfohlen.  
  
## <a name="consistency-checks"></a>Konsistenzprüfungen  
 Eine konsistenzprüfung wird automatisch vom Treiber ausgeführt, wenn eine Anwendung das SQL_DESC_DATA_PTR-Feld eines APD, ARD oder IPD festlegt. Wenn eines der Felder stimmt nicht mit anderen Feldern **SQLSetDescRec** SQLSTATE HY021 zurück (inkonsistente Deskriptorinformationen).  
  
 Wenn eine Anwendung das SQL_DESC_DATA_PTR-Feld eines APD, ARD oder IPD festlegt, überprüft der Treiber an, dass der Wert des Felds SQL_DESC_TYPE und gilt für das SQL_DESC_TYPE-Feld Werte sind gültig und konsistent. Diese Überprüfung wird immer ausgeführt, wenn **SQLBindParameter** oder **SQLBindCol** aufgerufen wird oder wenn **SQLSetDescRec** für eine APD, ARD oder IPD aufgerufen wird. Diese konsistenzprüfung umfasst die folgenden Überprüfungen auf deskriptorfelder:  
  
-   Das SQL_DESC_TYPE-Feld muss eine gültige ODBC C oder SQL-Typen oder ein Treiber-spezifische SQL-Typ sein. Das SQL_DESC_CONCISE_TYPE-Feld muss eine der gültigen ODBC C- oder SQL-Datentypen oder einen treiberspezifische C oder SQL aufweist, einschließlich der präzisen "DateTime" und das Intervall-Typen.  
  
-   Wenn SQL_DESC_TYPE-Datensatzfeld SQL_DATETIME oder SQL_INTERVAL hat, muss das Feld SQL_DESC_DATETIME_INTERVAL_CODE der gültiger DateTime-Wert oder Intervall Codes sein. (Siehe die Beschreibung des Felds SQL_DESC_DATETIME_INTERVAL_CODE in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Wenn das SQL_DESC_TYPE-Feld einen numerischen Typ gibt an, werden die Felder SQL_DESC_PRECISION und SQL_DESC_SCALE überprüft, um gültig zu sein.  
  
-   Ist das Feld SQL_DESC_CONCISE_TYPE eine Zeit oder Timestamp-Datentyp, ein Intervall Geben Sie mit einer Komponente für Sekunden oder eines der Interval-Datentypen mit einem Zeitkomponente Feld SQL_DESC_PRECISION wird überprüft, um eine gültige Sekunden Genauigkeit werden.  
  
-   Wenn die SQL_DESC_CONCISE_TYPE ein Intervall-Datentyp ist, wird Feld SQL_DESC_DATETIME_INTERVAL_PRECISION überprüft, um eine gültige führende Genauigkeit der Intervallwert sein.  
  
 Das SQL_DESC_DATA_PTR-Feld eine IPD ist normalerweise nicht festgelegt. Allerdings erreichen eine Anwendung, um eine konsistenzprüfung des IPD-Feldern zu erzwingen. Eine konsistenzprüfung kann nicht auf eine IRD ausgeführt werden. Der Wert, der das SQL_DESC_DATA_PTR-Feld der IPD festgelegt ist, werden eigentlich nicht gespeichert und kann nicht abgerufen werden, durch den Aufruf von **SQLGetDescField** oder **SQLGetDescRec**; die Einstellung erfolgt nur für das Erzwingen der Überprüfung der Projektkonsistenz.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einer Spalteninhalts|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ein Parameter gebunden|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Abrufen einer einzelnen Deskriptorfeld|[SQLGetDescField-Funktion](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Abrufen von mehreren deskriptorfelder|[SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Festlegen der einzelnen deskriptorfelder|[SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
