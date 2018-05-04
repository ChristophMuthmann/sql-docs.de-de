---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7074fcf6c6616c878b0cd4021aabb4359c2a40dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt das gemischte Cursormodell (keysetgesteuert/dynamisch) nicht. Der Versuch, die Keysetgröße mit SQL_ATTR_KEYSET_SIZE festzulegen, schlägt fehl, wenn der festgelegte Wert ungleich 0 (null) ist.  
  
 Die Anwendung legt SQL_ATTR_ROW_ARRAY_SIZE für alle Anweisungen, um die Anzahl der zurückgegebenen Zeilen zu deklarieren einer **SQLFetch** oder [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) Funktionsaufruf. Bei Anweisungen, die einen Servercursor angeben, verwendet der Treiber SQL_ATTR_ROW_ARRAY_SIZE, um die Größe des Zeilenblocks zu ermitteln, der vom Server als Reaktion auf eine Abrufanforderung des Cursors generiert wird. Innerhalb der Blockgröße eines dynamischen Cursors sind die Zeilenmitgliedschaft und -reihenfolge festgelegt, wenn die Isolationsstufe der Transaktion ausreichend ist, um wiederholbare Lesevorgänge von Transaktionen sicherzustellen, für die ein Commit ausgeführt wurde. Der Cursor ist außerhalb des von diesem Wert angegebenen Blocks vollkommen dynamisch. Die Blockgröße des Servercursors ist vollkommen dynamisch und kann zu jedem Zeitpunkt während der Abrufverarbeitung geändert werden.  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>'SQLSetStmtAttr' und Tabellenwertparameter  
 SQLSetStmtAttr kann verwendet werden, um SQL_SOPT_SS_PARAM_FOCUS im anwendungsparameterdeskriptor (APD) festzulegen, bevor auf deskriptorfelder für Tabellenwertparameter-Spalten.  
  
 Wenn versucht wird, legen Sie SQL_SOPT_SS_PARAM_FOCUS auf die Ordnungszahl für einen Parameter, d. h. ein nicht-Tabellenwertparameter, SQLSetStmtAttr gibt SQL_ERROR und ein Diagnosedatensatz mit SQLSTATE erstellt = HY024 und der Meldung "Ungültiger Attributwert". SQL_SOPT_SS_PARAM_FOCUS wird nicht geändert, wenn SQL_ERROR zurückgegeben wird.  
  
 Durch das Festlegen von SQL_SOPT_SS_PARAM_FOCUS auf 0 (null) wird der Zugriff auf Deskriptordatensätze für Parameter wiederhergestellt.  
  
 SQLSetStmtAttr kann auch zum Festlegen von SQL_SOPT_SS_NAME_SCOPE verwendet werden. Weitere Informationen finden Sie im Abschnitt zu SQL_SOPT_SS_NAME_SCOPE weiter unten in diesem Thema.  
  
 Weitere Informationen finden Sie unter [Tabellenwertparameter Parametermetadaten für vorbereitete Anweisungen](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>Unterstützung von 'SQLSetStmtAttr' für Spalten mit geringer Dichte  
 SQLSetStmtAttr kann zum Festlegen von SQL_SOPT_SS_NAME_SCOPE verwendet werden. Weitere Informationen finden Sie im Abschnitt SQL_SOPT_SS_NAME_SCOPE weiter unten in diesem Thema. Weitere Informationen zu Spalten mit geringer Dichte, finden Sie unter [Sparse Columns Support &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="statement-attributes"></a>Anweisungsattribute  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt auch die folgenden treiberspezifischen Anweisungsattribute.  
  
### <a name="sqlsoptsscursoroptions"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 Das SQL_SOPT_SS_CURSOR-Attribut gibt an, ob der Treiber treiberspezifische Leistungsoptionen für Cursor verwendet. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) ist nicht zulässig, wenn diese Optionen festgelegt werden. Die Standardeinstellung ist SQL_CO_OFF. Der *ValuePtr* -Wert ist vom Typ SQLLEN.  
  
|*ValuePtr* Wert|Description|  
|----------------------|-----------------|  
|SQL_CO_OFF|Standard. Deaktiviert schnelle Vorwärtscursor, schreibgeschützte Cursor und den automatischen Abruf, aktiviert die **SQLGetData** für Vorwärtscursor und schreibgeschützte Cursor. Wenn SQL_SOPT_SS_CURSOR_OPTIONS auf SQL_CO_OFF festgelegt ist, ändert sich der Cursortyp nicht. Das heißt, ein schneller Vorwärtscursor bleibt ein schneller Vorwärtscursor. Um den Cursortyp zu ändern, die Anwendung muss jetzt Festlegen eines anderen Cursor Typs unter Verwendung **SQLSetStmtAttr**/SQL_ATTR_CURSOR_TYPE.|  
|SQL_CO_FFO|Aktiviert schnelle Vorwärtscursor, schreibgeschützte Cursor und deaktiviert **SQLGetData** für Vorwärtscursor und schreibgeschützte Cursor.|  
|SQL_CO_AF|Aktiviert die automatische Abrufoption für jeden Cursortyp. Wenn diese Option, für ein Anweisungshandle festgelegt ist **SQLExecute** oder **SQLExecDirect** generiert einen impliziten **SQLFetchScroll** (SQL_FIRST). Der Cursor wird geöffnet, und der erste Batch Zeilen wird mit einem einzigen Roundtrip an den Server zurückgegeben.|  
|SQL_CO_FFO_AF|Aktiviert schnelle Vorwärtscursor mit der automatischen Abrufoption. Das entspricht der gleichzeitigen Angabe von SQL_CO_AF und SQL_CO_FFO.|  
  
 Wenn diese Optionen festgelegt sind, schließt der Server den Cursor automatisch, wenn er erkennt, dass die letzte Zeile abgerufen wurde. Die Anwendung muss trotzdem aufrufen [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) oder [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), aber der Treiber muss sich nicht in der schließen-Benachrichtigung an den Server gesendet.  
  
 Wenn die select-Liste enthält eine **Text**, **Ntext**, oder **Image** Spalte, die schnelle Vorwärtscursor in einen dynamischen Cursor konvertiert und **SQLGetData** ist zulässig.  
  
### <a name="sqlsoptssdeferprepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 Das SQL_SOPT_SS_DEFER_PREPARE-Attribut bestimmt, ob die Anweisung sofort vorbereitet oder, bis verzögert **SQLExecute**, [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) oder [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md) ausgeführt wird. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 und früheren Versionen wird diese Eigenschaft ignoriert (die Vorbereitung nicht verzögert). Der *ValuePtr* -Wert ist vom Typ SQLLEN.  
  
|*ValuePtr* Wert|Description|  
|----------------------|-----------------|  
|SQL_DP_ON|Standard. Nach dem Aufruf [SQLPrepare-Funktion](http://go.microsoft.com/fwlink/?LinkId=59360), die anweisungsvorbereitung verzögert, bis **SQLExecute** aufgerufen wird oder der metaeigenschaftsvorgang (**SQLDescribeCol** oder **SQLDescribeParam**) ausgeführt wird.|  
|SQL_DP_OFF|Die Anweisung wird vorbereitet, sobald **SQLPrepare** ausgeführt wird.|  
  
### <a name="sqlsoptssregionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 Das SQL_SOPT_SS_REGIONALIZE-Attribut wird verwendet, um die Datenkonvertierung auf Anweisungsebene zu bestimmen. Das Attribut bewirkt, dass der Treiber bei der Konvertierung von Datums-, Uhrzeit- und Währungswerten in Zeichenfolgen die Gebietsschemaeinstellung des Clients beachtet. Die Konvertierung erfolgt lediglich von systemeigenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen in Zeichenfolgen.  
  
 Der *ValuePtr* -Wert ist vom Typ SQLLEN.  
  
|*ValuePtr* Wert|Description|  
|----------------------|-----------------|  
|SQL_RE_OFF|Standard. Der Treiber konvertiert Datums-, Uhrzeit- und Währungsdaten nicht gemäß der Gebietsschemaeinstellung des Clients in Zeichenfolgendaten.|  
|SQL_RE_ON|Der Treiber konvertiert Datums-, Uhrzeit- und Währungsdaten gemäß der Gebietsschemaeinstellung des Clients in Zeichenfolgendaten.|  
  
 Regionale Konvertierungseinstellungen gelten für Währungs-, Zahlen-, Datums- und Uhrzeitdatentypen. Die Konvertierungseinstellungen gelten nur für Ausgabekonvertierungen, wenn Währungs-, Zahlen-, Datums- oder Uhrzeitwerte in Zeichenfolgen konvertiert werden.  
  
> [!NOTE]  
>  Wenn die SQL_SOPT_SS_REGIONALIZE-Anweisungsoption aktiviert ist, verwendet der Treiber die lokalen Registrierungseinstellungen für den aktuellen Benutzer. Der Treiber berücksichtigt das Gebietsschema des aktuellen Threads nicht, wenn die Anwendung es an, indem z. B. festlegt Aufrufen **SetThreadLocale**.  
  
 Das Verändern des regionalen Verhaltens einer Datenquelle kann Anwendungsfehler verursachen. Eine Anwendung, die Datumszeichenfolgen analysiert und erwartet, dass sie der ODBC-Definition entsprechen, wird durch die Änderung dieses Werts möglicherweise beeinträchtigt.  
  
### <a name="sqlsoptsstextptrlogging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 Das SQL_SOPT_SS_TEXTPTR_LOGGING-Attribut Schaltet zwischen der Protokollierung von Vorgängen für Spalten mit **Text** oder **Image** Daten. Der *ValuePtr* -Wert ist vom Typ SQLLEN.  
  
|*ValuePtr* Wert|Description|  
|----------------------|-----------------|  
|SQL_TL_OFF|Deaktiviert die Protokollierung der durchgeführten Operationen für **Text** und **Image** Daten.|  
|SQL_TL_ON|Standard. Aktiviert die Protokollierung der durchgeführten Operationen für **Text** und **Image** Daten.|  
  
### <a name="sqlsoptsshiddencolumns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 Das SQL_SOPT_SS_HIDDEN_COLUMNS-Attribut macht Spalten im Resultset verfügbar, die in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-SELECT FOR BROWSE-Anweisung verborgen sind. Der Treiber macht diese Spalten standardmäßig nicht verfügbar. Der *ValuePtr* -Wert ist vom Typ SQLLEN.  
  
|*ValuePtr* Wert|Description|  
|----------------------|-----------------|  
|SQL_HC_OFF|Standard. FOR BROWSE-Spalten werden aus dem Resultset ausgeblendet.|  
|SQL_HC_ON|Macht FOR BROWSE-Spalten verfügbar.|  
  
### <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 Das SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT-Attribut gibt den Meldungstext für die Abfragebenachrichtigungsanforderung zurück.  
  
### <a name="sqlsoptssquerynotificationoptions"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 Das SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS-Attribut gibt die Optionen an, die für die Abfragebenachrichtigungsanforderung verwendet werden. Diese werden in einer Zeichenfolge mit der Syntax `name=value` angegeben (siehe Code weiter unten). Die Anwendung ist für das Erstellen des Diensts und Lesen von Benachrichtigungen von der Warteschlange verantwortlich.  
  
 Die Syntax der Benachrichtigungen Optionen Abfragezeichenfolge lautet:  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 Beispiel:  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sqlsoptssquerynotificationtimeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 Das SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT-Attribut gibt die Dauer (in Sekunden) an, für die die Abfragebenachrichtigung aktiv bleiben soll. Der Standardwert lautet 432.000 Sekunden (5 Tage). Der *ValuePtr* -Wert ist vom Typ SQLLEN.  
  
### <a name="sqlsoptssparamfocus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 Das SQL_SOPT_SS_PARAM_FOCUS-Attribut gibt den Fokus für nachfolgende SQLBindParameter, SQLGetDescField, SQLSetDescField, SQLGetDescRec und SQLSetDescRec aufruft.  
  
 Der Typ für SQL_SOPT_SS_PARAM_FOCUS lautet SQLULEN.  
  
 Der Standardwert ist 0 (null). Das bedeutet, dass diese Aufrufe sich an Parameter richten, die Parametermarkierungen in der SQL-Anweisung entsprechen. Wenn diese Aufrufe auf die Parameternummer eines Tabellenwertparameters festgelegt sind, adressieren sie Spalten dieses Tabellenwertparameters. Wenn sie auf einen anderen Wert als die Parameternummer eines Tabellenwertparameters festgelegt sind, geben diese Aufrufe den Fehler IM020 zurück: "Parameterfokus verweist nicht auf einen Tabellenwertparameter."  
  
### <a name="sqlsoptssnamescope"></a>SQL_SOPT_SS_NAME_SCOPE  
 Das SQL_SOPT_SS_NAME_SCOPE-Attribut gibt den Namensbereich für nachfolgende Katalogfunktionsaufrufe an. Von SQLColumns zurückgegebene Resultset hängt von der Einstellung von SQL_SOPT_SS_NAME_SCOPE ab.  
  
 Der Typ für SQL_SOPT_SS_NAME_SCOPE lautet SQLULEN.  
  
|*ValuePtr* Wert|Description|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|Standard.<br /><br /> Gibt bei Verwendung von Tabellenwertparametern an, dass Metadaten für tatsächliche Tabellen zurückgegeben werden sollen.<br /><br /> Wenn Sie die Funktion für Spalten mit geringer Dichte verwenden, gibt SQLColumns nur Spalten, die nicht Mitglied mit geringer Dichte sind zurück **Column_set**.|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|Gibt an, dass die Anwendung Metadaten für einen Tabellentyp anstatt einer tatsächlichen Tabelle erfordert (Katalogfunktionen sollten Metadaten für Tabellentypen zurückgeben). Die Anwendung übergibt dann den TYPE_NAME des Tabellenwertparameters als die *TableName* Parameter.|  
|SQL_SS_NAME_SCOPE_EXTENDED|Wenn Sie die Funktion für Spalten mit geringer Dichte verwenden, gibt SQLColumns alle Spalten, unabhängig von **Column_set** Mitgliedschaft.|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|Wenn Sie die Funktion für Spalten mit geringer Dichte verwenden, SQLColumns nur Spalten zurückgegeben, die Elemente mit geringer Dichte **Column_set**.|  
|SQL_SS_NAME_SCOPE_DEFAULT|Identisch mit SQL_SS_NAME_SCOPE_TABLE|  
  
 SS_TYPE_CATALOG_NAME und SS_TYPE_SCHEMA_NAME wird mit der *CatalogName* und *SchemaName* Parameter, um den Katalog und das Schema für den Tabellenwertparameter zu identifizieren. Wenn eine Anwendung das Abrufen von Metadaten für Tabellenwertparameter abgeschlossen hat, muss sie SQL_SOPT_SS_NAME_SCOPE wieder auf den Standardwert SQL_SS_NAME_SCOPE_TABLE festlegen.  
  
 Wenn SQL_SOPT_SS_NAME_SCOPE auf SQL_SS_NAME_SCOPE_TABLE festgelegt ist, schlagen Abfragen von Verbindungsservern fehl. Aufrufen von SQLColumns oder SQLPrimaryKeys mit einem Katalog, der eine Serverkomponente enthält, schlägt fehl.  
  
 Wenn Sie versuchen, SQL_SOPT_SS_NAME_SCOPE auf einen ungültigen Wert festzulegen, wird SQL_ERROR zurückgegeben. Zudem wird ein Diagnosedatensatz mit SQLSTATE HY024 und der Meldung "Ungültiger Attributwert" generiert.  
  
 Wenn ein Katalog anderen Funktion dann SQLTables, SQLColumns oder SQLPrimaryKeys aufgerufen wird, wenn SQL_SOPT_SS_NAME_SCOPE einen Wert enthält, die andere als SQL_SS_NAME_SCOPE_TABLE, wird SQL_ERROR zurückgegeben. Ein Diagnosedatensatz mit SQLSTATE HY010 und der Meldung "Fehler in der Funktionsreihenfolge (SQL_SOPT_SS_NAME_SCOPE ist nicht auf SQL_SS_NAME_SCOPE_TABLE festgelegt)" wird generiert.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLGetStmtAttr-Funktion](http://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
