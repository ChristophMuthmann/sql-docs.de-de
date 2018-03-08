---
title: Sqlsrv_prepare | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: sqlsrv_prepare
apitype: NA
helpviewer_keywords:
- executing queries
- API Reference, sqlsrv_prepare
- sqlsrv_prepare
ms.assetid: 8c74c697-3296-4f5d-8fb9-e361f53f19a6
caps.latest.revision: "52"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 56dbdc5aad9e0c9362ee7d5f9ddb5650a920130d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrvprepare"></a>sqlsrv_prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Erstellt eine Anweisungsressource, die mit der angegebenen Verbindung verknüpft ist. Diese Funktion ist nützlich für die Ausführung mehrerer Abfragen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_prepare(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parameter  
*$conn*: Mit der erstellten Anweisung verknüpfte Verbindungsressource.  
  
*$tsql*: der Transact-SQL-Ausdruck, der erstellten Anweisung entspricht.  
  
*$params* [OPTIONAL]: ein **Array** von Werten, die Parametern in einer parametrisierten Abfrage entsprechen. Jedes Element des Arrays kann eines der folgenden sein:
  
-   Ein Literalwert  
  
-   Ein Verweis auf eine PHP-Variable.  
  
-   Ein **Array** mit der folgenden Struktur:  
  
    ```  
    array(&$value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    > [!NOTE]  
    > Als Abfrageparameter übergebene Variablen sollten durch Verweis und nicht als Wert übergeben werden. Übergeben Sie beispielsweise `&$myVariable` anstelle von `$myVariable`. Eine PHP-Warnung wird ausgelöst, wenn eine Abfrage mit Parametern per-Wert ausgeführt wird.  
  
    In der folgenden Tabelle sind die Elemente des Arrays beschrieben.  
  
    |Element|Beschreibung|  
    |-----------|---------------|  
    |*&$value*|Ein Literalwert oder ein Verweis auf eine PHP-Variable.|  
    |*$direction*[OPTIONAL]|Eines der folgenden **SQLSRV_PARAM_\***  Konstanten, um die parameterrichtung anzugeben: **SQLSRV_PARAM_IN**, **SQLSRV_PARAM_OUT**, **SQLSRV_PARAM_INOUT**. Der Standardwert ist **SQLSRV_PARAM_IN**.<br /><br />Weitere Informationen zu PHP-Konstanten finden Sie unter [Konstanten &#40; Microsoft Drivers for PHP for SQLServer &#41; ](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$phpType*[OPTIONAL]|Ein **SQLSRV_PHPTYPE_\***  Konstante, die PHP-Datentyp des zurückgegebenen Werts angibt.|  
    |*$sqlType*[OPTIONAL]|Ein **SQLSRV_SQLTYPE_\***  Konstante, die die SQL Server-Datentyp des Eingabewerts angibt.|  
  
*$options* [OPTIONAL]: ein assoziatives Array, das Abfrageeigenschaften festlegt. In der folgenden Tabelle sind die unterstützten Schlüssel und die entsprechenden Werte aufgeführt:  
  
|Key|Unterstützte Werte|Beschreibung|  
|-------|--------------------|---------------|  
|QueryTimeout|Ein positiver ganzzahliger Wert|Legt das Abfragetimeout in Sekunden fest. Standardmäßig wartet der Treiber unbegrenzt auf Ergebnisse.|  
|SendStreamParamsAtExec|**WAHR** oder **FALSCH**<br /><br />Der Standardwert ist **true**.|Konfiguriert den Treiber zur alle Streamdaten bei der Ausführung zu senden (**"true"**), oder Streamdaten in Blöcken zu senden (**"false"**). In der Standardeinstellung ist dieser Wert mit **true**festgelegt. Weitere Informationen finden Sie unter [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md).|  
|Bildlauffähigkeit|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|Weitere Informationen zu diesen Werten finden Sie unter [Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).|  
  
## <a name="return-value"></a>Rückgabewert  
Eine Anweisungsressource. Wenn die Anweisungsressource nicht erstellt werden kann, wird **false** zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
Wenn Sie eine Anweisung vorbereiten, die Variablen als Parameter verwendet, werden die Variablen an die Anweisung gebunden. Das bedeutet, dass die Anweisung beim nächsten Ausführen mit aktualisierten Parametern laufen wird, wenn Sie die Variablenwerte aktualisieren.  
  
Die Kombination von **sqlsrv_prepare** und **sqlsrv_execute** trennt Anweisungsvorbereitung und Ausführen der Anweisung in zwei Funktionsaufrufe und kann verwendet werden, um parametrisierte Abfragen ausführen. Diese Funktion eignet sich zum mehrfachen Ausführen einer Anweisung mit verschiedenen Parameterwerten für jede Ausführung.  
  
Alternative Strategien zum Schreiben und Lesen großer Datenmengen finden Sie unter [Batches von SQL-Anweisungen](http://go.microsoft.com/fwlink/?LinkId=104225) und [BULK INSERT](http://go.microsoft.com/fwlink/?LinkId=104226).  
  
Weitere Informationen finden Sie unter [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird eine Anweisung vorbereitet und ausgeführt. Die Anweisung ausgeführt (finden Sie unter [Sqlsrv_execute](../../connect/php/sqlsrv-execute.md)), aktualisiert diese ein Feld in der *Sales.SalesOrderDetail* Tabelle der AdventureWorks-Datenbank. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ?   
         WHERE SalesOrderDetailID = ?";  
  
/* Assign parameter values. */  
$param1 = 5;  
$param2 = 10;  
$params = array(&$param1, &$param2);  
  
/* Prepare the statement. */  
if ($stmt = sqlsrv_prepare($conn, $tsql, $params)) {
    echo "Statement prepared.\n";  
} else {  
    echo "Statement could not be prepared.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement. */  
if (sqlsrv_execute($stmt)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Statement could not be executed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird veranschaulicht, wie eine Anweisung vorbereitet wird und diese dann mit verschiedenen Parameterwerten erneut ausgeführt wird. Im Beispiel wird die *OrderQty* -Spalte der *Sales.SalesOrderDetail* -Tabelle der AdventureWorks-Datenbank aktualisiert. Nachdem die Updates abgeschlossen sind, wird die Datenbank abgefragt, um sicherzustellen, dass erfolgreich aktualisiert wurde. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  
  
/* Define the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail  
         SET OrderQty = ?  
         WHERE SalesOrderDetailID = ?";  
  
/* Initialize parameters and prepare the statement. Variables $qty  
and $id are bound to the statement, $stmt1. */  
$qty = 0; $id = 0;  
$stmt1 = sqlsrv_prepare($conn, $tsql, array(&$qty, &$id));  
if ($stmt1) {  
    echo "Statement 1 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the SalesOrderDetailID and OrderQty information. This array  
maps the order ID to order quantity in key=>value pairs. */  
$orders = array(1=>10, 2=>20, 3=>30);  
  
/* Execute the statement for each order. */  
foreach ($orders as $id => $qty) {  
    // Because $id and $qty are bound to $stmt1, their updated  
    // values are used with each execution of the statement.   
    if (sqlsrv_execute($stmt1) === false) {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
echo "Orders updated.\n";  
  
/* Free $stmt1 resources.  This allows $id and $qty to be bound to a different statement.*/  
sqlsrv_free_stmt($stmt1);  
  
/* Now verify that the results were successfully written by selecting   
the newly inserted rows. */  
$tsql = "SELECT OrderQty   
         FROM Sales.SalesOrderDetail   
         WHERE SalesOrderDetailID = ?";  
  
/* Prepare the statement. Variable $id is bound to $stmt2. */  
$stmt2 = sqlsrv_prepare($conn, $tsql, array(&$id));  
if ($stmt2) {  
    echo "Statement 2 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement for each order. */  
foreach (array_keys($orders) as $id)  
{  
    /* Because $id is bound to $stmt2, its updated value   
    is used with each execution of the statement. */  
    if (sqlsrv_execute($stmt2)) {  
        sqlsrv_fetch($stmt2);  
        $quantity = sqlsrv_get_field($stmt2, 0);  
        echo "Order $id is for $quantity units.\n";  
    } else {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
  
/* Free $stmt2 and connection resources. */  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> Es wird empfohlen, die Zeichenfolgen als Eingaben zu verwenden, wenn Werte zum Binden einer [decimal oder numeric-Spalte](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) und Genauigkeit sichergestellt werden, wie Sie PHP mit eingeschränkter Genauigkeit für [Gleitkommazahlen](http://php.net/manual/en/language.types.float.php).

## <a name="example"></a>Beispiel  
In diesem Codebeispiel wird gezeigt, wie einen decimal-Wert als Eingabeparameter gebunden werden.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_prepare($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);
sqlsrv_execute($stmt);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Vorgehensweise: Ausführen von parametrisierten Abfragen](../../connect/php/how-to-perform-parameterized-queries.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
[Vorgehensweise: Streamen von Daten](../../connect/php/how-to-send-data-as-a-stream.md)  
[Verwenden direktionaler Parameter](../../connect/php/using-directional-parameters.md)  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[Aktualisieren von Daten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
  
