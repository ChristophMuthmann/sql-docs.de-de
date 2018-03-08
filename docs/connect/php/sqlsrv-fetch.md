---
title: Sqlsrv_fetch | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: sqlsrv_fetch
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch
- API Reference, sqlsrv_fetch
- retrieving data, as a single field
ms.assetid: a5a640a1-6e7d-452e-8b66-850a4dc2ce89
caps.latest.revision: "39"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f9e7e835dbc1033fc5351f6a7af161c8ca021026
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="sqlsrvfetch"></a>sqlsrv_fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Macht die nächste Zeile eines Resultsets zum Lesen verfügbar. Verwendung [Sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) Felder einer Zeile zu lesen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_fetch( resource $stmt[, row[, ]offset])  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Anweisungsressource, die einer ausgeführten Anweisung entspricht.  
  
> [!NOTE]  
> Eine Anweisung muss ausgeführt werden, bevor Ergebnisse abgerufen werden können. Informationen zur Ausführung einer Anweisung finden Sie unter [sqlsrv_query](../../connect/php/sqlsrv-query.md) und [sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
*Zeile* [OPTIONAL]: einer der folgenden Werte, die Zeile spezifiziert, die auf in einem Resultset zugegriffen wird, welches einen bildlauffähigen Cursor verwendet:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Weitere Informationen zu diesen Werten finden Sie unter [Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
*Offset* [OPTIONAL]: SQLSRV_SCROLL_ABSOLUTE und sqlsrv_scroll_relative verwenden verwendet wird, um die abzurufende Zeile anzugeben. Der erste Datensatz im Resultset ist „0“.  
  
## <a name="return-value"></a>Rückgabewert  
Wenn die nächste Zeile des Resultsets erfolgreich abgerufen wurde, wird **true** zurückgegeben. Wenn keine weiteren Ergebnisse im Resultset vorhanden sind, wird **NULL** zurückgegeben. Wenn ein Fehler aufgetreten ist, wird **false** zurückgegeben.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird **sqlsrv_fetch** verwendet, um eine Zeile von Daten abzurufen, die eine Produktprüfung und den Namen des Bearbeiters enthält. Zum Abrufen von Daten aus dem Resultset [Sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) verwendet wird. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of SQL Server type nvarchar. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false)  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream ))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
