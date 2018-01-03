---
title: SQLGetStmtAttr-Funktion | Microsoft Docs
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
apiname: SQLGetStmtAttr
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetStmtAttr
helpviewer_keywords: SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10ef63cf77fc4668d9f9f80daaff8ab483d1876b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetStmtAttr** gibt die aktuelle Einstellung der ein Anweisungsattribut zurück.  
  
> [!NOTE]  
>  Weitere Informationen zu welcher der Treiber-Manager ordnet diese Funktion auf, wenn eine ODBC 3. *x* Anwendung arbeitet mit einer ODBC 2. *X* -Treiber verwenden, finden Sie unter [Ersatz-Zuordnungsfunktionen für Backward Compatibility Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Attribut*  
 [Eingabe] Abzurufenden Attributs.  
  
 *ValuePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem den Wert des Attributs im angegebenen zurückgegeben *Attribut*.  
  
 Wenn *ValuePtr* NULL ist, *StringLengthPtr* weiterhin die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) zurück in den Puffer verweist zurückzugebendenverfügbar *ValuePtr*.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *Attribut* ist ein ODBC-definierten Attribut und *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des \* *ValuePtr*. Wenn *Attribut* ist ein ODBC-definierten Attribut und \* *ValuePtr* ist eine ganze Zahl *Pufferlänge* wird ignoriert. Wenn der Rückgabewert in  *\*ValuePtr* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLGetStmtAttrW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 Wenn *Attribut* ist ein Attribut treiberdefinierten die Anwendung zeigt die Art des Attributs an den Treiber-Manager an, indem die *Pufferlänge* Argument. *Pufferlänge* können die folgenden Werte aufweisen:  
  
-   Wenn  *\*ValuePtr* ist ein Zeiger auf eine Zeichenfolge *Pufferlänge* ist die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn  *\*ValuePtr* ist ein Zeiger auf einen binären Puffer, und klicken Sie dann die Anwendung das Ergebnis von der SQL_LEN_BINARY_ATTR eingefügt (*Länge*)-Makro im *Pufferlänge*. Dies setzt einen negativen Wert in *Pufferlänge*.  
  
-   Wenn  *\*ValuePtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder Binärzeichenfolge, *Pufferlänge* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn  *\*ValuePtr* ist einen Datentyp fester Länge, dann enthält *Pufferlänge* ist SQL_IS_INTEGER oder SQL_IS_UINTEGER, nach Bedarf.  
  
 *StringLengthPtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden  *\*ValuePtr*. Wenn *ValuePtr* ist ein null-Zeiger, keine Länge zurückgegeben. Wenn der Wert des Attributs ist eine Zeichenfolge, und die Anzahl der Bytes, die für die Rückgabe verfügbar ist, größer als oder gleich *Pufferlänge*, die Daten in  *\*ValuePtr* auf abgeschnitten*Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen und wird vom Treiber Null-terminiert.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetStmtAttr** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einer *HandleType* von SQL Server _HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetStmtAttr** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Die Daten in  *\*ValuePtr* wurde abgeschnitten, um werden *Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen. Die Länge des Wertes ungekürzten Zeichenfolge wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|24000|Ungültiger Cursorstatus|Das Argument *Attribut* SQL_ATTR_ROW_NUMBER wurde und der Cursor konnte nicht geöffnet werden, oder der Cursor vor dem Start des Resultsets oder nach dem Ende des Resultsets positioniert wurde.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** im Argument *MessageText* beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLGetStmtAttr** Funktion aufgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|*(DM) \*ValuePtr* ist eine Zeichenfolge, und Pufferlänge war kleiner als 0 (null), aber nicht SQL_NTS gleich.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|Der Wert für das Argument angegebene *Attribut* war für die vom Treiber unterstützten ODBC-Version ungültig.|  
|HY109|Ungültige Cursorposition|Die *Attribut* Argument war SQL_ATTR_ROW_NUMBER und die Zeile wurde gelöscht oder konnte nicht abgerufen werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Wert für das Argument angegebene *Attribut* wurde eine gültige ODBC-Anweisungsattribut für ODBC-Version vom Treiber unterstützt, jedoch wurde vom Treiber nicht unterstützt.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber entspricht der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Allgemeine Informationen zu Anweisungsattribute, finden Sie unter [Anweisungsattribute](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Ein Aufruf von **SQLGetStmtAttr** gibt in  *\*ValuePtr* den Wert des Attributs im angegebenen Anweisung *Attribut*. Dieser Wert kann es sich entweder um einen SQLULEN-Wert oder ein Null-terminierte Zeichenfolge sein. Ist der Wert einen Wert SQLULEN erstellt wurde, schreibt einige Treiber möglicherweise nur die untere 32-Bit- oder 16-Bit, der einen Puffer und lassen Sie das Bit höherer Ordnung unverändert. Aus diesem Grund sollten Anwendungen verwendet einen Puffer SQLULEN erstellt wurde, und initialisieren den Wert auf 0 vor dem Aufrufen dieser Funktion. Darüber hinaus die *Pufferlänge* und *StringLengthPtr* Argumente werden nicht verwendet. Wenn der Wert eine Null-terminierte Zeichenfolge ist, gibt die Anwendung die maximale Länge der Zeichenfolge in der *Pufferlänge* Argument und der Treiber gibt die Länge der Zeichenfolge in der  *\* StringLengthPtr* Puffer.  
  
 Damit Anwendungen Aufrufen **SQLGetStmtAttr** zum Arbeiten mit ODBC 2. *X* -Treiber, die einen Aufruf von **SQLGetStmtAttr** zugeordnet ist, in der Treiber-Manager **SQLGetStmtOption**.  
  
 Die folgenden Anweisungsattribute sind schreibgeschützt, damit Sie abgerufen werden kann **SQLGetStmtAttr**, jedoch nicht festlegen, indem **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Eine Liste der Attribute, die festgelegt und abgerufen werden können, finden Sie unter [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
