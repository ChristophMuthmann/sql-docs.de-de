---
title: SQLSetDescField-Funktion | Microsoft Docs
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
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e6a0ee843ce2b78ebc611fee30a5ee8e16fc7e1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLSetDescField** legt den Wert für ein einzelnes Datenfeld in einem anwendungsparameterdeskriptor-Datensatz.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>Argumente  
 *DescriptorHandle*  
 [Eingabe] Deskriptorhandles.  
  
 *RecNumber*  
 [Eingabe] Gibt an, enthält das Feld, das die Anwendung sucht festzulegende Deskriptordatensatz. Deskriptordatensätze sind von 0 (null) mit Datensatznummer wird lesezeichendatensatzes 0 nummeriert. Die *RecNumber* Argument wird für Headerfelder ignoriert.  
  
 *FieldIdentifier*  
 [Eingabe] Gibt das Feld des Deskriptors, dessen Wert festgelegt werden. Weitere Informationen finden Sie unter "*FieldIdentifier* Argument" im Abschnitt "Kommentare".  
  
 *ValuePtr*  
 [Eingabe] Ein Zeiger auf einen Puffer, das die Deskriptorinformationen oder einen ganzzahligen Wert enthält. Der Datentyp hängt vom Wert der *FieldIdentifier*. Wenn *ValuePtr* ist ein Ganzzahlwert als angesehen als 8 Bytes (SQLLEN), 4 Bytes (SQLINTEGER) oder 2 Bytes (SQLSMALLINT), abhängig vom Wert der *FieldIdentifier* Argument.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *FieldIdentifier* ist ein ODBC-definierten Feld und *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des **ValuePtr*. Für Zeichenfolgendaten sollte dieses Argument die Anzahl der Bytes in der Zeichenfolge enthalten.  
  
 Wenn *FieldIdentifier* ist ein ODBC-definierten Feld und *ValuePtr* ist eine ganze Zahl *Pufferlänge* wird ignoriert.  
  
 Wenn *FieldIdentifier* ist ein Feld treiberdefinierten die Anwendung zeigt die Art des Felds um den Treiber-Manager an, indem die *Pufferlänge* Argument. *Pufferlänge* können die folgenden Werte aufweisen:  
  
-   Wenn *ValuePtr* ist ein Zeiger auf eine Zeichenfolge *Pufferlänge* ist die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn *ValuePtr* ist ein Zeiger auf einen binären Puffer, und klicken Sie dann die Anwendung das Ergebnis von der SQL_LEN_BINARY_ATTR eingefügt (*Länge*)-Makro im *Pufferlänge*. Dies setzt einen negativen Wert in *Pufferlänge*.  
  
