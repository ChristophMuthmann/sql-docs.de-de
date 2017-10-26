---
title: SQLGetDescField-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1cbf48f5346d507505573391598cbd98017ccd8d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetDescField** gibt die aktuelle Einstellung oder ein Wert, der ein einzelnes Datenfeld in einem anwendungsparameterdeskriptor-Datensatz zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *DescriptorHandle*  
 [Eingabe] Deskriptorhandles.  
  
 *RecNumber*  
 [Eingabe] Gibt an, von dem die Anwendung Informationen Suchvorgängen, Deskriptordatensatz. Deskriptordatensätze sind von 0 (null) mit Datensatznummer wird lesezeichendatensatzes 0 nummeriert. Wenn die *FieldIdentifier* Argument gibt an, ein Headerfeld *RecNumber* wird ignoriert. Wenn *RecNumber* ist kleiner oder gleich SQL_DESC_COUNT, aber die Zeile enthält keine Daten für eine Spalte oder Parameter, einen Aufruf von **SQLGetDescField** die Standardwerte der Felder zurück. (Weitere Informationen finden Sie unter "Initialisieren des Deskriptorfelder" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Eingabe] Gibt das Feld des Deskriptors, deren Wert zurückgegeben werden. Weitere Informationen finden Sie unter der "*FieldIdentifier* Argument" im Abschnitt [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Deskriptorinformationen zurückgegeben. Der Datentyp hängt vom Wert der *FieldIdentifier*.  
  
 Wenn *ValuePtr* Ganzzahltyp ist, Anwendungen einen Puffer von SQLULEN sollte verwendet werden, und initialisieren Sie den Wert auf 0 vor dem Aufrufen dieser Funktion wie einige Treiber kann nur schreiben die unteren 32-Bit- oder 16-Bit-eines Puffers und lassen Sie das Bit höherer Ordnung unverändert.  
  
 Wenn *ValuePtr* NULL ist, *StringLengthPtr* weiterhin die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) zurück in den Puffer verweist zurückzugebendenverfügbar* ValuePtr*.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *FieldIdentifier* ist ein ODBC-definierten Feld und *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des \* *ValuePtr*. Wenn *FieldIdentifier* ist ein ODBC-definierten Feld und \* *ValuePtr* ist eine ganze Zahl *Pufferlänge* wird ignoriert. Wenn der Wert in * \*ValuePtr* wird von einem Unicode-Datentyp (beim Aufrufen von **SQLGetDescFieldW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 Wenn *FieldIdentifier* ist ein Feld treiberdefinierten die Anwendung zeigt die Art des Felds um den Treiber-Manager an, indem die *Pufferlänge* Argument. *Pufferlänge* können die folgenden Werte aufweisen:  
  
-   Wenn * \*ValuePtr* ist ein Zeiger auf eine Zeichenfolge *Pufferlänge* ist die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn * \*ValuePtr* ist ein Zeiger auf einen binären Puffer, und klicken Sie dann die Anwendung das Ergebnis von der SQL_LEN_BINARY_ATTR eingefügt (*Länge*)-Makro im *Pufferlänge*. Dies setzt einen negativen Wert in *Pufferlänge*.  
  
-   Wenn * \*ValuePtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder Binärzeichenfolge, *Pufferlänge* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn * \*ValuePtr* ist einen Datentyp fester Länge, dann enthält *Pufferlänge* SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT oder SQL_IS_USMALLINT, nach Bedarf ist.  
  
 *StringLengthPtr*  
 [Ausgabe] Zeiger auf den Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Anzahl der Bytes, die erforderlich sind, für die Null-Abschlusszeichen) zurückgegeben zur Rückgabe in **ValuePtr*.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA oder SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA zurückgegeben wird, wenn *RecNumber* ist größer als die aktuelle Anzahl der deskriptordatensätze.  
  
 SQL_NO_DATA zurückgegeben wird, wenn *DescriptorHandle* ist ein IRD-Handle und die Anweisung befindet sich im Status vorbereitet oder ausgeführt, aber es wurde keine geöffneten Cursor zugeordnet.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetDescField** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetDescField** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *ValuePtr* war nicht groß genug ist, um das gesamte Deskriptorfeld zurückzugeben, damit das Feld abgeschnitten wurden. Die Länge des Felds den ungekürzten Deskriptor wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07009|Ungültiger Deskriptorindex|(DM) die *RecNumber* Argument wurde gleich 0, das Anweisungsattribut SQL_ATTR_USE_BOOKMARK war SQL_UB_OFF, und die *DescriptorHandle* Argument wurde ein IRD-Handle. (Dieser Fehler kann für einen explizit zugewiesenen Deskriptor zurückgegeben werden, nur dann, wenn der Deskriptor ein Anweisungshandle zugeordnet ist.)<br /><br /> Die *FieldIdentifier* Argument wurde ein Datensatzfeld der *RecNumber* -Argument lautete 0 (null) und die *DescriptorHandle* Argument wurde ein IPD-Handle.<br /><br /> Die *RecNumber* Arguments ist kleiner als 0.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht zum Belegen des Speichers zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY007|Die zugeordnete Anweisung ist nicht vorbereitet.|*DescriptorHandle* zugeordnet wurde eine *StatementHandle* als ein IRD und die zugehörige Anweisung Handle wurde nicht vorbereitet oder ausgeführt.|  
