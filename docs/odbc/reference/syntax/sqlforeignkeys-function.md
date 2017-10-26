---
title: SQLForeignKeys-Funktion | Microsoft Docs
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
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d56fd87c4c9612fb520b1a54b9d0c2cab645223
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLForeignKeys** zurückgeben kann:  
  
-   Eine Liste von Fremdschlüsseln in der angegebenen Tabelle (Spalten in der angegebenen Tabelle, die auf Primärschlüssel in anderen Tabellen verweisen).  
  
-   Eine Liste von Fremdschlüsseln in anderen Tabellen, die auf den Primärschlüssel in der angegebenen Tabelle verweisen.  
  
 Jede Liste, die als Resultset auf der angegebenen Anweisung gibt der Treiber.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *PKCatalogName*  
 [Eingabe] Primärschlüsseltabelle ein Name des Katalogs. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, denen keine Kataloge vorhanden sind. *PKCatalogName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *PKCatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *PKCatalogName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Eingabe] Länge des **PKCatalogName*, in Zeichen.  
  
 *PKSchemaName*  
 [Eingabe] Schemaname der Primärschlüsseltabelle. Wenn ein Treiber unterstützt die Schemas für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, die keine Schemas. *PKSchemaName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *PKSchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *PKSchemaName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength2*  
 [Eingabe] Länge des **PKSchemaName*, in Zeichen.  
  
 *PKTableName*  
 [Eingabe] Name der Primärschlüsseltabelle. *PKTableName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *PKTableName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *PKTableName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength3*  
 [Eingabe] Länge des **PKTableName*, in Zeichen.  
  
 *FKCatalogName*  
 [Eingabe] Katalogname der Fremdschlüsseltabelle. Wenn ein Treiber Kataloge unterstützt für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, denen keine Kataloge vorhanden sind. *FKCatalogName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *FKCatalogName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *FKCatalogName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength4*  
 [Eingabe] Länge des **FKCatalogName*, in Zeichen.  
  
 *FKSchemaName*  
 [Eingabe] Schemaname der Fremdschlüsseltabelle. Wenn ein Treiber unterstützt die Schemas für einige Tabellen jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS, eine leere Zeichenfolge ruft ("") gibt die Tabellen, die keine Schemas. *FKSchemaName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *FKSchemaName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *FKSchemaName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength5*  
 [Eingabe] Länge des **FKSchemaName*, in Zeichen.  
  
 *FKTableName*  
 [Eingabe] Name der Fremdschlüsseltabelle. *FKTableName* ein Zeichenfolgenmuster für die Suche nicht enthalten.  
  
 Wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt ist *FKTableName* wird als Bezeichner behandelt und seine Fall spielt keine Rolle. Ist er SQL_FALSE, *FKTableName* ist ein normales Argument; wird als solcher behandelt, und der Fall ist von Bedeutung.  
  
 *NameLength6*  
 [Eingabe] Länge des **FKTableName*, in Zeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLForeignKeys** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* SQL _HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLForeignKeys** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Ein Cursor auf geöffnet war die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde. Dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|40001|Serialisierungsfehler aufgetreten|Die Transaktion wurde aufgrund einer Ressourcendeadlock mit einer anderen Transaktion ein Rollback ausgeführt.|  
