---
title: 'Anhang A: ODBC-Fehlercodes | Microsoft Docs'
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
helpviewer_keywords:
- error codes [ODBC]
- SQLSTATE [ODBC]
- error codes [ODBC], SQLSTATE
ms.assetid: c06902e4-721d-42e2-b818-05f0e18e4ce0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 725d16d6326d5fb99ce8d923bd35c64351b3e6cb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-a-odbc-error-codes"></a>Anhang A: ODBC-Fehlercodes
Dieses Thema erläutert SQLSTATE-Werten für ODBC 3. *x*. Weitere Informationen zu ODBC 3. *x* SQLSTATE-Werten finden Sie unter [SQLSTATE-Zuordnungen](../../../odbc/reference/develop-app/sqlstate-mappings.md).  
  
 **SQLGetDiagRec** oder **SQLGetDiagField** SQLSTATE-Werten zurückgibt, gemäß der Definition von Open Group *Datenverwaltung: Structured Query Language (SQL), Version 2* (März 1995). SQLSTATE-Werten handelt es sich um Zeichenfolgen, die fünf Zeichen enthalten. Die folgende Tabelle enthält die SQLSTATE-Werten, die ein Treiber für zurückgeben können **SQLGetDiagRec**.  
  
 Der Zeichenfolgenwert, der für ein SQLSTATE zurückgegeben besteht aus einem zwei Zeichen-Wert, gefolgt von einem Wert dreistelligen-Unterklasse. Der Klassenwert "01" wird eine Warnung generiert und ist von den Rückgabecode SQL_SUCCESS_WITH_INFO begleitet. Andere Klassenwerte als "01", mit Ausnahme der Klasse "," geben einen Fehler an und werden von der Rückgabewert SQL_ERROR begleitet. Die Klasse bezieht sich "IM" auf Warnungen und Fehler, die von der Implementierung von ODBC selbst abgeleitet werden. Der Unterklasse-Wert "000" in einer Klasse gibt an, dass keine dieser SQLSTATE-Unterklasse. Die Zuweisung von Klassen und Unterklassen wird vom SQL-92 definiert.  
  
> [!NOTE]  
>  Obwohl die erfolgreicher Ausführung einer Funktion normalerweise durch einen Rückgabewert von SQL_SUCCESS bezeichnet wird, gibt der SQLSTATE-00000 auch Erfolg an.  
  
