---
title: SQLTables-Funktion | Microsoft Docs
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
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd6e505ee08d7162ef820c7c7c75195b3616e585
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-function"></a>SQLTables-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: Gruppe öffnen  
  
 **Zusammenfassung**  
 **SQLTables** gibt die Liste der Namen von Tabellen-, Katalog oder Schema und Tabellentypen, die in einer bestimmten Datenquelle gespeichert. Der Treiber gibt zurück, die Informationen als ein Resultset.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle für die abgerufenen Ergebnisse.  
  
 *Katalogname*  
 [Eingabe] Name des Katalogs. Die *CatalogName* -Argument akzeptiert Suchmustern, wenn das SQL_ODBC_VERSION Umgebung Attribut SQL_OV_ODBC3; Suchmustern nimmt nicht an, wenn SQL_OV_ODBC2 festgelegt ist. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn ein Treiber Daten von anderen DBMS, eine leere Zeichenfolge abruft ("") gibt an, die Tabellen, denen keine Kataloge vorhanden sind.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *CatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *CatalogName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Eingabe] Länge in Zeichen des **CatalogName*.  
  
 *SchemaName*  
 [Eingabe] Zeichenfolge Suchmuster für Schemanamen. Wenn ein Treiber unterstützt die Schemas für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt an, die Tabellen, die keine Schemas aufweisen.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *SchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *SchemaName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength2*  
 [Eingabe] Länge in Zeichen des **SchemaName*.  
  
 *Tabellenname*  
 [Eingabe] Zeichenfolge Suchmuster für Tabellennamen auf Richtigkeit.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *TableName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *TableName* ist ein Wert Pattern-Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength3*  
 [Eingabe] Länge in Zeichen des **TableName*.  
  
 *Für TableType*  
 [Eingabe] Liste der Tabellentypen entsprechend.  
  
 Beachten Sie, dass das Anweisungsattribut SQL_ATTR_METADATA_ID hat keine Auswirkung auf die *TableType* Argument. *TableType* ist ein Argument des Wert-Liste, unabhängig von der Einstellung der SQL_ATTR_METADATA_ID.  
  
 *NameLength4*  
 [Eingabe] Länge in Zeichen des **TableType*.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLTables** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLTables** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund einer Ressourcendeadlock mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *CatalogName* Argument wurde ein null-Zeiger und der SQL_CATALOG_NAME *Infotyp* gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *SchemaName* oder *TableName* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde noch ausgeführt werden, wenn SQLTables aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge ist kleiner als 0, aber ungleich-SQL_NTS.<br /><br /> Der Wert eines der Argumente Länge Namen überschritten, der Wert für die maximale Länge für den entsprechenden Namen.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Ein Katalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Ein Schema angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.<br /><br /> Eine Zeichenfolge Suchmuster für den Katalognamen, Tabellenschema oder Tabellenname angegeben wurde, und die Datenquelle unterstützt keine Suchmustern für mindestens eines dieser Argumente.<br /><br /> Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle, die das angeforderte Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLTables** Listet alle Tabellen im angeforderten Bereich. Ein Benutzer kann oder möglicherweise keine SELECT-Privilegien auf eine dieser Tabellen. Um Zugriff zu überprüfen, können eine Anwendung:  
  
-   Rufen Sie **SQLGetInfo** und der Typ der SQL_ACCESSIBLE_TABLES Informationen überprüfen.  
  
