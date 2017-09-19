---
title: SQLBindCol-Funktion | Microsoft Docs
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
- SQLBindCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 641b08ab3d3aec59f66dd0405770cf19d4690769
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindcol-function"></a>SQLBindCol-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLBindCol** Anwendung Datenpuffer an Spalten im Resultset gebunden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *ColumnNumber*  
 [Eingabe] Anzahl der das Ergebnis legen Spalte binden. Spalten werden in der zunehmenden Spaltenreihenfolge, beginnend mit 0, wobei die Lesezeichenspalte ist Spalte 0 nummeriert. Wenn das Lesezeichen nicht verwendet werden – d. h. das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_OFF festgelegt ist – Klicken Sie dann die spaltenzählung beginnt bei 1.  
  
 *TargetType*  
 [Eingabe] Der Bezeichner der C-Datentyp, der die \* *TargetValuePtr* Puffer. Wenn sie Daten aus der Datenquelle mit abruft **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, oder **SQLSetPos**, Treiber konvertiert die Daten in diesen Typ; Wenn Daten sendet, an die Datenquelle mit **SQLBulkOperations** oder **SQLSetPos**, konvertiert der Treiber die Daten von diesem Typ. Eine Liste der gültigen C-Datentypen und Typ-IDs, finden Sie unter der [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) Abschnitt im Anhang D:-Datentypen.  
  
 Wenn die *TargetType* Argument ist ein Intervall-Datentyp, der Intervall führende standardgenauigkeit (2) und die standardmäßige Intervall Sekunden Genauigkeit (6), wie in den Feldern SQL_DESC_DATETIME_INTERVAL_PRECISION und SQL_DESC_PRECISION des festgelegt die ARD, sind für die Daten verwendet. Wenn die *TargetType* Argument SQL_C_NUMERIC, die standardgenauigkeit (treiberdefinierten) wird und standardmäßig über Dezimalstellen (0), wie in die Felder SQL_DESC_PRECISION und SQL_DESC_SCALE der ARD festgelegt, für die Daten verwendet werden. Wenn alle Standardwerte für die Genauigkeit oder Dezimalstellen nicht geeignet ist, die Anwendung sollten explizit festlegen der entsprechenden Deskriptorfeld durch einen Aufruf von **SQLSetDescField** oder **SQLSetDescRec**.  
  
 Sie können auch einen erweiterte C-Datentyp angeben. Weitere Informationen finden Sie unter [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Verzögerte Eingabe/Ausgabe] Zeiger auf den Datenpuffer zum Binden an die Spalte. **SQLFetch** und **SQLFetchScroll** Daten in diesen Puffer zurück. **SQLBulkOperations** gibt Daten zurück, in diesem Puffer beim *Vorgang* SQL_FETCH_BY_BOOKMARK; wird abgerufen, Daten aus dieser gepuffert, wenn *Vorgang* ist SQL_ADD oder SQL_UPDATE_BY_BOOKMARK . **SQLSetPos** gibt Daten zurück, in diesem Puffer beim *Vorgang* SQL_REFRESH; ist er ruft Daten ab, aus dieser beim Puffern *Vorgang* SQL_UPDATE ist.  
  
 Wenn *TargetValuePtr* ist ein null-Zeiger der Treiber hebt die Bindung auf den Datenpuffer für die Spalte. Eine Anwendung kann alle Spalten durch den Aufruf Bindung **SQLFreeStmt** mit der Option SQL_UNBIND. Eine Anwendung heben Sie die Bindung des Datenpuffers für eine Spalte kann jedoch weiterhin eine für die Spalte gebundenen Längen-/Indikatorpuffers auftreten, wenn die *TargetValuePtr* Argument im Aufruf **SQLBindCol** ist ein null-Zeiger jedoch *StrLen_or_IndPtr* Argument ist ein gültiger Wert.  
  
 *Pufferlänge*  
 [Eingabe] Länge der **TargetValuePtr* Puffers in Bytes.  
  
 Verwendet der Treiber *Pufferlänge* zur Vermeidung von Schreiben nach dem Ende der \* *TargetValuePtr* Puffern Bindungsprozesses Daten variabler Länge, z. B. Zeichen- oder Binärdaten darstellen. Beachten Sie, dass der Treiber die Null-Abschlusszeichen zählt Bindungsprozesses Zeichendaten in \* *TargetValuePtr*. **TargetValuePtr* muss daher keine Leerzeichen für die Null-Abschlusszeichen oder der Treiber die Daten abgeschnitten wird.  
  
 Der Treiber Daten fester Länge, z. B. eine ganze Zahl oder eine Datumsstruktur Rückkehr ignoriert der Treiber *Pufferlänge* und davon aus, dass der Puffer groß genug ist, um die Daten aufzunehmen. Daher es ist wichtig für die Anwendung auf einen ausreichend großen Puffer für Daten fester Länge zuzuordnen, oder der Treiber wird hinter das Ende des Puffers geschrieben.  
  
 **SQLBindCol** SQLSTATE HY090 zurückgegeben (ungültige Zeichenfolgen- oder Pufferlänge.) Wenn *Pufferlänge* ist kleiner als 0, jedoch nicht, wenn *Pufferlänge* ist 0. Jedoch wenn *TargetType* gibt einen Zeichentyp handelt, eine Anwendung sollte nicht festgelegt. *Pufferlänge* auf 0, da CLI ISO-kompatible Treiber SQLSTATE HY090 zurückgeben (ungültige Zeichenfolgen- oder Pufferlänge), Fall.  
  
 *StrLen_or_IndPtr*  
 [Verzögerte Eingabe/Ausgabe] Ein Zeiger auf die Längen-/Indikatorpuffers auf die Spalte gebunden. **SQLFetch** und **SQLFetchScroll** Rückgabewert in diesem Puffer. **SQLBulkOperations** Ruft einen Wert aus diesem Puffer beim *Vorgang* SQL_ADD, SQL_UPDATE_BY_BOOKMARK oder SQL_DELETE_BY_BOOKMARK ist. **SQLBulkOperations** gibt einen Wert in diesem Puffer beim *Vorgang* SQL_FETCH_BY_BOOKMARK ist. **SQLSetPos** gibt einen Wert in diesem Puffer beim *Vorgang* ist SQL_REFRESH; er ruft einen Wert ab, aus dieser Puffer beim *Vorgang* SQL_UPDATE ist.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, und **SQLSetPos** können die folgenden Werte in die Längen-/Indikatorpuffers zurück:  
  
