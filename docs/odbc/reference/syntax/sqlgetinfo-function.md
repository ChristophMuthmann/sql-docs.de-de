---
title: SQLGetInfo-Funktion | Microsoft Docs
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
apiname: SQLGetInfo
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetInfo
helpviewer_keywords: SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
caps.latest.revision: "48"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 36682d5e3da85928a02a1315f8268b12630f31f0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetInfo** Gibt allgemeine Informationen zu den Treiber und die Datenquelle eine Verbindung zugeordnet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *Infotyp*  
 [Eingabe] Die Art der Informationen.  
  
 *InfoValuePtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem die Informationen zurückgegeben werden sollen. Je nach der *Infotyp* angefordert, die zurückgegebenen Informationen werden die folgenden: ein Null-terminierte Zeichenfolge, einen SQLUSMALLINT-Wert, eine SQLUINTEGER-Bitmaske, eine SQLUINTEGER-Flag, eine SQLUINTEGER-Binärwert oder eine SQLULEN-Wert.  
  
 Wenn die *Infotyp* Argument ist SQL_DRIVER_HDESC oder SQL_DRIVER_HSTMT, die *InfoValuePtr* Argument ist sowohl für ein- und Ausgabe. (Siehe die Deskriptoren SQL_DRIVER_HDESC oder SQL_DRIVER_HSTMT weiter unten in diesem funktionsbeschreibung für Weitere Informationen.)  
  
 Wenn *InfoValuePtr* NULL ist, *StringLengthPtr* gibt weiterhin zurück, die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) verfügbaren zurückzugebenden im Puffer verweist *InfoValuePtr*.  
  
 *Pufferlänge*  
 [Eingabe] Länge der \* *InfoValuePtr* Puffer. Wenn der Wert in  *\*InfoValuePtr* ist eine Zeichenfolge oder, wenn *InfoValuePtr* ist ein null-Zeiger der *Pufferlänge* Argument wird ignoriert. Der Treiber setzt voraus, dass die Größe des  *\*InfoValuePtr* ist SQLUSMALLINT oder SQLUINTEGER, basierend auf den *Infotyp*. Wenn  *\*InfoValuePtr* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLGetInfoW**), wird die *Pufferlänge* Argument muss eine gerade Zahl; Wenn nicht, SQLSTATE HY090 () Ungültige Zeichenfolgen- oder Pufferlänge) wird zurückgegeben.  
  
 *StringLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) zurückgegeben zur Rückgabe in **InfoValuePtr*.  
  
 Bei Zeichendaten ist die Anzahl der zurückzugebenden verfügbaren Bytes größer als oder gleich *Pufferlänge*, die Informationen in \* *InfoValuePtr* auf abgeschnitten  *Pufferlänge* Bytes abzüglich der Länge des ein Null-Terminierung Zeichen und endet auf Null vom Treiber.  
  
 Für alle anderen Typen von Daten, den Wert der *Pufferlänge* wird ignoriert, und der Treiber geht davon aus, die Größe des \* *InfoValuePtr* SQLUSMALLINT oder SQLUINTEGER, ist abhängig von der  *Infotyp*.  
  