-   Rufen Sie **SQLTablePrivileges** , überprüfen Sie die Berechtigungen für jede Tabelle.  
  
 Andernfalls muss die Anwendung kann mit der jeweiligen Situation, in denen der Benutzer eine Tabelle, für die wählt **wählen** Berechtigungen nicht erteilt wurden.  
  
 Die *SchemaName* und *TableName* Argumente Suchmustern zu akzeptieren. Die *CatalogName* -Argument akzeptiert Suchmustern, wenn das SQL_ODBC_VERSION Umgebung Attribut SQL_OV_ODBC3; Suchmustern nimmt nicht an, wenn SQL_OV_ODBC2 festgelegt ist. Wenn SQL_OV_ODBC3 festgelegt ist, wird ein ODBC 3.*.x* Treiber benötigen, Platzhalterzeichen den *CatalogName* Argument versehen werden, dass Sie als solcher behandelt werden. Weitere Informationen zu gültigen Suchmustern, finden Sie unter [Muster Value-Argumenten](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Um Enumeration der Kataloge, Schemas und Tabellentypen zu unterstützen, werden die folgende spezielle Semantik für definiert die *CatalogName*, *SchemaName*, *TableName*, und  *TableType* Argumente **SQLTables**:  
  
-   Wenn *CatalogName* sql_all_catalogs lautet und *SchemaName* und *TableName* sind leere Zeichenfolgen, das Resultset enthält eine Liste der gültigen Kataloge für die Datenquelle. (Alle Spalten außer der TABLE_CAT-Spalte NULL-Werte enthalten.)  
  
-   Wenn *SchemaName* ist SQL_ALL_SCHEMAS und *CatalogName* und *TableName* sind leere Zeichenfolgen, das Resultset enthält eine Liste der gültigen Schemas für die Datenquelle. (Alle Spalten außer der Spalte nach "TABLE_SCHEM" NULL-Werte enthalten.)  
  
-   Wenn *TableType* ist SQL_ALL_TABLE_TYPES und *CatalogName*, *SchemaName*, und *TableName* sind leere Zeichenfolgen, das Resultset enthält eine Liste der gültigen Tabellentypen für die Datenquelle an. (Alle Spalten außer der TABLE_TYPE-Spalte NULL-Werte enthalten.)  
  
 Wenn *TableType* ist eine leere Zeichenfolge ist, muss er eine Liste von durch Trennzeichen getrennten Werten für die Typen von Interesse enthalten; jeder Wert in einfache Anführungszeichen (') eingeschlossen werden können oder ohne Anführungszeichen, z. B. "TABLE", "Anzeigen" oder Tabelle anzeigen. Eine Anwendung sollten immer angeben, den "Table" in Großbuchstaben; der Treiber sollten den Tabellentyp konvertieren, um den Fall von der Datenquelle benötigt wird. Wenn die Datenquelle einen angegebenen Tabellentyp nicht unterstützt **SQLTables** keine Ergebnisse für diesen Typ.  
  
 **SQLTables** die Ergebnisse als standard Resultset, geordnet nach TABLE_TYPE, TABLE_CAT nach "TABLE_SCHEM" und TABLE_NAME zurückgegeben. Informationen, wie diese Informationen verwendet werden können, finden Sie unter [der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Um die tatsächliche Länge der Spalten TABLE_CAT, nach "TABLE_SCHEM" und TABLE_NAME zu bestimmen, kann eine Anwendung aufrufen **SQLGetInfo** mit den Informationen SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN und SQL_MAX_TABLE_NAME_LEN Typen.  
  
 Die folgenden Spalten wurden umbenannt für ODBC 3.*.x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC 3.*.x* Spalte|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 5 ("Hinweise") können vom Treiber definiert werden. Eine Anwendung sollte treiberspezifischen Spalten zuzugreifen, beginnend am Ende das Resultset statt eine explizite Ordnungsposition anzugeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spaltennummer|Datentyp|Kommentare|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Name des Katalogs; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, denen keine Kataloge vorhanden sind.|  
|NACH "TABLE_SCHEM" (ODBC 1.0)|2|Varchar|Schemanamen; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, die keine Schemas aufweisen.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|Tabellenname.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|Tabellentypname; eines der folgenden: "TABLE", "VIEW", "SYSTEMTABELLE", "Globale temporäre", "LOCAL TEMPORARY", "ALIAS", "Synonyms" oder einen datenquellenspezifischen Datentypnamen.<br /><br /> Die Bedeutung der "ALIAS" und "SYNONYM" sind treiberspezifisch.|  
|HINWEISE (ODBC 1.0)|5|Varchar|Eine Beschreibung der Tabelle.|  
  
## <a name="example"></a>Beispiel  
 Der folgende Beispielcode gibt keine Handles und Verbindungen frei. Finden Sie unter [SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md) und [SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md) für Codebeispiele Handles und Anweisungen frei.  
  
```  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Berechtigungen für eine Spalte oder Spalten|[SQLColumnPrivileges-Funktion](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Zurückgeben von Spalten in einer Tabelle oder Tabellen|[SQLColumns-Funktion](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Zurückgeben von Tabellenstatistiken und Indizes|[SQLStatistics-Funktion](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Zurückgeben von Berechtigungen für eine Tabelle oder Tabellen|[SQLTablePrivileges-Funktion](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

