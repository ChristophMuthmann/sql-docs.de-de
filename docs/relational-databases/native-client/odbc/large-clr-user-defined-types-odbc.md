---
title: "Große benutzerdefinierte CLR-Typen (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4da32a24c00ca9539cca04c3886d19f73f9ab578
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="large-clr-user-defined-types-odbc"></a>Große benutzerdefinierte CLR-Typen (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In diesem Abschnitt werden Änderungen an ODBC in SQL Server Native Client erläutert, durch die große benutzerdefinierte Common Language Runtime-Typen (CLR-UDTs) unterstützt werden.  
  
 Ein Beispiel, das ODBC-Unterstützung für große CLR-UDTs, finden Sie unter [Unterstützung für große UDTs](../../../relational-databases/native-client-odbc-how-to/support-for-large-udts.md).  
  
 Weitere Informationen zur Unterstützung großer CLR-UDTs in SQL Server Native Client finden Sie unter [Large CLR User-Defined Typen](../../../relational-databases/native-client/features/large-clr-user-defined-types.md).  
  
## <a name="data-format"></a>Datenformat  
 SQL Server Native Client verwendet SQL_SS_LENGTH_UNLIMITED, um anzugeben, dass die Größe einer Spalte 8.000 Bytes für LOB-Typen (Large Object) überschreitet. Ab SQL Server 2008 wird derselbe Wert für CLR-UDTs mit einer Größe von über 8.000 Bytes verwendet.  
  
 UDT-Werte werden als Bytearrays dargestellt. Konvertierungen zu und von hexadezimalen Zeichenfolgen werden unterstützt. Literalwerte werden mit dem Präfix 0x als hexadezimale Zeichenfolgen dargestellt.  
  
 In der folgenden Tabelle wird die Datentypzuordnung in Parametern und Resultsets gezeigt:  
  
|SQL Server-Datentyp|SQL-Datentyp|Wert|  
|--------------------------|-------------------|-----------|  
|CLR-UDT|SQL_SS_UDT|-151 (sqlncli.h)|  
  
 In der folgenden Tabelle werden die entsprechenden Strukturen und ODBC C-Typen erläutert. CLR-UDT ist grundsätzlich ein **Varbinary** -Typ mit zusätzlichen Metadaten.  
  
|SQL-Datentyp|Speicherlayout|C-Datentyp|Wert (sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (unsigned Char \*)|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>Deskriptorfelder für Parameter  
 In den IPD-Feldern werden Informationen wie folgt zurückgegeben:  
  
|Deskriptorfeld|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|Der Name des Katalogs, der den UDT enthält.|Der Name des Katalogs, der den UDT enthält.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|Der Name des Schemas, das den UDT enthält.|Der Name des Schemas, die den UDT enthält.|  
|SQL_CA_SS_UDT_TYPE_NAME|Der Name des UDT.|Der Name des UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|Der vollqualifizierte Name des UDT.|Der vollqualifizierte Name des UDT.|  
  
 Für UDT-Parameter muss SQL_CA_SS_UDT_TYPE_NAME immer über festgelegt werden **SQLSetDescField**. SQL_CA_SS_UDT_CATALOG_NAME und SQL_CA_SS_UDT_SCHEMA_NAME sind optional.  
  
 Ist der UDT in derselben Datenbank mit einem anderen Schema als die Tabelle definiert, muss SQL_CA_SS_UDT_SCHEMA_NAME festgelegt werden.  
  
 Ist der UDT in einer anderen Datenbank als die Tabelle definiert, müssen SQL_CA_SS_UDT_CATALOG_NAME und SQL_CA_SS_UDT_SCHEMA_NAME festgelegt werden.  
  
 Bei Fehlern oder Auslassungen in den Einstellungen für SQL_CA_SS_UDT_TYPE_NAME, SQL_CA_SS_UDT_CATALOG_NAME oder SQL_CA_SS_UDT_SCHEMA_NAME wird ein Diagnosedatensatz mit SQLSTATE HY000 und einem serverspezifischen Meldungstext generiert.  
  
## <a name="descriptor-fields-for-results"></a>Deskriptorfelder für Ergebnisse  
 In den IRD-Feldern werden Informationen wie folgt zurückgegeben:  
  
|Deskriptorfeld|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|Der Name des Katalogs, der den UDT enthält.|Der Name des Katalogs, der den UDT enthält.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|Der Name des Schemas, das den UDT enthält.|Der Name des Schemas, das den UDT enthält.|  
|SQL_CA_SS_UDT_TYPE_NAME|Der Name des UDT.|Der Name des UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|Der vollqualifizierte Name des UDT.|Der vollqualifizierte Name des UDT.|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>Von SQLColumns und SQLProcedureColumns zurückgegebene Spaltenmetadaten (Katalogmetadaten)  
 Die folgenden Spaltenwerte werden für UDTs zurückgegeben:  
  
|Spaltenname|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|Der Name des UDT.|Der Name des UDT.|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULL|NULL|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULL|NULL|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|Der Name des Katalogs, der den UDT enthält.|Der Name des Katalogs, der den UDT enthält.|  
|SS_UDT_SCHEMA_NAME|Der Name des Schemas, das den UDT enthält.|Der Name des Schemas, das den UDT enthält.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Der vollqualifizierte Name des UDT.|Der vollqualifizierte Name des UDT.|  
  
 Die letzten drei Spalten sind treiberspezifische Spalten. Sie werden nach ODBC-definierten Spalten, jedoch vor dem vorhandenen treiberspezifischen Spalten des Resultsets von SQLColumns oder SQLProcedureColumns hinzugefügt.  
  
 Für einzelne UDTs oder für den generischen Typ "Udt" werden keine Zeilen von ' SQLGetTypeInfo ', zurückgegeben.  
  
## <a name="bindings-and-conversions"></a>Bindungen und Konvertierungen  
 Die unterstützten Konvertierungen von SQL- zu C-Datentypen sind wie folgt:  
  
|Konvertierung von und zu:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Unterstützt *|  
|SQL_C_BINARY|Supported|  
|SQL_C_CHAR|Unterstützt *|  
  
 \*Binäre Daten werden in eine hexadezimale Zeichenfolge konvertiert.  
  
 Die unterstützten Konvertierungen von C- zu SQL-Datentypen sind wie folgt:  
  
|Konvertierung von und zu:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Unterstützt *|  
|SQL_C_BINARY|Supported|  
|SQL_C_CHAR|Unterstützt *|  
  
 \*Einer hexadezimalen Zeichenfolge in Binärdaten Konvertierung erfolgt.  
  
## <a name="sqlvariant-support-for-udts"></a>SQL_VARIANT-Unterstützung für UDTs  
 UDTs werden in SQL_VARIANT-Spalten nicht unterstützt.  
  
## <a name="bcp-support-for-udts"></a>BCP-Unterstützung für UDTs  
 UDT-Werte können nur als Zeichen oder Binärwerte importiert und exportiert werden.  
  
## <a name="downlevel-client-behavior-for-udts"></a>Verhalten von Clients der unteren Ebene für UDTs  
 Für UDTs gilt die folgende Typzuordnung zu Clients der unteren Ebene:  
  
|Serverversion|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|**UDT**|**varbinary(max)**|  
|SQL Server 2008 und höher|**UDT**|**UDT**|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>ODBC-Funktionen, die große CLR-UDTs unterstützen  
 In diesem Abschnitt werden Änderungen an SQL Server Native Client-ODBC-Funktionen erläutert, durch die große CLR-UDTs unterstützt werden.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 UDT-Ergebnisspaltenwerte werden von SQL- in C-Datentypen konvertiert, wie im Abschnitt "Bindungen und Konvertierungen" oben erläutert.  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 Für UDTs sind folgende Werte erforderlich:  
  
|SQL-Datentyp|*Parametertype*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Die für UDTs zurückgegebenen Werte sind im Abschnitt "Deskriptorfelder für Ergebnisse" oben erläutert.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 Für UDTs zurückgegebenen Werte werden wie im Abschnitt "Spalte Metadaten Zurückgeben von SQLColumns und SQLProcedureColumns (Katalogmetadaten)" weiter oben in diesem Thema beschrieben.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Für UDTs werden folgende Werte zurückgegeben:  
  
|SQL-Datentyp|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 Für UDTs werden folgende Werte zurückgegeben:  
  
|SQL-Datentyp|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 UDT-Ergebnisspaltenwerte werden von SQL- in C-Datentypen konvertiert, wie im Abschnitt "Bindungen und Konvertierungen" oben erläutert.  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 UDT-Ergebnisspaltenwerte werden von SQL- in C-Datentypen konvertiert, wie im Abschnitt "Bindungen und Konvertierungen" oben erläutert.  
  
### <a name="sqlgetdata"></a>SQLGetData  
 UDT-Ergebnisspaltenwerte werden von SQL- in C-Datentypen konvertiert, wie im Abschnitt "Bindungen und Konvertierungen" oben erläutert.  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 Die für die neuen Datentypen verfügbaren Deskriptorfelder sind in den Abschnitten "Deskriptorfelder für Parameter" und "Deskriptorfelder für Ergebnisse" oben erläutert.  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 Für UDTs werden folgende Werte zurückgegeben:  
  
|SQL-Datentyp|Typ|SubType|Länge|Genauigkeit|Dezimalstellen|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 Die für UDTs zurückgegebenen Werte sind im Abschnitt "Von SQLColumns und SQLProcedureColumns zurückgegebene Spaltenmetadaten (Katalogmetadaten)" oben erläutert.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 Die für UDTs zurückgegebenen Werte sind im Abschnitt "Von SQLColumns und SQLProcedureColumns zurückgegebene Spaltenmetadaten (Katalogmetadaten)" oben erläutert.  
  
### <a name="sqlputdata"></a>SQLPutData  
 UDT-Parameterwerte werden von C- in SQL-Datentypen konvertiert, wie im Abschnitt "Bindungen und Konvertierungen" oben erläutert.  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 Die neuen Datentypen verfügbaren Deskriptorfeld werden in der "Deskriptorfelder für Parameter" und den Abschnitten "Deskriptorfelder für Ergebnisse" oben in diesem Thema beschrieben.  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 Die zulässigen Werte für UDTs lauten wie folgt:  
  
|SQL-Datentyp|Typ|SubType|Länge|Genauigkeit|Dezimalstellen|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (Länge kleiner oder gleich 8.000 Bytes)|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> (Länge größer als 8.000 Bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>'SQLSpecialColumns'  
 Die für die Spalten DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH und DECIMAL_DIGTS zurückgegebenen UDT-Werte sind im Abschnitt "Von SQLColumns und SQLProcedureColumns zurückgegebene Spaltenmetadaten (Katalogmetadaten)" oben erläutert.  
  
## <a name="see-also"></a>Siehe auch  
 [Große benutzerdefinierte CLR-Typen](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
  
  
