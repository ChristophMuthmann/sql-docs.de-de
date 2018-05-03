---
title: Sqlsrv_field_metadata | Microsoft Docs
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
ms.topic: conceptual
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e7f7d66bb363ec42b6dc0ad5e0d9cd019ffe78f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvfieldmetadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ruft Metadaten für die Felder einer vorbereiteten Anweisung ab. Informationen zum Vorbereiten einer Anweisung finden Sie unter [sqlsrv_query](../../connect/php/sqlsrv-query.md) oder [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Beachten Sie, dass **Sqlsrv_field_metadata** für jede vorbereitete Anweisung, vor oder nach der Ausführung aufgerufen werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Anweisungsressource für die Feldmetadaten gewünscht werden.  
  
## <a name="return-value"></a>Rückgabewert  
Ein **Array** von Arrays oder **false**. Das Array besteht aus einem Array für jedes Feld im Resultset. Jedes Teilarray hat Schlüssel, wie in der unten stehenden Tabelle beschrieben. Falls beim Abrufen der Feldmetadaten ein Fehler auftritt, wird **false** zurückgegeben.  
  
|Key|Description|  
|-------|---------------|  
|Name|Name der Spalte, der das Feld entspricht|  
|Typ|Numerischer Wert, der einem SQL-Typ entspricht|  
|Größe|Anzahl der Zeichen für die Felder eines bestimmten Zeichentyps (char(n), varchar(n), nchar(n), nvarchar(n), XML) Anzahl der Bytes für Felder vom Typ „binär“ (binary(n), varbinary(n), UDT). **NULL** für andere SQL Server-Datentypen.|  
|Genauigkeit|Die Genauigkeit für die Typen mit variabler Genauigkeit (real, numeric, decimal, datetime2, datetimeoffset und time). **NULL** für andere SQL Server-Datentypen.|  
|Dezimalstellen|Die Skalierung für die Typen mit variabler Skalierung (numeric, decimal, datetime2, datetimeoffset und time). **NULL** für andere SQL Server-Datentypen.|  
|NULL zulassen|Ein Enumerationswert, der angibt, ob die Spalte NULL-Werte zulässt (**SQLSRV_NULLABLE_YES**), die Spalte ist keine NULL-Werte zulässt (**SQLSRV_NULLABLE_NO**), oder es ist nicht bekannt, wenn die Spalte NULL-Werte zulässt ( **SQLSRV_NULLABLE_UNKNOWN**).|  
  
Die folgende Tabelle enthält mehr Informationen zu den Schlüsseln für jedes Teilarray (weiter Informationen zu diesen Typen finden Sie in der Dokumentation zu SQL Server):   
  
|SQL Server 2008-Datentyp|Typ|Min/Max Genauigkeit|Min/Max Skalierung|Größe|  
|-----------------------------|--------|----------------------|------------------|--------|  
|bigint|SQL_BIGINT (-5)|||8|  
|BINARY|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|Datum|SQL_TYPE_DATE (91)|10/10|0/0||  
|datetime|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|Decimal|SQL_DECIMAL (3)|1/38|0/Genauigkeitswert||  
|float|SQL_FLOAT (6)|4/8|||  
|image|SQL_LONGVARBINARY (-4)|||2 GB|  
|int|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|NCHAR|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|numeric|SQL_NUMERIC (2)|1/38|0/Genauigkeitswert||  
|nvarchar|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|real|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|smallint|SQL_SMALLINT (5)|||2 Bytes|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|text|SQL_LONGVARCHAR (-1)|||2 GB|  
|Uhrzeit|SQL_SS_TIME2 (-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8 Byte|  
|tinyint|SQL_TINYINT (-6)|||1 Byte|  
|udt|SQL_SS_UDT (-151)|||variable|  
|uniqueidentifier|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) Die Null (0) gibt an, das die Maximalgröße zulässig ist.  
  
Ein Schlüssel der NULL-Werte zulässt, kann entweder „Ja“ oder „Nein“ sein.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel erstellt eine Anweisungsressource, ruft  die Feldmetadaten ab und stellt sie dar. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Prepare the statement. */  
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
  
/* Get and display field metadata. */  
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata)  
{  
      foreach( $fieldMetadata as $name => $value)  
      {  
           echo "$name: $value\n";  
      }  
      echo "\n";  
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement  
resource, pre- or post-execution. */  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  

[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
