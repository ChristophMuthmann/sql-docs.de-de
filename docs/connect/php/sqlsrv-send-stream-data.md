---
title: Sqlsrv_send_stream_data | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_send_stream_data
apitype: NA
helpviewer_keywords:
- sqlsrv_send_stream_data
- API Reference, sqlsrv_send_stream_data
- streaming data
ms.assetid: 826c2d45-694f-42b8-b12b-cd4523a31883
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8a1a99ec3ab0b84a90ad97bfc353d5f3c061057b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvsendstreamdata"></a>sqlsrv_send_stream_data
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Sendet Daten aus Parameterstreams an den Server. Bis zu acht Kilobyte (8 KB) Daten mit jedem Aufruf gesendet **Sqlsrv_send_stream_data**.  
  
> [!NOTE]  
> In der Standardeinstellung werden alle Streamdaten an den Server gesendet, wenn eine Abfrage ausgeführt wird. Wenn dieses Standardverhalten nicht geändert wird, müssen Sie **sqlsrv_send_stream_data** nicht verwenden, um Datenstromdaten an den Server zu senden. Informationen zum Ändern des Standardverhaltens finden Sie im Parameter-Abschnitt [sqlsrv_query](../../connect/php/sqlsrv-query.md) oder [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_send_stream_data( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Anweisungsressource, die einer ausgeführten Anweisung entspricht.  
  
## <a name="return-value"></a>Rückgabewert  
Boolescher Wert: **true** wenn weitere Daten gesendet werden sollen. Andernfalls lautet der Wert **false**.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird eine Produktprüfung als Stream geöffnet und an den Server gesendet. Das Standardverhalten, alle Streamdaten zum Zeitpunkt der Ausführung zu senden, ist deaktiviert. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Define the query. */  
$tsql = "UPDATE Production.ProductReview   
         SET Comments = ( ?)   
         WHERE ProductReviewID = 3";  
  
/* Open parameter data as a stream and put it in the $params array. */  
$comment = fopen( "data://text/plain,[ Insert lengthy comment.]", "r");  
$params = array( &$comment);  
  
/* Prepare the statement. Use the $options array to turn off the  
default behavior, which is to send all stream data at the time of query  
execution. */  
$options = array("SendStreamParamsAtExec"=>0);  
$stmt = sqlsrv_prepare( $conn, $tsql, $params, $options);  
  
/* Execute the statement. */  
sqlsrv_execute( $stmt);  
  
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
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Aktualisieren von Daten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  

