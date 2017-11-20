---
title: SQLSetCursorName-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 716170dc027cce47b29a11cc9a650cf4fbb3eb29
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLSetCursorName** eine aktive Anweisung ein Cursorname zugeordnet. Wenn eine Anwendung nicht aufruft **SQLSetCursorName**, generiert der Treiber Cursornamen Bedarf für die Verarbeitung der SQL-Anweisung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *CursorName*  
 [Eingabe] Name des Cursors. Für die effiziente Verarbeitung der Cursornamen sollte keinen keine führenden oder nachfolgenden Leerzeichen in den Cursornamen, und wenn der Name des Cursors einen Begrenzungsbezeichner enthält, sollte das Trennzeichen als erstes Zeichen in den Cursornamen positioniert sein.  
  
 *Namenslänge*  
 [Eingabe] Länge in Zeichen des **CursorName*.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetCursorName** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_STMT auf, und eine *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLSetCursorName** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Name des Cursors hat den Höchstwert überschritten, sodass nur die maximal zulässige Anzahl von Zeichen wurde verwendet.|  
|24000|Ungültiger Cursorstatus|Die Anweisung entspricht *StatementHandle* bereits im Zustand ausgeführt oder Cursor positioniert wurde.|  
|34000|Ungültiger Cursorname|Der Name des Cursors im angegebenen **CursorName* war ungültig, da er die maximale Länge überschritten wird, gemäß der Treiber, oder muss mit "SQLCUR" oder "SQL_CUR."|  
|3C000|Doppelte Cursorname|Der Name des Cursors im angegebenen **CursorName* ist bereits vorhanden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) das Argument *CursorName* wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese Funktion Aynchronous wurde weiterhin ausgeführt, wenn die **SQLSetCursorName** Funktion aufgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) das Argument *Namenslänge* war kleiner als 0, aber nicht SQL_NTS gleich.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Cursornamen dienen nur in positioniertes Update und delete-Anweisungen (z. B. **aktualisieren** *Tabellenname* ... **WHERE CURRENT OF** *Cursorname*). Weitere Informationen finden Sie unter [positioniert Update- und Delete-Anweisungen](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Wenn die Anwendung nicht aufruft **SQLSetCursorName** bei der Ausführung einer Abfrage-Anweisung ein Cursorname definiert der Treiber generiert einen Namen, die mit den Buchstaben SQL_CUR beginnt und bis zu 18 Zeichen Länge nicht überschreitet.  
  
 Alle Cursornamen innerhalb der Verbindung müssen eindeutig sein. Die maximale Länge des Namens eines Cursors wird vom Treiber definiert. Für eine optimale Interoperabilität wird empfohlen, dass Anwendungen Cursornamen auf nicht mehr als 18 Zeichen beschränkt. In ODBC 3.*.x*, wenn ein Cursorname ein Bezeichner in Anführungszeichen ist, es die Groß-und Kleinschreibung behandelt wird und darf die Zeichen, dass der SQL-Syntax würde nicht zulassen oder speziell, z. B. Leerzeichen behandelt und Schlüsselwörter reservierte enthalten. Wenn die Groß-und Kleinschreibung ein Cursorname behandelt werden muss, muss es als Bezeichner in Anführungszeichen übergeben werden.  
  
 Ein Cursorname, die entweder explizit festgelegt oder implizit bleibt festgelegt, bis die Anweisung, mit denen er zugeordnet ist, mit gelöscht wird, **SQLFreeHandle**. **SQLSetCursorName** aufgerufen werden, um ein Cursor für eine Anweisung umbenennen, solange der Cursor im zugeordneten oder vorbereitete Zustand befindet.  
  
## <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel verwendet eine Anwendung **SQLSetCursorName** einen Cursornamen für eine Anweisung fest. Anschließend wird diese Anweisung zum Abrufen von Ergebnissen aus der CUSTOMERS-Tabelle. Schließlich führt es ein positioniertes Update, um die Telefonnummer des John Smith zu ändern. Beachten Sie, dass die Anwendung für unterschiedliche Anweisungshandles verwendet die **wählen** und **UPDATE** Anweisungen.  
  
 Ein weiteres Codebeispiel finden Sie unter [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Ein Cursorname zurückgeben|[SQLGetCursorName-Funktion](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Cursor, Bildlauf Optionen festlegen|[SQLSetScrollOptions-Funktion](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