|SQLSTATE|Fehler|Kann von zurückgegeben werden|  
|--------------|-----------|--------------------------|  
|01000|Allgemeine Warnung|Alle ODBC-Funktionen mit Ausnahme von:<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|01001|Konflikt beim Cursorvorgang|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01002|Fehler beim Trennen|**SQLDisconnect**|  
|01003|NULL-Wert wurde in der Set-Funktion gelöscht|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01004|Zeichenfolgedaten Sie rechts abgeschnitten|**SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNative**<br /><br /> **SQL-SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetCursorName**|  
|01006|Berechtigung nicht aufgehoben.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01007|Berechtigung nicht gewährt.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01 S 00|Ungültiges Attribut für Verbindungszeichenfolge|**SQLBrowseConnect**<br /><br /> **SQLDriverConnec**|  
|01 S 01|Fehler in Zeile|**SQLBulkOperations**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLSetPos**|  
|01 S 02|Der Optionswert wurde geändert|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|01S06|Es wurde versucht abzurufen, bevor das Resultset das erste Rowset zurückgab|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|01S07|Teilbereiche wurden abgeschnitten.|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01S08|Fehler beim Speichern der Datei-DSN|**SQLDriverConnect**|  
|01S09|Ungültiges Schlüsselwort|**SQLDriverConnect**|  
|07001|Falsche Anzahl von Parametern|**SQLExecDirect**<br /><br /> **SQLExecute**|  
|07002|COUNT-Feld ist ungültig.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|07005|Vorbereitete Anweisung keine *Cursor-Spezifikation*|**SQLColAttribute**<br /><br /> **SQLDescribeCol**|  
|07006|Eingeschränkte Datentypattribut|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|07009|Ungültiger Deskriptorindex|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRecSQLSetPos**|  
|07S01|Ungültige Verwendung des Standardparameters|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**|  
|08001|Client kann keine Verbindung herstellen|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08002|Name der Verbindung verwendet|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|08003|Verbindung nicht geöffnet|**SQLAllocHandle**<br /><br /> **SQLDisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLSetConnectAttr**|  
|08004|Der Server wies die Verbindung|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08007|Verbindungsfehler während der Transaktion|**SQLEndTran**|  
|08S01|Kommunikations-Verbindungsfehler|**SQLBrowseConnect**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNativeSql**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|21S01|Die Liste einzufügender Werte stimmt nicht mit Spaltenliste überein.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|21S02|Die Spaltenzahl der abgeleiteten Tabelle stimmt nicht mit Spaltenliste überein.|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|22001|Zeichenfolgedaten Sie rechts abgeschnitten|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetPos**|  
|22002|Anzeigevariable erforderlich, aber nicht angegeben|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**|  
|22003|Numerischer Wert außerhalb des gültigen Bereichs|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22007|Ungültiges Datetime-format|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22008|Überlauf der DateTime-Feld.|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **QLParamData**<br /><br /> **SQLPutData**|  
|22012|Division durch 0 (null)|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLPutData**|  
|22015|Überlauf der Intervall-Feld.|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22019|Ungültiges Escapezeichen|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22025|Ungültige Escapesequenz|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22026|Zeichenfolgendaten, nicht übereinstimmende Länge|**SQLParamData**|  
|23000|Einschränkungsverletzung Integrität|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|24000|Ungültiger Cursorstatus|**SQLBulkOperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|25000|Ungültiger Transaktionsstatus|**SQLDisconnect**|  
|25 S 01|Transaktionsstatus|**SQLEndTran**|  
|25S02|Transaktion ist noch aktiv|**SQLEndTran**|  
|25S03|Transaktion wird ein Rollback ausgeführt.|**SQLEndTran**|  
|28000|Ungültige Autorisierungsangabe|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|34000|Ungültiger Cursorname|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetCursorName**|  
|3C000|Doppelte Cursorname|**SQLSetCursorName**|  
|3D000|Ungültiger Katalogname|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**|  
|3F000|Ungültiger Schemaname|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|40001|Serialisierungsfehler aufgetreten|**SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLParamData**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|40002|Einschränkungsverletzung Integrität|**SQLEndTran**|  
|40003|Unbekannte Anweisungsvervollständigung|**SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|42000|Syntaxfehler oder zugriffsverletzung|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|42S01|Basistabelle oder-Sicht ist bereits vorhanden.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S02|Die Basistabelle oder-Sicht wurde nicht gefunden.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S11|Index ist bereits vorhanden.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S12|Index wurde nicht gefunden|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S21|Spalte ist bereits vorhanden.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S22|Spalte wurde nicht gefunden.|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|44000|WITH CHECK OPTION-Verstoß|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY000|Allgemeiner Fehler|Alle ODBC-Funktionen mit Ausnahme von:<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY001|Fehler bei der speicherbelegung|Alle ODBC-Funktionen mit Ausnahme von:<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY003|Ungültiger Anwendungspuffertyp|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLGetData**|  
|HY004|Ungültiger SQL-Datentyp|**SQLBindParameter**<br /><br /> **SQLGetTypeInfo**|  
|HY007|Die zugeordnete Anweisung ist nicht vorbereitet.|**SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**|  
|HY008|Der Vorgang wurde abgebrochen|Alle ODBC-Funktionen, die asynchron verarbeitet werden können:<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDisconnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY009|Ungültige Verwendung des null-Zeiger|**SQLAllocHandle**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY010|Fehler bei Funktionssequenz|**SQLAllocHandle**<br /><br /> **SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLRowCount**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY011|Attribut kann jetzt nicht festgelegt werden|**SQLBulkOperations**<br /><br /> **SQLParamData**<br /><br /> **QLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY012|Ungültiger Transaktionsvorgangscode|**SQLEndTran**|  
|HY013|Speicherverwaltungsfehler|Alle ODBC-Funktionen mit Ausnahme von:<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY014|Das Limit für die Anzahl von Handles wurde überschritten|**SQLAllocHandle**|  
|HY015|Kein Cursorname verfügbar.|**SQLGetCursorName**|  
|HY016|Ein Implementierungszeilendeskriptor kann nicht geändert werden.|**SQLCopyDesc**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY017|Ungültige Verwendung eines automatisch zugeordneten Deskriptorhandles|**SQLFreeHandle**<br /><br /> **SQLSetStmtAttr**|  
|HY018|"Abbrechen"-Anforderung wurde vom Server abgelehnt|**SQLCancel**|  
|HY019|Die gesendeten Daten sind nicht-Zeichen oder Binärdaten|**SQLPutData**|  
|HY020|Bei dem Versuch, einen null-Wert zu verketten.|**SQLPutData**|  
|HY021|Inkonsistente Deskriptorinformationen|**SQLBindParameter**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY024|Ungültiger Attributwert|**SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY091|Ungültiger Deskriptorfeldbezeichner|**SQLColAttribute**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|**SQLAllocHandle**<br /><br /> **QLBulkOperations**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetEnvAttr**<br /><br /> **QLParamData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY095|Funktionstyp außerhalb des gültigen Bereichs|**SQLGetFunctions**|  
|HY096|Ungültiger Informationstyp|**SQLGetInfo**|  
|HY097|Spaltentyp außerhalb des gültigen Bereichs|**SQLSpecialColumns**|  
|HY098|Bereichstyp außerhalb des gültigen Bereichs|**SQLSpecialColumns**|  
|HY099|Nullable-Typ außerhalb des gültigen Bereichs|**SQLSpecialColumns**|  
|HY100|Der Eindeutigkeitsoptionstyp außerhalb des gültigen Bereichs|**SQLStatistics**|  
|HY101|Der Genauigkeitoptionstyp außerhalb des gültigen Bereichs|**SQLStatistics**|  
|HY103|Ungültiger Abrufcode|**SQLDataSources**<br /><br /> **SQLDrivers**|  
|HY104|Ungültiger Wert für Genauigkeit oder Dezimalstellen|**SQLBindParameter**|  
|HY105|Ungültiger Parametertyp|**SQLBindParameter**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**|  
|HY106|Der Fetchtyp außerhalb des gültigen Bereichs|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HY107|Zeilenwert außerhalb des gültigen Bereichs|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLSetPos**|  
|HY109|Ungültige Cursorposition|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY110|Ungültiger Treiberabschluss|**SQLDriverConnect**|  
|HY111|Ungültige lesezeichenwerts|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HYC00|Optionales Feature nicht implementiert|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT00|Timeout abgelaufen|**SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT01|Verbindungstimeout abgelaufen|Alle ODBC-Funktionen mit Ausnahme von:<br /><br /> **SQLDrivers**<br /><br /> **SQLDataSources**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLSetEnvAttr**|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|Alle ODBC-Funktionen mit Ausnahme von:<br /><br /> **SQLAllocHandle**<br /><br /> **SQLDataSources**<br /><br /> **SQLDrivers**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLGetFunctions**|  
|IM002|Datenquellenname nicht gefunden und kein Standardtreiber angegeben|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM003|Angegebene Treiber konnte nicht geladen werden|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM004|Des Treibers **SQLAllocHandle** auf SQL_HANDLE_ENV auf Fehler|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM005|Des Treibers **SQLAllocHandle** auf SQL_HANDLE_DBC auf Fehler|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM006|Des Treibers **SQLSetConnectAttr** fehlgeschlagen|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM007|Keine Datenquelle oder Treiber angegeben; Dialogfeld nicht zulässig|**SQLDriverConnect**|  
|IM008|Dialogfeld ' '|**SQLDriverConnect**|  
|IM009|Kann nicht geladen werden Konvertierungs-DLL|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|IM010|Der Datenquellenname ist zu lang|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM011|Der Treibername ist zu lang|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM012|Treiber-Schlüsselwort-Syntaxfehler|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM013|Fehler in der Ablaufverfolgungsdatei|Alle ODBC-Funktionen.|  
|IM014|Ungültiger Name der Datei-DSN|**SQLDriverConnect**|  
|IM015|Beschädigte Datei als Datenquelle|**SQLDriverConnect**|

