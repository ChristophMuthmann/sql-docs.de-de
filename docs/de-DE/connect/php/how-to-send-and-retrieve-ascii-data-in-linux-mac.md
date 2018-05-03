---
title: 'Vorgehensweise: Senden und Abrufen von ASCII-Daten in Linux und MacOS (SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 5b02a85e322ceb6fd5a2154f7da945a5d3c9ed8b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>Vorgehensweise: Senden und Abrufen von ASCII-Daten in Linux und MacOS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Artikel wird davon ausgegangen, die Gebietsschemas aus ASCII-(nicht UTF-8) generiert oder in Ihren Linux- oder MacOS-Systemen installiert wurden. 

Zum Senden oder Abrufen von ASCII-Zeichensätze an den Server:  

1.  Ist das gewünschte Gebietsschema nicht die Standardeinstellung in Ihrer Umgebung, stellen Sie sicher, dass Sie aufrufen `setlocale(LC_ALL, $locale)` vor dem Herstellen der ersten Verbindung. Die PHP-setlocale()-Funktion ändert das Gebietsschema nur für das aktuelle Skript, und wenn nach dem Herstellen der ersten Verbindungs aufgerufen, er kann ignoriert werden.
 
2.  Wenn Sie den SQLSRV-Treiber verwenden, können Sie angeben `'CharacterSet' => SQLSRV_ENC_CHAR` als Verbindung Option, aber dieser Schritt ist optional, da dies die Standardeinstellung ist Codierung.

3.  Wenn Sie den PDO_SQLSRV-Treiber verwenden, gibt es zwei Möglichkeiten. Legen Sie beim Herstellen der Verbindung zuerst `PDO::SQLSRV_ATTR_ENCODING` auf `PDO::SQLSRV_ENCODING_SYSTEM` (z. B. zum Festlegen einer Verbindungsoption, finden Sie unter [PDO:: __construct](../../connect/php/pdo-construct.md)). Auch nachdem die Verbindung erfolgreich hergestellt, fügen Sie dieser Zeile hinzu `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
Wenn Sie die Codierung des eine Verbindungsressource (im SQLSRV) oder ein Verbindungsobjekt (PDO_SQLSRV) angeben, wird vom Treiber angenommen, dass die anderen Optionszeichenfolgen dieselbe Codierung verwendet. Auch beim Servernamen und den Abfragezeichenfolgen geht er vom selben Zeichensatz aus.  
  
Die standardcodierung für PDO_SQLSRV-Treiber ist UTF-8 (PDO:: sqlsrv_encoding_utf8), im Gegensatz zu den SQLSRV-Treiber. Weitere Informationen zu diesen Konstanten finden Sie unter [Konstanten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). 
  
## <a name="example"></a>Beispiel  
Die folgenden Beispiele veranschaulichen, wie zum Senden und Abrufen von ASCII-Daten mithilfe der PHP-Treibern für SQL Server durch Angabe eines bestimmten Gebietsschemas vor dem Herstellen der Verbindung. Die Gebietsschemas in verschiedene Linux-Plattformen können aus der gleichen Gebietsschemas in MacOS unterschiedlich benannt werden. Das Gebietsschema uns ISO-8859-1 (Latin 1) ist z. B. `en_US.ISO-8859-1` unter Linux, während im MacOS heißt `en_US.ISO8859-1`.
  
In den Beispielen wird angenommen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] auf einem Server installiert ist. Alle Ausgabe wird an den Browser geschrieben, wenn die Beispiele über den Browser ausgeführt werden.  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[Arbeiten mit UTF-8-Daten](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[Datenupdates &#40;Microsoft Drivers for PHP for SQLServer&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Beispielanwendung &#40;SQLSRV-Treiber&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
