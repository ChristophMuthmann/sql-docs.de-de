---
title: SQLGetCursorName-Funktion | Microsoft Docs
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
apiname: SQLGetCursorName
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetCursorName
helpviewer_keywords: SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69a0da5196c5724284c2da75dc6c7deb3c3cedcd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetCursorName** gibt zurück, der Name des Cursors eine angegebene Anweisung zugeordnet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *CursorName*  
 [Ausgabe] Zeiger auf einen Puffer, in dem der Name des Cursors zurückgegeben.  
  
 Wenn *CursorName* NULL ist, *NameLengthPtr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbaren zurückzugebenden im Puffer verweist *CursorName*.  
  
 *Pufferlänge*  
 [Eingabe] Länge des \* *CursorName*, in Zeichen. Wenn der Wert in  *\*CursorName* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLGetCursorNameW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 *NameLengthPtr*  
 [Ausgabe] Zeiger auf den Arbeitsspeicher, in dem die Gesamtzahl der Zeichen (mit Ausnahme von Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *CursorName*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *Pufferlänge*, der Name des Cursors in \* *CursorName* auf abgeschnitten *Pufferlänge*abzüglich der Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetCursorName** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType*von SQL_HANDLE_STMT auf, und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetCursorName** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *CursorName* war nicht groß genug für den gesamten Cursornamen zurückgeben, damit der Name des Cursors abgeschnitten wurden. Die Länge des Cursornamens ungekürzte wird zurückgegeben, **NameLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLGetCursorName** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY015|Kein Cursorname verfügbar.|(DM) der Treiber wurde von einer ODBC 2.*.x* Treiber, gab es keinen geöffneten Cursor für die Anweisung und hatte kein Cursorname festgelegt wurde, mit **SQLSetCursorName**.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert im Argument angegebene *Pufferlänge* war kleiner als 0.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Cursornamen dienen nur in positioniertes Update und delete-Anweisungen (z. B. **aktualisieren** *Tabellenname* ... **WHERE CURRENT OF** *Cursorname*). Weitere Informationen finden Sie unter [positioniert Update- und Delete-Anweisungen](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Wenn die Anwendung nicht aufruft **SQLSetCursorName** um einen Cursornamen zu definieren, generiert der Treiber einen Namen. Dieser Name beginnt mit den Buchstaben SQL_CUR.  
  
> [!NOTE]  
>  In ODBC 2.*.x*, wenn es keine geöffneten Cursor wurde und kein Name wurde, durch einen Aufruf von festgelegt hatte **SQLSetCursorName**, einen Aufruf von **SQLGetCursorName** SQLSTATE HY015 zurückgegeben (es ist kein Cursorname verfügbar). In ODBC 3.*.x*, dies ist "true", unabhängig davon, wann nicht mehr **SQLGetCursorName** wird aufgerufen, gibt der Treiber den Cursornamen.  
  
 **SQLGetCursorName** gibt den Namen eines Cursors, und zwar unabhängig davon, ob der Name explizit oder implizit erstellt wurde. Name des Cursors wird implizit generiert, wenn **SQLSetCursorName** wird nicht aufgerufen. **SQLSetCursorName** aufgerufen werden, um ein Cursor für eine Anweisung umbenennen, solange der Cursor im zugeordneten oder vorbereitete Zustand befindet.  
  
 Kein Cursorname angegeben, die entweder explizit oder implizit festgelegt ist, bleibt festgelegt, bis die *StatementHandle* mit dem es zugeordnet ist wird gelöscht, mit **SQLFreeHandle** mit einem *HandleType* von SQL_HANDLE_STMT auf.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Vorbereiten einer Anweisung für die Ausführung|[SQLPrepare-Funktion](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Ein Cursorname festlegen|[SQLSetCursorName-Funktion](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
