---
title: SQLGetInfo zurückgegebenen Werte für dBASE | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- SQLGetInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetInfo
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: af64753c-c758-4b68-954b-2c84e3bbd93f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5ed1a4b22123a34cd8690a7a1b837da6c0373b2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinfo-returned-values-for-dbase"></a>SQLGetInfo zurückgegebenen Werte für dBASE
Die folgende Tabelle enthält die Programmiersprache C# defines für die *fInfoType* Argument und die entsprechenden Werte zurückgegebenes **SQLGetInfo**. Diese Informationen abgerufen werden kann, durch Übergeben der aufgelisteten Programmiersprache C# defines **SQLGetInfo** in der *fInfoType* Argument. Weitere Informationen zu den Werten zurückgegebenes **SQLGetInfo**, finden Sie unter der *ODBC Programmer's Reference*.  
  
> [!NOTE]  
>  Wobei **SQLGetInfo** gibt eine 32-Bit-Bitmaske, ein senkrechter Strich (&#124;) stellt ein bitweises OR.  
  
|Infotyp|Rückgabewert|  
|--------------|--------------------|  
|SQL_ACCESSIBLE_PROCEDURES|"N"|  
|SQL_ACCESSIBLE_TABLES|"Y"|  
|SQL_ACTIVE_ENVIRONMENTS|0|  
|SQL_AGGREGATE_FUNCTIONS|Alle festlegen|  
|SQL_ALTER_DOMAIN|0|  
|SQL_ALTER_TABLE|Mehrere Werte|  
|SQL_ASYNC_MODE|0|  
|SQL_BATCH_ROW_COUNT|0|  
|SQL_BATCH_SUPPORT|0|  
|SQL_BOOKMARK_PERSISTENCE|Mehrere Werte|  
|SQL_CATALOG_LOCATION|SQL_QL_START|  
|SQL_CATALOG_NAME|"Y"|  
|SQL_CATALOG_NAME_SEPARATOR|"\\"|  
|SQL_CATALOG_TERM|"Directory"|  
|SQL_CATALOG_USAGE|Mehrere Werte|  
|SQL_COLLATION_SEQ|""|  
|SQL_COLUMN_ALIAS|"Y"|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_CB_NON_NULL|  
|SQL_CONVERT_BIGINT|0|  
|SQL_CONVERT_BINARY|Mehrere Werte|  
|SQL_CONVERT_BIT|0|  
|SQL_CONVERT_CHAR|Mehrere Werte|  
|SQL_CONVERT_DATE|Mehrere Werte|  
|SQL_CONVERT_DECIMAL|0|  
|SQL_CONVERT_DOUBLE|Mehrere Werte|  
|SQL_CONVERT_FLOAT|Mehrere Werte|  
|SQL_CONVERT_FUNCTIONS|SQL_FN_CVT_CONVERT|  
|SQL_CONVERT_INTEGER|Mehrere Werte|  
|SQL_CONVERT_LONGVARBINARY|Mehrere Werte|  
|SQL_CONVERT_LONGVARCHAR|Mehrere Werte|  
|SQL_CONVERT_NUMERIC|Mehrere Werte|  
|SQL_CONVERT_REAL|Mehrere Werte|  
|SQL_CONVERT_SMALLINT|Mehrere Werte|  
|SQL_CONVERT_TIME|Mehrere Werte|  
|SQL_CONVERT_TIMESTAMP|Mehrere Werte|  
|SQL_CONVERT_TINYINT|Mehrere Werte|  
|SQL_CONVERT_VARBINARY|Mehrere Werte|  
|SQL_CONVERT_VARCHAR|Mehrere Werte|  
|SQL_CORRELATION_NAME|SQL_CN_ANY|  
|SQL_CREATE_ASSERTION|0|  
|SQL_CREATE_CHARACTER_SET|0|  
|SQL_CREATE_COLLATION|0|  
|SQL_CREATE_DOMAIN|0|  
|SQL_CREATE_SCHEMA|0|  
|SQL_CREATE_TABLE|SQL_CT_CREATE_TABLE|  
|SQL_CREATE_TRANSLATION|0|  
|SQL_CREATE_VIEW|0|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_CB_CLOSE|  
|SQL_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_DATA_SOURCE_NAME|Der DSN aus Odbc.ini, oder "" Wenn DRIVER-Schlüsselwort in Odbc.ini verwendet wird|  
|SQL_DATA_SOURCE_READ_ONLY|"N" (Dies hängt von der Datenquelle.)|  
|SQL_DATABASE_NAME|Aktuelle Datenbankverzeichnis|  
|SQL_DATETIME_LITERALS|0|  
|SQL_DBMS_NAME|"DBASE"|  
|SQL_DBMS_VER|Mehrere Werte|  
|SQL_DDL_INDEX|Mehrere Werte|  
|SQL_DEFAULT_TXN_ISOLATION|0|  
|SQL_DESCRIBE_PARAMETER|0|  
|SQL_DRIVER_HDBC|Verarbeitet die vom Treiber-Manager.|  
|SQL_DRIVER_HENV|Verarbeitet die vom Treiber-Manager.|  
|SQL_DRIVER_HLIB|Verarbeitet die vom Treiber-Manager.|  
|SQL_DRIVER_HSTMT|Verarbeitet die vom Treiber-Manager.|  
|SQL_DRIVER_NAME|"OdbcJt32.dll"|  
|SQL_DRIVER_ODBC_VER|"3.51.0000"|  
|SQL_DRIVER_VER|"4.00.*Nnnn*" (*Nnnn* gibt das Erstellungsdatum)|  
|SQL_DROP_ASSERTION|0|  
|SQL_DROP_CHARACTER_SET|0|  
|SQL_DROP_COLLATION|0|  
|SQL_DROP_DOMAIN|0|  
|SQL_DROP_SCHEMA|0|  
|SQL_DROP_TABLE|SQL_DT_DROP_TABLE|  
|SQL_DROP_TRANSLATION|0|  
|SQL_DROP_VIEW|SQL_DV_DROP_VIEW|  
|SQL_EXPRESSIONS_IN_ORDERBY|"Y"|  
|SQL_FILE_USAGE|SQL_FILE_TABLE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT|  
|SQL_GETDATA_EXTENSIONS|Mehrere Werte|  
|SQL_GROUP_BY|SQL_GB_GROUP_BY_CONTAINS_SELECT|  
|SQL_IDENTIFIER_CASE|SQL_IC_UPPER (der Qualifizierer ist in gemischter Schreibung zurückgegeben, sodass Windows NT das Verzeichnis suchen können.)|  
|SQL_IDENTIFIER_QUOTE_CHAR|"'" (Sichern Anführungszeichen)|  
|SQL_KEYWORDS|Mehrere Werte|  
|SQL_LIKE_ESCAPE_CLAUSE|"N"|  
|SQL_MAX_BINARY_LITERAL_LEN|255|  
|SQL_MAX_CATALOG_NAME_LEN|66|  
|SQL_MAX_CHAR_LITERAL_LEN|254|  
|SQL_MAX_COLUMN_NAME_LEN|10|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|10|  
|SQL_MAX_COLUMNS_IN_INDEX|0 (Beschränken von unbekannten oder nicht zutreffend)|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|10|  
|SQL_MAX_COLUMNS_IN_SELECT|255|  
|SQL_MAX_COLUMNS_IN_TABLE|255|  
|SQL_MAX_CONCURRENT_ACTIVITIES|0|  
|SQL_MAX_CURSOR_NAME_LEN|64|  
|SQL_MAX_DRIVER_CONNECTIONS|64|  
|SQL_MAX_INDEX_SIZE|220|  
|SQL_MAX_PROCEDURE_NAME_LEN|0|  
|SQL_MAX_ROW_SIZE|4000|  
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|"N"|  
|SQL_MAX_SCHEMA_NAME_LEN|0|  
|SQL_MAX_STATEMENT_LEN|65000|  
|SQL_MAX_TABLE_NAME_LEN|12|  
|SQL_MAX_TABLES_IN_SELECT|16|  
|SQL_MAX_USER_NAME_LEN|0|  
|SQL_MULT_RESULT_SETS|"N"|  
|SQL_MULTIPLE_ACTIVE_TXN|"Y"|  
|SQL_NEED_LONG_DATA_LEN|"N"|  
|SQL_NON_NULLABLE_COLUMNS|SQL_NNC_NON_NULL|  
|SQL_NULL_COLLATION|SQL_NC_LOW|  
|SQL_NUMERIC_FUNCTIONS|Mehrere Werte|  
|SQL_ODBC_SAG_CLI_-KONFORMITÄT|SQL_OSCC_COMPLIANT|  
|SQL_ODBC_SQL_INTEGRITY|"N"|  
|SQL_ODBC_VER|Vom Treiber-Manager|  
|SQL_OJ_CAPABILITIES|Mehrere Werte|  
|SQL_ORDER_BY_COLUMNS_IN_SELECT|"N"|  
|SQL_OUTER_JOINS|"Y"|  
|SQL_PROCEDURE_TERM|""|  
|SQL_PROCEDURES|"N"|  
|SQL_QUOTED_IDENTIFIER_CASE|SQL_IC_MIXED|  
|SQL_ROW_UPDATES|"N"|  
|SQL_SCHEMA_TERM|""|  
|SQL_SCHEMA_USAGE|0|  
|SQL_SCROLL_OPTIONS|Mehrere Werte|  
|SQL_SEARCH_PATTERN_ESCAPE|"\\"|  
|SQL_SERVER_NAME|"DBASE"|  
|SQL_SPECIAL_CHARACTERS|"~`@#$%^&*_-+=\\}{"';:?/><,.!'[]&#124;"|  
|SQL_STRING_FUNCTIONS|Mehrere Werte|  
|SQL_SUBQUERIES|Mehrere Werte|  
|SQL_SYSTEM_FUNCTIONS|0|  
|SQL_TABLE_TERM|"TABLE"|  
|SQL_TIMEDATE_ADD_INTERVALS|0|  
|SQL_TIMEDATE_DIFF_INTERVALS|0|  
|SQL_TIMEDATE_FUNCTIONS|Mehrere Werte|  
|SQL_TXN_CAPABLE|SQL_TC_NONE|  
|SQL_TXN_ISOLATION_OPTION|0|  
|SQL_UNION|Mehrere Werte|  
|SQL_USER_NAME|""|
