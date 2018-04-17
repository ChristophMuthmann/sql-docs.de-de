---
title: SQLGetDescRec-Funktion | Microsoft Docs
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
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f38ea81cf7eac8d670548382d8ffb4c0b79d503b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetDescRec** gibt den aktuellen Einstellungen oder Werte aus mehreren Feldern eines Datensatzes Deskriptor zurück. Die zurückgegebenen Felder werden Name, Datentyp und Speicherung von Daten für Spalte oder Parameter beschrieben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *DescriptorHandle*  
 [Eingabe] Deskriptorhandles.  
  
 *RecNumber*  
 [Eingabe] Gibt an, von dem die Anwendung Informationen Suchvorgängen, Deskriptordatensatz. Deskriptordatensätze werden von 1, mit der Datensatznummer lesezeichendatensatzes wird 0 nummeriert. Die *RecNumber* Argument muss kleiner oder gleich dem Wert des SQL_DESC_COUNT sein. Wenn *RecNumber* ist kleiner oder gleich SQL_DESC_COUNT, aber die Zeile enthält keine Daten für eine Spalte oder Parameter, einen Aufruf von **SQLGetDescRec** die Standardwerte der Felder zurück. (Weitere Informationen finden Sie unter "Initialisieren des Deskriptorfelder" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Name*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem SQL_DESC_NAME-Felds für den anwendungsparameterdeskriptor-Datensatz zurückgegeben.  
  
 Wenn *Namen* NULL ist, *StringLengthPtr* weiterhin die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) zurück in den Puffer verweist zurückzugebendenverfügbar *Namen*.  
  
 *Pufferlänge*  
 [Eingabe] Länge der **Namen* Puffers in Zeichen.  
  
 *StringLengthPtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem die Anzahl der Zeichen des zurückzugebenden in verfügbaren Daten zurückgegeben. die \* *Namen* Puffer, ausgenommen die Null-Abschlusszeichen. Die Anzahl der Zeichen war größer als oder gleich *Pufferlänge*, die Daten in \* *Namen* auf abgeschnitten *Pufferlänge* abzüglich der Länge des ein NULL-Abschlusszeichen und wird vom Treiber Null-terminiert.  
  
 *TypePtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem der Wert des Felds SQL_DESC_TYPE für den anwendungsparameterdeskriptor-Datensatz zurückgegeben.  
  
 *SubTypePtr*  
 [Ausgabe] Für Datensätze, deren Typ SQL_DATETIME oder SQL_INTERVAL hat, ist dies ein Zeiger auf einen Puffer, in dem der Wert des Felds SQL_DESC_DATETIME_INTERVAL_CODE zurückgegeben.  
  
 *LengthPtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem der Wert des Felds SQL_DESC_OCTET_LENGTH für den anwendungsparameterdeskriptor-Datensatz zurückgegeben.  
  
 *PrecisionPtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem der Wert des Felds SQL_DESC_PRECISION für den anwendungsparameterdeskriptor-Datensatz zurückgegeben.  
  
 *ScalePtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem der Wert des Felds SQL_DESC_SCALE für den anwendungsparameterdeskriptor-Datensatz zurückgegeben.  
  
 *NullablePtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem der Wert des Felds SQL_DESC_NULLABLE für den anwendungsparameterdeskriptor-Datensatz zurückgegeben.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA oder SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA zurückgegeben wird, wenn *RecNumber* ist größer als die aktuelle Anzahl der deskriptordatensätze.  
  
 SQL_NO_DATA zurückgegeben wird, wenn *DescriptorHandle* ist ein IRD-Handle und die Anweisung befindet sich im Status vorbereitet oder ausgeführt, aber es wurde keine geöffneten Cursor zugeordnet.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetDescRec** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_DESC und ein *behandeln* von *DescriptorHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLGetDescRec** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *Namen* war nicht groß genug ist, um das gesamte Deskriptorfeld zurückzugeben. Deshalb wurde das Feld abgeschnitten. Die Länge des Felds den ungekürzten Deskriptor wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07009|Ungültiger Deskriptorindex|Die *FieldIdentifier* Argument wurde ein Datensatzfeld der *RecNumber* Argument wurde auf 0 festgelegt, und die *DescriptorHandle* Argument wurde ein IPD-Handle.<br /><br /> (DM) die *RecNumber* Argument auf 0 festgelegt wurde, und das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF, festgelegt wurde und die *DescriptorHandle* Argument wurde ein IRD-Handle.<br /><br /> Die *RecNumber* Arguments ist kleiner als 0.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht zum Belegen des Speichers, der erforderlich ist, um die Ausführung oder den Abschluss der Funktion zu unterstützen.|  
|HY007|Die zugeordnete Anweisung ist nicht vorbereitet.|*DescriptorHandle* ein IRD zugeordnet wurde, und der zugehörigen Anweisungshandle wies nicht den Status vorbereitete oder ausgeführte.|  
|HY010|Fehler bei Funktionssequenz|(DM) *DescriptorHandle* zugeordnet wurde eine *StatementHandle* für den eine asynchron ausgeführte Funktion (nicht beziehungsproblemen) aufgerufen wurde, und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) *DescriptorHandle* zugeordnet wurde eine *StatementHandle* für die **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, oder **SQLSetPos** aufgerufen und SQL_NEED_DATA zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *DescriptorHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn **SQLGetDescRec** aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber zugeordneten *DescriptorHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Eine Anwendung kann Aufrufen **SQLGetDescRec** zum Abrufen der Werte der folgenden deskriptorfelder für eine einzelne Spalte oder Parameter:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (für Datensätze, deren Typ SQL_DATETIME oder SQL_INTERVAL wird)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** ruft nicht die Werte für die Felder ab.  
  
 Eine Anwendung kann die Rückgabe der Einstellung für ein Feld verhindern, durch das Argument, das entspricht dem Feld auf einen null-Zeiger festlegen.  
  
 Wenn eine Anwendung ruft **SQLGetDescRec** zum Abrufen des Werts eines Felds, das für einen bestimmten Deskriptortyp undefiniert ist, die Funktion gibt SQL_SUCCESS zurück, aber für das Feld zurückgegebene Wert ist nicht definiert. Beispielsweise Aufrufen **SQLGetDescRec** für das Feld SQL_DESC_NAME oder SQL_DESC_NULLABLE eines APD oder ARD SQL_SUCCESS jedoch einen nicht definierten Wert für das Feld zurück.  
  
 Wenn eine Anwendung ruft **SQLGetDescRec** zum Abrufen des Werts eines Felds an, für einen bestimmten Deskriptortyp definiert ist, aber hat keinen Standardwert und wurde noch nicht festgelegt, die Funktion gibt SQL_SUCCESS zurück, aber der zurückgegebene Wert für das Feld ist nicht definiert. Weitere Informationen finden Sie unter "Initialisieren des Deskriptorfelder" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Die Werte der Felder können auch einzeln von einem Aufruf abgerufen werden **SQLGetDescField**. Eine Beschreibung der Felder in einem Deskriptor Header oder Datensatz, finden Sie unter [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Weitere Informationen zu Deskriptoren, finden Sie unter [Deskriptoren](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einer Spalteninhalts|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ein Parameter gebunden|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Abrufen von einem Beschreibungsfeld|[SQLGetDescField-Funktion](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Mehrere deskriptorfelder festlegen|[SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
