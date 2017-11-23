---
title: SQLStatistics-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLStatistics
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLStatistics
helpviewer_keywords: SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f0e4b82221c78572d24c28717edb0f3209f29ea6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlstatistics-function"></a>SQLStatistics-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLStatistics** Ruft eine Liste der Statistiken zu einer einzelnen Tabelle und die Indizes der Tabelle zugeordnet. Der Treiber gibt zurück, die Informationen als ein Resultset.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *Katalogname*  
 [Eingabe] Name des Katalogs. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt an, die Tabellen, denen keine Kataloge vorhanden sind. *Katalogname* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *CatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *CatalogName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Eingabe] Länge in Zeichen des **CatalogName*.  
  
 *SchemaName*  
 [Eingabe] Name des Schemas. Wenn ein Treiber unterstützt die Schemas für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt an, die Tabellen, die keine Schemas aufweisen. *SchemaName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *SchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *SchemaName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength2*  
 [Eingabe] Länge in Zeichen des **SchemaName*.  
  
 *Tabellenname*  
 [Eingabe] Tabellenname. Dieses Argument darf nicht null-Zeiger sein. *SchemaName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *TableName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *TableName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength3*  
 [Eingabe] Länge in Zeichen des **TableName*.  
  
 *Eindeutig*  
 [Eingabe] Indextyp: SQL_INDEX_UNIQUE oder SQL_INDEX_ALL.  
  
 *Reserviert*  
 [Eingabe] Gibt die Bedeutung der KARDINALITÄT und Seiten Spalten im Resultset. Die folgenden Optionen Einfluss auf die Rückgabe von nur die KARDINALITÄT und Seiten Spalten. Informationen zu Indizes wird zurückgegeben, auch wenn die KARDINALITÄT und Seiten nicht zurückgegeben werden.  
  
 SQL_ENSURE fordert, dass der Treiber unbedingten Abrufen der Statistiken. (, Die nur für den Standard Open Group entsprechen und unterstützen keine Erweiterungen für ODBC-Treiber nicht SQL_ENSURE unterstützt werden.)  
  
 SQL_QUICK fordert, dass der Treiber die KARDINALITÄT und Seiten abgerufen, nur dann, wenn sie ohne weiteres auf dem Server verfügbar sind. In diesem Fall wird vom Treiber nicht sichergestellt, dass die Werte aktuell sind. (Anwendungen, die für den Standard Open Group geschrieben werden, immer erhalten SQL_QUICK-Verhalten aus ODBC 3.*.x*-kompatibel sind.)  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLStatistics** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLStatistics** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund einer Ressourcendeadlock mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*, und klicken Sie dann die Funktion aufgerufen wurde erneut auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Die *TableName* Argument wurde ein null-Zeiger.<br /><br /> Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *CatalogName* Argument wurde ein null-Zeiger und der SQL_CATALOG_NAME *Infotyp* gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *SchemaName* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLStatistics** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge "Name" ist kleiner als 0, aber ungleich-SQL_NTS.<br /><br /> Der Wert eines der Argumente Länge Namen überschritten, der Wert für die maximale Länge für den entsprechenden Namen.|  