|40003|Unbekannte Anweisungsvervollständigung|Die zugeordnete Verbindung konnte während der Ausführung dieser Funktion und der Status der Transaktion kann nicht bestimmt werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*, und klicken Sie dann die Funktion aufgerufen wurde erneut auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) die Argumente *PKTableName* und *FKTableName* wurden beide null-Zeiger.<br /><br /> Das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde die *FKCatalogName* oder *PKCatalogName* Argument wurde ein null-Zeiger und die SQL_CATALOG_NAME *Infotyp*gibt, die Namen Katalog unterstützt werden.<br /><br /> (DM) SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE, festgelegt wurde und die *FKSchemaName*, *PKSchemaName*, *FKTableName*, oder *PKTableName * Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde noch ausgeführt werden, wenn die SQLForeignKeys-Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die * StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) der Wert eines der Argumente Länge "Name" ist kleiner als 0, aber ungleich-SQL_NTS.|  
|||Der Wert eines der Argumente Länge Namen überschritten, der Wert für die maximale Länge für den entsprechenden Namen. (Siehe "Kommentare".)|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Ein Katalog angegeben wurde, und der Treiber oder die Datenquelle Kataloge nicht unterstützt.<br /><br /> Ein Schemaname angegeben wurde, und der Treiber oder die Datenquelle unterstützt keine Schemas.|  
|||Die Kombination der aktuellen Einstellungen der Anweisungsattribute SQL_ATTR_CONCURRENCY und SQL_ATTR_CURSOR_TYPE wurde von der Treiber oder die Datenquelle nicht unterstützt.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Informationen, wie die von dieser Funktion zurückgegebenen Informationen verwendet werden kann, finden Sie unter [der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Wenn \* *PKTableName* enthält einen Tabellennamen **SQLForeignKeys** gibt ein Resultset mit der primären Schlüssel für die angegebene Tabelle und alle Fremdschlüssel, die darauf verweisen. Die Liste der Fremdschlüssel in anderen Tabellen umfasst nicht den Fremdschlüssel, die auf die unique-Einschränkungen in der angegebenen Tabelle verweisen.  
  
 Wenn \* *FKTableName* enthält einen Tabellennamen **SQLForeignKeys** gibt ein Resultset, das alle Fremdschlüssel in der angegebenen Tabelle enthält, die auf Primärschlüssel in anderen Tabellen verweisen und die der Primärschlüssel in den anderen Tabellen, auf die sie verweisen. Die Liste der Fremdschlüssel in der angegebenen Tabelle enthält keine Fremdschlüssel, die unique-Einschränkungen in anderen Tabellen verweisen.  
  
 Wenn beide \* *PKTableName* und \* *FKTableName* Tabellennamen enthalten **SQLForeignKeys** gibt die Fremdschlüssel in der angegebenen Tabelle zurück. in \* *FKTableName* , verweisen auf den Primärschlüssel der Tabelle, angegeben **PKTableName*. Dies sollte höchstens einen Schlüssel verwendet.  
  
> [!NOTE]  
>  Weitere Informationen zu den allgemeinen Verwendung, die Argumente und die zurückgegebenen Daten des ODBC-Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLForeignKeys** gibt Ergebnisse als standard Resultset zurück. Wenn der Fremdschlüssel mit einem Primärschlüssel verknüpft sind angefordert werden, wird das Resultset nach FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME und KEY_SEQ sortiert. Wenn der Primärschlüssel verknüpft sind mit einem Fremdschlüssel angefordert werden, wird das Resultset nach PKTABLE_CAT, PKTABLE_SCHEM PKTABLE_NAME und KEY_SEQ sortiert. Die folgende Tabelle listet die Spalten im Resultset.  
  
 Die Länge von VARCHAR-Spalten werden nicht in der Tabelle angezeigt; die tatsächliche Länge hängen von der Datenquelle ab. Um zu bestimmen, die tatsächliche Länge der PKTABLE_CAT FKTABLE_CAT, PKTABLE_SCHEM oder FKTABLE_SCHEM, PKTABLE_NAME oder FKTABLE_NAME, und PKCOLUMN_NAME oder FKCOLUMN_NAME Spalten kann eine Anwendung aufrufen **SQLGetInfo** mit der SQL_MAX_ CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN SQL_MAX_TABLE_NAME_LEN und SQL_MAX_COLUMN_NAME_LEN-Optionen.  
  
 Die folgenden Spalten wurden umbenannt für ODBC 3*. X.* Die Spalte Namensänderungen wirken Abwärtskompatibilität sich nicht, da Anwendungen Spaltennummer binden.  
  
|ODBC 2.0-Spalte|ODBC 3*.x* Spalte|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 Die folgende Tabelle listet die Spalten im Resultset. Zusätzliche Spalten nach Spalte 14 ("Hinweise") können vom Treiber definiert werden. Eine Anwendung sollte treiberspezifischen Spalten zuzugreifen, beginnend am Ende das Resultset statt eine explizite Ordnungsposition anzugeben. Weitere Informationen finden Sie unter [Daten von Katalogfunktionen zurückgegeben](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Spaltenname|Spaltennummer|Datentyp|Kommentare|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|Katalogname der Primärschlüsseltabelle; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, denen keine Kataloge vorhanden sind.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|Schemaname der Primärschlüsseltabelle; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, die keine Schemas aufweisen.|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar, die nicht NULL|Name der Primärschlüsseltabelle.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar, die nicht NULL|Namen der Primärschlüsselspalte. Der Treiber gibt eine leere Zeichenfolge für eine Spalte, die nicht über einen Namen verfügt.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|Katalogname der Fremdschlüsseltabelle; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Kataloge für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, denen keine Kataloge vorhanden sind.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|Schemaname der Fremdschlüsseltabelle; NULL, wenn Sie auf die Datenquelle nicht verfügbar. Wenn ein Treiber Schemas für einige Tabellen unterstützt jedoch nicht für andere, z. B. wenn der Treiber Daten aus anderen DBMS abruft, wird eine leere Zeichenfolge zurückgegeben ("") für diese Tabellen, die keine Schemas aufweisen.|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar, die nicht NULL|Name der Fremdschlüsseltabelle.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar, die nicht NULL|Name der Fremdschlüsselspalte. Der Treiber gibt eine leere Zeichenfolge für eine Spalte, die nicht über einen Namen verfügt.|  
|KEY_SEQ (ODBC 1.0)|9|Smallint nicht NULL|Spalte Sequenznummer im Schlüssel (beginnend mit 1).|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|Aktion für den Fremdschlüssel angewendet werden, wenn der SQL-Vorgang ist **UPDATE**. Dabei kann es sich um einen der folgenden Werte aufweisen. (Die referenzierte Tabelle ist die Tabelle, die den primären Schlüssel aufweist, die verweisende Tabelle ist die Tabelle, die den Fremdschlüssel aufweist.)<br /><br /> SQL_CASCADE: Wenn der Primärschlüssel der Tabelle, auf die verwiesen wird, aktualisiert wird, wird auch die Fremdschlüssel der verweisenden Tabelle aktualisiert.<br /><br /> SQL_NO_ACTION: Wenn ein Update des Primärschlüssels von die referenzierte Tabelle würde dazu führen, dass "zurückbleiben Reference" in der verweisenden Tabelle (d. h. Zeilen in der verweisenden Tabelle müsste keine Entsprechungen in der referenzierten Tabelle), das Update abgelehnt. Wenn ein Update des Fremdschlüssels der verweisenden Tabelle einen Wert führen würde, der als Wert des Primärschlüssels der referenzierten Tabelle nicht vorhanden ist, wird das Update abgelehnt. (Diese Aktion ist identisch mit der Aktion SQL_RESTRICT in ODBC 2*.x*.)<br /><br /> SQL_SET_NULL: Wenn eine oder mehrere Zeilen in der referenzierten Tabelle so aktualisiert werden, die eine oder mehrere Komponenten des Primärschlüssels geändert werden, werden die Komponenten des Fremdschlüssels in der verweisenden Tabelle, die die geänderten Komponenten des primären Schlüssels entsprechen festgelegt auf NULL in der verweisenden Tabelle alle übereinstimmenden Zeilen.<br /><br /> SQL_SET_DEFAULT: Wenn eine oder mehrere Zeilen in der referenzierten Tabelle so aktualisiert werden, die eine oder mehrere Komponenten des Primärschlüssels geändert werden, werden die Komponenten des Fremdschlüssels in der verweisenden Tabelle, die die geänderten Komponenten des primären Schlüssels entsprechen Legen Sie auf die entsprechenden Standardwerte in der verweisenden Tabelle alle übereinstimmenden Zeilen.<br /><br /> NULL, wenn Sie auf die Datenquelle nicht verfügbar.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|Aktion für den Fremdschlüssel angewendet werden, wenn der SQL-Vorgang ist **löschen**. Dabei kann es sich um einen der folgenden Werte aufweisen. (Die referenzierte Tabelle ist die Tabelle, die den primären Schlüssel aufweist, die verweisende Tabelle ist die Tabelle, die den Fremdschlüssel aufweist.)<br /><br /> SQL_CASCADE: Wenn eine Zeile in der referenzierten Tabelle gelöscht wird, werden alle übereinstimmenden Zeilen in den verweisenden Tabellen ebenfalls gelöscht.<br /><br /> SQL_NO_ACTION: Wenn ein Löschvorgang einer Zeile in die referenzierte Tabelle würde dazu führen, dass "zurückbleiben Reference" in der verweisenden Tabelle (d. h. Zeilen in der verweisenden Tabelle müsste keine Entsprechungen in der referenzierten Tabelle), das Update abgelehnt. (Diese Aktion ist identisch mit der Aktion SQL_RESTRICT in ODBC 2*.x*.)<br /><br /> SQL_SET_NULL: Wenn eine oder mehrere Zeilen in der referenzierten Tabelle gelöscht werden, wird jede Komponente des Fremdschlüssels der verweisenden Tabelle auf NULL in der verweisenden Tabelle alle übereinstimmenden Zeilen festgelegt.<br /><br /> SQL_SET_DEFAULT: Wenn eine oder mehrere Zeilen in der referenzierten Tabelle gelöscht werden, wird jede Komponente des Fremdschlüssels der verweisenden Tabelle gilt in der verweisenden Tabelle alle übereinstimmenden Zeilen festgelegt.<br /><br /> NULL, wenn Sie auf die Datenquelle nicht verfügbar.|  
|FK_NAME (ODBC 2.0)|12|Varchar|Foreign Key-Name. NULL, wenn Sie auf die Datenquelle nicht verfügbar.|  
|PK_NAME (ODBC 2.0)|13|Varchar|Der Name für den Primärschlüssel. NULL, wenn Sie auf die Datenquelle nicht verfügbar.|  
|DEFERRABILITY (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>Codebeispiel  
 Wie in der folgenden Tabelle veranschaulicht wird, wird in diesem Beispiel drei Tabellen, die mit dem Namen ORDERS, Linien und Kunden verwendet.  
  
|ORDERS|ZEILEN|KUNDEN|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|ZEILEN|NAME|  
|OPENDATE|PARTID|ADRESSE|  
|VERTRIEBSMITARBEITER|MENGE|TELEFONNUMMER|  
|STATUS|||  
  
 In der Tabelle ORDERS identifiziert CUSTID, denen der Verkauf vorgenommen wurde. Es ist ein Fremdschlüssel, der auf CUSTID in der CUSTOMERS-Tabelle verweist.  
  
 In der Tabelle Zeilen identifiziert ORDERID den Auftrag, den das Zeilenelement zugeordnet ist. Es ist ein Fremdschlüssel, der OrderID in der ORDERS-Tabelle verweist.  
  
 Dieses Beispiel ruft **SQLPrimaryKeys** den Primärschlüssel der Tabelle ORDERS abgerufen. Das Resultset wird eine Zeile vorhanden sein; die wichtigen Spalten sind in der folgenden Tabelle gezeigt.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|ORDERID|1|  
  
 Im Beispiel wird als Nächstes ruft **SQLForeignKeys** abzurufenden die Fremdschlüssel in anderen Tabellen, die den Primärschlüssel der Tabelle ORDERS verweisen. Das Resultset wird eine Zeile vorhanden sein; die wichtigen Spalten sind in der folgenden Tabelle gezeigt.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|ZEILEN|CUSTID|1|  
  
 Im Beispiel zum Schluss ruft **SQLForeignKeys** die Fremdschlüssel in der ORDERS-Tabelle abgerufen, die auf den Primärschlüssel der anderen Tabellen verweisen. Das Resultset wird eine Zeile vorhanden sein; die wichtigen Spalten sind in der folgenden Tabelle gezeigt.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|KUNDEN|CUSTID|ORDERS|CUSTID|1|  
  
```  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Eine einzelne Zeile oder einen Block von Daten in eine Richtung Vorwärtscursor abrufen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Die Spalten des Primärschlüssels zurückgegeben werden|[SQLPrimaryKeys-Funktion](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|Zurückgeben von Tabellenstatistiken und Indizes|[SQLStatistics-Funktion](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

