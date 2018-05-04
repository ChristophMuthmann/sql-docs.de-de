---
title: 'Vorgehensweise: Senden von Daten als Stream | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
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
helpviewer_keywords:
- updating data
- streaming data
ms.assetid: ab6b95d6-b6e6-4bd7-a18c-50f2918f7532
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb37449d6175ed82b0acd1ac87f0771b14add570
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-send-data-as-a-stream"></a>Vorgehensweise: Streamen von Daten
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] nutzt PHP-Datenströme, um große Objekte an den Server zu senden. In diesem Thema wird erklärt, wie Sie Daten in Strömen senden können. Im ersten Beispiel wird mithilfe des SQLSRV-Treibers die Standardvorgehensweise veranschaulicht, bei der alle Datenstromdaten direkt bei der Abfrageausführung gesendet werden. Im zweiten Beispiel wird den SQLSRV-Treiber veranschaulicht, wie Sie bis zu acht Kilobyte (8 kB) Senden von datenstromdaten gleichzeitig an den Server.  
  
Im dritten Beispiel wird veranschaulicht, wie Sie mithilfe des PDO_SQLSRV-Treibers Datenstromdaten an den Server senden.  
  
## <a name="example-sending-stream-data-at-execution"></a>Beispiel: Senden von Datenstromdaten bei Ausführung
Im folgenden Beispiel wird eine einzelne Zeile in die *Production.ProductReview* Tabelle der AdventureWorks-Datenbank eingefügt. Die Kundenkommentare (*$comments*) werden als Datenstrom mithilfe der PHP geöffnet [Fopen](http://php.net/manual/en/function.fopen.php) Funktion, und klicken Sie dann an den Server nach der Ausführung der Abfrage gestreamt.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Die Ausgabe wird in die Konsole geschrieben.  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Execute the query. All stream data is sent upon execution.*/  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
else  
{  
     echo "The query was successfully executed.";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example-sending-stream-data-using-sqlsrvsendstreamdata"></a>Beispiel: Senden von Sqlsrv_send_stream_data Stream mithilfe von Daten
Das nächste Beispiel ähnelt dem vorherigen Beispiel identisch, aber das Standardverhalten Senden von datenstromdaten bei Ausführung deaktiviert ist. Im Beispiel wird [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md) verwendet, um Datenstromdaten an den Server zu senden. Bis zu acht Kilobyte (8 kB) Daten mit jedem Aufruf gesendet **Sqlsrv_send_stream_data**. Das Skript zählt die Anzahl der Aufrufe durch **sqlsrv_send_stream_data** und zeigt sie in der Konsole an.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Die Ausgabe wird in die Konsole geschrieben.  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
                                               ReviewerName,  
                                               ReviewDate,  
                                               EmailAddress,  
                                               Rating,  
                                               Comments)  
         VALUES (?, ?, ?, ?, ?, ?)";  
  
/* Set the parameter values and put them in an array.  
Note that $comments is opened as a stream. */  
$productID = '709';  
$name = 'Customer Name';  
$date = date("Y-m-d");  
$email = 'customer@name.com';  
$rating = 3;  
$comments = fopen( "data://text/plain,[ Insert lengthy comment here.]",  
                  "r");  
$params = array($productID, $name, $date, $email, $rating, $comments);  
  
/* Turn off the default behavior of sending all stream data at  
execution. */  
$options = array("SendStreamParamsAtExec" => 0);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params, $options);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Send up to 8K of parameter data to the server with each call to  
sqlsrv_send_stream_data. Count the calls. */  
$i = 1;  
while( sqlsrv_send_stream_data( $stmt))   
{  
     echo "$i call(s) made.\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Obwohl in den Beispielen in diesem Thema nur Zeichendaten an den Server gesendet werden, können Daten aller Formate als Strom gesendet werden. Sie können die in diesem Thema erläuterten Techniken beispielsweise nutzen, um Bilder im Binärformat als Ströme zu senden.  
  
## <a name="example-sending-an-image-as-a-stream"></a>Beispiel: Senden ein Bild als Stream 
  
```  
<?php  
   $server = "(local)";   
   $database = "Test";  
   $conn = new PDO( "sqlsrv:server=$server;Database = $database", "", "");  
  
   $binary_source = fopen( "data://text/plain,", "r");  
  
   $stmt = $conn->prepare("insert into binaries (imagedata) values (?)");  
   $stmt->bindParam(1, $binary_source, PDO::PARAM_LOB);   
  
   $conn->beginTransaction();  
   $stmt->execute();  
   $conn->commit();  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Aktualisieren von Daten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Abrufen von Daten als Stream mit dem SQLSRV-Treiber](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
