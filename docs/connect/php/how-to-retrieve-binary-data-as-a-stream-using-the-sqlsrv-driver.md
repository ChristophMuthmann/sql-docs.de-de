---
title: 'Gewusst wie: Abrufen von Binärdaten als Stream mithilfe des SQLSRV-Treibers'
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
- retrieving data, as a binary stream
- streaming data
ms.assetid: cd8d6382-abe6-48ee-9d10-4e6c52c0cb9a
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc64286141b6ec0736ae6427d4a55af8afa75269
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver"></a>Vorgehensweise: Abrufen von Binärdaten als Stream mithilfe des SQLSRV-Treibers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Das Abrufen von Daten als Stream ist nur im SQLSRV-Treiber von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] und nicht im PDO_SQLSRV-Treiber verfügbar.  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] nutzt PHP-Streams zum Abrufen großer Binärdatenmengen vom Server. Dieses Thema veranschaulicht, wie Binärdaten als Stream abgerufen werden.  
  
Verwenden der Streams zum Abrufen von Binärdaten, z. B. Bildern, verzichtet auf die Verwendung großer Mengen Skriptspeicher, indem nur Datenblöcke und nicht ganze Objekte in den Skriptspeicher geladen werden.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel werden Binärdaten, z. B. ein Bild, aus der *Production.ProductPhoto* -Tabelle der AdventureWorks-Datenbank abgerufen. Das Bild wird als Stream abgerufen und im Browser angezeigt.  
  
Das Abrufen von Bilddaten als Stream erfolgt mithilfe von [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) und [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) mit einem binären Stream als Rückgabetyp. Der Rückgabetyp wird unter Verwendung der Konstanten SQLSRV_PHPTYPE_STREAM** angegeben. Informationen zu **sqlsrv**-Konstanten finden Sie unter [Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über den Browser ausgeführt wird, werden alle Ausgaben im Browser geschrieben.  
  
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
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto   
         WHERE ProductPhotoID = ?";  
  
/* Set the parameter values and put them in an array. */  
$productPhotoID = 70;  
$params = array( $productPhotoID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data.  
The return data is retrieved as a binary stream. */  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0,   
                      SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY));  
   header("Content-Type: image/jpg");  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Die Angabe des Rückgabetyps im Beispiel veranschaulicht, wie der PHP-Rückgabetyp als binärer Stream angegeben wird. Technisch gesehen ist er nicht zwingend im Beispiel anzugeben, weil das *LargePhoto*-Feld den SQL Server-Typ „varbinarymax“ aufweist und dieser daher standardmäßig als binärer Stream zurückgegeben wird. Informationen zu PHP-Datentypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md). Weitere Informationen zum Angeben von PHP-Rückgabetypen finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Abrufen von Daten](../../connect/php/retrieving-data.md)

[Abrufen von Daten als Stream mit dem SQLSRV-Treiber](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
