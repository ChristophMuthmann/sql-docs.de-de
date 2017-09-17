---
title: Sqlsrv_query | Microsoft Docs
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
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1dbc5c20a1d9fb1210bb7729f36299ea4392ebc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Bereitet eine Anweisung vor und führt diese aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_query( resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parameter  
*$conn*: Die mit der vorbereiteten Anweisung verknüpfte Verbindungsressource.  
  
*$tsql*: der Transact-SQL-Ausdruck, der der vorbereiteten Anweisung entspricht.  
  
*$params* [OPTIONAL]: ein **Array** von Werten, die Parametern in einer parametrisierten Abfrage entsprechen. Jedes Element des Arrays kann eines der folgenden sein:  
  
-   Ein Literalwert  
  
-   Eine PHP-Variable.  
  
-   Ein **Array** mit der folgenden Struktur:  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    Die Beschreibung für jedes Element des Arrays finden Sie in der folgenden Tabelle:  
  
    |Element|Beschreibung|  
    |-----------|---------------|  
    |*$value*|Ein Literalwert, eine PHP-Variable oder eine PHP-Variable als Verweis.|  
    |*$direction*[OPTIONAL]|Eines der folgenden **SQLSRV_PARAM_\* ** Konstanten, um die parameterrichtung anzugeben: **SQLSRV_PARAM_IN**, **SQLSRV_PARAM_OUT**, **SQLSRV_PARAM_INOUT**. Der Standardwert ist **SQLSRV_PARAM_IN**.<br /><br />Weitere Informationen zu PHP-Konstanten finden Sie unter [Konstanten &#40; Microsoft Drivers for PHP for SQLServer &#41; ](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$phpType*[OPTIONAL]|Ein **SQLSRV_PHPTYPE_\* ** Konstante, die PHP-Datentyp des zurückgegebenen Werts angibt.<br /><br />Weitere Informationen zu PHP-Konstanten finden Sie unter [Konstanten &#40; Microsoft Drivers for PHP for SQLServer &#41; ](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$sqlType*[OPTIONAL]|Ein **SQLSRV_SQLTYPE_\* ** Konstante, die die SQL Server-Datentyp des Eingabewerts angibt.<br /><br />Weitere Informationen zu PHP-Konstanten finden Sie unter [Konstanten &#40; Microsoft Drivers for PHP for SQLServer &#41; ](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
  
*$options* [OPTIONAL]: ein assoziatives Array, das Abfrageeigenschaften festlegt. Die folgenden Schlüssel werden unterstützt:  
  
|Key|Unterstützte Werte|Beschreibung|  
|-------|--------------------|---------------|  
|QueryTimeout|Ein positiver ganzzahliger Wert|Legt das Abfragetimeout in Sekunden fest. Standardmäßig wartet der Treiber unbegrenzt auf Ergebnisse.|  
|SendStreamParamsAtExec|**WAHR** oder **FALSCH**<br /><br />Der Standardwert ist **true**.|Konfiguriert den Treiber zur alle Streamdaten bei der Ausführung zu senden (**"true"**), oder Streamdaten in Blöcken zu senden (**"false"**). In der Standardeinstellung ist dieser Wert mit **true**festgelegt. Weitere Informationen finden Sie unter [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md).|  
|Bildlauffähigkeit|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|Weitere Informationen zu diesen Werten finden Sie unter [Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).|  
  
## <a name="return-value"></a>Rückgabewert  
Eine Anweisungsressource. Wenn die Anweisung kann nicht erstellt und/oder ausgeführt wird, werden **"false"** wird zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
Die **Sqlsrv_query** Funktion eignet sich ideal für einmalige Abfragen sollte auch die Standardauswahl, um Abfragen auszuführen, es sei denn, besondere Umstände gelten. Diese Funktion bietet eine optimierte Methode zum Ausführen einer Abfrage mit einem Minimum von Codes. Die **sqlsrv_query** -Funktion führt jeweils eine Anweisungsvorbereitung und eine Anweisungsausführung durch und kann verwendet werden, um parametrisierte Abfragen auszuführen.  
  
Weitere Informationen finden Sie unter [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird eine einzelne Zeile in die *Sales.SalesOrderDetail* -Tabelle der AdventureWorks-Datenbank eingefügt. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
> [!NOTE]  
> Obwohl im folgenden Beispiel wird eine INSERT-Anweisung verwendet, um die Verwendung des **Sqlsrv_query** für Einmaliges Ausführen einer Anweisung, gilt das Konzept von Transact-SQL-Anweisungen.  
  
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
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if( $stmt )  
{  
     echo "Row successfully inserted.\n";  
}  
else  
{  
     echo "Row insertion failed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird ein Feld in der *Sales.SalesOrderDetail* -Tabelle der AdventureWorks-Datenbank aktualisiert. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ( ?)   
         WHERE SalesOrderDetailID = ( ?)";  
  
/* Assign literal parameter values. */  
$params = array( 5, 10);  
  
/* Execute the query. */  
if( sqlsrv_query( $conn, $tsql, $params))  
{  
      echo "Statement executed.\n";  
}   
else  
{  
      echo "Error in statement execution.\n";  
      die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Vorgehensweise: Ausführen von parametrisierten Abfragen](../../connect/php/how-to-perform-parameterized-queries.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
[Vorgehensweise: Streamen von Daten](../../connect/php/how-to-send-data-as-a-stream.md)  
[Verwenden direktionaler Parameter](../../connect/php/using-directional-parameters.md)  
  