-   Wenn *ValuePtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder eine binäre Zeichenfolge *Pufferlänge* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn *ValuePtr* enthält einen Wert fester Länge *Pufferlänge* SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT oder SQL_IS_USMALLINT, nach Bedarf ist.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetDescField** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_DESC und ein *behandeln* von *DescriptorHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLSetDescField** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Der Optionswert wurde geändert|Der Treiber nicht den Wert im angegebenen  *\*ValuePtr* (Wenn *ValuePtr* war ein Zeiger) oder den Wert in *ValuePtr* (Wenn *ValuePtr*  wurde ein ganzzahliger Wert), oder  *\*ValuePtr* ungültig aufgrund Implementierung Arbeitsbedingungen, damit der Treiber einen ähnlichen Wert ersetzt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07009|Ungültiger Deskriptorindex|Die *FieldIdentifier* Argument wurde ein Datensatzfeld der *RecNumber* -Argument lautete 0 (null) und die *DescriptorHandle* Argument bezeichnet ein IPD-Handle.<br /><br /> Die *RecNumber* Arguments ist kleiner als 0 (null) und die *DescriptorHandle* Argument ein ARD oder ein APD bezeichnet.<br /><br /> Die *RecNumber* Argument war größer als die maximale Anzahl von Spalten oder Parametern, die die Datenquelle unterstützt werden, und die *DescriptorHandle* Argument ein APD oder ARD bezeichnet.<br /><br /> (DM) die *FieldIdentifier* Argument war SQL_DESC_COUNT, und  *\*ValuePtr* Arguments ist kleiner als 0.<br /><br /> Die *RecNumber* Argument war gleich 0 (null) und die *DescriptorHandle* Argument ein implizit zugeordneten APD bezeichnet. (Dieser Fehler tritt nicht mit einer explizit zugewiesenen Anwendungsdiensts da nicht bekannt ist, ob eine explizit zugewiesene Anwendungsdiensts ein APD oder ARD bis Ausführungszeit.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22001|Zeichenfolgedaten wurden rechts abgeschnitten|Die *FieldIdentifier* Argument war SQL_DESC_NAME, und die *Pufferlänge* Argument wurde ein Wert größer als SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) die *DescriptorHandle* zugeordnet wurde eine *StatementHandle* für den eine asynchron ausgeführte Funktion (nicht beziehungsproblemen) aufgerufen wurde, und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* mit dem der *DescriptorHandle* verknüpft sind und SQL_NEED_DATA zurückgegeben wurde. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *DescriptorHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLSetDescField** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** für eines der zugeordneten Anweisungshandles hieß die *DescriptorHandle* und SQL_PARAM_DATA_AVAILABLE zurückgegeben. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY016|Ein Implementierungszeilendeskriptor kann nicht geändert werden.|Die *DescriptorHandle* Argument wurde ein IRD zugeordnet und die *FieldIdentifier* Argument war kein SQL_DESC_ARRAY_STATUS_PTR oder SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Inkonsistente Deskriptorinformationen|Die Felder SQL_DESC_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE bilden keine (für APDs oder ARDs) einen gültigen ODBC SQL-Typ oder einen gültigen treiberspezifischen SQL-Typ (für Descriptor, IPD) oder einen gültigen ODBC C-Typ.<br /><br /> Während einer konsistenzprüfung überprüft Deskriptorinformationen war nicht konsistent. (Finden Sie unter "Konsistenzprüfung" in **SQLSetDescRec**.)|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM)  *\*ValuePtr* ist eine Zeichenfolge und *Pufferlänge* war kleiner als null aber war nicht SQL_NTS gleich.<br /><br /> (DM) der Treiber wurde von einer ODBC 2.*.x* -Treiber der Deskriptor wurde ein ARD der *ColumnNumber* Argument wurde auf 0 festgelegt, sowie den Wert für das Argument angegebene *Pufferlänge* wurde nicht gleich 4.|  
|HY091|Ungültiger Deskriptorfeldbezeichner|Der angegebene Wert für die *FieldIdentifier* Argument kein Feld ODBC definiert und nicht wurde eine Implementierung definierte Wert.<br /><br /> Die *FieldIdentifier* Argument war ungültig für die *DescriptorHandle* Argument.<br /><br /> Die *FieldIdentifier* Argument wurde ein Feld schreibgeschützt, ODBC definiert.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|Der Wert in  *\*ValuePtr* war nicht gültig für die *FieldIdentifier* Argument.<br /><br /> Die *FieldIdentifier* Argument war SQL_DESC_UNNAMED, und *ValuePtr* SQL_NAMED wurde.|  
|HY105|Ungültiger Parametertyp|(DM) für das Feld SQL_DESC_PARAMETER_TYPE angegebene Wert war ungültig. (Weitere Informationen finden Sie unter der "*InputOutputType* Argument" im Abschnitt **SQLBindParameter**.)|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [Neuigkeiten in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *DescriptorHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Eine Anwendung kann Aufrufen **SQLSetDescField** alle Deskriptorfeld eine zu einem Zeitpunkt festgelegt. Ein Aufruf von **SQLSetDescField** legt ein einzelnes Feld in ein einzelnes Deskriptor fest. Diese Funktion wird aufgerufen, um jedes Feld in einen Deskriptortyp festzulegen, vorausgesetzt, dass das Feld festgelegt werden kann. (Siehe die Tabelle weiter unten in diesem Abschnitt.)  
  
> [!NOTE]  
>  Wenn ein Aufruf von **SQLSetDescField** ein Fehler auftritt, wird der Inhalt des identifizierten Deskriptordatensatz der *RecNumber* Argument sind nicht definiert.  
  
 Andere Funktionen können aufgerufen werden, um mehrere deskriptorfelder mit einem einzigen Aufruf der Funktion festlegen. Die **SQLSetDescRec** Funktion legt einer Vielzahl von Feldern, die Einfluss auf den Datentyp und Puffer gebunden werden, auf eine Spalte oder Parameter (die SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_ DESC_SCALE, SQL_DESC_DATA_PTR SQL_DESC_OCTET_LENGTH_PTR und SQL_DESC_INDICATOR_PTR Felder). **SQLBindCol** oder **SQLBindParameter** kann verwendet werden, um eine vollständige Spezifikation für die Bindung einer Spalte oder Parameter zu machen. Diese Funktionen legen Sie eine bestimmte Gruppe von deskriptorfelder mit einem Funktionsaufruf.  
  
 **SQLSetDescField** aufgerufen werden, um die Bindung Puffer zu ändern, indem Sie die Bindung Zeiger (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR) einen Offset hinzugefügt. Dadurch wird die Bindung Puffer ohne Aufruf **SQLBindCol** oder **SQLBindParameter**, die ermöglicht einer Anwendung SQL_DESC_DATA_PTR zu ändern, ohne dass andere Felder wie SQL_DESC_DATA_ GEBEN SIE EIN.  
  
 Wenn eine Anwendung ruft **SQLSetDescField** um ein Feld als SQL_DESC_COUNT oder zurückgestellten Felder SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR oder SQL_DESC_INDICATOR_PTR festgelegt, der Datensatz wird als ungebundene.  
  
 Deskriptorheaderfelder sind festgelegt werden, indem **SQLSetDescField** mit dem entsprechenden *FieldIdentifier*. Viele Headerfelder sind auch Anweisungsattribute, damit sie auch können, durch den Aufruf von festgelegt werden **SQLSetStmtAttr**. Dadurch können Anwendungen auf einem Beschreibungsfeld festlegen, ohne zunächst eine Deskriptorhandles abrufen. Wenn **SQLSetDescField** wird aufgerufen, um ein Headerfeld legen die *RecNumber* Argument wird ignoriert.  
  
 Ein *RecNumber* 0 wird zum Festlegen von Lesezeichen-Felder verwendet.  
  
> [!NOTE]  
>  Das Anweisungsattribut SQL_ATTR_USE_BOOKMARKS sollte immer festgelegt werden, bevor **SQLSetDescField** Lesezeichen Felder festlegen. Obwohl dies nicht erforderlich ist, wird dringend empfohlen.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Sequenz von Deskriptorfelder festlegen  
 Beim Festlegen von deskriptorfelder durch Aufrufen von **SQLSetDescField**, die Anwendung muss eine bestimmte Sequenz folgen:  
  
1.  Die Anwendung muss zunächst das Feld SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE oder SQL_DESC_DATETIME_INTERVAL_CODE festgelegt.  
  
2.  Nachdem Sie eines dieser Felder festgelegt wurde, die Anwendung kann ein Attribut mit einem Datentyp festlegen, und der Treiber setzt Datentyp Attributfelder auf die entsprechenden Standardwerte für den Datentyp. Automatische Standardwert des Typs Attributfelder sichergestellt, dass der Deskriptor immer verwendet wird, sobald die Anwendung einen-Datentyp angegeben wurde. Wenn die Anwendung explizit mit einem Datentypattribut festlegt, ist es das Standardattribut überschreiben.  
  
3.  Nachdem eine der in Schritt 1 aufgeführten Felder festgelegt wurde und Daten Typattribute festgelegt wurden, kann die Anwendung SQL_DESC_DATA_PTR festlegen. Dadurch wird eine konsistenzprüfung des deskriptorfelder aufgefordert. Wenn die Anwendung den Datentyp oder die Attribute ändert, nachdem Sie das SQL_DESC_DATA_PTR-Feld festgelegt haben, legt der Treiber SQL_DESC_DATA_PTR auf einen null-Zeiger, Aufheben der Bindung des Datensatzes. Dies erzwingt die Anwendung die richtigen Schritte nacheinander abgeschlossen werden, damit die anwendungsparameterdeskriptor-Datensatz verwendet werden kann.  
  
## <a name="initialization-of-descriptor-fields"></a>Initialisierung des Deskriptorfelder  
 Wenn ein Deskriptor, der belegt wurde, die Felder im Deskriptor können auf einen Standardwert initialisiert werden, ohne einen Standardwert initialisiert werden, oder für den Typ des Deskriptors nicht definiert werden. Die folgende Tabelle gibt an, die Initialisierung der einzelnen Felder für jeden Typ von ein Deskriptor, mit "D" gibt an, dass das Feld hat den Standardwert initialisiert wird, und "ND" gibt an, dass das Feld ohne Standardwert initialisiert wird. Wenn eine Zahl angezeigt wird, ist der Standardwert des Felds diese Anzahl an. Die Tabellen geben außerdem an, ob ein Feld (R/W) Lese-/Schreibzugriff oder schreibgeschützten (R) ist.  
  
 Die Felder von einem IRD über einen Standardwert verfügen, nur, nachdem die Anweisung vorbereitet oder ausgeführt wurde und IRD aufgefüllt wurden, nicht verwendet werden, wenn die Anweisungshandle oder Deskriptor zugeordnet wurde. Bis IRD aufgefüllt wurde, wird jeder Versuch, den Zugriff auf ein Feld von einem IRD einen Fehler zurück.  
  
 Einige deskriptorfelder sind für eine oder mehrere, aber nicht in allen Typen Deskriptor (ARDs und IRDs, und APDs und Descriptor, IPD) definiert. Wenn ein Feld für einen Typ des Deskriptors nicht definiert ist, ist es nicht durch eine der Funktionen benötigt, die diese Deskriptor verwenden.  
  
 Die Felder, die durch möglich **SQLGetDescField** nicht notwendigerweise durch festgelegt werden **SQLSetDescField**. Felder, die festgelegt werden können, indem Sie **SQLSetDescField** in den folgenden Tabellen aufgeführt sind.  
  
 Die Initialisierung des Headerfelder ist in der Tabelle beschriebenen, das folgt.  
  
|Header-Feldnamen|Typ|R/W|Default|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R-APD: R IRD: R IPD: R|ARD: SQL_DESC_ALLOC_AUTO für implizite oder SQL_DESC_ALLOC_USER für explizite<br /><br /> APD: SQL_DESC_ALLOC_AUTO für implizite oder SQL_DESC_ALLOC_USER für explizite<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN ERSTELLT WURDE|ARD: R/W APD: R/W IRD: nicht verwendeter IPD: nicht verwendeter|ARD: [1] APD: [1] IRD: nicht verwendeter IPD: nicht verwendeter|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|ARD: R/W-APD: R/W IRD: IPD R/W: R/W|ARD: Null Ptr APD: Null, Ptr IRD: Null, Ptr IPD: Null, Ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: nicht verwendeter IPD: nicht verwendeter|ARD: Null Ptr APD: Null, Ptr IRD: nicht verwendeter IPD: nicht verwendeter|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: nicht verwendeter IPD: nicht verwendeter|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: nicht verwendeter<br /><br /> IPD: nicht verwendeter|  
SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: 0 APD: IRD 0: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: IPD R/W: R/W|ARD: Nicht verwendeter APD: nicht verwendeter IRD: Null, Ptr IPD: Null, Ptr|  
  
 [1] für diese Felder werden definiert, nur, wenn die IPD vom Treiber automatisch aufgefüllt wird. Falls nicht, sind sie nicht definiert. Wenn eine Anwendung versucht, legen Sie diese Felder, SQLSTATE HY091 (Ungültiger Deskriptorfeldbezeichner) zurückgegeben werden.  
  
 Die Initialisierung des Datensatzfelder ist wie in der folgenden Tabelle gezeigt.  
  
|Datensatz-Feldnamen|Typ|R/W|Default|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: SQL_C_ STANDARD APD: SQL_C_ STANDARD IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD: R/W APD: R/W IRD: nicht verwendeter IPD: nicht verwendeter|ARD: Null Ptr APD: Null, Ptr IRD: nicht verwendeter IPD: nicht verwendeter [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: nicht verwendeter IPD: nicht verwendeter|ARD: Null Ptr APD: Null, Ptr IRD: nicht verwendeter IPD: nicht verwendeter|  
|SQL_DESC_LABEL|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_LENGTH|SQLULEN ERSTELLT WURDE|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: D [1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: nicht verwendeter IPD: nicht verwendeter|ARD: Null Ptr APD: Null, Ptr IRD: nicht verwendeter IPD: nicht verwendeter|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: nicht verwendeter IPD: R/W|ARD: Nicht verwendeter APD: nicht verwendeter IRD: nicht verwendeter IPD: D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: nicht verwendeter<br /><br /> APD: nicht verwendeter<br /><br /> IRD: R<br /><br /> IPD: R|ARD: nicht verwendeter<br /><br /> APD: nicht verwendeter<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
SQL_DESC_TYPE_NAME|SQLCHAR *|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: R|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: Nicht verwendeter APD: nicht verwendeter IRD: R IPD: nicht verwendeter|ARD: Nicht verwendeter APD: nicht verwendeter IRD: D IPD: nicht verwendeter|  
  
 [1] für diese Felder werden definiert, nur, wenn die IPD vom Treiber automatisch aufgefüllt wird. Falls nicht, sind sie nicht definiert. Wenn eine Anwendung versucht, legen Sie diese Felder, SQLSTATE HY091 (Ungültiger Deskriptorfeldbezeichner) zurückgegeben werden.  
  
 [2] ' ist das SQL_DESC_DATA_PTR-Feld in den IPD kann festgelegt werden, um eine konsistenzprüfung zu erzwingen. In einem nachfolgenden Aufruf **SQLGetDescField** oder **SQLGetDescRec**, der Treiber ist nicht erforderlich, um den Wert zurückzugeben, die zum SQL_DESC_DATA_PTR festgelegt wurde.  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier-Argument  
 Die *FieldIdentifier* Argument gibt an, das Deskriptorfeld festgelegt werden. Enthält eine Beschreibung der *Deskriptor-Header,* besteht im nächsten Abschnitt, "Headerfelder", und 0 (null) oder mehrere beschriebenen Headerfelder *deskriptordatensätze,* bestehend aus dem Datensatzfelder Im folgenden Abschnitt "Headerfelder" Abschnitt beschrieben.  
  
## <a name="header-fields"></a>Headerfelder  
 Jeder Deskriptor verfügt über einen Header, bestehend aus den folgenden Feldern:  
  
 **SQL_DESC_ALLOC_TYPE [All]**  
 Diese schreibgeschützte SQLSMALLINT-Headerfeld gibt an, ob es sich bei der Deskriptor automatisch vom Treiber oder explizit von der Anwendung belegt wurde. Die Anwendung kann abrufen, aber nicht zum Ändern dieses Felds. Das Feld wird vom Treiber auf SQL_DESC_ALLOC_AUTO festgelegt, wenn der Deskriptor automatisch vom Treiber zugewiesen wurde. Es wird auf SQL_DESC_ALLOC_USER vom Treiber festgelegt, wenn der Deskriptor explizit von der Anwendung belegt wurde.  
  
 **SQL_DESC_ARRAY_SIZE [Anwendungsdiensts]**  
 Diese SQLULEN-Headerfeld in ARDs gibt an, dass die Anzahl der Zeilen im Rowset. Dies ist die Anzahl der Zeilen durch einen Aufruf zurückzugebenden **SQLFetch** oder **SQLFetchScroll** oder durch einen Aufruf von verarbeitet werden sollen **SQLBulkOperations** oder **SQLSetPos** .  
  
 Diese SQLULEN-Headerfeld in APDs gibt an, dass die Anzahl der Werte für jeden Parameter.  
  
 Der Standardwert dieses Felds ist 1. Wenn SQL_DESC_ARRAY_SIZE größer als 1 ist, zeigen Sie SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR der APD oder ARD auf Arrays an. Die Kardinalität jedes Arrays ist gleich dem Wert dieses Felds.  
  
 Dieses Feld in der ARD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_ROW_ARRAY_SIZE-Attribut. Dieses Feld im APD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_PARAMSET_SIZE-Attribut.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [All]**  
 Für jede Deskriptortyp dieser SQLUSMALLINT * Header Feld zeigt auf ein Array von SQLUSMALLINT-Werten. Diese Arrays werden wie folgt benannt: Zeile Statusarray (IRD), Parameter Statusarray (Implementierungsparameterdeskriptor, Implementierungszeilendeskriptor), Zeile Operation-Array (ARD) und Vorgang Parameterarray (APD).  
  
 In IRD dieser-Headerfeld verweist, auf ein zeilenstatusarray mit Statuswerte nach einem Aufruf von **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, oder **SQLSetPos**. Das Array hat so viele Elemente als Zeilen im Rowset vorhanden sind. Die Anwendung muss ein Array von SQLUSMALLINTs zuordnen und setzen Sie dieses Feld, um auf das Array zu verweisen. Die Standardeinstellung für des Felds ist eines null-Zeigers. Der Treiber das Array aufgefüllt wird, es sei denn ist, das Feld SQL_DESC_ARRAY_STATUS_PTR in diesem Fall werden keine Statuswerte generiert einen null-Zeiger festgelegt und das Array wird nicht aufgefüllt.  
  
> [!CAUTION]  
>  Treiber Verhalten ist undefiniert, wenn die Anwendung die Elemente der zeilenstatusarray verweist das SQL_DESC_ARRAY_STATUS_PTR Feld vom IRD festlegt.  
  
 Das Array wird durch einen Aufruf von anfänglich aufgefüllt **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, oder **SQLSetPos**. Wenn der Aufruf nicht SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgegeben wurde, werden der Inhalt des Arrays, die auf dieses Feld zeigt nicht definiert. Die Elemente im Array können die folgenden Werte enthalten:  
  
-   SQL_ROW_SUCCESS: Die Zeile wurde erfolgreich abgerufen und seit dem letzten Abruf nicht geändert.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: Die Zeile wurde erfolgreich abgerufen und seit dem letzten Abruf nicht geändert. Allerdings wurde eine Warnung zur Zeile zurückgegeben.  
  
-   SQL_ROW_ERROR: Fehler beim Abrufen einer Zeile.  
  
-   SQL_ROW_UPDATED: Die Zeile wurde erfolgreich abgerufen, und es wurde seit dem letzten Abruf wurde aktualisiert. Wenn die Zeile erneut abgerufen wird, ist dessen Status SQL_ROW_SUCCESS an.  
  
-   SQL_ROW_DELETED: Die Zeile wurde gelöscht, seit dem letzten Abruf wurde.  
  
-   SQL_ROW_ADDED: Die Zeile eingefügt wurde von **SQLBulkOperations**. Wenn die Zeile erneut abgerufen wird, ist dessen Status SQL_ROW_SUCCESS an.  
  
-   SQL_ROW_NOROW: Das Rowset überlappenden das Ende des Resultsets und, dass, die auf dieses Element des Arrays Status Zeile zugestimmt haben, wurde keine Zeile zurückgegeben.  
  
 Dieses Feld in IRD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_ROW_STATUS_PTR-Attribut.  
  
 Feld SQL_DESC_ARRAY_STATUS_PTR vom IRD gilt nur, wenn SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgegeben wurde. Wenn der Rückgabecode nicht einer davon ist, ist der Speicherort, auf SQL_DESC_ROWS_PROCESSED_PTR nicht definiert.  
  
 In den IPD dieser-Headerfeld verweist, auf ein Parameterarray-Status enthält Statusinformationen für jeden Satz von Parameterwerten nach einem Aufruf von **SQLExecute** oder **SQLExecDirect**. Wenn der Aufruf von **SQLExecute** oder **SQLExecDirect** hat keine zurückgegeben SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, den Inhalt des Arrays, die auf dieses Feld zeigt sind nicht definiert. Die Anwendung muss ein Array von SQLUSMALLINTs zuordnen und setzen Sie dieses Feld, um auf das Array zu verweisen. Der Treiber das Array aufgefüllt wird, es sei denn ist, das Feld SQL_DESC_ARRAY_STATUS_PTR in diesem Fall werden keine Statuswerte generiert einen null-Zeiger festgelegt und das Array wird nicht aufgefüllt. Die Elemente im Array können die folgenden Werte enthalten:  
  
-   SQL_PARAM_SUCCESS: Die SQL-Anweisung wurde erfolgreich für diesen Satz von Parametern ausgeführt.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: Die SQL-Anweisung wurde erfolgreich für diesen Satz von Parametern ausgeführt. Warnungsinformationen steht jedoch in der Diagnose-Datenstruktur.  
  
-   SQL_PARAM_ERROR: Fehler bei der Verarbeitung dieser Satz von Parametern. Zusätzliche Fehlerinformationen ist in der Diagnose-Datenstruktur verfügbar.  
  
-   SQL_PARAM_UNUSED: Dieses Parametersatzes wurde nicht verwendet, möglicherweise darauf zurückzuführen, dass einige vorherigen Parametersatz einen Fehler verursacht hat, der weitere Verarbeitung abgebrochen, oder weil für diesen Satz von Parametern in das Array, das gemäß der SQL_DESC_ARRAY_ SQL_PARAM_IGNORE festgelegt wurde STATUS_PTR-Feld der APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: Diagnoseinformationen ist nicht verfügbar. Ein Beispiel hierfür ist, wenn der Treiber Arrays von Parametern als monolithischen Einheit behandelt und daher keine dieses Maß an Fehlerinformationen generiert.  
  
 Dieses Feld in den IPD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_PARAM_STATUS_PTR-Attribut.  
  
 In der ARD dieser-Headerfeld verweist, auf eine Zeile Operation-Array von Werten, die festgelegt werden können, von der Anwendung, um anzugeben, ob diese Zeile ist für ignoriert werden **SQLSetPos** Vorgänge. Die Elemente im Array können die folgenden Werte enthalten:  
  
-   SQL_ROW_PROCEED: Die Zeile in der Bulk-Vorgang mit einbezogen **SQLSetPos**. (Diese Einstellung kann nicht garantiert, dass der Vorgang für die Zeile wiederholt werden soll. Wenn die Zeile den Status SQL_ROW_ERROR in IRD-zeilenstatusarray verfügt, die Treiber zum Ausführen des Vorgangs in der Zeile möglicherweise nicht.)  
  
-   SQL_ROW_IGNORE: Die Zeile wird aus dem Bulk-Vorgang mit ausgeschlossen **SQLSetPos**.  
  
 Wenn keine Elemente des Arrays festgelegt werden, sind alle Zeilen in der Bulk-Vorgang enthalten. Wenn der Wert im Feld SQL_DESC_ARRAY_STATUS_PTR der ARD ein null-Zeiger ist, werden alle Zeilen des Massenvorgangs berücksichtigt; die Interpretation ist identisch, als ob der Zeiger auf ein gültiges Array verweist und alle Elemente des Arrays SQL_ROW_PROCEED wurden. Wenn ein Element im Array auf SQL_ROW_IGNORE festgelegt ist, wird der Wert in der zeilenstatusarray für die Zeile ignoriert nicht geändert.  
  
 Dieses Feld in der ARD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_ROW_OPERATION_PTR-Attribut.  
  
 In APD, dieser-Headerfeld verweist, auf ein Parameterarray Vorgang Werte, mit denen festgelegt werden kann, von der Anwendung an, ob dieser Satz von Parametern ist, werden ignoriert, wenn **SQLExecute** oder **SQLExecDirect**aufgerufen wird. Die Elemente im Array können die folgenden Werte enthalten:  
  
-   SQL_PARAM_PROCEED: Dient der Satz von Parametern in der **SQLExecute** oder **SQLExecDirect** aufrufen.  
  
-   SQL_PARAM_IGNORE: Der Satz an Parametern ausgeschlossen ist die **SQLExecute** oder **SQLExecDirect** aufrufen.  
  
 Wenn keine Elemente des Arrays festgelegt sind, werden alle Sätze von Parametern im Array verwendet, der **SQLExecute** oder **SQLExecDirect** aufrufen. Wenn der Wert im Feld SQL_DESC_ARRAY_STATUS_PTR APD ein null-Zeiger ist, werden alle Sätze von Parametern verwendet. die Interpretation ist identisch, als ob der Zeiger auf ein gültiges Array verweist und alle Elemente des Arrays SQL_PARAM_PROCEED wurden.  
  
 Dieses Feld im APD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_PARAM_OPERATION_PTR-Attribut.  
  
 **SQL_DESC_BIND_OFFSET_PTR [Anwendungsdiensts]**  
 Diese SQLLEN * Header Feld zeigt den Offset für die Bindung. Es ist standardmäßig auf einen null-Zeiger festgelegt. Wenn dieses Feld keinen null-Zeiger ist, wird der Treiber dereferenziert den Zeiger und fügt den verweislosen Wert jedem der zurückgestellten Felder, die im Deskriptordatensatz (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR) einen Wert ungleich Null aufweist Beim rufen Sie Zeit und verwendet die neuen Zeigerwerte ab, wenn bei der Bindung.  
  
 Die Bindung Offset wird immer direkt auf die Werte in den Feldern SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR hinzugefügt. Wenn der Offset in einen anderen Wert geändert wird, wird der neue Wert direkt auf den Wert in jedem Deskriptorfeld weiterhin hinzugefügt. Der neue Offset ist der Wert des Felds sowie alle früheren Offset nicht hinzugefügt.  
  
 Dieses Feld ist eine *verzögerte Feld*: Er wird nicht verwendet, zu dem Zeitpunkt festgelegt ist, aber es wird zu einem späteren Zeitpunkt vom Treiber verwendet, wenn die Adressen für Datenpuffer ermittelt werden muss.  
  
 Dieses Feld in der ARD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_ROW_BIND_OFFSET_PTR-Attribut. Dieses Feld in der ARD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit dem SQL_ATTR_PARAM_BIND_OFFSET_PTR-Attribut.  
  
 Weitere Informationen finden Sie unter der Beschreibung der zeilenbezogene Bindungen in [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) und [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [Anwendungsdiensts]**  
 Diese SQLUINTEGER-Headerfeld legt fest, die Bindung Ausrichtung zum Binden von Spalten oder Parametern verwendet werden soll.  
  
 In ARDs, dieses Feld gibt die Ausrichtung für die Bindung beim **SQLFetchScroll** oder **SQLFetch** für das zugeordnete Anweisungshandle aufgerufen wird.  
  
 Um spaltenbezogene Bindungen für Spalten auswählen, wird dieses Feld auf SQL_BIND_BY_COLUMN (Standardeinstellung) festgelegt.  
  
 Dieses Feld in der ARD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit der SQL_ATTR_ROW_BIND_TYPE *Attribut*.  
  
 Dieses Feld in APDs gibt an, dass die Bindung Ausrichtung für dynamische Parameter verwendet werden soll.  
  
 Um spaltenbezogene Bindungen für Parameter auswählen, wird dieses Feld auf SQL_BIND_BY_COLUMN (Standardeinstellung) festgelegt.  
  
 Dieses Feld im APD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit der SQL_ATTR_PARAM_BIND_TYPE *Attribut*.  
  
 **SQL_DESC_COUNT [All]**  
 Diese SQLSMALLINT-Headerfeld gibt an, der auf 1 basierende Index des höchsten nummerierten Datensatzes, der Daten enthält. Wenn der Treiber die Datenstruktur für den Deskriptor setzt, muss er auch festgelegt SQL_DESC_COUNT-Feld, um anzuzeigen, wie viele Datensätze von Bedeutung sind. Wenn eine Anwendung eine Instanz dieser Datenstruktur zuordnet, es keinen an, wie viele Datensätze, um Platz für zu reservieren. Wie die Anwendung den Inhalt der Datensätze angibt, verwendet der Treiber Eingreifen erforderlich auf, um sicherzustellen, dass die Deskriptorhandles auf eine Datenstruktur der angemessenen Größe bezieht.  
  
 SQL_DESC_COUNT ist nicht die Anzahl der alle Datenspalten, die gebunden sind (wenn das Feld in einer ARD ist) oder aller Parameter, die gebunden sind (wenn das Feld in einer APD), sondern die Anzahl der höchsten nummerierten Datensatz. Wenn der höchsten nummerierten Spalte oder des Parameters aufgehoben wird, wird SQL_DESC_COUNT in die Anzahl der nächsten höchsten nummerierten Spalte oder des Parameters geändert. Wenn eine Spalte oder einen Parameter mit einer Zahl ist, die kleiner als die Anzahl der höchsten nummerierten Spalte aufgehoben wird (durch Aufrufen von **SQLBindCol** mit der *TargetValuePtr* Argument festgelegt wird, um einen null-Zeiger oder **SQLBindParameter** mit der *ParameterValuePtr* -Argument ein null-Zeiger festgelegt), SQL_DESC_COUNT wird nicht geändert. Wenn Sie zusätzliche Spalten oder Parametern mit Zahlen, die größer ist als der höchsten nummerierten Datensatz, die Daten enthält gebunden sind, wird der Treiber automatisch den Wert im Feld SQL_DESC_COUNT erhöht. Wenn alle Spalten durch Aufrufen von ungebundenen sind **SQLFreeStmt** mit der Option SQL_UNBIND SQL_DESC_COUNT Felder in den ARD und IRD auf 0 festgelegt werden. Wenn **SQLFreeStmt** wird aufgerufen, mit der Option SQL_RESET_PARAMS werden die Felder SQL_DESC_COUNT in APD und IPD auf 0 festgelegt.  
  
 Der Wert in SQL_DESC_COUNT kann festgelegt werden explizit von einer Anwendung durch Aufrufen von **SQLSetDescField**. Wenn der Wert in SQL_DESC_COUNT explizit verringert wird, werden alle Datensätze mit Zahlen, die größer als der neue Wert in SQL_DESC_COUNT effektiv entfernt. Wenn der Wert in SQL_DESC_COUNT explizit auf 0 festgelegt ist, und das Feld "" ein ARD ist, werden alle Datenpuffer außer einer gebundenen Lesezeichenspalte freigegeben.  
  
 Die Anzahl der Datensätze in diesem Feld der ein ARD umfasst eine gebundene Lesezeichenspalte nicht. Die einzige Möglichkeit zum Aufheben der Bindung einer Lesezeichenspalte ist das SQL_DESC_DATA_PTR-Feld auf einen null-Zeiger festgelegt.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [Implementierung Deskriptoren]**  
 In einer IRD dieser SQLULEN \* Header Feld verweist auf einen Puffer, der die Anzahl der nach einem Aufruf von abgerufenen Zeilen enthält **SQLFetch** oder **SQLFetchScroll**, oder die Anzahl der betroffenen Zeilen in einem Massenvorgang durch einen Aufruf ausgeführt **SQLBulkOperations** oder **SQLSetPos**, einschließlich der Fehlerzeilen.  
  
 In einem IPD, diese SQLUINTEGER * Header Feld verweist auf einen Puffer, der die Anzahl von Parametersätzen, die verarbeitet worden sind, einschließlich Fehler, enthält. Wenn dies ein null-Zeiger ist, wird keine Anzahl zurückgegeben.  
  
 SQL_DESC_ROWS_PROCESSED_PTR ist gültig, erst nach einem Aufruf von SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgegeben wurde **SQLFetch** oder **SQLFetchScroll** (für ein IRD-Feld) oder **SQLExecute** , **SQLExecDirect**, oder **SQLParamData** (für ein IPD-Feld). Wenn der Aufruf, der im Puffer füllt, zeigt dieses Feld keinen SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgibt, den Inhalt des Puffers sind nicht definiert ist, es sei denn, es SQL_NO_DATA, zurückgegeben, in dem der Wert im Puffer auf 0 festgelegt ist.  
  
 Dieses Feld in der ARD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** mit das SQL_ATTR_ROWS_FETCHED_PTR-Attribut. Dieses Feld im APD kann auch festgelegt werden, durch den Aufruf **SQLSetStmtAttr** durch das SQL_ATTR_PARAMS_PROCESSED_PTR-Attribut.  
  
 Der Puffer, die auf dieses Feld wird von der Anwendung zugeordnet. Es ist eine verzögerte Ausgabepuffer, der vom Treiber festgelegt wird. Es ist standardmäßig auf einen null-Zeiger festgelegt.  
  
## <a name="record-fields"></a>Datensatzfelder  
 Jeder Deskriptor enthält einen oder mehrere Datensätze, Felder, die Spaltendaten oder dynamische Parameter – je nach Art des Deskriptors definieren besteht. Jeder Datensatz ist eine vollständige Definition einer einzelnen Spalte oder Parameter.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 Diese schreibgeschützte SQLINTEGER-Datensatzfeld enthält SQL_TRUE, wenn die Spalte eine Spalte automatisch erhöht oder SQL_FALSE ist, wenn die Spalte keiner automatisch inkrementierten Spalte ist. Dieses Feld ist schreibgeschützt, aber die zugrunde liegende automatisch inkrementierten Spalte ist nicht notwendigerweise schreibgeschützt.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält der Name der Basisspalte aus, für die Resultsetspalte. Wenn der Name der Basisspalte nicht (wie im Fall von Spalten, die Ausdrücke sind) vorhanden ist, enthält diese Variable eine leere Zeichenfolge.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält der Name der Basistabelle, für die Resultsetspalte. Wenn Sie ein Namen für die Basistabelle kann nicht definiert werden oder ist nicht anwendbar, enthält diese Variable eine leere Zeichenfolge.  
  
 **SQL_DESC_CASE_SENSITIVE [Implementierung Deskriptoren]**  
 Dieses Feld schreibgeschützt SQLINTEGER Datensatz enthält SQL_TRUE, Spalte oder des Parameters so behandelt, wie Groß-/Kleinschreibung für Sortierungen und Vergleiche oder SQL_FALSE oder wenn die Spalte ist nicht für Sortierungen und Vergleiche Groß-und Kleinschreibung wird jedoch eine nicht auf Zeichen basierende die Spalte.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält den Katalog für die Basistabelle, die die Spalte enthält. Der Rückgabewert ist Treiber abhängiges aus, wenn die Spalte ein Ausdruck ist, oder wenn die Spalte Teil einer Ansicht ist. Wenn die Datenquelle keine Kataloge unterstützt oder der Katalog kann nicht bestimmt werden, enthält diese Variable eine leere Zeichenfolge.  
  
 **SQL_DESC_CONCISE_TYPE [All]**  
 Diese SQLSMALLINT-Headerfeld gibt den präzisen Datentyp für alle Datentypen, einschließlich der Datentypen "DateTime" und das Intervall an.  
  
 Die Werte in den Feldern SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE sind voneinander abhängig sind. Jedes Mal eines der Felder wird festgelegt, die andere muss ebenfalls festgelegt werden. SQL_DESC_CONCISE_TYPE kann festgelegt werden, durch den Aufruf von **SQLBindCol** oder **SQLBindParameter**, oder **SQLSetDescField**. SQL_DESC_TYPE kann festgelegt werden, durch den Aufruf von **SQLSetDescField** oder **SQLSetDescRec**.  
  
 Wenn SQL_DESC_CONCISE_TYPE auf einen präzisen Datentyp als ein Intervall oder Datetime-Datentyp festgelegt ist, das SQL_DESC_TYPE-Feld auf den gleichen Wert festgelegt ist und das Feld SQL_DESC_DATETIME_INTERVAL_CODE auf 0 festgelegt ist.  
  
 Wenn SQL_DESC_CONCISE_TYPE in den präzisen Datentyp "DateTime" oder einen Zeitraum festgelegt ist, das SQL_DESC_TYPE-Feld mit dem entsprechenden verbose-Datentyp (SQL_DATETIME oder SQL_INTERVAL) festgelegt ist, und das SQL_DESC_DATETIME_INTERVAL_CODE-Feld auf dem entsprechenden Subcode festgelegt ist.  
  
 **SQL_DESC_DATA_PTR [Anwendungsdiensts und Descriptor, IPD]**  
 Diese SQLPOINTER Datensatzfeldaustausch verweist auf eine Variable, die den Parameterwert (für APDs) oder der Spaltenwert (für ARDs) enthalten soll. Dieses Feld ist eine *verzögerte Feld*. Sie dient nicht zum Zeitpunkt festgelegt ist, aber es wird zu einem späteren Zeitpunkt vom Treiber verwendet, um Daten abzurufen.  
  
 Die durch das SQL_DESC_DATA_PTR-Feld der ARD angegebene Spalte ist aufgehoben, wenn die *TargetValuePtr* Argument in einem Aufruf von **SQLBindCol** ein null-Zeiger ist oder wenn das SQL_DESC_DATA_PTR im Feld wird der ARD festlegen, indem ein Aufruf von **SQLSetDescField** oder **SQLSetDescRec** auf einen null-Zeiger. Andere Felder sind nicht betroffen, wenn das SQL_DESC_DATA_PTR-Feld auf einen null-Zeiger festgelegt ist.  
  
 Wenn der Aufruf von **SQLFetch** oder **SQLFetchScroll** füllt den Puffer, die auf dieses Feld zeigt keine SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgegeben hat, den Inhalt des Puffers nicht definiert sind.  
  
 Wenn das SQL_DESC_DATA_PTR-Feld eines APD, ARD oder IPD festgelegt ist, überprüft der Treiber an, dass der Wert in das SQL_DESC_TYPE-Feld eines der gültigen ODBC C-Datentypen oder treiberspezifische-Datentyp enthält und alle anderen Felder, die Auswirkungen auf die Datentypen konsistent sind. Fordert eine konsistenzprüfung ist die einzige Verwendung von das SQL_DESC_DATA_PTR-Feld eine IPD. Insbesondere, wenn eine Anwendung das SQL_DESC_DATA_PTR-Feld eine IPD und spätere Aufrufe festlegt **SQLGetDescField** auf dieses Feld nicht unbedingt zurückgegeben den Wert, der es festgelegt wurden. Weitere Informationen finden Sie unter "Konsistenzprüfungen" in [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [All]**  
 Diese SQLSMALLINT-Datensatzfeld enthält dem Subcode für den bestimmten Datentyp "DateTime" oder das Intervall aus, wenn das SQL_DESC_TYPE-Feld SQL_DATETIME oder SQL_INTERVAL hat. Dies gilt für SQL und C-Datentypen. Der Code besteht aus den Namen des Datentyps mit "CODE" ersetzt "TYPE" oder "C_TYPE" (für "DateTime"-Typen) oder "CODE" für "Intervall" oder "C_INTERVAL" (für die Intervalltypen) ersetzt.  
  
 Wenn SQL_DESC_TYPE und SQL_DESC_CONCISE_TYPE in eine Anwendungsdiensts SQL_C_DEFAULT festgelegt und der Deskriptor kein Anweisungshandle zugeordnet, ist der Inhalt des SQL_DESC_DATETIME_INTERVAL_CODE nicht definiert.  
  
 Dieses Feld kann für die Datetime-Datentypen, die in der folgenden Tabelle aufgeführten festgelegt werden.  
  
|DateTime-Typen|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP / SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Dieses Feld kann für die Interval-Datentypen, die in der folgenden Tabelle aufgeführten festgelegt werden.  
  
|Intervalltyp|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR / SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE / SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND / SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
QL_INTERVAL_HOUR_TO_MINUTE / SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE / SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND / SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
QL_INTERVAL_SECOND / SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Weitere Informationen zu den Datenintervalle und dieses Feld, finden Sie unter [-datentypbezeichnungen und Deskriptoren](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [All]**  
 Diese SQLINTEGER-Datensatzfeld enthält die Genauigkeit für anführenden Intervallwert, wenn das SQL_DESC_TYPE-Feld SQL_INTERVAL ist. Wenn das Feld SQL_DESC_DATETIME_INTERVAL_CODE auf ein Intervall-Datentyp festgelegt ist, wird dieses Feld auf die standardmäßige Genauigkeit für anführenden Intervallwert festgelegt.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 Dieses Feld schreibgeschützt SQLINTEGER Datensatz enthält die maximale Anzahl von Zeichen, die zum Anzeigen der Daten aus der Spalte erforderlich.  
  
 **SQL_DESC_FIXED_PREC_SCALE [Implementierung Deskriptoren]**  
 Dieses Feld schreibgeschützt SQLSMALLINT Datensatz wird auf SQL_TRUE, wenn die Spalte eine genaue numerische Spalte ist und weist einer festen Genauigkeit und festen Dezimalstellen ungleich NULL oder SQL_FALSE festgelegt, wenn die Spalte nicht um eine genaue numerische Spalte mit einer festen Genauigkeit und festen Dezimalstellen ist.  
  
 **SQL_DESC_INDICATOR_PTR [Anwendungsdiensts]**  
 In ARDs, diese SQLLEN * Feld verweist auf die Indikatorvariable aufzeichnen. Diese Variable enthält SQL_NULL_DATA, wenn der Spaltenwert NULL ist. Für APDs wird die Indikatorvariable auf SQL_NULL_DATA festgelegt, dynamische Argumente NULL angeben. Die Variable ist, andernfalls 0 (null), (es sei denn, die Werte in SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR derselbe Zeiger).  
  
 Wenn das SQL_DESC_INDICATOR_PTR-Feld in einer ARD ein null-Zeiger ist, wird verhindert, dass der Treiber Zurückgeben von Informationen, ob die Spalte NULL ist. Wenn die Spalte NULL ist und SQL_DESC_INDICATOR_PTR ist ein null-Zeiger, SQLSTATE 22002 (Indikatorvariable erforderlich, jedoch nicht bereitgestellt) wird zurückgegeben, wenn der Treiber zum Auffüllen des Puffers nach einem Aufruf von versucht **SQLFetch** oder  **SQLFetchScroll**. Wenn der Aufruf von **SQLFetch** oder **SQLFetchScroll** hat keine zurückgegeben SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, den Inhalt des Puffers nicht definiert werden.  
  
 Das Feld SQL_DESC_INDICATOR_PTR bestimmt, ob das Feld verweist SQL_DESC_OCTET_LENGTH_PTR festgelegt ist. Wenn der Datenwert für eine Spalte NULL ist, legt der Treiber die Indikatorvariable auf SQL_NULL_DATA fest. Das Feld verweist SQL_DESC_OCTET_LENGTH_PTR wird nicht festgelegt. Wenn ein NULL-Wert während der Abruf nicht gefunden wird, verweist SQL_DESC_INDICATOR_PTR Puffer auf 0 (null) festgelegt ist und der Puffer SQL_DESC_OCTET_LENGTH_PTR verweist auf die Länge der Daten festgelegt ist.  
  
 Wenn das SQL_DESC_INDICATOR_PTR-Feld in einem APD ein null-Zeiger ist, können die Anwendung diese anwendungsparameterdeskriptor-Datensatz NULL-Argumente angeben.  
  
 Dieses Feld ist eine *verzögerte Feld*: Er wird nicht verwendet, zu dem Zeitpunkt festgelegt ist, aber es wird zu einem späteren Zeitpunkt vom Treiber verwendet, um NULL-Zulässigkeit (für ARDs) anzugeben oder um NULL-Zulässigkeit (für APDs) zu bestimmen.  
  
 **SQL_DESC_LABEL [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält den Spaltenüberschrift oder-Titel. Wenn die Spalte nicht über eine Bezeichnung verfügt, enthält diese Variable den Namen der Spalte an. Wenn die Spalte nicht benannt ist und ohne Beschriftung ist, enthält diese Variable eine leere Zeichenfolge.  
  
 **SQL_DESC_LENGTH [All]**  
 Diese SQLULEN Datensatzfeld ist entweder die maximale oder die tatsächliche Länge einer Zeichenfolge in Zeichen oder einen binary-Datentyp in Bytes. Es ist die maximale Länge für einen Datentyp mit fester Länge oder die tatsächliche Länge für einen Datentyp mit variabler Länge. Der Wert schließt immer Null-Abschlusszeichen, die die Zeichenfolge endet. Für Werte, deren Typ SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP oder eine der SQL-Intervalldatentypen ist, ist dieses Feld die Länge in Zeichen von der Darstellung der Zeichenfolge Zeichen des Werts "DateTime" oder einen Zeitraum an.  
  
 Der Wert in dieses Feld möglicherweise ungleich dem Wert für "Length" als definiert, in ODBC 2.*.x*. Weitere Informationen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält, oder der Zeichen, die der Treiber als Präfix für ein Literal dieses Datentyps erkennt. Diese Variable enthält eine leere Zeichenfolge für einen Datentyp für den ein Zeichenfolgenliteral-Präfix nicht anwendbar ist.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält, oder der Zeichen, die der Treiber als Suffix für ein Literal dieses Datentyps erkennt. Diese Variable enthält eine leere Zeichenfolge für einen Datentyp für den ein literales Suffix nicht anwendbar ist.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [Implementierung Deskriptoren]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält lokalisierte (native Language)-Namen für den Datentyp, der sich vom Namen des Datentyps reguläre sein kann. Wenn kein lokalisierter Name vorhanden ist, wird eine leere Zeichenfolge zurückgegeben. Dieses Feld ist nur zu Anzeigezwecken.  
  
 **SQL_DESC_NAME [Implementierung Deskriptoren]**  
 Diese SQLCHAR * Datensatzfeld im ein Zeilendeskriptor, der enthält den Spaltenalias, wenn zutreffend. Wenn der Spaltenalias nicht anwendbar ist, wird der Spaltenname zurückgegeben. In beiden Fällen setzt der Treiber das SQL_DESC_UNNAMED-Feld auf SQL_NAMED an, wenn SQL_DESC_NAME-Felds festgelegt. Wenn Sie keinen Spaltennamen oder Spaltenalias vorhanden ist, wird der Treiber gibt eine leere Zeichenfolge in SQL_DESC_NAME-Felds zurück und legt die Feld SQL_DESC_UNNAMED SQL_UNNAMED fest.  
  
 Eine Anwendung kann der Parametername oder Alias, Parameter gespeicherter Prozeduren mit Namen anzugeben SQL_DESC_NAME-Felds einen IPD fest. (Weitere Informationen finden Sie unter [Bindungsparameter von Namen (Parameter genannt)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) SQL_DESC_NAME-Felds einen IRD ist ein Feld schreibgeschützt. SQLSTATE HY091 (Ungültiger Deskriptorfeldbezeichner) wird zurückgegeben, wenn eine Anwendung versucht, sie festzulegen.  
  
 In Descriptor, IPD ist dieses Feld nicht definiert, wenn der Treiber keine benannten Parameter unterstützt. Wenn der Treiber benannte Parameter unterstützt und ist in der Lage, Parameter zu beschreiben, wird der Name des Parameters in diesem Feld zurückgegeben.  
  
 **SQL_DESC_NULLABLE [Implementierung Deskriptoren]**  
 In IRDs ist dieses Feld schreibgeschützt SQLSMALLINT Datensatz SQL_NULLABLE aus, wenn die Spalte NULL-Werte SQL_NO_NULLS, wenn die Spalte keinen NULL-Werte oder SQL_NULLABLE_UNKNOWN aufweisen darf, wenn nicht bekannt ist, ob die Spalte NULL-Werte annimmt. Dieses Feld bezieht sich auf die Resultset-Spalte, nicht der Basisspalte.  
  
 In Descriptor, IPD ist dieses Feld immer auf SQL_NULLABLE festgelegt, da der dynamische Parameter sind immer NULL-Werte zulässt und nicht durch eine Anwendung festgelegt werden.  
  
 **SQL_DESC_NUM_PREC_RADIX [All]**  
 Dieses SQLINTEGER-Feld enthält den Wert 2 ist der Datentyp im Feld SQL_DESC_TYPE einen ungefähren numerischen Datentyp ab, weil das SQL_DESC_PRECISION-Feld die Anzahl der Bits enthält. Dieses Feld enthält einen Wert von 10 ist der Datentyp im Feld SQL_DESC_TYPE einen exakten numerischen Datentyp ab, weil das SQL_DESC_PRECISION-Feld die Anzahl von Dezimalstellen enthält. Dieses Feld ist für alle nicht-numerische Datentypen auf 0 festgelegt.  
  
 **SQL_DESC_OCTET_LENGTH [All]**  
 Diese SQLLEN Datensatzfeld enthält die Länge in Bytes einer Zeichenfolge oder den binary-Datentyp. Für Zeichen fester Länge oder binary-Typen ist dies die tatsächliche Länge in Bytes. Für variabler Länge Zeichen- oder Binärdatentypen ist dies die maximale Länge in Bytes. Dieser Wert immer schließt das Leerzeichen nach dem Zeichen Null-Terminierung für Deskriptoren für Implementierung und immer einschließlich Platz für das Null-Terminierung Zeichen für Anwendungsdiensts. Für Anwendungsdaten enthält dieses Feld die Größe des Puffers. Für APDs ist dieses Feld nur für die Ausgabe- oder Eingabe-/Ausgabeparameter definiert.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [Anwendungsdiensts]**  
 Diese SQLLEN * aufzeichnen Feld zeigt auf eine Variable, die die gesamte Länge in Byte eines dynamischen Arguments (für Parameter Deskriptoren) oder eines Werts gebundene Spalte (für Deskriptoren für Zeile) enthalten soll.  
  
 Dieser Wert ist für eine APD für alle Argumente außer Zeichen Zeichenfolgen- und Binärtypen ignoriert. Wenn dieses Feld auf SQL_NTS verweist, muss das dynamische Argument Null-terminiert sein. Führen Sie auf die Zeit, um anzugeben, dass ein gebundener Parameter ein Data-at-Execution-Parameter, eine Anwendung setzt dieses Feld in den entsprechenden Datensatz der APD auf eine Variable, die enthält den Wert SQL_DATA_AT_EXEC oder das Ergebnis des Makros SQL_LEN_DATA_AT_EXEC . Ist mehr als ein Feld, können SQL_DESC_DATA_PTR werden auf einen Wert festgelegt, die den Parameter eindeutig identifiziert die Anwendung zu bestimmen, welche Parameter angefordert werden können.  
  
 Wenn das OCTET_LENGTH_PTR-Feld des ein ARD ein null-Zeiger ist, gibt der Treiber keinen Längeninformationen für die Spalte zurück. Wenn Feld SQL_DESC_OCTET_LENGTH_PTR ein APD ein null-Zeiger ist, wird der Treiber davon ausgegangen, dass Zeichenfolgen und binäre Werte nullterminiertes sind. (Binärwerte darf nicht Null-terminiert sein. aber Unternehmensservern eine lang ist, um das Abschneiden zu vermeiden.)  
  
 Wenn der Aufruf von **SQLFetch** oder **SQLFetchScroll** füllt den Puffer, die auf dieses Feld zeigt keine SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgegeben hat, den Inhalt des Puffers nicht definiert sind. Dieses Feld ist eine *verzögerte Feld*. Sie dient nicht zum Zeitpunkt festgelegt ist, aber es wird zu einem späteren Zeitpunkt vom Treiber verwendet, um zu bestimmen, oder die Oktettlänge der Daten anzugeben.  
  
 **SQL_DESC_PARAMETER_TYPE [Descriptor, IPD]**  
 Diese SQLSMALLINT-Datensatzfeld ist für einen Eingabeparameter für ein Eingabe-/Ausgabeparameter, SQL_PARAM_OUTPUT für ein Output-Parameter SQL_PARAM_INPUT_OUTPUT_STREAM für eine gestreamte Eingabe/Ausgabe-Parameter oder SQL_ SQL_PARAM_INPUT_OUTPUT auf SQL_PARAM_INPUT festgelegt. PARAM_OUTPUT_STREAM für gestreamt Output-Parameter. Es ist standardmäßig auf SQL_PARAM_INPUT festgelegt.  
  
 Für eine IPD ist das Feld SQL_PARAM_INPUT standardmäßig auf festgelegt, wenn die IPD (SQL_ATTR_ENABLE_AUTO_IPD-Anweisungsattribut wird SQL_FALSE) nicht automatisch vom Treiber aufgefüllt wird. Eine Anwendung sollte dieses Feld in den IPD für Parameter festgelegt, die keine Eingabeparameter sind.  
  
 **SQL_DESC_PRECISION [All]**  
 Diese SQLSMALLINT-Datensatzfeld enthält die Anzahl von Ziffern für einen exakten numerischen Typ, die Anzahl der Bits in der Mantisse (Genauigkeit) für einen ungefähren numerischen Typ oder die Anzahl der Ziffern in der Komponente für Sekundenbruchteile für die SQL_TYPE_TIME SQL_TYPE _TIMESTAMP oder SQL_INTERVAL_SECOND-Datentyp. Dieses Feld ist nicht für alle anderen Datentypen definiert.  
  
 Der Wert in dieses Feld möglicherweise ungleich dem Wert für "Precision" als definiert, in ODBC 2.*.x*. Weitere Informationen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [Implementierung Deskriptoren]**  
 Dieses Feld SQLSMALLINTrecord gibt an, ob eine Spalte vom DBMS automatisch, beim Aktualisieren von Zeilen (z. B. eine Spalte des Datentyps "Timestamp" in SQL Server geändert wird). Der Wert dieses Felds Datensatz festgelegt ist, SQL_TRUE, wenn die Spalte eine Spalte mit zeilenversionsverwaltung und SQL_FALSE andernfalls. Dieses Spaltenattribut gleicht dem Aufruf **SQLSpecialColumns** mit der SQL_ROWVER IdentifierType, um zu bestimmen, ob eine Spalte automatisch aktualisiert wird.  
  
 **SQL_DESC_SCALE [All]**  
 Diese SQLSMALLINT-Datensatzfeld enthält definierte Anzahl von Dezimalstellen für die Datentypen decimal und numeric. Das Feld ist nicht für alle anderen Datentypen definiert.  
  
 Der Wert in dieses Feld möglicherweise ungleich dem Wert für "Scale" gemäß Definition in ODBC 2.*.x*. Weitere Informationen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält den Schemanamen der Basistabelle, die die Spalte enthält. Der Rückgabewert ist Treiber abhängiges aus, wenn die Spalte ein Ausdruck ist, oder wenn die Spalte Teil einer Ansicht ist. Wenn die Datenquelle keine Schemas unterstützt oder der Schemaname kann nicht bestimmt werden kann, enthält diese Variable eine leere Zeichenfolge.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 Dieses Feld schreibgeschützt SQLSMALLINT Datensatz wird auf einen der folgenden Werte festgelegt:  
  
-   SQL_PRED_NONE, wenn die Spalte kann, in verwendet werden einem **, in denen** Klausel. (Dies ist identisch mit der SQL_UNSEARCHABLE-Wert in ODBC 2.*.x*.)  
  
-   SQL_PRED_CHAR, ob die Spalte kann, in verwendet werden eine **, in denen** -Klausel jedoch nur mit der **wie** Prädikat. (Dies ist identisch mit der SQL_LIKE_ONLY-Wert in ODBC 2.*.x*.)  
  
-   SQL_PRED_BASIC, ob die Spalte kann, in verwendet werden einem **, in dem** -Klausel mit allen Vergleichsoperatoren mit Ausnahme **wie**. (Dies ist identisch mit der SQL_EXCEPT_LIKE-Wert in ODBC 2.*.x*.)  
  
-   SQL_PRED_SEARCHABLE, ob die Spalte kann, in verwendet werden einem **, in dem** -Klausel mit jedem Vergleichsoperator.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält den Namen der Basistabelle, die diese Spalte enthält. Der Rückgabewert ist Treiber abhängiges aus, wenn die Spalte ein Ausdruck ist, oder wenn die Spalte Teil einer Ansicht ist.  
  
 **SQL_DESC_TYPE [All]**  
 Diese SQLSMALLINT-Datensatzfeld gibt präzise SQL- oder C-Datentyp für alle Datentypen mit Ausnahme der Datentypen "DateTime" und das Intervall an. Dieses Feld für die Datentypen "DateTime" und das Intervall gibt an, dass die ausführliche Datentyp, der SQL_DATETIME oder SQL_INTERVAL hat.  
  
 Wenn dieses Feld SQL_DATETIME oder SQL_INTERVAL enthält, muss das SQL_DESC_DATETIME_INTERVAL_CODE-Feld dem entsprechenden Subcode für den präzise Typ enthalten. Für Datetime-Datentyp SQL_DESC_TYPE enthält SQL_DATETIME und das SQL_DESC_DATETIME_INTERVAL_CODE-Feld enthält eine Subcode für den bestimmten Datetime-Datentyp. Für die Interval-Datentypen SQL_DESC_TYPE enthält SQL_INTERVAL und das Feld SQL_DESC_DATETIME_INTERVAL_CODE ein Subcode für den bestimmten Intervall-Datentyp.  
  
 Die Werte in den Feldern SQL_DESC_TYPE und SQL_DESC_CONCISE_TYPE sind voneinander abhängig sind. Jedes Mal eines der Felder wird festgelegt, die andere muss ebenfalls festgelegt werden. SQL_DESC_TYPE kann festgelegt werden, durch den Aufruf von **SQLSetDescField** oder **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE kann festgelegt werden, durch den Aufruf von **SQLBindCol** oder **SQLBindParameter**, oder **SQLSetDescField**.  
  
 Wenn SQL_DESC_TYPE auf einen präzisen Datentyp als ein Intervall oder Datetime-Datentyp festgelegt ist, Feld SQL_DESC_CONCISE_TYPE auf den gleichen Wert festgelegt ist, und das Feld SQL_DESC_DATETIME_INTERVAL_CODE auf 0 festgelegt ist.  
  
 Wenn SQL_DESC_TYPE auf den ausführlichen "DateTime" oder die Intervall-Datentyp (SQL_DATETIME oder SQL_INTERVAL) festgelegt ist, und das SQL_DESC_DATETIME_INTERVAL_CODE-Feld auf dem entsprechenden Subcode festgelegt ist, wird mit dem entsprechenden präzisen Datentyp SQL_DESC_CONCISE TYPE-Felds festgelegt. SQL_DESC_TYPE eine präzise "DateTime" oder Intervall Typen vornehmen möchten SQLSTATE HY021 zurück (inkonsistente Deskriptorinformationen).  
  
 Wenn das SQL_DESC_TYPE-Feld festgelegt ist, durch den Aufruf von **SQLBindCol**, **SQLBindParameter**, oder **SQLSetDescField**, die folgenden Felder werden auf die folgenden Standardwerte festgelegt. wie in der folgenden Tabelle dargestellt. Die Werte für die verbleibenden Felder eines Datensatzes sind nicht definiert.  
  
|Wert des SQL_DESC_TYPE|Andere Felder festgelegt implizit.|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH wird auf 1 festgelegt. SQL_DESC_PRECISION wird auf 0 festgelegt.|  
|SQL_DATETIME|Wenn SQL_CODE_DATE oder SQL_CODE_TIME SQL_DESC_DATETIME_INTERVAL_CODE festgelegt ist, wird die SQL_DESC_PRECISION auf 0 festgelegt. Wenn es auf SQL_DESC_TIMESTAMP festgelegt ist, wird die SQL_DESC_PRECISION auf 6 festgelegt.|  
|SQL_DECIMAL SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE wird auf 0 festgelegt. SQL_DESC_PRECISION wird auf die Implementierung definierten Genauigkeit für den jeweiligen Datentyp festgelegt.<br /><br /> Finden Sie unter [SQL "c:" numerischen](../../../odbc/reference/appendixes/sql-to-c-numeric.md) für Informationen dazu, wie Sie manuell einen Wert SQL_C_NUMERIC binden.|  
|SQL_FLOAT SQL_C_FLOAT|SQL_DESC_PRECISION wird auf die standardmäßige Implementierung definierten Genauigkeit für SQL_FLOAT festgelegt.|  
|SQL_INTERVAL|Wenn SQL_DESC_DATETIME_INTERVAL_CODE auf ein Intervall-Datentyp festgelegt ist, wird SQL_DESC_DATETIME_INTERVAL_PRECISION auf 2 (die Intervall führende standardgenauigkeit) festgelegt. Wenn das Intervall eine Komponente für Sekunden aufweist, wird die SQL_DESC_PRECISION auf 6 (die Standard-Intervall Sekunden Genauigkeit) festgelegt.|  
  
 Wenn eine Anwendung ruft **SQLSetDescField** festzulegende Felder einen Deskriptor anstelle von Aufrufen **SQLSetDescRec**, die Anwendung muss zuerst den Datentyp deklarieren. Wenn dies der Fall ist, werden die anderen Felder, die in der vorherigen Tabelle aufgeführten implizit festgelegt. Wenn die Werte implizit festgelegt sind unzulässig, die Anwendung kann dann aufrufen **SQLSetDescField** oder **SQLSetDescRec** den unzulässigen Wert explizit festgelegt.  
  
 **SQL_DESC_TYPE_NAME [Implementierung Deskriptoren]**  
 Diese schreibgeschützte SQLCHAR * Datensatzfeld enthält den Namen des Quelle vom Änderungsmanagement angeforderten Typ (z. B. "CHAR", "VARCHAR", usw.). Wenn Sie den Namen des Datentyps unbekannt ist, enthält diese Variable eine leere Zeichenfolge.  
  
 **SQL_DESC_UNNAMED [Implementierung Deskriptoren]**  
 Diese SQLSMALLINT-Datensatzfeld in einem Zeilendeskriptor wird vom Treiber SQL_NAMED oder SQL_UNNAMED festgelegt, wenn SQL_DESC_NAME-Felds festgelegt. Wenn SQL_DESC_NAME-Felds einen Spaltenalias enthält, oder wenn der Spaltenalias nicht anwendbar ist, legt der Treiber die SQL_DESC_UNNAMED Feld SQL_NAMED fest. Wenn eine Anwendung, der Parametername oder Alias SQL_DESC_NAME-Felds einen IPD festlegt, legt der Treiber das SQL_DESC_UNNAMED-Feld, der die IPD auf SQL_NAMED fest. Wenn Sie keinen Spaltennamen oder Spaltenalias vorhanden ist, legt der Treiber die Feld SQL_DESC_UNNAMED SQL_UNNAMED fest.  
  
 Eine Anwendung kann das SQL_DESC_UNNAMED Feld von einem IPD auf SQL_UNNAMED festgelegt. Gibt ein Treiber SQLSTATE HY091 (Ungültiger Deskriptorfeldbezeichner), wenn eine Anwendung versucht, SQL_NAMED Feld SQL_DESC_UNNAMED ein IPD fest. Feld SQL_DESC_UNNAMED ein IRD ist schreibgeschützt. SQLSTATE HY091 (Ungültiger Deskriptorfeldbezeichner) wird zurückgegeben, wenn eine Anwendung versucht, sie festzulegen.  
  
 **SQL_DESC_UNSIGNED [Implementierung Deskriptoren]**  
 Dieses Feld schreibgeschützt SQLSMALLINT-Eintrag ist auf SQL_TRUE, wenn der Spaltentyp nicht signierte oder nicht numerisch ist oder SQL_FALSE festgelegt, wenn der Spaltentyp signiert ist.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 Dieses Feld schreibgeschützt SQLSMALLINT Datensatz wird auf einen der folgenden Werte festgelegt:  
  
-   SQL_ATTR_READ_ONLY, wenn das Resultset-Spalte ist schreibgeschützt.  
  
-   SQL_ATTR_WRITE, wenn die Resultsetspalte ist Lese-/ Schreibzugriff.  
  
-   SQL_ATTR_READWRITE_UNKNOWN, wenn nicht bekannt ist, ob das Resultset-Spalte kann aktualisiert werden oder nicht.  
  
 SQL_DESC_UPDATABLE beschreibt die aktualisierbarkeit der Spalte im Resultset, nicht die Spalte in der Basistabelle. Möglicherweise anders als der Wert in diesem Feld die aktualisierbarkeit der Spalte in der Basistabelle, die auf dem dieses Resultset-Spalte basiert. Ob eine Spalte aktualisiert werden kann, kann auf den Datentyp, Benutzerberechtigungen und die Definition des Resultsets selbst basieren. Wenn unklar ist, ob eine Spalte aktualisiert werden kann, sollte SQL_ATTR_READWRITE_UNKNOWN zurückgegeben werden.  
  
## <a name="consistency-checks"></a>Konsistenzprüfungen  
 Eine konsistenzprüfung wird automatisch vom Treiber ausgeführt, wenn eine Anwendung in einen Wert für das SQL_DESC_DATA_PTR-Feld des ARD, APD oder IPD übergibt. Wenn eines der Felder stimmt nicht mit anderen Feldern **SQLSetDescField** SQLSTATE HY021 zurück (inkonsistente Deskriptorinformationen). Weitere Informationen finden Sie unter "Konsistenzprüfung" in [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einer Spalteninhalts|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Ein Parameter gebunden|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Abrufen von einem Beschreibungsfeld|[SQLGetDescField-Funktion](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Abrufen von mehreren deskriptorfelder|[SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Mehrere deskriptorfelder festlegen|[SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)
