---
title: Abrufen von Zeichendaten als Stream mit dem SQLSRV-Treiber | Microsoft Docs
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
- retrieving data, as a character stream
- streaming data
ms.assetid: 3c0dbca4-abfc-4449-b133-66c819681840
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a2af695b619c54e23d2d08cc451408c7aa9889e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver"></a>Vorgehensweise: Abrufen von Zeichendaten als Stream mit dem SQLSRV-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Abrufen von Daten als Stream ist nur verfügbar im SQLSRV-Treiber von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], und ist nicht im PDO_SQLSRV-Treiber verfügbar.  
  
Der SQLSRV-Treiber nutzt PHP-Streams zum Abrufen großer Datenmengen vom Server. Im Beispiel in diesem Thema wird veranschaulicht, wie Zeichendaten als Stream abgerufen werden.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird eine einzelne Zeile von der *Production.ProductReview* -Tabelle der AdventureWorks-Datenbank abgerufen. Die *Kommentare* -Feld der zurückgegebenen Zeile wird als Stream abgerufen und angezeigt, indem Sie die PHP [Fpassthru](http://php.net/manual/function.fpassthru.php) Funktion.  
  
Das Abrufen von Daten als Stream erfolgt mithilfe von [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) und [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) als Zeichenstream spezifizierten Rückgabetyp. Der Rückgabetyp wird angegeben, unter Verwendung der Konstanten **SQLSRV_PHPTYPE_STREAM**. Informationen zu **Sqlsrv** -Konstanten finden Sie [Konstanten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
Das Beispiel setzt voraus, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
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
$tsql = "SELECT ReviewerName,   
               CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
               Rating,   
               Comments   
         FROM Production.ProductReview   
         WHERE ProductReviewID = ? ";  
  
/* Set the parameter value. */  
$productReviewID = 1;  
$params = array( $productReviewID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first three fields are retrieved  
as strings and the fourth as a stream with character encoding. */  
if(sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
echo "Date: ".sqlsrv_get_field( $stmt, 1 )."\n";  
echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
echo "Comments: ";  
$comments = sqlsrv_get_field( $stmt, 3,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
fpassthru($comments);  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Die ersten drei Felder werden entsprechend des jeweiligen PHP-Standardtyps zurückgegeben, da für sie kein PHP-Rückgabetyp angegeben ist. Informationen zu PHP-Datentypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md). Weitere Informationen zum Angeben von PHP-Rückgabetypen finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)

[Abrufen von Daten als Stream mit dem SQLSRV-Treiber](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
