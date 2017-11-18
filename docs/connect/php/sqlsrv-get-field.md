---
title: Sqlsrv_get_field | Microsoft Docs
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
- sqlsrv_get_field
apitype: NA
helpviewer_keywords:
- sqlsrv_get_field
- API Reference, sqlsrv_get_field
- retrieving data, as a single field
ms.assetid: fa17cc56-fb38-433b-a40d-65642f04dc23
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5251bb4c0c2118ccff1985cc512094fb3a8340b4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvgetfield"></a>sqlsrv_get_field
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ruft Daten vom angegebenen Feld der aktuellen Zeile ab. Auf die Felddaten muss gemäß der Reihenfolge zugegriffen werden. So kann beispielsweise nicht auf Daten aus dem ersten Feld zugegriffen werden nachdem auf Daten vom zweiten Feld zugegriffen wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_get_field( resource $stmt, int $fieldIndex [, int $getAsType])  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Anweisungsressource, die einer ausgeführten Anweisung entspricht.  
  
*$fieldIndex*: Der Index des abzurufenden Felds. Indizes beginnen mit 0.  
  
*$getAsType* [OPTIONAL]: ein **SQLSRV** Konstanten (**SQLSRV_PHPTYPE_\***), die den PHP-Datentyp für die zurückgegebenen Daten bestimmt. Informationen zu unterstützten Datentypen finden Sie unter [Konstanten &#40; Microsoft Drivers for PHP for SQLServer &#41; ](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). Wenn kein Rückgabetyp spezifiziert ist, wird ein PHP-Typ zurückgegeben. Informationen zu PHP-Standardtypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md). Informationen zum Spezifizieren von PHP-Datentypen finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="return-value"></a>Rückgabewert  
Die Felddaten. Sie können den PHP-Datentyp der zurückgegebenen Daten festlegen, indem Sie den *$getAsType* -Parameter verwenden. Falls kein Rückgabedatentyp festgelegt ist, wird der PHP-Standarddatentyp zurückgegeben. Informationen zu PHP-Standardtypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md). Informationen zum Spezifizieren von PHP-Datentypen finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="remarks"></a>Hinweise  
Die Kombination von **Sqlsrv_fetch** und **Sqlsrv_get_field** Vorwärtscursor Zugriff auf Daten bereitstellt.  
  
Die Kombination von **Sqlsrv_fetch**/**Sqlsrv_get_field** lädt nur ein Feld aus einem Resultset Zeile in den Skriptspeicher und erlaubt die Festlegung PHP-Rückgabetypen. (Informationen über das Angeben von PHP-Rückgabetyps finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).) Diese Kombination von Funktionen macht es möglich Daten als Stream abzurufen. (Informationen zum Abrufen von Daten als Stream finden Sie unter [Abrufen von Daten als Stream mit dem SQLSRV-Treiber](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md).)  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel ruft eine Datenzeile ab, die eine Produktprüfung enthält, sowie den Namen des Prüfers. Zum Abrufen von Daten aus dem Resultset wird **sqlsrv_get_field** verwendet. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
Comments are of the SQL Server nvarchar type. */  
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
if( sqlsrv_fetch( $stmt ) === false )  
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
while( !feof( $stream))  
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
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  