## <a name="return-value"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetInfo** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_DBC und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLGetInfo** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *InfoValuePtr* war nicht groß genug, um die angeforderten Informationen zurückzugeben. Aus diesem Grund wurden die Daten abgeschnitten. Die Länge der angeforderten Informationen in den ungekürzten Format wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08003|Verbindung nicht geöffnet|(DM) in der Typ der Informationen angefordert *Infotyp* ist eine geöffnete Verbindung erforderlich. Reservierte ODBC Informationen Typ kann nur SQL_ODBC_VER ohne eine offene Verbindung zurückgegeben werden.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY010|Fehler bei Funktionssequenz|(DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY024|Ungültiger Attributwert|(DM) die *Infotyp* Argument wurde SQL_DRIVER_HSTMT und der Wert verweist *InfoValuePtr* war keinem gültigen Anweisungshandle.<br /><br /> (DM) die *Infotyp* Argument wurde SQL_DRIVER_HDESC und der Wert verweist *InfoValuePtr* war keinem gültigen Deskriptorhandles.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *Pufferlänge* war kleiner als 0.<br /><br /> (DM) der angegebene Wert für *Pufferlänge* wurde eine ungerade Anzahl und  *\*InfoValuePtr* wurde von einem Unicode-Datentyp.|  
|HY096|Informationstyp außerhalb des gültigen Bereichs|Der Wert für das Argument angegebene *Infotyp* war für die vom Treiber unterstützten ODBC-Version ungültig.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feld, die nicht implementiert.|Der Wert für das Argument angegebene *Infotyp* wurde ein treiberspezifische-Wert, der vom Treiber nicht unterstützt wird.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber, die entspricht der *Verbindungshandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Die aktuell definierten Datentypen werden in "Informationstypen" weiter unten in diesem Abschnitt; angezeigt. Es wird erwartet, dass mehr Daten von verschiedenen Datenquellen nutzen möchten definiert werden. ODBC ist eine Palette von Informationstypen reserviert. Entwickler müssen Werte für die eigene Verwendung treiberspezifische von Open Group reservieren. **SQLGetInfo** führt keine Unicode-Konvertierung oder *thunking* (finden Sie unter [Anhang A: ODBC-Fehlercodes](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) von der *ODBC Programmer's Reference*) für treiberdefinierten *Infotypen*. Weitere Informationen finden Sie unter [Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnosetypen und Attribute](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md). Das Format des zurückgegebenen Informationen \* *InfoValuePtr* richtet sich nach der *Infotyp* angefordert. **SQLGetInfo** Informationen in einem der fünf verschiedenen Formaten zurück:  
  
-   Eine Null-terminierte Zeichenfolge  
  
-   Ein Wert SQLUSMALLINT  
  
-   Eine Bitmaske SQLUINTEGER  
  
-   Eine SQLUINTEGER-Wert  
  
-   Ein Binärwert SQLUINTEGER  
  
 Das Format der einzelnen die folgenden Typen von Informationen wird in der Beschreibung des Typs aufgeführt. Die Anwendung muss den zurückgegebenen Wert umgewandelt **InfoValuePtr* entsprechend. Ein Beispiel dafür, wie eine Anwendung Daten von einer Bitmaske SQLUINTEGER abgerufen werden konnten finden Sie unter "Codebeispiel".  
  
 Ein Treiber muss es sich um einen Wert für jeden Datentyp zurückgeben, die in den folgenden Tabellen definiert ist. Wenn ein Informationstyp dem Treiber oder die Datenquelle nicht anwendbar ist, gibt der Treiber einen der in der folgenden Tabelle aufgeführten Werte zurück.  
  
 Zeichenfolge ("Y" oder "N")  
 "N"  
  
 Zeichenfolge (nicht "Y" oder "N")  
 Leere Zeichenfolge  
  
 SQLUSMALLINT  
 0  
  
 SQLUINTEGER Bitmaske oder SQLUINTEGER Binärwert  
 0L  
  
 Angenommen, eine Datenquelle Prozeduren nicht unterstützt **SQLGetInfo** gibt in der folgenden Tabelle werden die Werte der aufgelisteten Werte *Infotyp* , beziehen sich auf Verfahren.  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 Leere Zeichenfolge  
  
 **SQLGetInfo** SQLSTATE HY096 zurückgibt (Ungültiger Argumentwert) für Werte des *Infotyp* , die im Bereich von Typen von Informationen für die Verwendung von ODBC reserviert sind, jedoch nicht von der Version von ODBC, die vom Treiber unterstützten definiert sind. Um zu bestimmen, welche Version der ODBC-Treiber entspricht, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_DRIVER_ODBC_VER-Informationen. **SQLGetInfo** SQLSTATE HYC00 zurückgibt (optionales Feature nicht implementiert) für die Werte der *Infotyp* , die im Bereich von Typen von Informationen für die Verwendung von treiberspezifischen reserviert sind, jedoch werden vom Treiber nicht unterstützt.  
  
 Alle Aufrufe an **SQLGetInfo** offene Verbindung notwendig, außer wenn die *Infotyp* SQL_ODBC_VER, der die Version der Treiber-Manager zurückgegeben wird.  
  
## <a name="information-types"></a>Typen von Informationen  
 In diesem Abschnitt listet die Typen von Informationen von unterstützten **SQLGetInfo**. Typen von Informationen sind kategorisch gruppiert und alphabetisch aufgeführt. Typen von Informationen, die hinzugefügt oder ODBC 3. umbenannt wurden*.x* sind ebenfalls aufgeführt.  
  
## <a name="driver-information"></a>Treiberinformationen  
 Die folgenden Werte für die *Infotyp* Argument Zurückgeben von Informationen zu den ODBC-Treiber, wie z. B. die Anzahl der aktiven Anweisungen der Datenquellenname und die Kompatibilitätsstufe aus Schnittstelle Standards:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
>  Bei der Implementierung **SQLGetInfo**, ein Treiber kann die Leistung verbessern, minimiert die Anzahl der Fälle, in denen Informationen gesendet bzw. vom Server angefordert.  
  
## <a name="dbms-product-information"></a>DBMS-Produktinformationen  
 Die folgenden Werte für die *Infotyp* Argument Zurückgeben von Informationen zu dem DBMS-Produkt, z. B. DBMS-Name und Version:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>Datenquelleninformationen  
 Die folgenden Werte für die *Infotyp* Argument Zurückgeben von Informationen über die Datenquelle, z. B. der Cursormerkmale und Transaktionsfunktionen:  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>Unterstützte SQL  
 Die folgenden Werte für die *Infotyp* Argument Zurückgeben von Informationen zu den SQL-Anweisungen, die von der Datenquelle unterstützt. Die SQL-Syntax der einzelnen Funktionen beschrieben, die von diesen Typen von Informationen ist die SQL-92-Syntax. Diese Typen von Informationen werden die gesamte SQL-92-Grammatik nicht ausführlich beschrieben. Stattdessen wird die Teile der Grammatik für welche, die Daten verschiedene Ebenen der Unterstützung von Quellen in der Regel bieten beschrieben. Insbesondere werden die meisten der DDL-Anweisung im SQL-92 behandelt.  
  
 Anwendungen sollten bestimmen den allgemeinen Umfang der unterstützten Grammatik aus den Informationstyp SQL_SQL_CONFORMANCE und mit den anderen Informationstypen, Variationen aus die Kompatibilitätsstufe genannten Standards.  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>Einschränkungen für SQL  
 Die folgenden Werte für die *Infotyp* Argument Zurückgeben von Informationen zu den Grenzwerten für IDs und Klauseln in der SQL-Anweisungen, wie z. B. die maximale Länge von IDs und die maximale Anzahl der Spalten in einer select-Liste angewendet. Durch den Treiber oder die Datenquelle können Einschränkungen auferlegt werden.  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>Skalarfunktion-Informationen  
 Die folgenden Werte für die *Infotyp* Argument Zurückgeben von Informationen zu den skalaren Funktionen, die von der Datenquelle und der Treiber unterstützt werden. Weitere Informationen zu Skalarfunktionen, finden Sie unter [Anhang E: Skalarfunktionen](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>Konvertierungsinformationen  
 Die folgenden Werte von der *Infotyp* Argument Zurückgeben einer Liste der SQL-Datentypen, die Datenquelle mit der angegebenen SQL-Datentyp konvertieren kann, die **konvertieren** skalare Funktion:  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>Typen von Informationen hinzugefügt, für ODBC 3.x  
 Die folgenden Werte für die *Infotyp* Argument wurde für ODBC 3.*.x*:  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>Typen von Informationen umbenannt für ODBC 3.x  
 Die folgenden Werte für die *Infotyp* Argument wurde für ODBC 3. umbenannt*.x*.  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>Typen von Informationen veraltetes Feature in ODBC 3.x  
 Die folgenden Werte für die *Infotyp* Argument sind veraltet in ODBC 3.*.x*. ODBC 3.*.x* Treiber müssen weiterhin unterstützen diese Typen von Informationen zur Abwärtskompatibilität mit ODBC 2.*.x* Anwendungen. (Weitere Informationen zu diesen Projekttypen finden Sie unter [SQLGetInfo Unterstützung](../../../odbc/reference/appendixes/sqlgetinfo-support.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>Eine Beschreibung der Art von Informationen  
 In der folgenden Tabelle sind in alphabetischer Reihenfolge aufgeführt, jeder Informationstyp muss die Version des ODBC-eingeführt wurde und dessen Beschreibung.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn der Benutzer alle Prozeduren zurückgegebenes ausführen kann **SQLProcedures**; "N", wenn Prozeduren möglicherweise zurückgegeben, dass der Benutzer ausführen kann.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn der Benutzer **wählen** Berechtigungen, um alle Tabellen zurückgegebenes **SQLTables**; "N", wenn es möglicherweise Tabellen zurückgegeben, dass der Benutzer zugreifen kann.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl von aktiven Umgebungen angibt, die der Treiber unterstützt werden. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Unterstützung für Aggregationsfunktionen:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber werden immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ALTER DOMAIN** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt. Ein vollständige SQL-92-Ebene – kompatibler Treiber wird immer alle Bitmasken zurückgegeben. Ein Rückgabewert von "0" bedeutet, dass die **ALTER DOMAIN** Anweisung wird nicht unterstützt.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = hinzufügen, die eine Einschränkung für die Domäne unterstützt wird (vollständige Ebene)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<Domäne alter > \<Set Domain Default-Klausel > wird unterstützt (vollständige Ebene)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<Definition von Einschränkungsklausel-Name > wird unterstützt, für die Benennung von Domäne Einschränkung (Intermediate-Stufe)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<Drop Domäne Constraint-Klausel > wird unterstützt (vollständige Ebene)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<Domäne alter > \<Drop Domain Default-Klausel > wird unterstützt (vollständige Ebene)  
  
 Geben Sie die folgenden Bits unterstützten \<Einschränkung Attribute > Wenn \<Domäne-Einschränkung hinzufügen > unterstützt wird (das SQL_AD_ADD_DOMAIN_CONSTRAINT Bit festgelegt ist):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (vollständige Stufe) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (vollständige Stufe) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (vollständige Stufe) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (vollständige Stufe)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ALTER TABLE** Anweisung, die von der Datenquelle unterstützt.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<Spalte hinzufügen >-Klausel unterstützt wird, mit der Funktion Spaltensortierreihenfolge (vollständige Stufe) angeben (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<Spalte hinzufügen >-Klausel unterstützt wird, mit der Einrichtung von spaltenstandards (FIPS Transitional Stufe) angeben (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<Spalte hinzufügen > ist (FIPS Transitional Stufe) unterstützt (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<Spalte hinzufügen >-Klausel unterstützt wird, mit der Funktion spalteneinschränkungen (FIPS Transitional Stufe) angeben (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<tabelleneinschränkung hinzufügen >-Klausel unterstützt (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<Einschränkungsdefinition-Name > ist für die Benennung von Spalten- und tabelleneinschränkungen (Intermediate-Stufe) unterstützt (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<Drop Spalte > CASCADE unterstützt wird (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<Spalte alter > \<Drop Column-Standard-Klausel > ist (Intermediate-Stufe) unterstützt (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<Drop Spalte > RESTRICT unterstützt wird (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<Drop Spalte > RESTRICT unterstützt wird (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<Spalte alter > \<Satz Spalte Default-Klausel > ist (Intermediate-Stufe) unterstützt (ODBC 3.0)  
  
 Geben Sie die folgenden Bits die Unterstützung \<Einschränkung Attribute > Wenn das Angeben von Spalten- oder tabelleneinschränkungen unterstützt wird (das SQL_AT_ADD_CONSTRAINT Bit festgelegt ist):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (vollständige Stufe) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (vollständige Stufe) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (vollständige Stufe) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (vollständige Stufe) (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 Eine SQLUINTEGER-Wert, der angibt, ob der Treiber Funktionen asynchron auf dem Verbindungshandle ausgeführt werden kann.  
  
 SQL_ASYNC_DBC_CAPABLE = der Treiber Verbindungsfunktionen asynchron ausführen.  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = der Treiber kann nicht ausgeführt werden Verbindungsfunktionen asynchron.  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der die Ebene der asynchrone Unterstützung im Treiber angibt:  
  
 SQL_AM_CONNECTION = Verbindung zum Servicelevel asynchrone Ausführung wird unterstützt. Alle Anweisungshandle eines bestimmten Verbindungshandles zugeordnet sind, im asynchronen Modus oder im synchronen Modus sind. Ein Anweisungshandle für eine Verbindung darf nicht im asynchronen Modus sein, während ein anderes Anweisungshandle über dieselbe Verbindung im synchronen Modus (und umgekehrt) ist.  
  
 SQL_AM_STATEMENT =-Anweisung Ebene asynchrone Ausführung wird unterstützt. Im asynchronen Modus können einige Anweisungshandle eines Verbindungshandles zugeordnet sein, während andere Anweisungshandles auf die gleiche Verbindung im synchronen Modus sind.  
  
 SQL_AM_NONE = asynchrone Modus wird nicht unterstützt.  
  
 SQL_ASYNC_NOTIFICATION  
 Eine SQLUINTEGER-Wert, der angibt, ob der Treiber die asynchrone Benachrichtigung unterstützt:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE** asynchrone Ausführung Benachrichtigung wird vom Treiber unterstützt.  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE** asynchrone Ausführung Benachrichtigung wird vom Treiber nicht unterstützt.  
  
 Es gibt zwei Kategorien von asynchronen Vorgängen ODBC: Verbindung Ebene asynchrone Vorgänge und Anweisung Ebene asynchrone Vorgänge.  Wenn ein Treiber SQL_ASYNC_NOTIFICATION_CAPABLE zurückgibt, muss es Benachrichtigung für alle APIs unterstützen, die asynchron ausgeführt werden kann.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die das Verhalten des Treibers in Bezug auf die Verfügbarkeit der Zeile listet zählt. Die folgenden Bitmasken werden zusammen mit der Typ der Informationen verwendet:  
  
 SQL_BRC_ROLLED_UP = Zeilenanzahl für aufeinander folgende INSERT-, DELETE- oder UPDATE-Anweisungen in einem Rollup enthalten sind. Wenn dieses Bit nicht festgelegt ist, sind die Zeilenanzahl für jede Anweisung verfügbar.  
  
 SQL_BRC_PROCEDURES = Zeilenanzahl, falls vorhanden, sind verfügbar, wenn ein Batch in einer gespeicherten Prozedur ausgeführt wird. Wenn Zeilenanzahl verfügbar sind, können sie nach oben oder einzeln erhältlich, je nach den SQL_BRC_ROLLED_UP Bit rückgängig gemacht werden.  
  
 SQL_BRC_EXPLICIT = Zeilenanzahl, falls vorhanden, sind verfügbar, wenn ein Batch ausgeführt wird, direkt durch Aufrufen **SQLExecute** oder **SQLExecDirect**. Wenn Zeilenanzahl verfügbar sind, können sie nach oben oder einzeln erhältlich, je nach den SQL_BRC_ROLLED_UP Bit rückgängig gemacht werden.  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die treiberunterstützung für Batches auflisten. Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Ebene unterstützt wird:  
  
 SQL_BS_SELECT_EXPLICIT = der Treiber unterstützt explizite Batches, die Resultsets können haben Anweisungen generieren.  
  
 SQL_BS_ROW_COUNT_EXPLICIT = der Treiber unterstützt explizite Batches, die Anzahl der Zeilen Generieren von Anweisungen haben kann.  
  
 SQL_BS_SELECT_PROC = die Treiber unterstützt explizite Prozeduren, die Resultsets können haben Anweisungen generieren.  
  
 SQL_BS_ROW_COUNT_PROC = der Treiber unterstützt explizite Prozeduren, die Zeilenanzahl Generieren von Anweisungen haben können.  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Vorgänge, die über denen Lesezeichen beibehalten werden.  
  
 Die folgenden Bitmasken werden zusammen mit dem Flag verwendet, um zu bestimmen, über die Optionen Lesezeichen beibehalten:  
  
 SQL_BP_CLOSE = Lesezeichen sind gültig, nachdem eine Anwendung ruft **SQLFreeStmt** mit der Option SQL_CLOSE oder **SQLCloseCursor** Schließen des Cursors eine Anweisung zugeordnet.  
  
 SQL_BP_DELETE = das Lesezeichen für eine Zeile gültig ist, nachdem diese Zeile gelöscht wurde.  
  
 SQL_BP_DROP = Lesezeichen sind gültig, nachdem eine Anwendung ruft **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_STMT auf, um eine Anweisung zu löschen.  
  
 SQL_BP_TRANSACTION = Lesezeichen sind gültig, nachdem eine Anwendung ein Commit oder Rollback einer Transaktion.  
  
 SQL_BP_UPDATE = das Lesezeichen für eine Zeile gültig ist, nachdem eine Spalte in dieser Zeile aktualisiert wurde, einschließlich Schlüsselspalten.  
  
 SQL_BP_OTHER_HSTMT = ein Lesezeichen einer zugeordneten Anweisung kann in einer anderen Anweisung verwendet werden. Es sei denn, SQL_BP_CLOSE oder SQL_BP_DROP angegeben ist, muss der Cursor auf die erste Anweisung geöffnet sein.  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der die Position des Katalogs in einem qualifizierten Tabellennamen angibt:  
  
 SQL_CL_STARTSQL_CL_END  
  
 Xbase-Treiber gibt beispielsweise SQL_CL_START zurück, da der Name des Verzeichnisses (Katalog) am Anfang der Tabellenname, wie in \EMPDATA\EMP ist. DBF. Ein ORACLE-Server-Treiber gibt SQL_CL_END zurück, da es sich bei der Katalog am Ende der Tabellenname ist, wie in ADMIN.EMP@EMPDATA.  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird SQL_CL_START immer zurückgegeben werden. Der Wert 0 wird zurückgegeben, wenn Kataloge nicht von der Datenquelle unterstützt werden. Um zu bestimmen, ob Kataloge unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_CATALOG_NAME-Informationen.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_QUALIFIER_LOCATION.  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 Eine Zeichenfolge: "Y", wenn der Server Katalognamen oder "N" unterstützt, wenn dies nicht der Fall.  
  
 Ein vollständige SQL-92-Ebene – konforme-Treiber gibt immer "Y" zurück.  
  
 SQL_CATALOG_NAME_SEPARATOR (ODBC 1.0)  
 Eine Zeichenfolge: das Zeichen oder Zeichen, die die Datenquelle definiert wird, als Trennzeichen zwischen einen Katalognamen und den qualifizierten Namen-Element, das folgt, oder er vorangestellt ist.  
  
 Wenn Kataloge nicht von der Datenquelle unterstützt werden, wird eine leere Zeichenfolge zurückgegeben. Um zu bestimmen, ob Kataloge unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_CATALOG_NAME-Informationen. Ein vollständige SQL-92-Ebene – konforme-Treiber gibt stets ".".  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_QUALIFIER_NAME_SEPARATOR.  
  
 SQL_CATALOG_TERM (ODBC 1.0)  
 Eine Zeichenfolge mit der Quelle-Herstellers Namen für einen Katalog; "Datenbank" oder "Directory fest". Diese Zeichenfolge kann oberen, unteren oder mixed sein.  
  
 Wenn Kataloge nicht von der Datenquelle unterstützt werden, wird eine leere Zeichenfolge zurückgegeben. Um zu bestimmen, ob Kataloge unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_CATALOG_NAME-Informationen. Ein vollständige SQL-92-Ebene – konforme-Treiber gibt immer "Catalog" zurück.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_QUALIFIER_TERM.  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Anweisungen in denen Kataloge verwendet werden können.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, wo die Kataloge verwendet werden können:  
  
 SQL_CU_DML_STATEMENTS = Volltextkataloge werden in allen Data Manipulation Language-Anweisungen unterstützt: **wählen**, **einfügen**, **UPDATE**, **DELETE**, und falls unterstützt, **für aktualisieren wählen** und positioniert Update und delete-Anweisungen.  
  
 SQL_CU_PROCEDURE_INVOCATION = Volltextkataloge werden in der ODBC-Prozedur aufrufanweisung unterstützt.  
  
 SQL_CU_TABLE_DEFINITION = Volltextkataloge werden in alle Table-Anweisungen Definition unterstützt: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, **DROP TABLE** , und **DROP VIEW**.  
  
 SQL_CU_INDEX_DEFINITION = Volltextkataloge werden in alle indexanweisungen Definition unterstützt: **CREATE INDEX** und **DROP INDEX**.  
  
 SQL_CU_PRIVILEGE_DEFINITION = Volltextkataloge werden in alle Berechtigungen datendefinitionsanweisungen unterstützt: **GRANT** und **widerrufen**.  
  
 Der Wert 0 wird zurückgegeben, wenn Kataloge nicht von der Datenquelle unterstützt werden. Um zu bestimmen, ob Kataloge unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_CATALOG_NAME-Informationen. Ein vollständige SQL-92-Ebene – konforme-Treiber gibt immer eine Bitmaske mit allen diesen festgelegten Bits zurück.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_QUALIFIER_USAGE.  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 Der Name der Sortierung Sequenz. Dies ist eine Zeichenfolge, die den Namen der standardsortierung für den Standardzeichensatz für diesen Server angibt (z. B. "ISO 8859-1" oder EBCDIC). Wenn dies unbekannt ist, wird eine leere Zeichenfolge zurückgegeben. Ein vollständige SQL-92-Ebene – konforme Treiber wird immer eine leere Zeichenfolge zurückgegeben.  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle Spaltenaliase; unterstützt. andernfalls, "N".  
  
 Ein Spaltenalias ist ein alternativer Name, der für eine Spalte in der select-Liste mit einer AS-Klausel angegeben werden kann. Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt immer "Y" zurück.  
  
 SQL_CONCAT_NULL_BEHAVIOR (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der angibt, wie die Datenquelle für die Verkettung von NULL behandelt Werten Zeichendatenspalten mit Werten ungleich NULL-Zeichen-datentypspalten:  
  
 SQL_CB_NULL = Ergebnis NULL-Werten ist.  
  
 SQL_CB_NON_NULL = Ergebnis ist die Verkettung von Werten ungleich NULL-Spalte oder Spalten.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer SQL_CB_NULL zurückgegeben.  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_ DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 Eine Bitmaske SQLUINTEGER. Die Bitmaske, die angibt, der von der Datenquelle mit unterstützten Konvertierungen der **konvertieren** Skalarfunktion für Daten des Typs mit dem Namen der *Infotyp*. Wenn die Bitmaske gleich 0 (null) ist, ist die Datenquelle eine Konvertierung von Daten eines benannten Typs, einschließlich der Konvertierung in den gleichen Datentyp nicht unterstützt.  
  
 Um festzustellen, ob eine Datenquelle die Konvertierung von SQL_INTEGER Daten in den Datentyp SQL_BIGINT unterstützt, z. B. eine Anwendung ruft **SQLGetInfo** mit der *Infotyp* von SQL_CONVERT_INTEGER. Die Anwendung führt eine **AND** Vorgang mit dem zurückgegebene Bitmaske und SQL_CVT_BIGINT. Wenn der resultierende Wert ungleich NULL ist, wird die Konvertierung unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Konvertierungen unterstützt werden:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL _CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_ ZEITSTEMPEL (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS (ODBC 1.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der skalaren Konvertierungsfunktionen, die vom Treiber und zugeordneten Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Funktionen für die typkonvertierung unterstützt werden:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der angibt, ob abhängige Tabellennamen unterstützt werden:  
  
 SQL_CN_NONE = Korrelation Namen werden nicht unterstützt.  
  
 SQL_CN_DIFFERENT = Korrelation Namen werden unterstützt, jedoch müssen unterscheiden sich die Namen der Tabellen, die sie darstellen.  
  
 SQL_CN_ANY = Korrelation Namen werden unterstützt und können einen beliebigen gültigen benutzerdefinierten Namen.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer SQL_CN_ANY zurückgegeben.  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **erstellen ASSERTION** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CA_CREATE_ASSERTION  
  
 Die folgenden Bits das unterstützten Einschränkung-Attribut angeben, wenn die Möglichkeit, Einschränkung Attribute explizit anzugeben unterstützt wird (siehe die Informationstypen SQL_ALTER_TABLE und SQL_CREATE_TABLE):  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt. Ein Rückgabewert von "0" bedeutet, dass die **erstellen ASSERTION** Anweisung wird nicht unterstützt.  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ZEICHENSATZ erstellen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt. Ein Rückgabewert von "0" bedeutet, dass die **ZEICHENSATZ erstellen** Anweisung wird nicht unterstützt.  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **SORTIERUNG erstellen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 Diese Option wird ein vollständige SQL-92-Ebene – konforme Treiber wie unterstützt immer zurückgegeben werden. Ein Rückgabewert von "0" bedeutet, dass die **SORTIERUNG erstellen** Anweisung wird nicht unterstützt.  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **Domäne erstellen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CDO_CREATE_DOMAIN = der erstellen-DOMAIN-Anweisung unterstützt wird (Intermediate-Stufe).  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<Einschränkungsdefinition-Name > für die Benennung von Beschränkungen (Intermediate-Stufe) unterstützt wird.  
  
 Die folgenden Bits Geben Sie die Fähigkeit zum Erstellen der Spalte Constraints: SQL_CDO_DEFAULT = angeben von Einschränkungen der Domäne unterstützt wird (Intermediate-Stufe) SQL_CDO_CONSTRAINT = angeben von Standardwerten Domäne unterstützt wird (Intermediate-Stufe) SQL_CDO_COLLATION = Angeben der Domäne Sortierung wird unterstützt (vollständige Ebene)  
  
 Die folgenden Bits der unterstützten Einschränkung-Attribute angeben, wenn angeben von Einschränkungen der Domäne unterstützt wird (SQL_CDO_DEFAULT festgelegt ist):  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (vollständige Stufe) SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (vollständige Stufe) SQL_CDO_CONSTRAINT_DEFERRABLE (vollständige Stufe) SQL_CDO_CONSTRAINT_NON_DEFERRABLE (vollständige Stufe)  
  
 Ein Rückgabewert von "0" bedeutet, dass die **Domäne erstellen** Anweisung wird nicht unterstützt.  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **CREATE SCHEMA** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 Ein SQL-92-Intermediate-Ebene – konforme Treiber wird immer die Optionen SQL_CS_CREATE_SCHEMA und SQL_CS_AUTHORIZATION unterstützt zurückgegeben. Diese müssen außerdem auf der Ebene der SQL-92-Eintrag, jedoch nicht notwendigerweise als SQL-Anweisungen unterstützt werden. Ein vollständige SQL-92-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **CREATE TABLE** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CT_CREATE_TABLE = die CREATE TABLE-Anweisung wird unterstützt. (Entry Level)  
  
 SQL_CT_TABLE_CONSTRAINT = das Angeben von tabelleneinschränkungen unterstützt wird (FIPS Transitional Stufe)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION = die \<Einschränkungsdefinition-Name >-Klausel wird für die Benennung von Spalten- und tabelleneinschränkungen (Intermediate-Stufe) unterstützt.  
  
 Die folgenden Bits Geben Sie die Möglichkeit zum Erstellen von temporären Tabellen:  
  
 SQL_CT_COMMIT_PRESERVE = der gelöschte Zeilen werden nach dem Commit beibehalten. (Vollständige Stufe) SQL_CT_COMMIT_DELETE = der gelöschte Zeilen werden nach dem Commit gelöscht. (Vollständige Stufe) SQL_CT_GLOBAL_TEMPORARY = globale temporäre Tabellen erstellt werden können. (Vollständige Stufe) SQL_CT_LOCAL_TEMPORARY = lokale temporäre Tabellen erstellt werden können. (Vollständige Stufe)  
  
 Die folgenden Bits Geben Sie die Möglichkeit zum Erstellen von spalteneinschränkungen:  
  
 SQL_CT_COLUMN_CONSTRAINT = angeben spalteneinschränkungen unterstützt wird (FIPS Transitional Stufe) SQL_CT_COLUMN_DEFAULT = angeben von Standardwerten für Spalten unterstützt wird (FIPS Transitional Stufe) SQL_CT_COLUMN_COLLATION = spaltensortierung angegeben ist unterstützt (vollständige Stufe)  
  
 Die folgenden Bits geben die unterstützten Einschränkung Attribute aus, wenn das Angeben von Spalten- oder tabelleneinschränkungen unterstützt wird:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (vollständige Stufe) SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (vollständige Stufe) SQL_CT_CONSTRAINT_DEFERRABLE (vollständige Stufe) SQL_CT_CONSTRAINT_NON_DEFERRABLE (vollständige Stufe)  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **Übersetzung erstellen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird immer diese Optionen zurück, da unterstützt. Ein Rückgabewert von "0" bedeutet, dass die **Übersetzung erstellen** Anweisung wird nicht unterstützt.  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **CREATE VIEW** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 Ein Rückgabewert von "0" bedeutet, dass die **CREATE VIEW** Anweisung wird nicht unterstützt.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer die Optionen SQL_CV_CREATE_VIEW und SQL_CV_CHECK_OPTION unterstützt zurückgegeben.  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der angibt wie eine **COMMIT** Vorgang wirkt sich auf Cursor und vorbereiteten Anweisungen in der Datenquelle (das Verhalten der Datenquelle beim commit einer Transaktion).  
  
 Der Wert dieses Attributs wird den aktuellen Status der nächste Einstellung wider: SQL_COPT_SS_PRESERVE_CURSORS.  
  
 SQL_CB_DELETE = Cursor schließen und Löschen von vorbereiteten Anweisungen. Verwendung den Cursor erneut, die Anwendung muss reprepare und führen Sie die Anweisung erneut aus.  
  
 SQL_CB_CLOSE = Close Cursor. Die Anwendung kann für vorbereitete Anweisungen Aufrufen **SQLExecute** für die Anweisung ohne Aufruf **SQLPrepare** erneut aus. Der Standardwert für den SQL ODBC-Treiber ist SQL_CB_CLOSE. Dies bedeutet, dass der SQL ODBC-Treiber die Cursor schließt beim commit einer Transaktion geschlossen wird.  
  
 SQL_CB_PRESERVE Preserve-Cursor in der gleichen Position wie zuvor = die **COMMIT** Vorgang. Die Anwendung kann zum Abrufen von Daten weiterhin, oder schließen Sie den Cursor und führen Sie die Anweisung erneut aus, ohne erneute vorbereiten können.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der angibt wie eine **ROLLBACK** Vorgang wirkt sich auf Cursor und vorbereiteten Anweisungen in der Datenquelle:  
  
 SQL_CB_DELETE = Cursor schließen und Löschen von vorbereiteten Anweisungen. Verwendung den Cursor erneut, die Anwendung muss reprepare und führen Sie die Anweisung erneut aus.  
  
 SQL_CB_CLOSE = Close Cursor. Die Anwendung kann für vorbereitete Anweisungen Aufrufen **SQLExecute** für die Anweisung ohne Aufruf **SQLPrepare** erneut aus.  
  
 SQL_CB_PRESERVE Preserve-Cursor in der gleichen Position wie zuvor = die **ROLLBACK** Vorgang. Die Anwendung kann zum Abrufen von Daten fortfahren, oder schließen Sie den Cursor und die Anweisung ohne repreparing es Ausgangsstellung werden können.  
  
 SQL_CURSOR_SENSITIVITY FEST (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der die Unterstützung für Cursor Empfindlichkeit angibt:  
  
 SQL_INSENSITIVE = alle Cursor auf Anweisung Handle zum Anzeigen des Resultsets ohne spiegeln alle Änderungen, die vorgenommen wurden alle anderen Cursor innerhalb derselben Transaktion.  
  
 SQL_UNSPECIFIED = es ist nicht angegeben, ob Cursor über das Anweisungshandle sichtbar die Änderungen vornehmen, die ein Resultset von einem anderen Cursor innerhalb derselben Transaktion vorgenommen wurden. Der Cursor über das Anweisungshandle möglicherweise keine, einige oder alle solche Änderungen sichtbar.  
  
 SQL_SENSITIVE = Cursor sind empfindlich gegenüber Änderungen, die von anderen Cursorn innerhalb derselben Transaktion vorgenommen wurden.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer die Option SQL_UNSPECIFIED zurückgegeben, als unterstützt.  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird immer die Option SQL_INSENSITIVE zurück, da unterstützt.  
  
 SQL_DATA_SOURCE_NAME (ODBC 1.0)  
 Eine Zeichenfolge mit den Datenquellennamen, der beim Herstellen der Verbindung verwendet wurde. Wenn die Anwendung rief **SQLConnect**, dies ist der Wert, der die *SzDSN* Argument. Wenn die Anwendung rief **SQLDriverConnect** oder **SQLBrowseConnect**, dies ist der Wert, der das DSN-Schlüsselwort in der Verbindungszeichenfolge, die an den Treiber übergeben. Wenn die Verbindungszeichenfolge nicht enthalten hat die **DSN** Schlüsselwort (z. B. wenn es enthält die **Treiber** Schlüsselwort), dies ist eine leere Zeichenfolge.  
  
 SQL_DATA_SOURCE_READ_ONLY (ODBC 1.0)  
 Eine Zeichenfolge. "Y", wenn die Datenquelle in den READ ONLY-Modus ist, wird "N" festgelegt ist, wird jedoch andernfalls.  
  
 Dieses Merkmal bezieht sich nur auf der Datenquelle selbst; Es ist kein Merkmal des Treibers, der Zugriff auf die Datenquelle ermöglicht. Ein Treiber, der Lese-/Schreibzugriff aufweist, kann mit einer Datenquelle verwendet werden, die schreibgeschützt ist. Wenn ein Treiber schreibgeschützt ist, wird alle zugehörigen Datenquellen müssen schreibgeschützt sein sowie SQL_DATA_SOURCE_READ_ONLY zurückgeben.  
  
 SQL_DATABASE_NAME (ODBC 1.0)  
 Eine Zeichenfolge mit dem Namen der aktuellen Datenbank verwendet, wenn die Datenquelle ein benanntes Objekt mit dem Namen "Datenbank" definiert.  
  
> [!NOTE]  
>  In ODBC 3.*.x*, der Rückgabewert für diesen *Infotyp* kann auch zurückgegeben werden, indem **SQLGetConnectAttr** mit einer *Attribut* Argument SQL_ATTR_CURRENT_CATALOG.  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der SQL-92-Datetime-Literale, die von der Datenquelle unterstützt. Beachten Sie, dass diese die Datetime-Literale, die in der SQL-92-Spezifikation aufgelistet sind, und getrennt von den mit "DateTime" literal Escape-Klauseln von ODBC definiert sind. Weitere Informationen zu den ODBC-"DateTime" literal Escape-Klauseln, finden Sie unter [Date, Time und Timestamp-Literale](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Ein Transitional FIPS-Ebene – konforme-Treiber gibt immer den Wert "1" in der Bitmaske für die Bits in der folgenden Liste zurück. Der Wert "0" bedeutet, dass die SQL-92-Datetime-Literale nicht unterstützt werden.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Literale unterstützt werden:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_ SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME (ODBC 1.0)  
 Eine Zeichenfolge mit dem Namen des DBMS-Produkts, die vom Treiber zugegriffen werden soll.  
  
 SQL_DBMS_VER (ODBC 1.0)  
 Eine Zeichenfolge, die die Version des Produkts DBMS zugegriffen, die vom Treiber angibt. Die Version ist im Format ##. ##. ###, wobei die ersten beiden Ziffern die Hauptversion, die nächsten beiden Ziffern die Nebenversion und die letzten vier Ziffern der endgültigen Produktversion werden. Der Treiber die DBMS-Produktversion oben im Formular gerendert werden muss, aber es kann auch das DBMS produktspezifische Version angefügt. Z. B. "04.01.0000 Rdb 4.1".  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der Unterstützung für das Erstellen und Löschen von Indizes angibt:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION (ODBC 1.0)  
 Ein SQLUINTEGER-Wert, der angibt, dass die standardmäßige Transaktionsisolationsstufe von der Treiber oder die Datenquelle unterstützt, oder NULL, wenn die Datenquelle unterstützt keine Transaktionen. Die folgenden Begriffe werden verwendet, um Transaktionsisolationsstufen zu definieren:  
  
 **Dirty Read** Transaktion 1 geändert wird, eine Zeile. Transaktion 2 liest die geänderte Zeile vor der Transaktion 1 die Änderung ein Commit ausgeführt wird. Wenn die Transaktion 1 die Änderung ein Rollback, wird Transaktion 2 eine Zeile gelesen haben, das nie vorhanden gewesen wären haben betrachtet wird.  
  
 **Nicht wiederholbarer Lesevorgang** Transaktion 1 liest eine Zeile. Transaktion 2 aktualisiert oder löscht diese Zeile und führt einen Commit für diese Änderung. Wenn Transaktion 1 versucht, die Zeile liest, wird es anderen Zeilenwerte empfangen oder feststellen, dass die Zeile gelöscht wurde.  
  
 **Berührte** Transaktion 1 liest eine Gruppe von Zeilen, die einige Suchkriterien erfüllen. Transaktion 2 generiert eine oder mehrere Zeilen (durch einfügungen oder Updates), die den Suchkriterien entsprechen. Wenn die Transaktion 1 die Anweisung reexecutes, die die Zeilen liest, erhält sie einen anderen Satz von Zeilen.  
  
 Wenn die Datenquelle Transaktionen unterstützt, gibt der Treiber einen der folgenden Bitmasks zurück:  
  
 SQL_TXN_READ_UNCOMMITTED = Dirty Reads, nicht wiederholbaren Lesevorgängen und Phantome sind möglich.  
  
 SQL_TXN_READ_COMMITTED = Dirty Reads sind nicht möglich. Nicht wiederholbaren Lesevorgängen und Phantome sind möglich.  
  
 SQL_TXN_REPEATABLE_READ = Dirty Reads und nicht wiederholbaren Lesevorgängen sind nicht möglich. Phantome sind möglich.  
  
 Sql_txn_serializable festgelegt sind = Transaktionen sind serialisierbar. Dirty Reads, nicht wiederholbaren Lesevorgängen oder Phantome zulassen Schlüsselbereichssperren werden serialisierbare Transaktionen nicht.  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 Eine Zeichenfolge: "Y", wenn die Parameter beschrieben werden können; "N", wenn nicht.  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber in der Regel "Y" zurückgegeben, da unterstützt, wird die **BESCHREIBEN Eingabe** Anweisung. Da dies die zugrunde liegende SQL-Unterstützung nicht direkt angegeben ist, kann allerdings, beschreibt die Parameter nicht, auch in eine vollständige SQL-92-Ebene – konforme-Treiber unterstützt.  
  
 SQL_DM_VER (ODBC 3.0)  
 Eine Zeichenfolge mit der Version des Treiber-Managers. Die Version ist im Format ##. ##. ###. ###, wobei:  
  
 Der erste Satz von zwei Ziffern ist die Hauptversion von ODBC durch die Konstante SQL_SPEC_MAJOR festgelegte.  
  
 Die zweite Gruppe von zwei Ziffern ist die Nebenversion von ODBC durch die Konstante SQL_SPEC_MINOR festgelegte.  
  
 Die dritte Gruppe vier Ziffern wird die Buildnummer des Treiber-Manager-Hauptversion.  
  
 Der letzte Satz von vier Ziffern ist die Anzahl der Treiber-Manager-Nebenversionsnummer des Builds an.  
  
 Die Windows 7-Treiber-Manager-Version ist 03.80. Die Windows 8-Treiber-Manager-Version ist 03.81.  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 Eine SQLUINTEGER-Wert, der angibt, wenn der Treiber treiberfähiges Verbindungspooling unterstützen. (Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE gibt an, dass der Treiber treiberfähiges Verbindungspooling Mechanismus unterstützen kann.  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE gibt an, dass der Treiber treiberfähiges Verbindungspooling Mechanismus nicht unterstützt.  
  
 Ein Treiber muss nicht SQL_DRIVER_AWARE_POOLING_SUPPORTED implementieren, und der Treiber-Manager hat keine Auswirkungen auf den Treiber-Rückgabewert.  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV (ODBC 1.0)  
 Umgebungshandle oder Verbindungshandle, durch das Argument bestimmt ein SQLULEN-Wert, des Treibers *Infotyp*.  
  
 Diese Typen von Informationen werden vom Treiber-Manager allein implementiert.  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 Ein SQLULEN-Wert, der Treiber Deskriptorhandles ermittelt der Treiber-Manager-Deskriptorhandles, die bei der Eingabe in übergeben werden muss \* *InfoValuePtr* aus der Anwendung. In diesem Fall *InfoValuePtr* ist ein Eingabe- und Ausgabespalten Argument. Die Eingabe Deskriptorhandles übergebene \* *InfoValuePtr* müssen entweder explizit oder implizit zugeordnet wurde auf die *Verbindungshandle*.  
  
 Die Anwendung sollte, eine Kopie der Treiber-Manager-Deskriptor behandeln, bevor er ruft **SQLGetInfo** mit diesem Informationstyp, um sicherzustellen, dass das Handle in der Ausgabe nicht überschrieben wird.  
  
 Dieser Informationstyp wird vom Treiber-Manager allein implementiert.  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 Ein Wert SQLULEN der *Hinst* aus der Bibliothek laden zurückgegeben an den Treiber-Manager, wenn es sich um die Treiber-DLL für ein Microsoft Windows-Betriebssystem oder dessen Entsprechung auf einem anderen Betriebssystem geladen. Das Handle ist nur für das Verbindungshandle im Aufruf angegebenen **SQLGetInfo**.  
  
 Dieser Informationstyp wird vom Treiber-Manager allein implementiert.  
  
 SQL_DRIVER_HSTMT (ODBC 1.0)  
 Ein SQLULEN-Wert, bestimmt, indem das Anweisungshandle-Treiber-Managers, die bei der Eingabe in übergeben werden, muss der Treiber-Anweisungshandle \* *InfoValuePtr* aus der Anwendung. In diesem Fall *InfoValuePtr* ist sowohl Eingabe-als auch ein Output-Argument. Die eingabeanweisung Handle übergeben \* *InfoValuePtr* muss für das Argument zugeordnet wurde *Verbindungshandle*.  
  
 Die Anwendung sollte, eine Kopie der Treiber-Manager-Anweisung verarbeiten, bevor er ruft **SQLGetInfo** mit diesem Informationstyp, um sicherzustellen, dass das Handle in der Ausgabe nicht überschrieben wird.  
  
 Dieser Informationstyp wird vom Treiber-Manager allein implementiert.  
  
 SQL_DRIVER_NAME (ODBC 1.0)  
 Eine Zeichenfolge mit dem Dateinamen des Treibers, der Zugriff auf die Datenquelle.  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 Eine Zeichenfolge mit der Version von ODBC, die der Treiber unterstützt. Die Version ist im Format ##. ##, wobei die ersten beiden Ziffern die Hauptversion sind und die nächsten beiden Ziffern die Nebenversion sind. Definieren die Nummern für Haupt-und Nebenversionsnummern SQL_SPEC_MAJOR und SQL_SPEC_MINOR. In diesem Handbuch beschriebenen ODBC-Version Dies sind 3 und 0 und der Treiber sollte "03.00" zurück.  
  
 Der ODBC-Treiber-Manager wird den Rückgabewert der SQLGetInfo(SQL_DRIVER_ODBC_VER) Abwärtskompatibilität für vorhandene Anwendungen nicht ändern. Der Treiber gibt an, welcher Wert zurückgegeben wird. Allerdings muss ein Treiber, die Erweiterbarkeit von C Daten unterstützt 3.8 (oder höher) When zurückgeben eine Anwendung ruft **SQLSetEnvAttr** für 3.8 SQL_ATTR_ODBC_VERSION festzulegen. Weitere Informationen finden Sie unter [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 SQL_DRIVER_VER (ODBC 1.0)  
 Eine Zeichenfolge mit der Version des Treibers und optional eine Beschreibung des Treibers. Mindestens die Version ist, im Format ##. ##. ###, wobei die ersten beiden Ziffern die Hauptversion, die nächsten beiden Ziffern die Nebenversion und die letzten vier Ziffern der endgültigen Produktversion werden.  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **löschen ASSERTION** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DA_DROP_ASSERTION  
  
 Diese Option wird ein vollständige SQL-92-Ebene – konforme Treiber wie unterstützt immer zurückgegeben werden.  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ZEICHENSATZ löschen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 Diese Option wird ein vollständige SQL-92-Ebene – konforme Treiber wie unterstützt immer zurückgegeben werden.  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **SORTIERUNG löschen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DC_DROP_COLLATION  
  
 Diese Option wird ein vollständige SQL-92-Ebene – konforme Treiber wie unterstützt immer zurückgegeben werden.  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **DROP DOMAIN** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 Ein SQL-92-Intermediate-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **DROP SCHEMA** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 Ein SQL-92-Intermediate-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **DROP TABLE** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 Ein Transitional FIPS-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **Übersetzung löschen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmaske wird verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 Diese Option wird ein vollständige SQL-92-Ebene – konforme Treiber wie unterstützt immer zurückgegeben werden.  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **DROP VIEW** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 Ein Transitional FIPS-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute eines dynamischen Cursors beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die erste Teilmenge der Attribute. die zweite Teilmenge finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES2.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA1_NEXT = A *FetchOrientation* Argument sql_fetch_next wird in einem Aufruf unterstützt **SQLFetchScroll** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_ABSOLUTE = *FetchOrientation* Argumente SQL_FETCH_FIRST, SQL_FETCH_LAST und SQL_FETCH_ABSOLUTE werden in einem Aufruf unterstützt **SQLFetchScroll** Wenn der Cursor einen dynamischen Cursor befindet. (Das Rowset, das abgerufen werden ist unabhängig von der aktuellen Cursorposition.)  
  
 SQL_CA1_RELATIVE = *FetchOrientation* Argumente der SQL_FETCH_PRIOR und SQL_FETCH_RELATIVE werden in einem Aufruf unterstützt **SQLFetchScroll** Wenn der Cursor einen dynamischen Cursor befindet. (Das Rowset, das übernommen werden, hängt von der aktuellen Cursorposition ab. Beachten Sie, dass dies von SQL_FETCH_NEXT getrennt ist, weil in einem Vorwärtscursor nur SQL_FETCH_NEXT unterstützt wird.)  
  
 SQL_CA1_BOOKMARK = A *FetchOrientation* Argument von SQL_FETCH_BOOKMARK wird in einem Aufruf unterstützt **SQLFetchScroll** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_LOCK_EXCLUSIVE = A *LockType* SQL_LOCK_EXCLUSIVE Argument wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_LOCK_NO_CHANGE = A *LockType* SQL_LOCK_NO_CHANGE Argument wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_LOCK_UNLOCK = A *LockType* SQL_LOCK_UNLOCK Argument wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_POS_POSITION = ein *Vorgang* SQL_POSITION Argument wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_POS_UPDATE = ein *Vorgang* Argument SQL_UPDATE wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_POS_DELETE = ein *Vorgang* SQL_DELETE Argument wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_POS_REFRESH = ein *Vorgang* Argument SQL_REFRESH wird in einem Aufruf unterstützt **SQLSetPos** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_POSITIONED_UPDATE = ein UPDATE, auf dem aktuellen der SQL-Anweisung wird unterstützt, wenn der Cursor über einen dynamischen Cursor befindet. (Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt diese Option stets als unterstützt.)  
  
 SQL_CA1_POSITIONED_DELETE = A löschen, auf dem aktuellen der SQL-Anweisung wird unterstützt, wenn der Cursor über einen dynamischen Cursor befindet. (Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt diese Option stets als unterstützt.)  
  
 SQL_CA1_SELECT_FOR_UPDATE = eine SELECT-Anweisung für UPDATE-SQL-Anweisung unterstützt wird, wenn der Cursor über einen dynamischen Cursor befindet. (Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt diese Option stets als unterstützt.)  
  
 SQL_CA1_BULK_ADD = ein *Vorgang* SQL_ADD Argument wird in einem Aufruf unterstützt **SQLBulkOperations** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = ein *Vorgang* SQL_UPDATE_BY_BOOKMARK Argument wird in einem Aufruf unterstützt **SQLBulkOperations** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = ein *Vorgang* SQL_DELETE_BY_BOOKMARK Argument wird in einem Aufruf unterstützt **SQLBulkOperations** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = ein *Vorgang* SQL_FETCH_BY_BOOKMARK Argument wird in einem Aufruf unterstützt **SQLBulkOperations** Wenn der Cursor einen dynamischen Cursor befindet.  
  
 Ein SQL-92-Intermediate-Ebene – konforme Treiber wird in der Regel die SQL_CA1_NEXT SQL_CA1_ABSOLUTE und SQL_CA1_RELATIVE Optionen wie zurückgegeben werden unterstützt, da bildlauffähige Cursor über die eingebettete SQL FETCH-Anweisung unterstützt. Da dies die zugrunde liegende SQL-Unterstützung nicht direkt bestimmt, können jedoch bildlauffähige Cursor nicht, auch für eine SQL-92-Intermediate-Ebene – konforme-Treiber unterstützt werden.  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute eines dynamischen Cursors beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die zweite Teilmenge der Attribute. die erste Teilmenge finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES1.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = ein schreibgeschütztes dynamischer Cursor, in dem keine Updates zulässig sind, wird unterstützt. (Das SQL_ATTR_CONCURRENCY-Anweisungsattribut kann SQL_CONCUR_READ_ONLY für einen dynamischen Cursor werden).  
  
 SQL_CA2_LOCK_CONCURRENCY = einen dynamischen Cursor, die die niedrigste Ebene verwendet Sperren ausreichend, um sicherzustellen, dass die Zeile aktualisiert werden kann wird unterstützt. (Das SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_LOCK für einen dynamischen Cursor möglich.) Diese Sperren müssen konsistent mit die Isolationsebene der Transaktion, die durch das Verbindungsattribut SQL_ATTR_TXN_ISOLATION festgelegt sein.  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = einen dynamischen Cursor, verwendet die vollständige Parallelität Steuerelement Vergleichen von Zeilenversionen wird unterstützt. (Das SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_ROWVER für einen dynamischen Cursor möglich.)  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = einen dynamischen Cursor, dass verwendet vollständige Parallelität Vergleichen von Steuerelementwerte wird unterstützt. (Das SQL_ATTR_CONCURRENCY-Anweisungsattribut SQL_CONCUR_VALUES für einen dynamischen Cursor möglich.)  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = Added Zeilen sind sichtbar, in einen dynamischen Cursor; der Cursor kann auf jene Zeilen einen Bildlauf durchführen. (Das, in denen diese Zeilen hinzugefügt werden, bis zum Cursor ist Treiber abhängig.)  
  
 SQL_CA2_SENSITIVITY_DELETIONS = der gelöschte Zeilen sind nicht mehr verfügbar, um einen dynamischen Cursor, und lassen Sie nicht "Loch" im Resultset; nach der dynamische Cursor aus einer gelöschten Zeile einen Bildlauf durchführt, können keine Zeile zurückgegeben.  
  
 SQL_CA2_SENSITIVITY_UPDATES = Updates von Zeilen sind sichtbar, in einen dynamischen Cursor; Wenn der dynamische Cursor einen Bildlauf durchführt, aus und auf eine aktualisierte Zeile zurückgibt, ist die vom Cursor zurückgegebenen Daten die aktualisierten Daten, nicht die ursprünglichen Daten.  
  
 SQL_CA2_MAX_ROWS_SELECT = die SQL_ATTR_MAX_ROWS Anweisung Attribut wirkt sich auf **wählen** Anweisungen, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_MAX_ROWS_INSERT = die SQL_ATTR_MAX_ROWS Anweisung Attribut wirkt sich auf **einfügen** Anweisungen, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_MAX_ROWS_DELETE = die SQL_ATTR_MAX_ROWS Anweisung Attribut wirkt sich auf **löschen** Anweisungen, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_MAX_ROWS_UPDATE = die SQL_ATTR_MAX_ROWS Anweisung Attribut wirkt sich auf **UPDATE** Anweisungen, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_MAX_ROWS_CATALOG = die SQL_ATTR_MAX_ROWS Anweisung Attribut wirkt sich auf **Katalog** Resultsets aus, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = die SQL_ATTR_MAX_ROWS Anweisung Attribut wirkt sich auf **wählen**, **einfügen**, **löschen**, und **UPDATE** Anweisungen und **Katalog** Resultsets, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_CRC_EXACT = die genaue Zeilenanzahl im Feld SQL_DIAG_CURSOR_ROW_COUNT diagnostische verfügbar ist, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_CRC_APPROXIMATE = geschätzte Zeilenanzahl im Feld SQL_DIAG_CURSOR_ROW_COUNT diagnostische verfügbar ist, wenn der Cursor über einen dynamischen Cursor befindet.  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = den Treiber ist nicht gewährleistet, die simulierte positioniert Update oder Delete-Anweisungen wirkt nur eine Zeile, wenn der Cursor einen dynamischen Cursor; befindet. Es ist die Anwendung dafür verantwortlich, um dies zu garantieren. (Wenn eine Anweisung mehrere Zeilen betrifft **SQLExecute** oder **SQLExecDirect** SQLSTATE 01001 [Cursor Vorgang Konflikt] zurückgegeben.) Dieses Verhalten, die Anwendung ruft festzulegende **SQLSetStmtAttr** -Attribut Sie mit der SQL_ATTR_SIMULATE_CURSOR auf SQL_SC_NON_UNIQUE festgelegt.  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = versucht der Treiber, um sicherzustellen, dass die simulierten positionierte Update- oder Delete-Anweisungen nur eine Zeile auswirken, wenn der Cursor über einen dynamischen Cursor befindet. Der Treiber führt immer solchen Aussagen ist, auch wenn sie mehr als eine Zeile, z. B. wenn beeinflussen können keine eindeutiger Schlüssel vorhanden ist. (Wenn eine Anweisung mehrere Zeilen betrifft **SQLExecute** oder **SQLExecDirect** SQLSTATE 01001 [Cursor Vorgang Konflikt] zurückgegeben.) Dieses Verhalten, die Anwendung ruft festzulegende **SQLSetStmtAttr** -Attribut Sie mit der SQL_ATTR_SIMULATE_CURSOR auf SQL_SC_TRY_UNIQUE festgelegt.  
  
 SQL_CA2_SIMULATE_UNIQUE = den Treiber Garantien, die simulierte positioniert, Update oder Delete-Anweisungen beeinflussen nur eine Zeile aus, wenn der Cursor über einen dynamischen Cursor befindet. Wenn der Treiber dies für eine gegebene Anweisung nicht garantieren kann **SQLExecDirect** oder **SQLPrepare** SQLSTATE 01001 (Cursor Vorgang Konflikt) zurück. Dieses Verhalten, die Anwendung ruft festzulegende **SQLSetStmtAttr** -Attribut Sie mit der SQL_ATTR_SIMULATE_CURSOR auf SQL_SC_UNIQUE festgelegt.  
  
 SQL_EXPRESSIONS_IN_ORDERBY (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle Ausdrücke in unterstützt die **ORDER BY** auflisten. "N", wenn dies nicht der Fall.  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der angibt, wie ein ein-Ebenen-Treiber direkt Dateien in einer Datenquelle behandelt:  
  
 SQL_FILE_NOT_SUPPORTED = der Treiber ist keinen ein-Ebenen-Treiber. Beispielsweise ist ein ORACLE-Treiber ein 2-Ebenen-Treiber.  
  
 SQL_FILE_TABLE = eine einzelne Ebene behandelt Treiberdateien in einer Datenquelle als Tabellen. Xbase-Treiber werden z. B. jede Xbase-Datei als Tabelle behandelt.  
  
 SQL_FILE_CATALOG = einer ein-Ebenen-Treiber behandelt Dateien in einer Datenquelle als Katalog. Ein Microsoft Access-Treiber werden z. B. jede Microsoft Access-Datei als eine gesamte Datenbank behandelt.  
  
 Eine Anwendung kann diese verwenden, um zu bestimmen, wie Benutzer die Daten ausgewählt werden. Z. B. vorstellen Xbase Benutzer häufig Daten in Dateien gespeichert, wohingegen ORACLE und Microsoft Access-Benutzer in der Regel Daten vorstellen, wie in Tabellen gespeichert.  
  
 Wenn ein Benutzer eine Datenquelle Xbase auswählt, konnte die Anwendung die Fenster anzeigen **Datei öffnen** Standarddialogfeld; Wenn der Benutzer eine Microsoft Access oder ORACLE-Datenquelle, wählt die Anwendung konnte eine benutzerdefinierte anzeigen  **Wählen Sie die Tabelle** (Dialogfeld).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute eines Cursors Vorwärtscursor beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die erste Teilmenge der Attribute. die zweite Teilmenge finden Sie unter SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_ UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Beschreibungen dieser Bitmasken finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (und Ersetzen Sie "Forward-only-Cursor" für "dynamische Cursor" in den Beschreibungen).  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute eines Cursors Vorwärtscursor beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die zweite Teilmenge der Attribute. die erste Teilmenge finden Sie unter SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Beschreibungen dieser Bitmasken finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (und Ersetzen Sie "Forward-only-Cursor" für "dynamische Cursor" in den Beschreibungen).  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Erweiterungen für **SQLGetData**.  
  
 Die folgenden Bitmasken werden zusammen mit dem Flag verwendet, um zu bestimmen, welche häufig verwendete Erweiterungen der Treiber für unterstützt **SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData** für alle ungebundenen Spalten, einschließlich der vor der letzten Spalte gebundenen aufgerufen werden kann. Beachten Sie, dass die Spalten werden, in der Reihenfolge aufsteigend Spaltennummer aufgerufen müssen, es sei denn, SQL_GD_ANY_ORDER wird ebenfalls zurückgegeben.  
  
 SQL_GD_ANY_ORDER = **SQLGetData** für ungebundene Spalten in einer beliebigen Reihenfolge aufgerufen werden können. Beachten Sie, dass **SQLGetData** kann nur für Spalten aufgerufen werden, nachdem der letzten gebundenen Spalte auf, es sei denn, SQL_GD_ANY_COLUMN wird ebenfalls zurückgegeben.  
  
 SQL_GD_BLOCK = **SQLGetData** kann für einen ungebundenen Spalte in einer Zeile in einem Block (wobei die Rowsetgröße ist größer als 1) von Daten aufgerufen werden, nach dem Positionieren Zeile mit **SQLSetPos**.  
  
 SQL_GD_BOUND = **SQLGetData** für gebundene Spalten zusätzlich zu ungebundenen Spalten aufgerufen werden können. Ein Treiber kann nicht auf diesen Wert zurück, es sei denn, sie überdies SQL_GD_ANY_COLUMN gibt.  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData** aufgerufen werden, um die Werte der Ausgabeparameter zurückgeben. Weitere Informationen finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
 **SQLGetData** ist erforderlich, um nur Daten von ungebundenen Spalten, die nach der letzten Spalte gebundenen, auftreten in der Reihenfolge der spaltenzahlfolge aufgerufen werden und sind nicht in einer Zeile in einem Block von Zeilen zurück.  
  
 Wenn ein Treiber Lesezeichen (fester oder variabler Länge) unterstützt, muss er aufrufen unterstützen **SQLGetData** für die Spalte 0. Diese Unterstützung ist erforderlich, unabhängig davon, was für einen Aufruf der Treiber gibt **SQLGetInfo** mit der SQL_GETDATA_EXTENSIONS *Infotyp*.  
  
 SQL_GROUP_BY (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der angibt, die Beziehung zwischen den Spalten in der **GROUP BY** -Klausel und den nicht zusammengesetzten Spalten in der select-Liste:  
  
 SQL_GB_COLLATE = A **COLLATE** -Klausel am Ende der jeden Gruppierungsspalte angegeben werden kann. (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY** Klauseln werden nicht unterstützt. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = die **GROUP BY** -Klausel muss alle nicht zusammengesetzten Spalten in der select-Liste enthalten. Es darf keine andere Spalten enthalten. Beispielsweise **wählen DEPT, MAX(SALARY) aus EMPLOYEE-Gruppe BY DEPT**. (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = die **GROUP BY** -Klausel muss alle nicht zusammengesetzten Spalten in der select-Liste enthalten. Sie können Spalten enthalten, die nicht in der select-Liste enthalten sind. Beispielsweise **wählen DEPT, MAX(SALARY) aus EMPLOYEE-Gruppe nach Abteilung, Alter**. (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = die Spalten in der **GROUP BY** -Klausel und die select-Liste beziehen sich nicht. Die Bedeutung der nongrouped, aggregierte Spalten in der Auswahlliste ist datenquellenabhängig. Beispielsweise **wählen DEPT, Gehalt aus EMPLOYEE-Gruppe nach Abteilung, Alter**. (ODBC 2.0)  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer die Option SQL_GB_GROUP_BY_EQUALS_SELECT zurückgegeben, als unterstützt. Ein vollständige SQL-92-Ebene – konforme Treiber wird immer die Option SQL_GB_COLLATE zurückgegeben, als unterstützt. Wenn keine der Optionen unterstützt wird, die **GROUP BY** -Klausel wird von der Datenquelle nicht unterstützt.  
  
 SQL_IDENTIFIER_CASE (ODBC 1.0)  
 Ein SQLUSMALLINT Wert wie folgt aus:  
  
 SQL_IC_UPPER = Bezeichnern in SQL Groß-/Kleinschreibung nicht und werden in gespeicherten im Systemkatalog in Großbuchstaben.  
  
 SQL_IC_LOWER = Bezeichnern in SQL Groß-/Kleinschreibung nicht und werden in Kleinbuchstaben im Systemkatalog gespeichert.  
  
 SQL_IC_SENSITIVE = Bezeichnern in SQL wird die Groß-/Kleinschreibung beachtet und werden in gemischter Schreibung im Systemkatalog gespeichert.  
  
 SQL_IC_MIXED = Bezeichnern in SQL Groß-/Kleinschreibung nicht und werden in gemischter Schreibung im Systemkatalog gespeichert.  
  
 Da Bezeichner in SQL-92 nie Groß-/Kleinschreibung beachtet werden, wird ein Treiber, der ausschließlich SQL-92 (keinerlei) entspricht die Option SQL_IC_SENSITIVE nie zurück, da unterstützt.  
  
 SQL_IDENTIFIER_QUOTE_CHAR (ODBC 1.0)  
 Die Zeichenfolge, die als Trennzeichen Start- und Enddatum des eine in Anführungszeichen verwendet wird (-Begrenzungsbezeichner) in SQL-Anweisungen. (Bezeichner, die als Argumente übergeben werden, um ODBC-Funktionen nicht müssen in Anführungszeichen gesetzt werden.) Wenn Bezeichner in Anführungszeichen in die Datenquelle nicht unterstützt wird, wird ein leerer Wert zurückgegeben.  
  
 Diese Zeichenfolge kann auch verwendet werden, für die Funktionsargumente Katalog zitieren, wenn das SQL_ATTR_METADATA_ID-Verbindungsattribut auf SQL_TRUE festgelegt ist.  
  
 Da das Anführungszeichen Bezeichner in SQL-92 das doppelte Anführungszeichen (") ist, wird ein Treiber, der entspricht streng an SQL-92 immer das doppelte Anführungszeichen zurückgegeben.  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die Schlüsselwörter in der CREATE INDEX-Anweisung aufgeführt werden, die vom Treiber unterstützt werden:  
  
 SQL_IK_NONE = keines der Schlüsselwörter wird unterstützt.  
  
 SQL_IK_ASC = ASC Schlüsselwort wird unterstützt.  
  
 SQL_IK_DESC = "DESC"-Schlüsselwort wird unterstützt.  
  
 SQL_IK_ALL = alle Schlüsselwörter werden unterstützt.  
  
 Um festzustellen, ob die CREATE INDEX-Anweisung unterstützt wird, eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_DLL_INDEX-Informationen.  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Sichten in der INFORMATION_SCHEMA, die vom Treiber unterstützt werden. Die Ansichten und den Inhalt von, INFORMATION_SCHEMA sind, wie in SQL-92 definiert.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Ansichten unterstützt werden:  
  
 SQL_ISV_ASSERTIONS = identifiziert den Katalog Assertionen, die von einem angegebenen Benutzer gehören. (Vollständige Stufe)  
  
 SQL_ISV_CHARACTER_SETS = gibt den Katalog Zeichensätze, die ein angegebener Benutzer zugreifen kann. (Intermediate-Stufe)  
  
 SQL_ISV_CHECK_CONSTRAINTS = gibt die CHECK-Einschränkungen, die von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_COLLATIONS = identifiziert die Sortierungen Zeichen für den Katalog, die ein angegebener Benutzer zugreifen kann. (Vollständige Stufe)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = gibt Spalten für den Katalog, die abhängig von Domänen, die im Katalog definierten und von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_COLUMN_PRIVILEGES = gibt die Berechtigungen für die Spalten der persistente Tabellen, die verfügbar sind oder von diesem erteilt, die von einem angegebenen Benutzer sind. (FIPS Transitional Stufe)  
  
 SQL_ISV_COLUMNS = identifiziert die Spalten der persistente Tabellen, die ein angegebener Benutzer zugreifen können. (FIPS Transitional Stufe)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = ähnlich wie Spalten prognostiziert, CONSTRAINT_TABLE_USAGE-Sicht, für die verschiedenen Einschränkungen, die von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = identifiziert die Tabellen, die von Einschränkungen verwendet werden (referenzielle, eindeutig ist, und Assertionen), und von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = gibt die Domäne Einschränkungen (der Domänen im Katalog), die ein angegebener Benutzer zugreifen können. (Intermediate-Stufe)  
  
 SQL_ISV_DOMAINS = gibt die Domänen definiert, in einem Katalog, die vom Benutzer zugegriffen werden kann. (Intermediate-Stufe)  
  
 SQL_ISV_KEY_COLUMN_USAGE = im Katalog definierten gibt Spalten, die von einem bestimmten Benutzer als Schlüssel eingeschränkt sind. (Intermediate-Stufe)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = gibt die referenziellen Einschränkungen, die von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_SCHEMATA = gibt die Schemas, die von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_SQL_LANGUAGES = gibt die SQL-Übereinstimmungsebenen, Optionen und Dialekte von SQL-Implementierung unterstützt. (Intermediate-Stufe)  
  
 SQL_ISV_TABLE_CONSTRAINTS = gibt die tabelleneinschränkungen an, die von einem angegebenen Benutzer gehören. (Intermediate-Stufe)  
  
 SQL_ISV_TABLE_PRIVILEGES = gibt die Berechtigungen für persistente Tabellen, die verfügbar sind oder von diesem erteilt, die von einem angegebenen Benutzer sind. (FIPS Transitional Stufe)  
  
 SQL_ISV_TABLES = gibt die persistenten Tabellen definiert werden, in einem Katalog, die ein angegebener Benutzer zugreifen kann. (FIPS Transitional Stufe)  
  
 SQL_ISV_TRANSLATIONS = identifiziert Übersetzungen für den Katalog, die ein angegebener Benutzer zugreifen kann. (Vollständige Stufe)  
  
 SQL_ISV_USAGE_PRIVILEGES = gibt die Verwendung auf Catalog-Objekten, die verfügbar sind oder von einem bestimmten Benutzer im Besitz befindlichen sind Berechtigungen. (FIPS Transitional Stufe)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = identifiziert die Spalten, die auf dem des Katalogs, die anzeigt von einem angegebenen Benutzer gehören abhängig sind. (Intermediate-Stufe)  
  
 SQL_ISV_VIEW_TABLE_USAGE = identifiziert die Tabellen, auf dem des Katalogs, die anzeigt, von einem angegebenen Benutzer gehören abhängig sind. (Intermediate-Stufe)  
  
 SQL_ISV_VIEWS = gibt die angezeigten Tabellen definiert werden, im Katalog, die ein angegebener Benutzer zugreifen kann. (FIPS Transitional Stufe)  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die Unterstützung für angibt **einfügen** Anweisungen:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber werden immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_INTEGRITY (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle;-Integritätserweiterungsfunktion unterstützt. "N", wenn dies nicht der Fall.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_ODBC_SQL_OPT_IEF.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute ein Keyset-Cursor beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die erste Teilmenge der Attribute. die zweite Teilmenge finden Sie unter SQL_KEYSET_CURSOR_ATTRIBUTES2.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Beschreibungen dieser Bitmasken finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (und Ersetzen Sie "keysetgesteuerte Cursor" für "dynamische Cursor" in den Beschreibungen).  
  
 Ein SQL-92-Intermediate-Ebene – konforme-Treiber gibt in der Regel die SQL_CA1_NEXT SQL_CA1_ABSOLUTE und SQL_CA1_RELATIVE Optionen zurück, da unterstützt, da der Treiber bildlauffähige Cursor über die eingebettete SQL FETCH-Anweisung unterstützt. Da dies die zugrunde liegende SQL-Unterstützung nicht direkt bestimmt, können jedoch bildlauffähige Cursor nicht, auch für eine SQL-92-Intermediate-Ebene – konforme-Treiber unterstützt werden.  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute ein Keyset-Cursor beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die zweite Teilmenge der Attribute. die erste Teilmenge finden Sie unter SQL_KEYSET_CURSOR_ATTRIBUTES1.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Beschreibungen dieser Bitmasken finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (und Ersetzen Sie "keysetgesteuerte Cursor" für "dynamische Cursor" in den Beschreibungen).  
  
 SQL_KEYWORDS (ODBC 2.0)  
 Eine Zeichenfolge, die eine durch Trennzeichen getrennte Liste aller Data Source-spezifische Schlüsselwörter enthält. Diese Liste enthält keine ODBC-spezifische Schlüsselwörter oder Schlüsselwörter, die von der Datenquelle und die ODBC verwendet. Diese Liste stellt die reservierten Schlüsselwörter dar; interoperable Anwendungen sollten diese Wörter nicht in Objektnamen verwenden.  
  
 Eine Liste der ODBC-Schlüsselwörter finden Sie unter [reservierte Schlüsselwörter](../../../odbc/reference/appendixes/reserved-keywords.md) in [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Die **#define** Wert SQL_ODBC_KEYWORDS enthält eine durch Trennzeichen getrennte Liste der ODBC-Schlüsselwörter.  
  
 Anhang C: SQL-Grammatik  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle ein Escape-Zeichen unterstützt, für das Prozentzeichen (%) und Unterstrich (_) Zeichen, in einer **wie** Prädikat und der Treiber unterstützt die ODBC-Syntax zum Definieren einer **wie** Prädikat Escapezeichen; "N" andernfalls.  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der die maximale Anzahl gleichzeitiger aktiver-Anweisungen im asynchronen Modus angibt, die der Treiber für eine gegebene Verbindung unterstützen kann. Wenn es keine bestimmte Beschränkung oder das Limit unbekannt ist, ist dieser Wert 0 (null).  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 Eine SQLUINTEGER-Wert, der die maximale Länge angibt (Anzahl von hexadezimalen Zeichen, ohne das Zeichenfolgenliteral-Präfix und Suffix zurückgegebenes **SQLGetTypeInfo**) der ein binäres literal in einer SQL-Anweisung. Der binäre Literale 0xFFAA hat beispielsweise eine Länge von 4. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MAX_CATALOG_NAME_LEN (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge des Namens eines Katalogs in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 Ein vollständige FIPS Ebene – konforme-Treiber gibt mindestens 128 zurück.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_MAX_QUALIFIER_NAME_LEN.  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 Eine SQLUINTEGER-Wert, der die maximale Länge angibt (Anzahl der Zeichen, ohne das Zeichenfolgenliteral-Präfix und Suffix zurückgegebenes **SQLGetTypeInfo**) von einem Zeichenliteral in einer SQL­Anweisung. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MAX_COLUMN_NAME_LEN (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge von Namen einer Spalte in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 18 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 128 zurück.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der angibt, die maximale Anzahl zulässiger Spalten in einem **GROUP BY** Klausel. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 6 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 15 zurück.  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl zulässiger Spalten in einem Index angibt. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der angibt, die maximale Anzahl zulässiger Spalten in einer **ORDER BY** Klausel. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 6 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 15 zurück.  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl zulässiger Spalten in einer select-Liste angibt. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 100 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 250 zurück.  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl zulässiger Spalten in einer Tabelle angibt. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 100 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 250 zurück.  
  
 SQL_MAX_CONCURRENT_ACTIVITIES (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl aktiver Anweisungen angibt, die der Treiber für eine Verbindung unterstützen kann. Eine Anweisung als aktiv definiert ist, verfügt die Ergebnisse wartet, mit dem Begriff "Ergebnisse" Bedeutung Zeilen aus einer **wählen** Vorgang oder von betroffenen Zeilen ein **einfügen**, **UPDATE**, oder **Löschen** Vorgang (z. B. eine Zeilenanzahl), oder wenn es in einem NEED_DATA Zustand befindet. Dieser Wert kann aufgrund von der Treiber oder die Datenquelle widerspiegeln. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_ACTIVE_STATEMENTS.  
  
 SQL_MAX_CURSOR_NAME_LEN (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge des Namens eines Cursors in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 18 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 128 zurück.  
  
 SQL_MAX_DRIVER_CONNECTIONS (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl der aktiven Verbindungen angibt, die der Treiber für eine Umgebung unterstützen kann. Dieser Wert kann aufgrund von der Treiber oder die Datenquelle widerspiegeln. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_ACTIVE_CONNECTIONS.  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 Ein SQLUSMALLINT, der die maximale Größe in Zeichen angibt, die die Datenquelle für den benutzerdefinierten Namen unterstützt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 18 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 128 zurück.  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 Eine SQLUINTEGER-Wert, der die maximale Anzahl von Bytes in den kombinierten Feldern eines Indexes angibt. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MAX_PROCEDURE_NAME_LEN (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge der Name einer Prozedur in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 Eine SQLUINTEGER-Wert, der die maximale Länge aus einer einzelnen Zeile in einer Tabelle angibt. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 2.000 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 8.000 zurück.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 Eine Zeichenfolge: "Y", wenn die maximale Zeilengröße zurückgegeben wird, für den Informationstyp SQL_MAX_ROW_SIZE die Länge aller SQL_LONGVARCHAR und SQL_LONGVARBINARY Spalten in der Zeile enthält. "N" andernfalls.  
  
 SQL_MAX_SCHEMA_NAME_LEN (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge des Namens eines Schemas in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 18 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 128 zurück.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_MAX_OWNER_NAME_LEN.  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 Eine SQLUINTEGER-Wert, der die maximale Länge (Anzahl der Zeichen, einschließlich Leerzeichen) einer SQL-Anweisung angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MAX_TABLE_NAME_LEN (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge von Namen einer Tabelle in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 18 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 128 zurück.  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl der zulässigen Tabellen gibt an, die **FROM** -Klausel einer **wählen** Anweisung. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 Ein FIPS-Eintrag-Ebene – konforme-Treiber gibt mindestens 15 zurück. Ein FIPS-Intermediate-Ebene – konforme-Treiber gibt mindestens 50 zurück.  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Länge des einen Benutzernamen in der Datenquelle angibt. Wenn es keine maximale Länge oder die Länge unbekannt ist, ist dieser Wert auf 0 (null) festgelegt.  
  
 SQL_MULT_RESULT_SETS (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle mehrere Resultsets, "N" unterstützt, wenn dies nicht der Fall.  
  
 Weitere Informationen zu mehreren Resultsets finden Sie unter [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 SQL_MULTIPLE_ACTIVE_TXN (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn der Treiber mehr als eine aktive Transaktion zur gleichen Zeit, "N" unterstützt, wenn nur eine Transaktion zu einem beliebigen Zeitpunkt aktiv sein kann.  
  
 Für diesen Informationstyp zurückgegebene Informationen gilt nicht für verteilte Transaktionen.  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle die Länge eines Werts long-Daten vor dem Wert benötigt (der Datentyp ist SQL_LONGVARCHAR, SQL_LONGVARBINARY oder einem long-Daten datenquellenspezifischen-Datentyp) wird mit der Datenquelle "N" gesendet, wenn dies nicht der Fall. Weitere Informationen finden Sie unter [SQLBindParameter-Funktion](../../../odbc/reference/syntax/sqlbindparameter-function.md) und [SQLSetPos-Funktion](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 SQL_NON_NULLABLE_COLUMNS (ODBC 1.0)  
 Ein SQLUSMALLINT-Wert, der angibt, ob die Datenquelle NOT NULL in Spalten unterstützt:  
  
 SQL_NNC_NULL = alle Spalten müssen auf NULL festlegbar sein.  
  
 SQL_NNC_NON_NULL = Spalten darf nicht NULL sein. (Die Datenquelle unterstützt die **NOT NULL** spalteneinschränkung in **CREATE TABLE** Anweisungen.)  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt SQL_NNC_NON_NULL zurück.  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 Ein SQLUSMALLINT-Wert, der angibt, in denen NULL-Werte in einem Resultset sortiert werden:  
  
 SQL_NC_END = NULL-Werte werden am Ende des Resultsets, unabhängig von den Schlüsselwörtern ASC oder DESC sortiert.  
  
 SQL_NC_HIGH = NULL-Werte werden am oberen Endpunkt des Resultsets, je nach den Schlüsselwörtern ASC oder DESC sortiert.  
  
 SQL_NC_LOW = NULL-Werte werden im unteren Bereich des Resultsets, je nach den Schlüsselwörtern ASC oder DESC sortiert.  
  
 SQL_NC_START = NULL-Werte zu Beginn des Resultsets, unabhängig von den Schlüsselwörtern ASC oder DESC sortiert werden.  
  
 SQL_NUMERIC_FUNCTIONS (ODBC 1.0)  
 Hinweis: Der Typ der Informationen wurde in ODBC 1.0 eingeführt. Jede Bitmaske ist mit der Version mit der Bezeichnung eingeführt wurde.  
  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der numerischen Skalarfunktionen des Treibers und der zugeordneten Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche numerischen Funktionen unterstützt werden:  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_ FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_ NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der das Maß an die ODBC 3. angibt*.x* Schnittstelle, die der Treiber einhält.  
  
 SQL_OIC_CORE: Mindestberechtigungen, die alle ODBC-Treiber sind erwartet einhalten. Diese Ebene umfasst grundlegende Benutzeroberflächenelemente z. B. Verbindungsfunktionen, Funktionen für das Vorbereiten und Ausführen einer SQL­Anweisung, grundlegende Ergebnis Satz Metadatenfunktionen, grundlegende Katalogfunktionen usw. an.  
  
 SQL_OIC_LEVEL1: Eine Ebene, einschließlich der Core Standards Compliance-Level-Funktionen sowie bildlauffähige Cursor Lesezeichen positioniert aktualisiert und gelöscht und so weiter.  
  
 SQL_OIC_LEVEL2: Eine Ebene, einschließlich Stufe 1 Standards Compliance-Level-Funktionen sowie erweiterte Funktionen wie Sensitivcursor; Aktualisieren Sie, löschen Sie und aktualisieren Sie, indem Sie Lesezeichen; Unterstützung für gespeicherte Prozeduren; Katalogfunktionen für Primär-und Fremdschlüssel; Unterstützung des Multi-Katalogs; Und so weiter.  
  
 Weitere Informationen finden Sie unter [Übereinstimmungsebenen Schnittstelle](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 SQL_ODBC_VER (ODBC 1.0)  
 Eine Zeichenfolge mit der Version des ODBC-Treiber-Manager entspricht. Die Version ist im Format ##. ##. 0000, wobei die ersten beiden Ziffern die Hauptversion und die nächsten beiden Ziffern sind die Nebenversion. Dies ist nur in der Treiber-Manager implementiert.  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 Eine SQLUINTEGER-Bitmaske Auflisten der Typen von äußeren Verknüpfungen, die von der Treiber und die Datenquelle unterstützt. Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Typen werden unterstützt:  
  
 SQL_OJ_LEFT = linke äußere Joins werden unterstützt.  
  
 SQL_OJ_RIGHT = Right outer-Joins werden unterstützt.  
  
 SQL_OJ_FULL = vollständige äußere Joins werden unterstützt.  
  
 SQL_OJ_NESTED = geschachtelte äußere Joins werden unterstützt.  
  
 SQL_OJ_NOT_ORDERED = die Spalte mit dem Namen in der ON-Klausel der äußeren Verknüpfung nicht in der gleichen Reihenfolge wie ihre entsprechenden Tabellennamen in werden müssen die **ÄUßERER JOIN** Klausel.  
  
 SQL_OJ_INNER = den inneren Tabelle (die rechte Tabelle in einem linken äußeren Join) oder in einem rechten äußeren Join der linken Tabelle auch in einem inner Join verwendet werden. Dies gilt nicht für vollständige äußere Joins, die nicht über eine interne Tabelle verfügen.  
  
 SQL_OJ_ALL_COMPARISON_OPS Vergleich =-Operator in der ON-Klausel kann die ODBC-Vergleichsoperatoren. Wenn dieses Bit nicht festgelegt ist, kann nur der Vergleichsoperator gleich (=) im äußeren Joins verwendet werden.  
  
 Wenn keine dieser Optionen zurückgegeben wird, da unterstützt, wird keine outer Join-Klausel unterstützt.  
  
 Informationen zur Unterstützung von relationalen Join-Operatoren in einer SELECT-Anweisung gemäß der SQL-92 finden Sie unter SQL_SQL92_RELATIONAL_JOIN_OPERATORS.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 Eine Zeichenfolge: "Y" Wenn die Spalten in der **ORDER BY** -Klausel in der Auswahlliste; sein muss, andernfalls "N".  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 Eine SQLUINTEGER beim Aufzählen der Treibereigenschaften bezüglich der Verfügbarkeit der Zeile wird in der Ausführung einer parametrisierten gezählt. Hat die folgenden Werte an:  
  
 SQL_PARC_BATCH = individuell Zeilenanzahl für jeden Satz von Parametern stehen. Dies ist im Prinzip entspricht der Treiber generiert einen Batch SQL-Anweisungen, eine für jeden Parameter im Array festgelegt. Erweiterte Fehlerinformationen kann mithilfe der SQL_PARAM_STATUS_PTR Deskriptorfeld abgerufen werden.  
  
 SQL_PARC_NO_BATCH = es ist nur eine Zeilenanzahl verfügbar ist, der die kumulative Zeilenanzahl, die aufgrund der Ausführung der Anweisung für das gesamte Array von Parametern ist. Dies ist der Auflistungskapazität auf die Anweisung zusammen mit der vollständigen Parameterarray als eine unteilbare Einheit behandelt. Fehler werden gleich behandelt, als ob eine Anweisung ausgeführt wurden.  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 In der Ausführung einer parametrisierten legt eine SQLUINTEGER beim Aufzählen der Treibereigenschaften bezüglich der Verfügbarkeit des Ergebnisses fest. Hat die folgenden Werte an:  
  
 SQL_PAS_BATCH = es wird ein Resultset pro Satz von Parametern zur Verfügung. Dies ist im Prinzip entspricht der Treiber generiert einen Batch SQL-Anweisungen, eine für jeden Parameter im Array festgelegt.  
  
 SQL_PAS_NO_BATCH = es ist nur ein Resultset verfügbar ist, womit das kumulierte Ergebnis der Ausführung der Anweisung für das vollständige Array von Parametern erstellten Nachrichtensatz. Dies ist der Auflistungskapazität auf die Anweisung zusammen mit der vollständigen Parameterarray als eine unteilbare Einheit behandelt.  
  
 SQL_PAS_NO_SELECT = A Treiber lässt sich nicht auf eine Resultset Generieren von mit einem Array von Parametern auszuführenden Anweisung.  
  
 SQL_PROCEDURE_TERM (ODBC 1.0)  
 Eine Zeichenfolge mit der Quelle-Herstellers Namen für eine Prozedur; z. B. "Datenbankprozedur", "gespeicherte Prozedur", "Procedure", "Paket" oder "gespeicherte Abfrage".  
  
 SQL_PROCEDURES (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn die Datenquelle, Prozeduren unterstützt und der Treiber die Syntax der ODBC-Prozedur-Aufruf unterstützt; "N" andernfalls.  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 Eine SQLINTEGER-Bitmaske, die beim Aufzählen der Unterstützung für Vorgänge im **SQLSetPos**.  
  
 Die folgenden Bitmasken werden zusammen mit dem Flag verwendet, um zu bestimmen, welche Optionen unterstützt werden.  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 Ein SQLUSMALLINT Wert wie folgt aus:  
  
 SQL_IC_UPPER = in Anführungszeichen Bezeichner in SQL Groß-/Kleinschreibung nicht und werden gespeichert, Großbuchstaben im Systemkatalog.  
  
 SQL_IC_LOWER = in Anführungszeichen Bezeichner in SQL Groß-/Kleinschreibung nicht und werden in Kleinbuchstaben im Systemkatalog gespeichert.  
  
 SQL_IC_SENSITIVE = in Anführungszeichen Bezeichner in SQL wird die Groß-/Kleinschreibung beachtet und werden in gemischter Schreibung im Systemkatalog gespeichert. (In einer SQL-92-kompatible Datenbank sind Bezeichner in Anführungszeichen immer Groß-/Kleinschreibung beachtet.)  
  
 SQL_IC_MIXED = in Anführungszeichen Bezeichner in SQL Groß-/Kleinschreibung nicht und werden in gemischter Schreibung im Systemkatalog gespeichert.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer SQL_IC_SENSITIVE zurückgegeben.  
  
 SQL_ROW_UPDATES (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn ein keysetgesteuerter oder gemischter Cursor Zeilenversionen verwaltet oder Werte für alle Zeilen abgerufen, und daher erkennt alle Updates, die auf eine Zeile von einem Benutzer vorgenommen wurden, seitdem die Zeile zuletzt abgerufen wurde. (Dies gilt nur für Updates, löschungen oder einfügungen). Der Treiber kann das SQL_ROW_UPDATED-Flag zurück, um den Zeilenstatus array-Wenn **SQLFetchScroll** aufgerufen wird. Andernfalls, "N".  
  
 SQL_SCHEMA_TERM (ODBC 1.0)  
 Eine Zeichenfolge mit der Quelle-Herstellers Namen für ein Schema; z. B. "Besitzer", "Autorisierungs-ID" oder "Schema".  
  
 Die Zeichenfolge kann in der oberen, unteren oder gemischten Fall zurückgegeben werden.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt immer "Schema" zurück.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_OWNER_TERM.  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Anweisungen in denen Schemas verwendet werden können:  
  
 SQL_SU_DML_STATEMENTS = Schemas werden in allen Data Manipulation Language-Anweisungen unterstützt: **wählen**, **einfügen**, **UPDATE**, **DELETE**, und falls unterstützt, **für aktualisieren wählen** und positioniert Update und delete-Anweisungen.  
  
 SQL_SU_PROCEDURE_INVOCATION = Schemas werden in der ODBC-Prozedur aufrufanweisung unterstützt.  
  
 SQL_SU_TABLE_DEFINITION = Schemas werden in allen Table-Anweisungen Definition unterstützt: **CREATE TABLE**, **CREATE VIEW**, **ALTER TABLE**, **DROP TABLE** , und **DROP VIEW**.  
  
 SQL_SU_INDEX_DEFINITION = Schemas werden in alle indexanweisungen Definition unterstützt: **CREATE INDEX** und **DROP INDEX**.  
  
 SQL_SU_PRIVILEGE_DEFINITION = Schemas werden in alle Berechtigungen datendefinitionsanweisungen unterstützt: **GRANT** und **widerrufen**.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer die SQL_SU_DML_STATEMENTS SQL_SU_TABLE_DEFINITION und SQL_SU_PRIVILEGE_DEFINITION Optionen zurückgegeben, als unterstützt.  
  
 Dies *Infotyp* umbenannt wurde für ODBC 3.0 von der ODBC 2.0 *Infotyp* SQL_OWNER_USAGE.  
  
 SQL_SCROLL_OPTIONS (ODBC 1.0)  
 Hinweis: Der Typ der Informationen wurde in ODBC 1.0 eingeführt. Jede Bitmaske ist mit der Version mit der Bezeichnung eingeführt wurde.  
  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der das Scroll-Optionen für scrollfähige Cursor unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Optionen unterstützt werden:  
  
 SQL_SO_FORWARD_ONLY = der Cursor nur einen Bildlauf vorwärts. ODBC (1.0)  
  
 SQL_SO_STATIC = die Daten in das Ergebnis ist statisch. (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = der Treiber gespeichert, und der Schlüssel für jede Zeile im Resultset verwendet. ODBC (1.0)  
  
 SQL_SO_DYNAMIC = der Treiber behält die Schlüssel für jede Zeile im Rowset (die Keysetgröße ist identisch mit der Rowsetgröße). ODBC (1.0)  
  
 SQL_SO_MIXED = der Treiber behält die Schlüssel für jede Zeile in das Keyset, und die Keysetgröße die Rowsetgröße größer ist. Der Cursor ist in das Keyset keysetgesteuerte und dynamische außerhalb der Keyset. ODBC (1.0)  
  
 Informationen des bildlauffähigen Cursor finden Sie unter [bildlauffähige Cursor](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 SQL_SEARCH_PATTERN_ESCAPE (ODBC 1.0)  
 Eine Zeichenfolge, die angeben, was als Escapezeichen verwendet der Treiber unterstützt, die die Verwendung des Musters Übereinstimmung Metazeichen Unterstrich (_) und Prozentzeichen (%) als gültige Zeichen in Suchmustern zulässt. Das Escapezeichen gilt nur für diese Argumente der Katalog-Funktion, die die Suchzeichenfolgen unterstützen. Wenn diese Zeichenfolge leer ist, unterstützt der Treiber nicht die einem Suchmuster Escape-Zeichen.  
  
 Da diesen Informationstyp nicht allgemeine Unterstützung des Escapezeichens in angeben, dass die **wie** Prädikat, SQL-92 enthält keine Anforderungen für diese Zeichenfolge.  
  
 Dies *Infotyp* auf Katalogfunktionen beschränkt ist. Eine Beschreibung der Verwendung von Escapezeichen im Muster Suchzeichenfolgen, finden Sie unter [Muster Value-Argumenten](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 SQL_SERVER-NAME (ODBC 1.0)  
 Eine Zeichenfolge mit den tatsächlichen Daten datenquellenspezifischen Servernamen; ist nützlich, wenn Sie ein Datenquellennamen verwendet wird, während der **SQLConnect**, **SQLDriverConnect**, und **SQLBrowseConnect**.  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 Eine Zeichenfolge, die alle Sonderzeichen (d. h. alle Zeichen mit Ausnahme von a bis Z, A bis Z, 0 bis 9 und Unterstriche) enthält, die in einem Bezeichnernamen, z. B. einen Tabellennamen, Spaltennamen oder Indexname für die Datenquelle verwendet werden kann. Z. B. "#$^". Wenn ein Bezeichner eine oder mehrere der folgenden Zeichen enthält, muss der Bezeichner ein Begrenzungsbezeichner sein.  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der die Ebene der SQL-92 vom Treiber unterstützten angibt:  
  
 SQL_SC_SQL92_ENTRY = Entry Level SQL-92 kompatibel.  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = Sie FIPS 127-2-transitional-Level kompatibel.  
  
 SQL_SC_SQL92_FULL = vollständige Level SQL-92 kompatibel.  
  
 SQL_SC_ SQL92_INTERMEDIATE = Intermediate Ebene SQL-92 kompatibel.  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske Auflisten von "DateTime"-Skalarfunktionen, die vom Treiber und der zugeordneten Datenquelle unterstützt werden, gemäß SQL-92.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Funktionen "DateTime" unterstützt werden:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Regeln für einen Fremdschlüssel in unterstützt eine **löschen** gemäß SQL-92-Anweisung.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln, die von der Datenquelle unterstützt werden:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 Ein Transitional FIPS-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Regeln für einen Fremdschlüssel in unterstützt eine **UPDATE** gemäß SQL-92-Anweisung.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln, die von der Datenquelle unterstützt werden:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 Ein vollständige SQL-92-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in unterstützt die **GRANT** gemäß SQL-92-Anweisung.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln, die von der Datenquelle unterstützt werden:  
  
 Die SQL_SG_INSERT_COLUMN (Intermediate-Stufe) SQL_SG_INSERT_TABLE (Entry Level) SQL_SG_REFERENCES_TABLE (Entry Level) SQL_SG_REFERENCES_COLUMN (Entry Level) SQL_SG_SELECT_TABLE (Entry Level) SQL_SG_UPDATE_COLUMN (SQL_SG_DELETE_TABLE (Entry Level) Entry Level) SQL_SG_UPDATE_TABLE (Entry Level) SQL_SG_USAGE_ON_DOMAIN (FIPS Transitional Stufe) SQL_SG_USAGE_ON_CHARACTER_SET (FIPS Transitional Stufe) SQL_SG_USAGE_ON_COLLATION (FIPS Transitional Stufe) SQL_SG_USAGE_ON_TRANSLATION (FIPS Transitional Stufe) SQL_SG_WITH_GRANT_OPTION (Entry Level)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der numerische Wert Skalarfunktionen, die vom Treiber und der zugeordneten Datenquelle unterstützt werden, gemäß SQL-92.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche numerischen Funktionen unterstützt werden:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Prädikate in unterstützt Auflisten einer **wählen** gemäß SQL-92-Anweisung.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Optionen von der Datenquelle unterstützt werden:  
  
 SQL_SP_BETWEEN (Entry Level) SQL_SP_COMPARISON (Entry Level) SQL_SP_EXISTS (Entry Level) SQL_SP_IN (Entry Level) SQL_SP_ISNOTNULL (Entry Level) SQL_SP_ISNULL (Entry Level) SQL_SP_LIKE (Entry Level) SQL_SP_MATCH_PARTIAL SQL_SP_MATCH_FULL (vollständige Stufe) (Vollständige Stufe) SQL_SP_MATCH_UNIQUE_FULL (vollständige Stufe) SQL_SP_MATCH_UNIQUE_PARTIAL (vollständige Stufe) SQL_SP_OVERLAPS (FIPS Transitional Stufe) SQL_SP_QUANTIFIED_COMPARISON (Entry Level) SQL_SP_UNIQUE (Entry Level)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die den relationalen Join-Operatoren in unterstützt Auflisten einer **wählen** gemäß SQL-92-Anweisung.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Optionen von der Datenquelle unterstützt werden:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE (Intermediate-Stufe) SQL_SRJO_CROSS_JOIN (vollständige Stufe) SQL_SRJO_EXCEPT_JOIN (Intermediate-Stufe) SQL_SRJO_FULL_OUTER_JOIN (Intermediate-Stufe) SQL_SRJO_INNER_JOIN (FIPS Transitional Stufe) SQL_SRJO_INTERSECT_JOIN (Intermediate-Stufe) SQL_SRJO_LEFT_OUTER_JOIN (FIPS Transitional Stufe) SQL_SRJO_NATURAL_JOIN (FIPS Transitional Stufe) SQL_SRJO_RIGHT_OUTER_JOIN (FIPS Transitional Stufe) SQL_SRJO_UNION_JOIN (vollständige Stufe)  
  
 SQL_SRJO_INNER_JOIN gibt Unterstützung für die **INNER JOIN** nicht für die Joinfunktion, inner-Syntax. Unterstützung für die **INNER JOIN** Syntax ist TRANSITIONAL FIPS, wohingegen der inner Joinfunktion ist eine Unterstützung für **Eintrag**.  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in unterstützt die **widerrufen** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln, die von der Datenquelle unterstützt werden:  
  
 SQL_SR_CASCADE (FIPS Transitional Stufe) SQL_SR_DELETE_TABLE (Entry Level) SQL_SR_GRANT_OPTION_FOR (Intermediate-Stufe) SQL_SR_INSERT_COLUMN (Intermediate-Stufe) SQL_SR_INSERT_TABLE (Entry Level) SQL_SR_REFERENCES_COLUMN (Entry Level) SQL_SR_ REFERENCES_TABLE (Entry Level) SQL_SR_RESTRICT (FIPS Transitional Stufe) SQL_SR_SELECT_TABLE (Entry Level) SQL_SR_UPDATE_COLUMN (Entry Level) SQL_SR_UPDATE_TABLE (Entry Level) SQL_SR_USAGE_ON_DOMAIN (FIPS Transitional Stufe) SQL_SR_USAGE_ON_ CHARACTER_SET (FIPS Transitional Stufe) SQL_SR_USAGE_ON_COLLATION (FIPS Transitional Stufe) SQL_SR_USAGE_ON_TRANSLATION (FIPS Transitional Stufe)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Konstruktor zeilenwertausdrücke in unterstützt eine **wählen** gemäß SQL-92-Anweisung. Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Optionen von der Datenquelle unterstützt werden:  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske Auflisten von skalaren Zeichenfolgenfunktionen, die vom Treiber und der zugeordneten Datenquelle unterstützt werden, gemäß SQL-92.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Funktionen für Zeichenfolgen unterstützt werden:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Wertausdrücke unterstützt, auflisten, wie in SQL-92 definiert.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Optionen von der Datenquelle unterstützt werden:  
  
 SQL_SVE_CASE (Intermediate-Stufe) SQL_SVE_CAST (FIPS Transitional Stufe) SQL_SVE_COALESCE (Intermediate-Stufe) SQL_SVE_NULLIF (Intermediate-Stufe)  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der CLI-Standard oder Standards, die der Treiber entspricht. Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Ebenen der Treiber entspricht:  
  
 SQL_SCC_XOPEN_CLI_VERSION1: Der Treiber entspricht der Open Group CLI-Version 1.  
  
 SQL_SCC_ISO92_CLI: Der Treiber entspricht der ISO-92-CLI.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute eines statischen Cursors beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die erste Teilmenge der Attribute. die zweite Teilmenge finden Sie unter SQL_STATIC_CURSOR_ATTRIBUTES2.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_ UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 Beschreibungen dieser Bitmasken finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (und Ersetzen Sie "statische Cursor" für "dynamische Cursor" in den Beschreibungen).  
  
 Ein SQL-92-Intermediate-Ebene – konforme-Treiber gibt in der Regel die SQL_CA1_NEXT SQL_CA1_ABSOLUTE und SQL_CA1_RELATIVE Optionen zurück, da unterstützt, da der Treiber bildlauffähige Cursor über die eingebettete SQL FETCH-Anweisung unterstützt. Da dies die zugrunde liegende SQL-Unterstützung nicht direkt bestimmt, können jedoch bildlauffähige Cursor nicht, auch für eine SQL-92-Intermediate-Ebene – konforme-Treiber unterstützt werden.  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die die Attribute eines statischen Cursors beschreibt, die vom Treiber unterstützt werden. Diese Bitmaske enthält die zweite Teilmenge der Attribute. die erste Teilmenge finden Sie unter SQL_STATIC_CURSOR_ATTRIBUTES1.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Attribute unterstützt werden:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_ CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_ SIMULATE_UNIQUE  
  
 Beschreibungen dieser Bitmasken finden Sie unter SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (und Ersetzen Sie "statische Cursor" für "dynamische Cursor" in den Beschreibungen).  
  
 SQL_STRING_FUNCTIONS (ODBC 1.0)  
 Hinweis: Der Typ der Informationen wurde in ODBC 1.0 eingeführt. Jede Bitmaske ist mit der Version mit der Bezeichnung eingeführt wurde.  
  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der skalaren Zeichenfolgenfunktionen, die vom Treiber und zugeordneten Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Funktionen für Zeichenfolgen unterstützt werden:  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC 1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_ STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 Wenn eine Anwendung aufrufen kann die **suchen** Skalarfunktion mit der *string_exp1*, *string_exp2 und*, und *starten* Argumente, des Treibers Gibt die Bitmaske SQL_FN_STR_LOCATE zurück. Wenn eine Anwendung die suchen-Skalarfunktion mit nur aufrufen, kann die *string_exp1* und *string_exp2 und* Argumente, gibt der Treiber die Bitmaske SQL_FN_STR_LOCATE_2. Treiber, die vollständig unterstützen die **suchen** Skalarfunktion geben beide Bitmasken zurück.  
  
 (Weitere Informationen finden Sie unter [Zeichenfolgenfunktionen](../../../odbc/reference/appendixes/string-functions.md) in Anhang E "Skalarfunktionen.")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Prädikate, die Unterabfragen unterstützen:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 Die Bitmaske SQL_SQ_CORRELATED_SUBQUERIES gibt an, dass alle Prädikate, die Unterabfragen unterstützt korrelierte Unterabfragen unterstützt.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt immer eine Bitmaske zurück, in der alle diese Bits festgelegt sind.  
  
 SQL_SYSTEM_FUNCTIONS (ODBC 1.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der skalaren Systemfunktionen, die vom Treiber und zugeordneten Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Systemfunktionen unterstützt werden:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM (ODBC 1.0)  
 Eine Zeichenfolge mit der Quelle-Herstellers Namen für eine Tabelle; beispielsweise "Table" oder "File".  
  
 Diese Zeichenfolge kann oberen, unteren oder mixed sein.  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer mit "Table" zurückgegeben.  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die Timestamp-Intervalle vom Treiber und zugeordnete Datenquelle für die Skalarfunktion TIMESTAMPADD auflisten.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Intervalle unterstützt werden:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Ein Transitional FIPS-Ebene – konforme-Treiber gibt immer eine Bitmaske zurück, in der alle diese Bits festgelegt sind.  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die Timestamp-Intervalle vom Treiber und zugeordnete Datenquelle für die Skalarfunktion TIMESTAMPDIFF auflisten.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Intervalle unterstützt werden:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 Ein Transitional FIPS-Ebene – konforme-Treiber gibt immer eine Bitmaske zurück, in der alle diese Bits festgelegt sind.  
  
 SQL_TIMEDATE_FUNCTIONS (ODBC 1.0)  
 Hinweis: Der Typ der Informationen wurde in ODBC 1.0 eingeführt. Jede Bitmaske ist mit der Version mit der Bezeichnung eingeführt wurde.  
  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der skalaren Datums- und Zeitfunktionen, die vom Treiber und zugeordneten Datenquelle unterstützt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Funktionen für Datum und Uhrzeit unterstützt werden:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK () ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_ ZWEITE (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE (ODBC 1.0)  
 Hinweis: Der Typ der Informationen wurde in ODBC 1.0 eingeführt. jede zurückgegebene Wert ist mit der Version mit der Bezeichnung eingeführt wurde.  
  
 Ein SQLUSMALLINT-Wert, der Unterstützung von Transaktionen in der Treiber oder die Datenquelle beschreiben:  
  
 SQL_TC_NONE = Transaktionen nicht unterstützt. ODBC (1.0)  
  
 SQL_TC_DML = Transaktionen können nur die Anweisungen (Data Manipulation Language, DML) enthalten (**wählen**, **einfügen**, **UPDATE**, **löschen** ). Anweisungen von Data Definition Language (DDL), die in einer Transaktion verursacht ein Fehler aufgetreten. ODBC (1.0)  
  
 SQL_TC_DDL_COMMIT = Transaktionen können nur DML-Anweisungen enthalten. DDL-Anweisungen (**CREATE TABLE**, **DROP INDEX**usw.) in einer Transaktion Ursache gefunden, die Transaktion ein Commit ausgeführt werden. (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = Transaktionen können nur DML-Anweisungen enthalten. DDL-Anweisungen, die in einer Transaktion gefunden werden ignoriert. (ODBC 2.0)  
  
 SQL_TC_ALL = Transaktionen können DDL-Anweisungen und DML-Anweisungen in beliebiger Reihenfolge enthalten. ODBC (1.0)  
  
 (Da die Unterstützung von Transaktionen in SQL-92 obligatorisch ist, wird ein SQL-92-konforme Treiber [keinerlei] nie SQL_TC_NONE zurück.)  
  
 DEM SQL_TXN_ISOLATION_OPTION (ODBC 1.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Transaktionsisolationsstufen aus die Treiber oder die Datenquelle.  
  
 Die folgenden Bitmasken werden zusammen mit dem Flag verwendet, um zu bestimmen, welche Optionen unterstützt werden:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 Beschreibungen der folgenden Isolationsstufen finden Sie in die Beschreibung des SQL_DEFAULT_TXN_ISOLATION.  
  
 Zum Festlegen der Isolationsstufe für Transaktionen, die eine Anwendung ruft **SQLSetConnectAttr** das SQL_ATTR_TXN_ISOLATION-Attribut festgelegt. Weitere Informationen finden Sie unter [Funktion SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber gibt sql_txn_serializable festgelegt sind stets, unterstützt. Ein Transitional FIPS-Ebene – konforme Treiber wird immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_UNION (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Unterstützung für die **UNION** Klausel:  
  
 SQL_U_UNION = der Datenquelle unterstützt die **UNION** Klausel.  
  
 SQL_U_UNION_ALL = der Datenquelle unterstützt die **alle** -Schlüsselwort in der **UNION** Klausel. (**SQLGetInfo** SQL_U_UNION und SQL_U_UNION_ALL in diesem Fall gibt.)  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber wird immer diese beiden Optionen zurück, da unterstützt.  
  
 SQL_USER_NAME (ODBC 1.0)  
 Eine Zeichenfolge mit dem Namen in einer bestimmten Datenbank, die von den Anmeldenamen ein unterscheiden kann verwendet werden soll.  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 Eine Zeichenfolge, die das Jahr der Veröffentlichung der Open Group-Spezifikation gibt an, mit denen die Version des ODBC-Treiber-Managers vollständig entspricht.  
  
 SQL_ACCESSIBLE_PROCEDURES (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn der Benutzer alle Prozeduren zurückgegebenes ausführen kann **SQLProcedures**; "N", wenn Prozeduren möglicherweise zurückgegeben, dass der Benutzer ausführen kann.  
  
 SQL_ACCESSIBLE_TABLES (ODBC 1.0)  
 Eine Zeichenfolge: "Y", wenn der Benutzer **wählen** Berechtigungen, um alle Tabellen zurückgegebenes **SQLTables**; "N", wenn es möglicherweise Tabellen zurückgegeben, dass der Benutzer zugreifen kann.  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 Ein SQLUSMALLINT-Wert, der die maximale Anzahl von aktiven Umgebungen angibt, die der Treiber unterstützt werden. Wenn angegebene unbegrenzt ist, oder der Grenzwert unbekannt ist, wird dieser Wert auf 0 (null) festgelegt.  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Unterstützung für Aggregationsfunktionen:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 Ein SQL-92-Eintrag-Ebene – konforme-Treiber werden immer alle diese Optionen zurück, da unterstützt.  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ALTER DOMAIN** Anweisung, wie definiert in SQL-92, von der Datenquelle unterstützt. Ein vollständige SQL-92-Ebene – kompatibler Treiber wird immer alle den Bitmasken zurückgegeben. Ein Rückgabewert von "0" bedeutet, dass die **ALTER DOMAIN** Anweisung wird nicht unterstützt.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = hinzufügen, die eine Einschränkung für die Domäne unterstützt wird (vollständige Ebene)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<Domäne alter > \<Set Domain Default-Klausel > wird unterstützt (vollständige Ebene)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION = \<Definition von Einschränkungsklausel-Name > wird unterstützt, für die Benennung von Domäne Einschränkung (Intermediate-Stufe)  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<Drop Domäne Constraint-Klausel > wird unterstützt (vollständige Ebene)  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<Domäne alter > \<Drop Domain Default-Klausel > wird unterstützt (vollständige Ebene)  
  
 Geben Sie die folgenden Bits unterstützten \<Einschränkung Attribute > Wenn \<Domäne-Einschränkung hinzufügen > unterstützt wird (das SQL_AD_ADD_DOMAIN_CONSTRAINT Bit festgelegt ist):  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE (vollständige Stufe) SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (vollständige Stufe) SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (vollständige Stufe) SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (vollständige Stufe)  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 Eine SQLUINTEGER-Bitmaske, die beim Aufzählen der Klauseln in der **ALTER TABLE** Anweisung, die von der Datenquelle unterstützt.  
  
 Die SQL-92 oder FIPS-Konformität-Ebene, die an der diese Funktion unterstützt werden muss, wird in Klammern neben jeder Bitmaske angezeigt.  
  
 Die folgenden Bitmasken werden verwendet, um zu bestimmen, welche Klauseln unterstützt werden:  
  
 SQL_AT_ADD_COLUMN_COLLATION = \<Spalte hinzufügen >-Klausel unterstützt wird, mit der Funktion Spaltensortierreihenfolge (vollständige Stufe) angeben (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT = \<Spalte hinzufügen >-Klausel unterstützt wird, mit der Einrichtung von spaltenstandards (FIPS Transitional Stufe) angeben (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE = \<Spalte hinzufügen > ist (FIPS Transitional Stufe) unterstützt (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT = \<Spalte hinzufügen >-Klausel unterstützt wird, mit der Funktion spalteneinschränkungen (FIPS Transitional Stufe) angeben (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT = \<tabelleneinschränkung hinzufügen >-Klausel unterstützt (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION = \<Einschränkungsdefinition-Name > ist für die Benennung von Spalten- und tabelleneinschränkungen (Intermediate-Stufe) unterstützt (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE = \<Drop Spalte > CASCADE unterstützt wird (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT = \<Spalte alter > \<Drop Column-Standard-Klausel > ist (Intermediate-Stufe) unterstützt (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT = \<Drop Spalte > RESTRICT unterstützt wird (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<Drop Spalte > RESTRICT unterstützt wird (FIPS Transitional Stufe) (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT = \<Spalte alter > \<Satz Spalte Default-Klausel > ist (Intermediate-Stufe) unterstützt (ODBC 3.0)  
  
 Geben Sie die folgenden Bits die Unterstützung \<Einschränkung Attribute > Wenn das Angeben von Spalten- oder tabelleneinschränkungen unterstützt wird (das SQL_AT_ADD_CONSTRAINT Bit festgelegt ist):  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (vollständige Stufe) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (vollständige Stufe) (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE (vollständige Stufe) (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE (vollständige Stufe) (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 Eine SQLUINTEGER-Wert, der die Ebene der asynchrone Unterstützung im Treiber angibt:  
  
 SQL_AM_CONNECTION = Verbindung zum Servicelevel asynchrone Ausführung wird unterstützt. Alle Anweisungshandle eines bestimmten Verbindungshandles zugeordnet sind, im asynchronen Modus oder im synchronen Modus sind. Ein Anweisungshandle für eine Verbindung darf nicht im asynchronen Modus sein, während ein anderes Anweisungshandle über dieselbe Verbindung im synchronen Modus (und umgekehrt) ist.  
  
 SQL_AM_STATEMENT =-Anweisung Ebene asynchrone Ausführung wird unterstützt. Einige Anweisungshandle eines Verbindungshandles zugeordnet können im asynchronen Modus sein, wohingegen andere Anweisungshandles auf die gleiche Verbindung im synchronen Modus sind.  
  
 SQL_AM_NONE = asynchrone Modus wird nicht unterstützt.  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 Eine SQLUINTEGER-Bitmaske, die das Verhalten des Treibers in Bezug auf die Verfügbarkeit der Zeile auflisten zählt. Die folgenden Bitmasken werden zusammen mit der Typ der Informationen verwendet:  
  
 SQL_BRC_ROLLED_UP = Zeilenanzahl für aufeinander folgende INSERT-, DELETE- oder UPDATE-Anweisungen in einem Rollup enthalten sind. Wenn dieses Bit nicht festgelegt ist, sind die Zeilenanzahl für jede Anweisung verfügbar.  
  
 SQL_BRC_PROCEDURES = Zeilenanzahl, falls vorhanden, sind verfügbar, wenn ein Batch in einer gespeicherten Prozedur ausgeführt wird. Wenn Zeilenanzahl verfügbar sind, können sie nach oben oder einzeln erhältlich, je nach den SQL_BRC_ROLLED_UP Bit rückgängig gemacht werden.  
  
 SQL_BRC_EXPLICIT = Zeilenanzahl, falls vorhanden, sind verfügbar, wenn ein Batch ausgeführt wird, direkt durch Aufrufen **SQLExecute** oder **SQLExecDirect**. Wenn Zeilenanzahl verfügbar sind, können sie nach oben oder einzeln erhältlich, je nach den SQL_BRC_ROLLED_UP Bit rückgängig gemacht werden.  
  
## <a name="example"></a>Beispiel  
 **SQLGetInfo** gibt Listen von unterstützten Optionen als eine SQLUINTEGER-Bitmaske in **InfoValuePtr*. Die Bitmaske für jede Option wird zusammen mit dem Flag verwendet, um zu bestimmen, ob die Option unterstützt wird.  
  
 Beispielsweise konnte eine Anwendung den folgenden Code verwenden, um festzustellen, ob die skalare SUBSTRING-Funktion, durch den Treiber, die der Verbindung zugeordnet unterstützt wird.  
  
 Ein weiteres Beispiel der Verwendung von **SQLGetInfo**, finden Sie unter [SQLTables-Funktion](../../../odbc/reference/syntax/sqltables-function.md).  
  
```  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,   
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)   
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>Verwandte Funktionen  
 Die Einstellung der Verbindungsattribut zurückgeben  
 [SQLGetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 Bestimmen, ob ein Treiber eine Funktion unterstützt.  
 [SQLGetFunctions-Funktion](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Die Einstellung eines Attributs Anweisung zurückgeben  
 [SQLGetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 Zurückgeben von Informationen zu Datentypen für eine Datenquelle  
 [SQLGetTypeInfo-Funktion](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