|HY010|Fehler bei Funktionssequenz|(DM) *DescriptorHandle* zugeordnet wurde eine *StatementHandle* für den eine asynchron ausgeführte Funktion (nicht beziehungsproblemen) aufgerufen wurde, und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) *DescriptorHandle* zugeordnet wurde eine *StatementHandle* für die **SQLExecute**, **SQLExecDirect**, ** SQLBulkOperations**, oder **SQLSetPos** aufgerufen und SQL_NEED_DATA zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *DescriptorHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLGetDescField** Funktion aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY021|Inkonsistente Deskriptorinformationen|Die Felder SQL_DESC_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE bilden keine (für APDs oder ARDs) einen gültigen ODBC SQL-Typ, ein gültiger treiberspezifischen SQL-Typ (für Descriptor, IPD) oder einen gültigen ODBC C-Typ.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) * \*ValuePtr* wurde eine Zeichenfolge und *Pufferlänge* war kleiner als 0 (null).|  
|HY091|Ungültiger Deskriptorfeldbezeichner|*FieldIdentifier* kein Feld ODBC definiert und nicht wurde ein Implementierung definierte Wert.<br /><br /> *FieldIdentifier* wurde nicht definiert, für die *DescriptorHandle*.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *DescriptorHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Eine Anwendung kann Aufrufen **SQLGetDescField** den Wert ein einzelnes Datenfeld in einem anwendungsparameterdeskriptor-Datensatz zurückgegeben. Ein Aufruf von **SQLGetDescField** kann die Einstellung der jedes Feld in einen Deskriptortyp, einschließlich Headerfelder, Datensatzfelder und Lesezeichen Felder zurückgeben. Eine Anwendung kann die Einstellungen aus mehreren Feldern in der gleichen oder unterschiedliche Deskriptoren, in willkürlicher Reihenfolge durch wiederholte Aufrufe von abrufen **SQLGetDescField**. **SQLGetDescField** kann auch aufgerufen werden, um deskriptorfelder treiberdefinierten zurückzugeben.  
  
 Aus Gründen der Leistung eine Anwendung sollte nicht aufrufen **SQLGetDescField** für eine IRD vor der Ausführung einer Anweisung.  
  
 Die Einstellungen aus mehreren Feldern, die beschreiben, Name, Datentyp und Speicherung von Daten für Spalte oder Parameter können auch in einem einzigen Aufruf abgerufen werden **SQLGetDescRec**. **SQLGetStmtAttr** aufgerufen werden, um die Einstellung von einem einzelnen Feld im Deskriptor-Header zurück, das auch ein Anweisungsattribut ist. **SQLColAttribute**, **SQLDescribeCol**, und **SQLDescribeParam** Rückgabefelder Datensatz oder ein lesezeichenklick.  
  
 Wenn eine Anwendung ruft **SQLGetDescField** zum Abrufen des Werts eines Felds, das für einen bestimmten Deskriptortyp undefiniert ist, die Funktion gibt SQL_SUCCESS zurück, aber für das Feld zurückgegebene Wert ist nicht definiert. Beispielsweise Aufrufen **SQLGetDescField** für das Feld SQL_DESC_NAME oder SQL_DESC_NULLABLE eines APD oder ARD SQL_SUCCESS jedoch einen nicht definierten Wert für das Feld zurück.  
  
 Wenn eine Anwendung ruft **SQLGetDescField** zum Abrufen des Werts eines Felds an, für einen bestimmten Deskriptortyp definiert ist, aber hat keinen Standardwert und wurde noch nicht festgelegt, die Funktion gibt SQL_SUCCESS zurück, aber der Wert zurückgegeben für das Feld ist nicht definiert. Weitere Informationen für die Initialisierung der deskriptorfelder und Beschreibungen der Felder finden Sie unter "Initialisierung von Deskriptorfelder" in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Weitere Informationen zu Deskriptoren, finden Sie unter [Deskriptoren](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abrufen von mehreren deskriptorfelder|[SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Festlegen einer einzelnen Deskriptorfeld|[SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Mehrere deskriptorfelder festlegen|[SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