|HY100|Der Eindeutigkeitsoptionstyp außerhalb des gültigen Bereichs|(DM) eine ungültige *Unique* Wert angegeben wurde.|  
|HY101|Der Genauigkeitoptionstyp außerhalb des gültigen Bereichs|(DM) eine ungültige *reserviert* Wert angegeben wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Ein Katalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Ein Schema angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.<br /><br /> Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle, die das angeforderte Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLStatistics** gibt Informationen zu einer einzelnen Tabelle als standard Resultset, geordnet nach NON_UNIQUE, TYPE, INDEX_QUALIFIER, INDEX_NAME und ORDINAL_POSITION zurück. Das Resultset kombiniert Statistikinformationen (in der KARDINALITÄT und Seiten Spalten des Resultsets) für die Tabelle mit Informationen zu jedem Index. Informationen, wie diese Informationen verwendet werden können, finden Sie unter [der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Um zu bestimmen, die tatsächliche Länge der Spalten TABLE_CAT, nach "TABLE_SCHEM" Tabellenname und Spaltenname, eine Anwendung aufrufen kann **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, und SQL_MAX_COLUMN_NAME_LEN-Optionen.  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Die folgenden Spalten wurden umbenannt für ODBC 3.*.x*. Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC 3.*.x* Spalte|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 13 (FILTER_CONDITION) können vom Treiber definiert werden. Eine Anwendung sollte treiberspezifischen Spalten zuzugreifen, beginnend am Ende das Resultset statt eine explizite Ordnungsposition anzugeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spaltennummer|Datentyp|Kommentare|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Der Katalogname der Tabelle der Statistik oder der Index gilt; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, denen keine Kataloge vorhanden sind.|  
|NACH "TABLE_SCHEM" (ODBC 1.0)|2|Varchar|Der Schemaname der Tabelle der Statistik oder der Index gilt; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, die keine Schemas aufweisen.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar, die nicht NULL|Der Tabellenname der Tabelle der Statistik oder der Index gilt.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Gibt an, ob der Index keine doppelten Werte zulässt:<br /><br /> SQL_TRUE, wenn die Indexwerte nicht eindeutig sein können.<br /><br /> SQL_FALSE, wenn die Indexwerte eindeutig sein müssen.<br /><br /> NULL wird zurückgegeben, wenn der Typ SQL_TABLE_STAT ist.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|Der Bezeichner, der verwendet wird, um den Index zu qualifizieren nennen dies einen **DROP INDEX**; NULL wird zurückgegeben, wenn ein Index Qualifizierer nicht von der Datenquelle unterstützt wird oder Typ SQL_TABLE_STAT ist. Wenn ein Wert ungleich Null in dieser Spalte zurückgegeben wird, muss er qualifizieren Sie den Namen des Indexes auf verwendet eine **DROP INDEX** -Anweisung, andernfalls sollte der nach "TABLE_SCHEM" verwendet werden, um den Namen des Indexes zu qualifizieren.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Indexname; NULL wird zurückgegeben, wenn der Typ SQL_TABLE_STAT ist.|  
|TYP (ODBC 1.0)|7|Smallint nicht NULL|Die Art der Informationen, die zurückgegeben wird:<br /><br /> SQL_TABLE_STAT zeigt eine Statistik für die Tabelle (in der Spalte "KARDINALITÄT" oder "Seiten") an.<br /><br /> SQL_INDEX_BTREE zeigt einen B-Struktur-Index.<br /><br /> SQL_INDEX_CLUSTERED gibt einen gruppierten Index an.<br /><br /> SQL_INDEX_CONTENT gibt einen Inhaltsindex an.<br /><br /> SQL_INDEX_HASHED gibt einen Hash-Indexes an.<br /><br /> SQL_INDEX_OTHER gibt einen anderen Typ des Indexes an.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Spalte Sequenznummer im Index (beginnend mit 1); NULL wird zurückgegeben, wenn der Typ SQL_TABLE_STAT ist.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Spaltenname. Wenn die Spalte auf einem Ausdruck basiert, z. B. Gehalt + Vorteile des Ausdrucks zurückgegeben wird. Wenn der Ausdruck kann nicht bestimmt werden, ist eine leere Zeichenfolge zurückgegeben. NULL wird zurückgegeben, wenn der Typ SQL_TABLE_STAT ist.|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|Sequenz für die Spalte zu sortieren: "A" für eine aufsteigende; "D" für eine absteigende; NULL wird zurückgegeben, wenn die Sortierreihenfolge der Spalte von der Datenquelle nicht unterstützt wird oder Typ SQL_TABLE_STAT ist.|  
|DIE KARDINALITÄT (ODBC 1.0)|11|Integer|Die Kardinalität der Tabelle oder des Indexes; die Anzahl der Zeilen in der Tabelle, wenn der Typ SQL_TABLE_STAT ist; die Anzahl der eindeutigen Werte im Index, wenn der Typ nicht SQL_TABLE_STAT ist; NULL wird zurückgegeben, wenn der Wert aus der Datenquelle nicht verfügbar ist.|  
|SEITEN (ODBC 1.0)|12|Integer|Die Anzahl der Seiten, die zum Speichern des Indexes oder der Tabelle; die Anzahl der Seiten für die Tabelle, sofern der Typ SQL_TABLE_STAT ist; die Anzahl der Seiten, die für den Index, wenn der Typ nicht SQL_TABLE_STAT ist; NULL wird zurückgegeben, wenn der Wert aus der Datenquelle nicht verfügbar ist oder wenn Sie auf die Datenquelle nicht verfügbar.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Wenn der Index ein gefilterter Index ist, ist dies die filterbedingung, z. B. Gehalt > 30000; Wenn die filterbedingung nicht bestimmt werden kann, ist dies eine leere Zeichenfolge.<br /><br /> NULL, wenn der Index nicht als ein gefilterter Index ist, kann nicht bestimmt werden, ob der Index ein gefilterter Index ist oder Typ SQL_TABLE_STAT.|  
  
 Wenn die Zeile im Resultset eine Tabelle entspricht, der Treiber legt Typ auf SQL_TABLE_STAT und NON_UNIQUE, INDEX_QUALIFIER INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME und ASC_OR_DESC auf NULL. Wenn die KARDINALITÄT oder Seiten aus der Datenquelle keine stehen, legt Sie in der Treiber auf NULL fest.  
  
## <a name="code-example"></a>Codebeispiel  
 Ein Codebeispiel eine ähnliche Funktion, finden Sie unter [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor werden abgerufen.|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Zurückgeben von Spalten von Fremdschlüsseln|[SQLForeignKeys-Funktion](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Die Spalten des Primärschlüssels zurückgegeben werden|[SQLPrimaryKeys-Funktion](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