-   Die Länge der zurückzugebenden verfügbaren Daten  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Die Anwendung kann die folgenden Werte in Längen-/Indikatorpuffers für die Verwendung mit nehmen **SQLBulkOperations** oder **SQLSetPos**:  
  
-   Die Länge der gesendeten Daten  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   Das Ergebnis der SQL_LEN_DATA_AT_EXEC-Makro  
  
-   SQL_COLUMN_IGNORE  
  
 Wenn der Indikatorpuffer und der Länge Puffer separate Puffer sind, kann die Indikatorpuffers nur SQL_NULL_DATA zurück, während der Länge Puffer alle anderen Werte zurückgeben kann.  
  
 Weitere Informationen finden Sie unter [SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md), [SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md), und [mit Längenindikator/Werten](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Wenn *StrLen_or_IndPtr* ist ein null-Zeiger, keine Länge bzw. der Indikatorwert-Wert verwendet wird. Dies ist ein Fehler beim Abrufen von Daten und die Daten NULL ist.  
  
 Finden Sie unter [ODBC-64-Bit-Informationen](../../../odbc/reference/odbc-64-bit-information.md), wenn die Anwendung auf einem 64-Bit-Betriebssystem ausgeführt wird.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLBindCol** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLBindCol** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07006|Eingeschränkte Datentypattribut|(DM) die *ColumnNumber* -Argument lautete 0 (null) und die *TargetType* Argument war kein SQL_C_BOOKMARK oder SQL_C_VARBOOKMARK.|  
|07009|Ungültiger Deskriptorindex|Der Wert für das Argument angegebene *ColumnNumber* die maximale Anzahl von Spalten im Resultset überschritten.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY003|Ungültiger Anwendungspuffertyp|Das Argument *TargetType* wurde weder SQL_C_DEFAULT als auch einen gültigen Datentyp.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn **SQLBindCol** aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert für das Argument angegebene *Pufferlänge* war kleiner als 0.<br /><br /> (DM) der Treiber wurde eine ODBC-2. *x* -Treiber die *ColumnNumber* Argument wurde auf 0 festgelegt, sowie den Wert für das Argument angegebene *Pufferlänge* war nicht gleich 4.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber oder die Datenquelle unterstützt nicht die Konvertierung angegeben, durch die Kombination der *TargetType* Argument und der Treiber-spezifische SQL-Datentyp der entsprechenden Spalte.<br /><br /> Das Argument *ColumnNumber* 0 wurde und der Treiber unterstützt keine Lesezeichen.<br /><br /> Der Treiber unterstützt nur ODBC 2. *x* und dem Argument *TargetType* war es eines der folgenden:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> und das Intervall C-Datentypen in [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) in Anhang D:-Datentypen.<br /><br /> Der Treiber unterstützt nur die ODBC-Versionen vor 3.50 und dem Argument *TargetType* SQL_C_GUID wurde.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 **SQLBindCol** wird verwendet, um zuzuordnen, oder *zu binden,* Spalten im Resultset auf Daten Buffers "und" Längenindikator/Puffer in der Anwendung festgelegt. Wenn die Anwendung aufruft, **SQLFetch**, **SQLFetchScroll**, oder **SQLSetPos** um Daten abzurufen, gibt der Treiber die Daten für die gebundenen Spalten in den angegebenen Puffern; Weitere Informationen finden Sie unter [SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md). Wenn die Anwendung aufruft, **SQLBulkOperations** zum Aktualisieren oder Einfügen einer Zeile oder **SQLSetPos** um eine Zeile zu aktualisieren, ruft der Treiber die Daten für die gebundenen Spalten aus der angegebenen Puffer; Weitere Informationen , finden Sie unter [SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md) oder [SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md). Weitere Informationen zur Bindung finden Sie unter [Abrufen von Ergebnissen (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Beachten Sie, dass Spalten nicht gebunden werden, um Daten daraus abzurufen. Eine Anwendung kann auch aufrufen **SQLGetData** zum Abrufen von Daten aus Spalten. Obwohl es möglich ist, binden Sie einige Spalten in einer Zeile und der Aufruf **SQLGetData** für andere dies einige Einschränkungen unterliegt. Weitere Informationen finden Sie unter [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Bindung aufheben der Bindung und erneutes Binden von Spalten  
 Eine Spalte kann gebunden, aufgehoben oder jederzeit, auch nachdem die Daten aus dem Resultset abgerufen wurde neu. Die neue Bindung wird wirksam, das nächste Mal, das eine Funktion, die Bindungen verwendet aufgerufen wird. Nehmen wir beispielsweise an eine Anwendung bindet die Spalten in einem Resultset und Aufrufe **SQLFetch**. Der Treiber zurückgegeben die Daten in den Puffern mit gebundenen. Nehmen Sie die Anwendung bindet die Spalten auf einen anderen Satz von Puffern. Der Treiber ist nicht die Daten für den gerade abgerufenen Zeile in die neu gebundenen Puffer abgelegt. Stattdessen erst **SQLFetch** erneut aufgerufen wird, und klicken Sie dann die Daten für die nächste Zeile platziert, in dem neu gebundenen Puffer.  
  
> [!NOTE]  
>  Das Anweisungsattribut SQL_ATTR_USE_BOOKMARKS sollte immer vor dem Binden einer Spalte auf 0 festgelegt werden. Dies ist nicht erforderlich, jedoch wird dringend empfohlen.  
  
## <a name="binding-columns"></a>Binden von Spalten  
 Um eine Spalte binden, ruft die Anwendung **SQLBindCol** und übergibt die Spaltennummer, Typ, Adresse und die Länge eines Datenpuffers mit und die Adresse des ein Längen-/Indikatorpuffers. Informationen, wie diese Adressen verwendet werden finden Sie unter "Puffer Adressen" weiter unten in diesem Abschnitt. Weitere Informationen zum Binden von Spalten finden Sie unter [SQLBindCol verwenden](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Die Verwendung dieser Puffer ist verzögert; d. h. die Anwendung bindet in **SQLBindCol** , aber der Treiber greift auf sie von anderen Funktionen – nämlich **SQLBulkOperations**, **SQLFetch**, ** SQLFetchScroll**, oder **SQLSetPos**. Es ist die Anwendung dafür verantwortlich, um sicherzustellen, dass der Zeiger im angegebenen **SQLBindCol** bleibt gültig, solange die Bindung wirksam ist. Wenn die Anwendung diese Zeiger ungültig werden kann – z. B. einen Puffer freigegeben, und klicken Sie dann eine Funktion, die sie ungültig werden erwartet, die Folgen sind nicht definiert. Weitere Informationen finden Sie unter [Puffer verzögert](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 Die Bindung bleibt wirksam, bis sie durch eine neue Bindung ersetzt wird, die Spalte entfernt wird oder die Anweisung wird freigegeben.  
  
## <a name="unbinding-columns"></a>Aufheben der Bindung von Spalten  
 Zum Aufheben der Bindung einer einzelnen Spalteninhalts, eine Anwendung ruft **SQLBindCol** mit *ColumnNumber* legen die Anzahl der betroffenen Spalte und *TargetValuePtr* auf ein null-Zeiger festgelegt. Wenn *ColumnNumber* bezieht sich auf einer ungebundenen Spalte **SQLBindCol** weiterhin gibt SQL_SUCCESS zurück.  
  
 Um alle Spalten aufheben, eine Anwendung ruft **SQLFreeStmt** mit *fOption* auf SQL_UNBIND festgelegt ist. Dies kann auch durch Festlegen von Feld SQL_DESC_COUNT der ARD 0 (null) erfolgen.  
  
## <a name="rebinding-columns"></a>Erneutes Binden von Spalten  
 Eine Anwendung kann eine der beiden Vorgänge so ändern Sie eine Bindung durchführen:  
  
-   Rufen Sie **SQLBindCol** an eine neue Bindung für eine Spalte, die bereits gebunden ist. Der Treiber wird die alte Bindung mit den neuen Wert überschrieben.  
  
-   Geben Sie einen Offset Pufferadresse hinzugefügt werden, die von der Bindung Aufruf angegeben wurde **SQLBindCol**. Weitere Informationen finden Sie im nächsten Abschnitt, "Bindung Offsets".  
  
## <a name="binding-offsets"></a>Binden von Offsets  
 Ein Bindung-Offset ist ein Wert, der die Adressen der Daten und Längenindikator /-Puffer hinzugefügt wird (gemäß der *TargetValuePtr* und *StrLen_or_IndPtr* Argument), bevor sie dereferenziert werden. Wenn Offsets verwendet werden, die Bindungen sind "Template" des wie die Anwendung Puffer angelegt werden, und die Anwendung kann auf unterschiedliche Bereiche des Arbeitsspeichers dieser "Vorlage" verschieben, durch Ändern des Offsets. Da der gleiche Offset an jede Adresse in jeder Bindung hinzugefügt wird, müssen die relative Offsets zwischen Puffern für verschiedene Spalten mit dem innerhalb jedes Satzes von Puffer übereinstimmen. Dies ist immer "true", wenn die zeilenweise Bindung verwendet wird; die Anwendung muss sorgfältig das Layout der Puffer für diesen auf "true" sein, wenn spaltenbezogene Bindung verwendet wird.  
  
 Mit einem Offset von Bindung ist im Grunde dieselbe Wirkung wie das erneute Binden einer Spalte durch den Aufruf **SQLBindCol**. Der Unterschied besteht darin, eine neue Aufruf **SQLBindCol** neue Adressen für den Datenpuffer und Längen-/Indikatorpuffers gibt an, während die Verwendung einer Bindung Offset ändert sich nicht auf die Adressen, aber nur auf diese addiert einen Offset. Die Anwendung kann einen neuen Offset angeben, wenn er möchte und dieser Offset wird immer an die ursprünglich gebundenen Adressen hinzugefügt. Insbesondere verwendet der Treiber, wenn der Offset auf 0 festgelegt ist, oder wenn das-Anweisungsattribut auf einen null-Zeiger festgelegt ist, die ursprünglich gebundenen Adressen.  
  
 Zum Angeben eines Bindung Offsets legt die Anwendung das Anweisungsattribut SQL_ATTR_ROW_BIND_OFFSET_PTR an die Adresse des eine SQLINTEGER-Puffers fest. Bevor die Anwendung eine Funktion, die Bindungen verwendet aufruft, einen Offset in Bytes, die in diesem Puffer eingefügt. Um die Adresse des zu verwendenden Puffers zu bestimmen, fügt der Treiber den Offset in die Adresse in der Bindung. Die Summe der Adresse und den Offset muss eine gültige Adresse sein, aber die Adresse, die der Offset hinzugefügt wird, keine gültig ist. Weitere Informationen zur Verwendung von Bindung Offsets finden Sie unter "Puffer Adressen" weiter unten in diesem Abschnitt.  
  
## <a name="binding-arrays"></a>Binden von Arrays  
 Wenn die Rowsetgröße (der Wert des Attributs SQL_ATTR_ROW_ARRAY_SIZE-Anweisung) größer als 1 ist, bindet die Anwendung Arrays von Puffern, statt der einzelnen Puffer an. Weitere Informationen finden Sie unter [Blockcursor](../../../odbc/reference/develop-app/block-cursors.md).  
  
 Die Anwendung kann auf zwei Arten Arrays binden:  
  
-   Binden Sie ein Array für jede Spalte ein. Dies wird als bezeichnet *spaltenbezogene Bindungen* da jede Data-Struktur (Array) Daten für eine einzelne Spalte enthält.  
  
-   Definieren Sie eine Struktur zum Speichern der Daten für eine gesamte Zeile und ein Array dieser Strukturen binden. Dies wird als bezeichnet *zeilenbezogene Bindungen* da jede Datenstruktur, die Daten für eine einzelne Zeile enthält.  
  
 Jedes Array von Puffer muss über mindestens so viele Elemente als die Größe des Rowsets aufweisen.  
  
> [!NOTE]  
>  Eine Anwendung muss sicherstellen, dass Ausrichtung gültig ist. Weitere Informationen zu Überlegungen hinsichtlich der Ausrichtung finden Sie unter [Ausrichtung](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>Spaltenweises binden  
 In spaltenbezogene Bindungen bindet die Anwendung unterschiedliche Daten- und Längenindikator/Arrays auf jede Spalte an.  
  
 Um spaltenbezogene Bindungen zu verwenden, legt die Anwendung zuerst das Anweisungsattribut SQL_ATTR_ROW_BIND_TYPE auf SQL_BIND_BY_COLUMN ein. (Dies ist die Standardeinstellung.) Für jede Spalte gebunden ist führt die Anwendung die folgenden Schritte aus:  
  
1.  Ordnet ein Datenarray-Puffer.  
  
2.  Ordnet ein Array von Längenindikator/Puffer.  
  
    > [!NOTE]  
    >  Wenn die Anwendung direkt in Deskriptoren geschrieben, wenn spaltenbezogene Bindung verwendet wird, können die separaten Arrays für Länge und der Indikator Daten verwendet werden.  
  
3.  Aufrufe **SQLBindCol** mit den folgenden Argumenten:  
  
    -   *TargetType* ist der Typ der ein einzelnes Element im Array Puffer Daten.  
  
    -   *TargetValuePtr* ist die Adresse des Pufferarrays Daten.  
  
    -   *Pufferlänge* ist die Größe der ein einzelnes Element im Array Puffer Daten. Die *Pufferlänge* Argument wird ignoriert, wenn die Daten Daten fester Länge ist.  
  
    -   *StrLen_or_IndPtr* ist die Adresse des Längenindikator/Arrays.  
  
 Weitere Informationen, wie diese Informationen verwendet werden finden Sie unter "Puffer Adressen" weiter unten in diesem Abschnitt. Weitere Informationen zur spaltenbezogene Bindung finden Sie unter [spaltenweise Bindung](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>Zeilenweise Bindung  
 In zeilenbezogene Bindung definiert die Anwendung eine Struktur, die Daten und Längenindikator/Puffer für jede Spalte gebunden ist.  
  
 Um die zeilenweise Bindung zu verwenden, führt die Anwendung die folgenden Schritte aus:  
  
1.  Definiert eine Struktur, um eine einzelne Zeile mit Daten (einschließlich Daten und Längenindikator/Puffer) zu speichern, und weist ein Array dieser Strukturen.  
  
    > [!NOTE]  
    >  Wenn die Anwendung direkt in Deskriptoren geschrieben, wenn die zeilenweise Bindung verwendet wird, können separate Felder für Länge und der Indikator Daten verwendet werden.  
  
2.  Das SQL_ATTR_ROW_BIND_TYPE-Anweisungsattribut fest auf die Größe der Struktur, die eine einzelne Zeile mit Daten enthält oder die Größe einer Instanz eines Puffers, in dem die Ergebnisspalten gebunden werden. Die Länge muss Platz für alle gebundenen Spalten und möglicherweise vorhandene Auffüllzeichen der Struktur bzw. des Puffers, um sicherzustellen, dass bei der die Adresse einer gebundenen Spalte mit der angegebenen Länge erhöht wird, wird das Ergebnis an den Anfang derselben Spalte in der nächsten Zeile zeigen enthalten. Bei Verwendung der *"sizeof"* -Operator in ANSI C, wird dieses Verhalten garantiert.  
  
3.  Aufrufe **SQLBindCol** mit den folgenden Argumenten für jede Spalte gebunden werden soll:  
  
    -   *TargetType* ist der Typ des Datenmembers Puffer, an die Spalte gebunden werden.  
  
    -   *TargetValuePtr* ist die Adresse des Datenmembers Puffer in das erste Arrayelement.  
  
    -   *Pufferlänge* ist die Größe des Puffers Datenmembers.  
  
    -   *StrLen_or_IndPtr* ist die Adresse des Elements Längenindikator/gebunden werden.  
  
 Weitere Informationen, wie diese Informationen verwendet werden finden Sie unter "Puffer Adressen" weiter unten in diesem Abschnitt. Weitere Informationen zur spaltenbezogene Bindung finden Sie unter [zeilenweise Bindung](../../../odbc/reference/develop-app/row-wise-binding.md).  
  
## <a name="buffer-addresses"></a>Puffer-Adressen  
 Die *Puffer Adresse* ist die tatsächliche Adresse des Puffers Daten oder Längenindikator /. Der Treiber berechnet Pufferadresse, kurz bevor in den Puffern (z. B. während der Zeit fetch) geschrieben. Er wird berechnet, aus der folgenden Formel, der die Adressen im angegebenen verwendet die *TargetValuePtr* und *StrLen_or_IndPtr* Argumente, die Bindung Offset und die Nummer der Zeile:  
  
 *Adresse gebunden* + *binden Offset* + ((*Zeilennummer* – 1) X *Elementgröße*)  
  
 auf die Formel Variablen definiert werden, wie in der folgenden Tabelle beschrieben.  
  
|Variable|Description|  
|--------------|-----------------|  
|*Adresse gebunden*|Für Datenpuffer, die Adresse angegeben, mit der *TargetValuePtr* Argument in **SQLBindCol**.<br /><br /> Für Längenindikator/Puffer, die Adresse angegeben, mit der *StrLen_or_IndPtr* Argument in **SQLBindCol**. Weitere Informationen finden Sie unter "Zusätzliche Kommentare" im Abschnitt "Deskriptoren und SQLBindCol".<br /><br /> Wenn die gebundene Adresse 0 ist, wird kein Datenwert zurückgegeben, auch wenn die Adresse als von der vorherigen Formel berechnete Wert ungleich NULL ist.|  
|*Binden von Offset*|Wenn zeilenbezogene Bindungen verwendet wird, der Wert an der Adresse gespeichert, die mit SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut angegeben werden.<br /><br /> Wenn spaltenbezogene Bindungen verwendet werden, oder wenn der Wert des Attributs Anweisung SQL_ATTR_ROW_BIND_OFFSET_PTR ein null-Zeiger ist *Bindung Offset* ist 0.|  
|*Zeilennummer*|Die 1-basierten Nummer der Zeile im Rowset. Einzeiliges Abrufe, die standardmäßig, die werden zu können, ist dies 1.|  
|*Elementgröße*|Die Größe eines Elements in die gebundene Array.<br /><br /> Wenn spaltenbezogene Bindungen verwendet wird, ist dies die **sizeof(SQLINTEGER)** für Längenindikator/Puffer. Für Datenpuffer, es ist der Wert des der *Pufferlänge* Argument in **SQLBindCol** , wenn der Datentyp variabler Länge und die Größe des Datentyps ist, wenn der Datentyp über eine feste Länge aufweist.<br /><br /> Wenn die zeilenweise Bindung verwendet wird, ist dies der Wert des Attributs SQL_ATTR_ROW_BIND_TYPE-Anweisung für die Daten und Längenindikator/Puffer.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Deskriptoren und SQLBindCol  
 In den folgenden Abschnitten wird beschrieben, wie **SQLBindCol** interagiert mit Deskriptoren.  
  
> [!CAUTION]  
>  Aufrufen von **SQLBindCol** für eine Anweisung auf andere Anweisungen auswirken kann. Dieser Fehler tritt bei der der Anweisung zugeordneten ARD explizit zugeordnet, und auch andere Anweisungen zugeordnet ist. Da **SQLBindCol** ändert die Beschreibung der Änderungen zu übernehmen, um alle Anweisungen, denen dieses Deskriptors zugeordnet ist. Wenn dies nicht das erforderliche Verhalten ist, die Anwendung sollte trennen dieses Deskriptors aus den anderen Anweisungen vor **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Arguments-Zuordnungen  
 Im Prinzip **SQLBindCol** führt Sie nacheinander die folgenden Schritte aus:  
  
1.  Aufrufe **SQLGetStmtAttr** um ARD-Handle abzurufen.  
  
2.  Aufrufe **SQLGetDescField** zum Abrufen dieser Deskriptorfeld SQL_DESC_COUNT und, wenn der Wert in der *ColumnNumber* Arguments überschreitet den Wert von SQL_DESC_COUNT Aufrufe **SQLSetDescField ** erhöhen den Wert der SQL_DESC_COUNT auf *ColumnNumber*.  
  
3.  Aufrufe **SQLSetDescField** mehrere Male auf, um die folgenden Felder von der ARD Werte zuzuweisen:  
  
    -   Legt SQL_DESC_TYPE und SQL_DESC_CONCISE_TYPE auf den Wert der *TargetType*, außer wenn *TargetType* ist eine präzise Bezeichner eines Untertyps "DateTime" oder ein Zeitintervall, SQL_DESC_TYPE auf SQL_ festgelegt "DateTime" oder SQL_INTERVAL, bzw.; Legt SQL_DESC_CONCISE_TYPE präzise Identifier; und legt SQL_DESC_DATETIME_INTERVAL_CODE auf den entsprechenden "DateTime" oder das Intervall Subcode.  
  
    -   Legt eine oder mehrere der SQL_DESC_LENGTH, SQL_DESC_PRECISION SQL_DESC_SCALE und SQL_DESC_DATETIME_INTERVAL_PRECISION, je nach *TargetType*.  
  
    -   Legt das Feld SQL_DESC_OCTET_LENGTH auf den Wert der *Pufferlänge*.  
  
    -   Legt das SQL_DESC_DATA_PTR-Feld auf den Wert der *TargetValue*.  
  
    -   Legt das Feld SQL_DESC_INDICATOR_PTR auf den Wert der *StrLen_or_Ind*. (Siehe im folgenden Abschnitt.)  
  
    -   Legt das Feld SQL_DESC_OCTET_LENGTH_PTR auf den Wert der *StrLen_or_Ind*. (Siehe im folgenden Abschnitt.)  
  
 Die Variable, die die *StrLen_or_Ind* -Argument bezieht sich auf Informationen zur Anzeige und Länge verwendet wird. Wenn eine Abrufoperation für die Spalte einen null-Wert erkennt, SQL_NULL_DATA in dieser Variable gespeichert; Andernfalls werden die Datenlänge in dieser Variable gespeichert. Übergeben einen null-Zeiger als *StrLen_or_Ind* behält den Fetch-Vorgang die Datenlänge zurückgeben, aber macht die Fetch fehl, wenn einen null-Wert gefunden werden können, und keine Möglichkeit hat, SQL_NULL_DATA zurückgegeben.  
  
 Wenn der Aufruf von **SQLBindCol** ein Fehler auftritt, der Inhalt der deskriptorfelder, die in der ARD festgelegt haben, würden sind nicht definiert, und der Wert des Felds SQL_DESC_COUNT, der die ARD bleibt unverändert.  
  
## <a name="implicit-resetting-of-count-field"></a>Implizite Zurücksetzen des COUNT-Feld  
 **SQLBindCol** SQL_DESC_COUNT auf den Wert des legt die *ColumnNumber* Argument nur, wenn dies den Wert der SQL_DESC_COUNT erhöhen würde. Wenn der Wert in der *TargetValuePtr* Argument ist ein null-Zeiger und der Wert in der *ColumnNumber* Argument SQL_DESC_COUNT gleich ist (d. h. wenn Aufheben der Bindung die höchste Spalte gebunden ist), dann SQL_DESC_ Anzahl wird auf die Anzahl der verbleibenden gebundene Spalte mit der höchsten festgelegt.  
  
## <a name="cautions-regarding-sqldefault"></a>Warnhinweise zur SQL_DEFAULT  
 Zum erfolgreichen Spaltendaten abrufen möchten, muss die Anwendung ordnungsgemäß die Länge und den Ausgangspunkt der Daten in den Anwendungspuffer bestimmen. Wenn die Anwendung gibt eine explizite *TargetType*, Anwendung Missverständnisse leicht erkannt werden. Jedoch, wenn die Anwendung gibt eine *TargetType* von SQL_DEFAULT, **SQLBindCol** angewendet können für eine Spalte mit einem anderen Datentyp aus das gewünschte durch die Anwendung von Änderungen an den Metadaten oder durch den Code in eine andere Spalte anwenden. In diesem Fall kann die Anwendung nicht immer der Start oder die Länge der abgerufenen Spaltendaten ermittelt werden. Dies kann zu nicht berichtete Datenfehler oder einen Arbeitsspeicher führen.  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel führt eine Anwendung eine **wählen** Anweisung in der Customers-Tabelle, um ein Resultset des Kunden-IDs, Namen und Telefonnummern zurückzugeben, die nach Namen sortiert. Er ruft dann **SQLBindCol** zum Binden von Datenspalten an lokalen Puffern. Zum Schluss die Anwendung ruft jede Zeile der Daten mit **SQLFetch** und gibt Name, ID und Telefonnummer des Kunden.  
  
 Weitere Codebeispiele finden Sie unter [SQLBulkOperations-Funktion](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLColumns-Funktion](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md), und [SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Siehe auch [ODBC-Beispielprogramm](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLDescribeCol-Funktion](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Das Abrufen mehrerer Datenzeilen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Freigeben von Puffern mit Spalten für die Anweisung|[SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Abrufen des Teils oder aller eine Spalte mit Daten|[SQLGetData-Funktion](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Zurückgeben der Anzahl der Ergebnis Resultsetspalten|[SQLNumResultCols-Funktion](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
