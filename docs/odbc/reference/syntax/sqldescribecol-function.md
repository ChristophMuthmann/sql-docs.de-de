---
title: SQLDescribeCol-Funktion | Microsoft Docs
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
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f19de730a9755627863ad2b8e12df6a5e0b1dbc1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLDescribeCol** gibt das Ergebnis Deskriptor – Spaltenname, Datentyp, Spaltengröße, Dezimalstellen und NULL-Zulässigkeit – legen Sie für eine Spalte im Resultset. Diese Information ist auch in den Feldern des IRD verfügbar.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *ColumnNumber*  
 [Eingabe] Die Spaltennummer der Ergebnisdaten, sortiert sequenziell in aufsteigender Spaltenreihenfolge, beginnend mit 1. Die *ColumnNumber* Argument kann auch auf 0 festgelegt werden, um die Lesezeichenspalte zu beschreiben.  
  
 *ColumnName*  
 [Ausgabe] Ein Zeiger auf einen Null-terminierte Puffer in den Namen der Spalte zurückgegeben. Dieser Wert wird aus dem SQL_DESC_NAME-Feld der IRD gelesen. Wenn die Spalte keinen Namen hat oder den Namen der Spalte nicht bestimmt werden kann, gibt der Treiber eine leere Zeichenfolge zurück.  
  
 Wenn *ColumnName* NULL ist, *NameLengthPtr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbaren zurückzugebenden im Puffer verweist *ColumnName*.  
  
 *Pufferlänge*  
 [Eingabe] Länge der **ColumnName* Puffers in Zeichen.  
  
 *NameLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen (mit Ausnahme der null-Terminierung) zurückgegeben verfügbar im zurückzugebenden \* *ColumnName*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *Pufferlänge*, den Spaltennamen im \* *ColumnName* auf abgeschnitten *Pufferlänge*abzüglich der Länge des ein Null-Abschlusszeichen.  
  
 *DataTypePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem den SQL-Datentyp der Spalte zurückgegeben. Dieser Wert wird aus dem Feld SQL_DESC_CONCISE_TYPE vom IRD gelesen. Dadurch wird einer der Werte in [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md), oder treiberspezifischen SQL-Datentyp. Wenn der Datentyp bestimmt werden kann, kehrt der Treiber SQL_UNKNOWN_TYPE zurück.  
  
 In ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP wird zurückgegeben,  *\*DataTypePtr* für Datum, Uhrzeit oder Zeitstempeldaten bzw.; in ODBC 2. *X*, SQL_DATE, SQL_TIME oder SQL_TIMESTAMP zurückgegeben wird. Der Treiber-Manager führt die erforderlichen Zuordnungen, wenn eine ODBC-2. *x* Anwendung arbeitet mit einer ODBC-3. *X* Treiber oder wenn eine ODBC 3. *X* Anwendung arbeitet mit einer ODBC 2. *X* Treiber.  
  
 Wenn *ColumnNumber* entspricht 0 (für eine Lesezeichenspalte), wird im SQL_BINARY zurückgegeben  *\*DataTypePtr* für Lesezeichen variabler Länge. (SQL_INTEGER wird zurückgegeben, wenn von einer ODBC 3. Lesezeichen verwendet werden. *x* Anwendung arbeiten mit einer ODBC 2. *X* Treiber oder von einer ODBC 2. *X* Anwendung arbeiten mit einem ODBC 3. *X* Treiber.)  
  
 Weitere Informationen zu diesen Datentypen finden Sie unter [SQL-Datentypen](../../../odbc/reference/appendixes/sql-data-types.md) in Anhang D:-Datentypen. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation.  
  
 *ColumnSizePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Größe (in Zeichen) der Spalte in der Datenquelle zurückgegeben. Wenn die Spaltengröße nicht bestimmt werden kann, kehrt der Treiber 0 zurück. Weitere Informationen zu Spaltengröße, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.  
  
 *DecimalDigitsPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Anzahl der Dezimalstellen der Spalte in der Datenquelle zurückgegeben. Der Treiber gibt 0 zurück, wenn die Anzahl der Dezimalstellen kann nicht bestimmt werden oder nicht anwendbar ist. Weitere Informationen über Dezimalstellen, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.  
  
 *NullablePtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem einen Wert zurückgegeben, der angibt, ob die Spalte NULL-Werte zulässt. Dieser Wert wird aus dem Feld SQL_DESC_NULLABLE vom IRD gelesen. Der Wert ist eine der folgenden:  
  
 SQL_NO_NULLS: Die Spalte lässt keine NULL-Werte.  
  
 SQL_NULLABLE: Die Spalte lässt NULL-Werte zu.  
  
 SQL_NULLABLE_UNKNOWN: Der Treiber kann nicht feststellen, ob die Spalte NULL-Werte zulässt.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLDescribeCol** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType*von SQL_HANDLE_STMT auf, und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLDescribeCol** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *ColumnName* war nicht groß genug für den gesamten Spaltennamen zurück, damit Sie den Namen der Spalte abgeschnitten wurden. Die Länge des Spaltennamens den ungekürzten wird zurückgegeben, **NameLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07005|Vorbereitete Anweisung keine *Cursor-Spezifikation*|Die zugeordnete Anweisung die *StatementHandle* hat kein Resultset zurückgegeben. Es wurden keine Spalten zu beschreiben.|  
|07009|Ungültiger Deskriptorindex|(DM) der Wert für das Argument angegebene *ColumnNumber* gleich 0 und die Option-Anweisung SQL_ATTR_USE_BOOKMARKS wurde SQL_UB_OFF.<br /><br /> Der Wert für das Argument angegebene *ColumnNumber* war größer als die Anzahl der Spalten im Resultset.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Speicherbelegungsfehler|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn **SQLDescribeCol** aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) hieß die Funktion vor dem Aufruf **SQLPrepare**, **SQLExecute**, oder eine Katalogfunktion des Anweisungshandles.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *Pufferlänge* war kleiner als 0.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
 **SQLDescribeCol** zurückgeben kann eine beliebige SQLSTATE, die von zurückgegeben werden kann **SQLPrepare** oder **SQLExecute** beim Aufruf nach **SQLPrepare** und vor dem **SQLExecute**, je nachdem, wenn die Datenquelle für die SQL-Anweisung, die das Anweisungshandle zugeordnet auswertet.  
  
 Aus Gründen der Leistung eine Anwendung sollte nicht aufrufen **SQLDescribeCol** vor der Ausführung einer Anweisung.  
  
## <a name="comments"></a>Kommentare  
 Ruft eine Anwendung in der Regel **SQLDescribeCol** nach einem Aufruf von **SQLPrepare** und vor oder nach dem zugehörigen Aufruf von **SQLExecute**. Eine Anwendung kann auch aufrufen **SQLDescribeCol** nach einem Aufruf von **SQLExecDirect**. Weitere Informationen finden Sie unter [Ergebnismetadaten festgelegt](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** Ruft ab, der Spaltenname, Typ und Länge von generiert eine **wählen** Anweisung. Wenn die Spalte ein Ausdruck ist **ColumnName* ist eine leere Zeichenfolge oder einen treiberdefinierten Namen.  
  
> [!NOTE]  
>  ODBC unterstützt SQL_NULLABLE_UNKNOWN als eine Erweiterung, obwohl die Open Group und SQL Zugriff Gruppe aufrufen Level-Interface-Spezifikation nicht die Option zum angeben, wird **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Das Abrufen mehrerer Datenzeilen|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Zurückgeben der Anzahl der Ergebnis Resultsetspalten|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Vorbereiten einer Anweisung für die Ausführung|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
