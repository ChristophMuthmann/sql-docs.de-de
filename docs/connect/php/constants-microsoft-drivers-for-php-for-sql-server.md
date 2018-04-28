---
title: Konstanten (Microsoft Drivers for PHP for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
caps.latest.revision: 72
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a54937aab5ffad32eb4e2531234485058ecb6af5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>Konstanten (Microsoft-Treiber für PHP für SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema werden die Konstanten erläutert, die durch [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]definiert sind.  
  
## <a name="pdosqlsrv-driver-constants"></a>Konstanten zum Treiber PDO_SQLSRV  
Die Konstanten aufgelistet, auf die [PDO Website](http://php.net/manual/book.pdo.php) gelten in der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Im folgenden werden die Microsoft-spezifischen Konstanten im PDO_SQLSRV-Treiber beschrieben.  
  
### <a name="transaction-isolation-level-constants"></a>Konstanten der Transaktionsisolationsebene  
Der **TransactionIsolation** -Schlüssel, der mit [PDO::__construct](../../connect/php/pdo-construct.md)verwendet wird, akzeptiert eine der folgenden Konstanten:  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
Weitere Informationen zum **TransactionIsolation** -Schlüssel finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
  
### <a name="encoding-constants"></a>Codierungskonstanten  
Das Attribut PDO:: sqlsrv_attr_encoding übergeben werden kann, um [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO:: setAttribute](../../connect/php/pdo-setattribute.md), [PDO:: Prepare](../../connect/php/pdo-prepare.md), [PDOStatement: : BindColumn](../../connect/php/pdostatement-bindcolumn.md), und [Bindparam](../../connect/php/pdostatement-bindparam.md).  
  
Die verfügbaren Werte, die an PDO::SQLSRV_ATTR_ENCODING übergeben werden können, sind  
  
|Konstanten zum Treiber PDO_SQLSRV|Description|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|Die Daten sind ein einfacher, uncodierter und nicht übersetzter Strom aus unbearbeiteten Bytes.<br /><br />Dies gilt nicht für PDO::setAttribute.|  
|PDO::SQLSRV_ENCODING_SYSTEM|Daten stellen 8-Bit-Zeichen gemäß der Codepage des im System eingestellten Windows-Gebietsschemas dar. Alle Multi-Byte-Zeichen oder Zeichen, die nicht in dieser Codepage zugeordnet sind, werden mit einem Einzelbyte-Fragezeichen (?) Zeichen durch ersetzt.|  
|PDO::SQLSRV_ENCODING_UTF8|Daten sind in UTF-8-Codierung. Diese ist die Standardcodierung.|  
|PDO::SQLSRV_ENCODING_DEFAULT|Verwendet PDO::SQLSRV_ENCODING_SYSTEM, wenn bei der Verbindung angegeben.<br /><br />Verwenden Sie die Codierung der Verbindung, wenn diese in einer Prepare-Anweisung angegeben ist.|  
  
### <a name="query-timeout"></a>Abfragetimeout  
Das PDO::SQLSRV_ATTR_QUERY_TIMEOUT-Attribut ist eine beliebige positive ganze Zahl, die das Timeout in Sekunden darstellt. Null (0) ist die Standardeinstellung und bedeutet kein Timeout.  
  
Sie können angeben, das PDO:: sqlsrv_attr_query_timeout-Attribut mit [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO:: setAttribute](../../connect/php/pdo-setattribute.md), und [PDO:: Prepare](../../connect/php/pdo-prepare.md).  
  
### <a name="direct-or-prepared-execution"></a>Direkte oder vorbereitete Ausführung  
Sie können die Ausführung von direkten Abfragen oder die vorbereitete Ausführung mit dem Attribut PDO::SQLSRV_ATTR_DIRECT_QUERY auswählen. PDO:: sqlsrv_attr_direct_query kann festgelegt werden, mit [PDO:: Prepare](../../connect/php/pdo-prepare.md) oder [PDO:: setAttribute](../../connect/php/pdo-setattribute.md). Weitere Informationen zu PDO:: sqlsrv_attr_direct_query finden Sie unter [direkte Anweisungsausführung und vorbereitete Anweisungsausführung im PDO_SQLSRV-Treiber](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  

### <a name="handling-numeric-fetches"></a>Behandlung von numerischen abruft
Das PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE-Attribut kann verwendet werden, numerische Abrufvorgängen von Spalten mit numerischen SQL-Typen (Bit, ganze Zahl, "smallint", "tinyint", "float" und Real) behandelt. Wenn PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE festgelegt ist, auf "true", die Ergebnisse aus einer Spalte mit ganzen Zahlen werden dargestellt als int-Elementen, während SQL: verschiebt und versendeten als Gleitkommawerte dargestellt werden. Dieses Attribut kann festgelegt werden, mit [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md). 


## <a name="sqlsrv-driver-constants"></a>SQLSRV-Treiberkonstanten  
Die folgenden Abschnitte listen die Konstanten auf, die der SQLSRV-Treiber verwendet.  
  
### <a name="err-constants"></a>ERR-Konstanten  
Die folgende Tabelle enthält die Konstanten, die verwendet werden, um anzugeben, ob [Sqlsrv_errors](../../connect/php/sqlsrv-errors.md) Fehler, Warnungen oder beides zurückgibt.  
  
|Wert|Description|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Fehler und Warnungen, die beim letzten **sqlsrv** -Funktionsaufruf generiert wurden, werden zurückgegeben. Dies ist der Standardwert.|  
|SQLSRV_ERR_ERRORS|Fehler und Warnungen aus dem letzten **sqlsrv** -Funktionsaufruf werden zurückgegeben.|  
|SQLSRV_ERR_WARNINGS|Warnungen aus dem letzten **sqlsrv** -Funktionsaufruf werden zurückgegeben.|  
  
### <a name="fetch-constants"></a>FETCH-Konstanten  
Die folgende Tabelle enthält die Konstanten, die verwendet werden, um den Typ des von [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)zurückgegebenen Arrays anzugeben.  
  
|SQLSRV-Konstante|Description|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** gibt die nächste Datenzeile als assoziatives Array zurück.|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** gibt die nächste Datenzeile als Array zurück, das sowohl numerische als auch assoziative Schlüssel aufweist. Dies ist der Standardwert.|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** gibt die nächste Datenzeile als numerisch indiziertes Array zurück.|  
  
### <a name="logging-constants"></a>Protokollierungskonstanten  
In diesem Abschnitt sind die Konstanten aufgelistet, die verwendet werden, um die Protokollierungseinstellungen mit [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)zu ändern. Weitere Informationen zur Protokollierung von Aktivitäten finden Sie unter [Logging Activity](../../connect/php/logging-activity.md).  
  
Die folgende Tabelle beschreibt die Konstanten, die als Wert für die **LogSubsystems** Einstellung verwendet werden können:  
  
|SQLSRV-Konstante (entsprechende Ganzzahl in Klammern)|Description|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Aktiviert die Protokollierung aller Subsysteme.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Aktiviert die Protokollierung der Verbindungsaktivität.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Aktiviert die Protokollierung der Initialisierungsaktivität.|  
|SQLSRV_LOG_SYSTEM_OFF(0)|Deaktiviert die Protokollierung.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Aktiviert die Protokollierung der Anweisungsaktivität.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Aktiviert die Protokollierung der fehlerfunktionsaktivität (z. B. **Handle_error** und **Handle_warning**).|  
  
Die folgende Tabelle listet die Konstanten auf, die als Wert für die **LogSeverity** -Einstellung verwendet werden können:  
  
|SQLSRV-Konstante (entsprechende Ganzzahl in Klammern)|Description|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Gibt an, dass Fehler, Warnungen und Hinweise protokolliert werden.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Gibt an, dass Fehler protokolliert werden.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Gibt an, dass Hinweise protokolliert werden.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Gibt an, dass Warnungen protokolliert werden.|  
  
### <a name="nullable-constants"></a>NULL-Wert-Konstanten  
Die folgende Tabelle enthält die Konstanten, die Sie verwenden können, um zu bestimmen, ob eine Spalte NULL-Werte zulässt oder ob diese Information nicht verfügbar ist. Sie können den Wert des **Nullable** -Schlüssels vergleichen, der von [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) zurückgegeben wird, um den Status der NULL-Wert-Behandlung der Spalte zu bestimmen.  
  
|SQLSRV-Konstante (entsprechende Ganzzahl in Klammern)|Description|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|In der Spalte ist NULL zulässig.|  
|SQLSRV_NULLABLE_NO (1)|NULL-Werte sind in der Spalte nicht zulässig.|  
|SQLSRV_NULLABLE_UNKNOWN (2)|Es ist nicht bekannt, ob die Spalte NULL-Werte zulässt.|  
  
### <a name="param-constants"></a>PARAM-Konstanten  
Die folgende Liste enthält die Konstanten für die Angabe der Parameterrichtung, wenn Sie [sqlsrv_query](../../connect/php/sqlsrv-query.md) oder [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)aufrufen.  
  
|SQLSRV-Konstante|Description|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|Gibt einen Eingabeparameter an.|  
|SQLSRV_PARAM_INOUT|Gibt einen bidirektionalen Parameter an.|  
|SQLSRV_PARAM_OUT|Gibt einen Ausgabeparameter an.|  
  
### <a name="phptype-constants"></a>PHPTYPE-Konstanten  
Die folgende Tabelle enthält die Konstanten, die verwendet werden, um die PHP-Datentypen zu beschreiben. Informationen zu PHP-Datentypen finden Sie unter [PHP-Typen](http://php.net/manual/en/language.types.php).  
  
|SQLSRV-Konstante|PHP-Datentyp|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Integer|  
|SQLSRV_PHPTYPE_DATETIME|Datetime|  
|SQLSRV_PHPTYPE_FLOAT|Float|  
|SQLSRV_PHPTYPE_STREAM($encoding<sup>1</sup>)|STREAM|  
|SQLSRV_PHPTYPE_STRING($encoding<sup>1</sup>)|String|  
  
1. **SQLSRV_PHPTYPE_STREAM** und **SQLSRV_PHPTYPE_STRING** akzeptieren einen Parameter, der die Codierung des Streams angibt. Die folgende Tabelle enthält die SQLSRV-Konstanten, die als Parameter akzeptiert werden sowie eine Beschreibung der zugehörigen Codierung.  
  
|SQLSRV-Konstante|Description|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|Die Daten werden als uncodierter und nicht übersetzter Strom aus unbearbeiteten Bytes vom Server zurückgegeben.|  
|SQLSRV_ENC_CHAR|Daten werden in 8-Bit-Zeichen gemäß der Codepage des Windows-Gebietsschemas zurückgegeben, das auf dem System installiert ist. Alle Multi-Byte-Zeichen oder Zeichen, die nicht in dieser Codepage zugeordnet sind, werden mit einem Einzelbyte-Fragezeichen (?) Zeichen durch ersetzt.<br /><br />Diese ist die Standardcodierung.|  
|„UTF-8“|Daten werden zurückgegeben, in UTF-8-Codierung. Diese Konstante wurde in Version 1.1 von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt. Weitere Informationen zur Unterstützung von UTF-8 finden Sie unter [Vorgehensweise: Senden und Abrufen UTF-8-Daten mithilfe von integrierten UTF-8 unterstützen](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|  
  
> [!NOTE]  
> Bei Verwendung von **SQLSRV_PHPTYPE_STREAM** oder **SQLSRV_PHPTYPE_STRING**, die Codierung angegeben werden. Wenn kein Parameter angegeben wird, wird ein Fehler zurückgegeben.  
  
Weiter Informationen zu diesen Konstanten finden Sie unter [Gewusst wie: Angeben von PHP-Datentypen](../../connect/php/how-to-specify-php-data-types.md), [Gewusst wie: Abrufen von Zeichendaten als Stream mit dem SQLSRV-Treiber](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md).  
  
### <a name="sqltype-constants"></a>SQLTYPE-Konstanten  
Die folgende Tabelle enthält die Konstanten, die verwendet werden, um die SQL Server-Datentypen zu beschreiben. Einige Konstanten sind funktionsähnliche und können mehrere Parameter, die entsprechen mit einfacher Genauigkeit, Dezimalstellen und/oder der Länge.  Beim Binden von Parametern, sollte die funktionsähnliche Konstanten verwendet werden. Für Vergleiche des Datentyps sind die Konstanten für standard (nicht funktionsähnliche) erforderlich. Informationen zu SQL Server-Datentypen finden Sie unter [-Datentypen (Transact-SQL).](../../t-sql/data-types/data-types-transact-sql.md) Informationen zu Genauigkeit, Dezimalstellen und Länge finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge (Transact-SQL).](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
|SQLSRV-Konstante|SQL Server-Datentyp|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|bigint|  
|SQLSRV_SQLTYPE_BINARY|BINARY|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|Char<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char|  
|SQLSRV_SQLTYPE_DATE|Datum<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|datetime|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|Decimal<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|Decimal|  
|SQLSRV_SQLTYPE_FLOAT|float|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|int|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|NCHAR<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|numerische<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|numeric|  
|SQLSRV_SQLTYPE_NVARCHAR,|Nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|nvarchar|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|real|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|smallint|  
|SQLSRV_SQLTYPE_SMALLMONEY|smallmoney|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|timestamp|  
|SQLSRV_SQLTYPE_TINYINT|tinyint|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|uniqueidentifier|  
|SQLSRV_SQLTYPE_UDT|UDT|  
|SQLSRV_SQLTYPE_VARBINARY|Varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary(MAX)|  
|SQLSRV_SQLTYPE_VARCHAR,|Varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|xml|  
  
1.  Dies ist ein veralteter Typ, der dem varbinary(max)-Typ zugeordnet ist.  
  
2.  Dies ist ein veralteter Typ, der dem neueren nvarchar-Typ zugeordnet ist.  
  
3.  Dies ist ein veralteter Typ, der dem neueren varchar-Typ zugeordnet ist.  
  
4.  Unterstützung für diesen Typ wurde in Version 1.1 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  

5.  Diese Konstanten in Vergleichsvorgängen Typ verwendet werden soll und nicht die Konstanten funktionsähnliche mit ähnlichen Syntax ersetzen. Für das Binden von Parametern, sollten Sie die funktionsähnliche Konstanten verwenden.

  
Die folgende Tabelle enthält die SQLTYPE-Konstanten, die Parameter und den Bereich der zulässigen Werte für den Parameter akzeptieren.  
  
|SQLTYPE|Parameter|Für Parameter zulässiger Bereich|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR,<br /><br />SQLSRV_SQLTYPE_VARCHAR,|charCount|1 - 8000|  
|SQLSRV_SQLTYPE_NCHAR,<br /><br />SQLSRV_SQLTYPE_NVARCHAR,|charCount|1 - 4000|  
|SQLSRV_SQLTYPE_BINARY,<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1 - 8000|  
|SQLSRV_SQLTYPE_DECIMAL<br /><br />SQLSRV_SQLTYPE_NUMERIC|precision|1 - 38|  
|SQLSRV_SQLTYPE_DECIMAL<br /><br />SQLSRV_SQLTYPE_NUMERIC|scale|1 - Genauigkeit|  
  
### <a name="transaction-isolation-level-constants"></a>Konstanten der Transaktionsisolationsebene  
Der **TransactionIsolation** -Schlüssel, der mit [sqlsrv_connect](../../connect/php/sqlsrv-connect.md)verwendet wird, akzeptiert eine der folgenden Konstanten:  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>Konstanten für Cursor und Durchführen eines Bildlaufs  
Die folgenden Konstanten geben die Art des Cursors an, den Sie in einem Resultset verwenden können:  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
Die folgenden Konstanten geben an, welche Zeile im Resultset ausgewählt werden soll:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Weitere Informationen zu diesen Konstanten finden Sie unter [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
  
