---
title: SQLPrepare-Funktion | Microsoft Docs
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
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a1ad2c08c1b2df085e98581576fabfb93ba6236
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlprepare-function"></a>SQLPrepare-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLPrepare** bereitet eine SQL-Zeichenfolge für die Ausführung vor.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *StatementText*  
 [Eingabe] SQL-Text-Zeichenfolge.  
  
 *TextLength*  
 [Eingabe] Länge des **StatementText* in Zeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLPrepare** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_STMT und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLPrepare** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S02|Der Optionswert wurde geändert|Ein Attribut angegebene Anweisung war ungültig aufgrund Implementierung Arbeitsbedingungen, damit ein ähnlichen Wert vorübergehend ersetzt wurde. (**SQLGetStmtAttr** aufgerufen werden können, um zu bestimmen, was vorübergehend ersetzten Werts ist.) Der Ersatzwert ist gültig für die *StatementHandle* , bis der Cursor geschlossen wird. Sind die Anweisungsattribute, die geändert werden können: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|21S01|Die Liste einzufügender Werte stimmt nicht mit Spaltenliste überein.|\**StatementText* enthalten eine **einfügen** -Anweisung und die Anzahl der einzufügenden Werte entsprach nicht den Grad der abgeleiteten Tabelle.|  
|21S02|Die Spaltenzahl der abgeleiteten Tabelle stimmt nicht mit Spaltenliste überein.|\**StatementText* enthalten eine **CREATE VIEW** -Anweisung und die Anzahl der angegebenen Namen ist nicht demselben Sicherheitsgrad wie die abgeleitete Tabelle, die durch die Abfragespezifikation definiert.|  
|22018|Ungültiger Zeichenwert für Konvertierungsangabe|**StatementText* enthalten eine SQL-Anweisung, die ein Literal oder einen Parameter enthalten, und der Wert mit dem Datentyp der Spalte zugeordneten Tabelle nicht kompatibel war.|  
|22019|Ungültiges Escapezeichen|Das Argument *StatementText* enthalten eine **wie** Prädikat mit einer **ESCAPE** in der **, in dem** -Klausel und die Länge der Escape folgende Zeichen **ESCAPE** war nicht gleich 1.|  
|22025|Ungültige Escapesequenz|Das Argument *StatementText* enthaltenen "**wie** *Musterwert* **ESCAPE** *Escapezeichen*"in der **, in dem** -Klausel, und folgende Escape-Zeichen in den Musterwert Zeichen war weder"%"noch"_".|  
|24000|Ungültiger Cursorstatus|(DM) ein Cursor geöffnet wurde die *StatementHandle*, und **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde.<br /><br /> Ein Cursor auf geöffnet war die *StatementHandle*, aber **SQLFetch** oder **SQLFetchScroll** nicht aufgerufen wurde.|  
|34000|Ungültiger Cursorname|\**StatementText* enthalten eine positionierte **löschen** oder eine positionierte **UPDATE**, und der Cursor die vorbereitete Anweisung verweist auf konnte nicht geöffnet werden.|  
|3D000|Ungültiger Katalogname|Der Name des Katalogs im angegebenen *StatementText* war ungültig.|  
|3F000|Ungültiger Schemaname|Der Schemaname, der im angegebenen *StatementText* war ungültig.|  
|42000|Syntaxfehler oder zugriffsverletzung|\**StatementText* enthielt eine SQL­Anweisung, die nicht preparable war oder einen Syntaxfehler enthalten.<br /><br /> **StatementText* enthielt eine Anweisung für die der Benutzer verfügte nicht über die erforderlichen Berechtigungen.|  
|42S01|Basistabelle oder-Sicht ist bereits vorhanden.|\**StatementText* enthalten eine **CREATE TABLE** oder **CREATE VIEW** -Anweisung, und die Tabellen- oder Sicht angegebenen Namen vorhanden ist.|  
|42S02|Die Basistabelle oder-Sicht wurde nicht gefunden.|\**StatementText* enthalten eine **DROP TABLE** oder ein **DROP VIEW** -Anweisung, und die angegebene Tabelle oder Sichtname Name ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **ALTER TABLE** -Anweisung und der angegebene Tabellenname ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **CREATE VIEW** -Anweisung, und ein Tabellen- oder Sicht, die von der Abfragespezifikation definierten Namen nicht vorhanden war.<br /><br /> \**StatementText* enthalten eine **CREATE INDEX** -Anweisung und der angegebene Tabellenname ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **GRANT** oder **widerrufen** -Anweisung, und die angegebene Tabelle oder Sichtname Name ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **wählen** -Anweisung und eine angegebene Tabelle oder Sichtname Name ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **löschen**, **einfügen**, oder **UPDATE** -Anweisung und der angegebene Tabellenname ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **CREATE TABLE** -Anweisung und einer Tabelle in einer Einschränkung (verweisen auf eine Tabelle nicht erstellt werden) nicht vorhanden war.|  
|42S11|Index ist bereits vorhanden.|\**StatementText* enthalten eine **CREATE INDEX** -Anweisung und der angegebene Indexname bereits vorhanden.|  
|42S12|Index wurde nicht gefunden|\**StatementText* enthalten eine **DROP INDEX** -Anweisung und der angegebene Indexname ist nicht vorhanden.|  
|42S21|Spalte ist bereits vorhanden.|\**StatementText* enthalten eine **ALTER TABLE** -Anweisung und die Spalte angegeben wird, der **hinzufügen** -Klausel ist nicht eindeutig oder eine vorhandene Spalte in der Basistabelle bezeichnet.|  
|42S22|Spalte wurde nicht gefunden.|\**StatementText* enthalten eine **CREATE INDEX** -Anweisung, und mindestens eine der Spalte in der Spaltenliste angegebene Namen ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **GRANT** oder **widerrufen** -Anweisung und einen Namen für die angegebene Spalte nicht vorhanden war.<br /><br /> \**StatementText* enthalten eine **wählen**, **löschen**, **einfügen**, oder **UPDATE** -Anweisung und eine angegebene Spaltenname ist nicht vorhanden.<br /><br /> \**StatementText* enthalten eine **CREATE TABLE** -Anweisung und eine Spalte in einer Einschränkung (verweisen auf eine Tabelle nicht erstellt werden) angegeben war nicht vorhanden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*, und klicken Sie dann die Funktion aufgerufen wurde erneut auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) *StatementText* wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese asynchronen Funktion wurde weiterhin ausgeführt, wenn die **SQLPrepare** Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) das Argument *TextLength* war kleiner oder gleich 0, aber nicht SQL_NTS gleich.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Einstellung für die Parallelität ist ungültig für den Typ des Cursors definiert.<br /><br /> SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festgelegt wurde, und das SQL_ATTR_CURSOR_TYPE-Anweisungsattribut auf einen Cursortyp, die für den der Treiber nicht Lesezeichen unterstützt festgelegt wurde.|  
|HYT00|Timeout abgelaufen|Das Timeout ist abgelaufen, bevor die Datenquelle über das Resultset zurückgegeben. Das Zeitlimit wird über festgelegt **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
## <a name="comments"></a>Kommentare  
 Ruft die Anwendung **SQLPrepare** zur Vorbereitung für die Datenquelle eine SQL-Anweisung an. Weitere Informationen über die vorbereitete Ausführung finden Sie unter [vorbereitete Ausführung](../../../odbc/reference/develop-app/prepared-execution-odbc.md). Die Anwendung kann eine oder mehrere parametermarkierungen in der SQL-Anweisung enthalten. Um eine parametermarkierung einzuschließen, bettet die Anwendung ein Fragezeichen (?) in der SQL-Zeichenfolge an der entsprechenden Position an. Weitere Informationen zu Parametern finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Wenn eine Anwendung verwendet **SQLPrepare** vorbereiten und **SQLExecute** beim Übermitteln einer **COMMIT** oder **ROLLBACK** -Anweisung ist nicht möglich Interoperabilität zwischen DBMS-Produkte. Rufen Sie einen commit oder Rollback für eine Transaktion, **SQLEndTran**.  
  
 Der Treiber kann die Anweisung aus, um verwenden Sie das Format von SQL Server, die von der Datenquelle verwendet, und senden Sie es dann an die Datenquelle für die Vorbereitung ändern. Insbesondere ändert der Treiber die Escapesequenzen, die zum Definieren von SQL-Syntax für bestimmte Funktionen verwendet. (Eine Beschreibung der SQL-Anweisung-Grammatik, finden Sie unter [Escapesequenzen in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) und [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Für den Treiber ähnelt einem Anweisungshandle Anweisungsbezeichner im eingebetteten SQL-Code. Wenn die Datenquelle Anweisung Bezeichner unterstützt, kann der Treiber Anweisungsbezeichner und Parameterwerte an die Datenquelle senden.  
  
 Nachdem eine Anweisung vorbereitet ist, verwendet die Anwendung das Anweisungshandle zum Verweisen auf die Anweisung in späteren Funktionsaufrufen. Die vorbereitete Anweisung, die das Anweisungshandle zugeordneten kann erneut ausgeführt werden, durch den Aufruf **SQLExecute** bis die Anwendung die Anweisung mit einem Aufruf von freigibt **SQLFreeStmt** mit der Option SQL_DROP oder bis das Anweisungshandle, in einem Aufruf von verwendet wird **SQLPrepare**, **SQLExecDirect**, mindestens die Katalogfunktionen (**SQLColumns**,  **SQLTables**usw.). Sobald die Anwendung eine Anweisung vorbereitet hat, können sie Informationen zum Format des Resultsets anfordern. Bei einigen Implementierungen Aufrufen **SQLDescribeCol** oder **SQLDescribeParam** nach **SQLPrepare** möglicherweise nicht so effizient wie das Aufrufen der Funktion nach **SQLExecute** oder **SQLExecDirect**.  
  
 Einige Treiber Syntaxfehler zurückgeben oder zugriffsverletzungen, wenn die Anwendung aufruft, können nicht **SQLPrepare**. Ein Treiber Syntaxfehler behandelt und Zugriff auf Verstöße gegen nur Syntaxfehler, oder Syntaxfehler weder zugriffsverletzungen. Daher muss eine Anwendung diese Bedingungen zu behandeln, bei nachfolgenden Aufrufen von Funktionen wie z. B. im Zusammenhang **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**, und **SQLExecute**.  
  
 Abhängig von den Funktionen des Treibers und der Datenquelle Parameterinformationen (z. B. Datentypen) kann überprüft werden, wenn die Anweisung vorbereitet ist (wenn alle Parameter gebunden wurden), oder wenn er ausgeführt wird (wenn nicht alle Parameter gebunden wurden). Für eine optimale Interoperabilität sollte eine Anwendung alle Parameter Aufheben der Bindung, die auf eine alte SQL-Anweisung vor der Vorbereitung einer neuen SQL­Anweisung in derselben Anweisung angewendet. Dies verhindert, dass Fehler, die aufgrund von alten Parameterinformationen für die neue Anweisung angewendet wird.  
  
> [!IMPORTANT]  
>  Ausführen eines Commits für eine Transaktion, entweder durch explizites Aufrufen **SQLEndTran** oder im Autocommit-Modus arbeiten, können dazu führen, dass die Datenquelle die Zugriffspläne für alle Anweisungen für eine Verbindung zu löschen. Weitere Informationen finden Sie unter den Informationstypen SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR in [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) und [Auswirkungen von Transaktionen für Cursor und vorbereitete Anweisungen](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), und [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Zuordnen eines Anweisungshandles|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Binden einen Puffer, an einen parameter|[SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ausführen eines Commit- oder Rollback-Vorgangs|[SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Die Anzahl der von einer Anweisung betroffenen Zeilen zurückgeben|[SQLRowCount-Funktion](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Ein Cursorname festlegen|[SQLSetCursorName-Funktion](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
