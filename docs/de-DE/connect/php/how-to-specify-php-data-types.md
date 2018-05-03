---
title: 'Vorgehensweise: Angeben von PHP-Datentypen | Microsoft Docs'
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
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8b80353cc49c37da13b8e8e46ef3b758ed47aef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-specify-php-data-types"></a>Vorgehensweise: PHP-Datentypen festlegen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Wenn Sie den PDO_SQLSRV-Treiber verwenden, können Sie mittels „PDOStatement::bindColumn“ und „PDOStatement::bindParam“ den PHP-Datentyp festlegen, wenn Sie Daten vom Server abrufen. Weitere Informationen finden Sie unter [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) und [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) .  
  
Die folgenden Schritten zeigen zusammenfassend, wie PHP-Datentypen beim Abruf vom Server mit dem SQLSRV-Treiber festgelegt werden:  
  
1.  Einrichten und Ausführen einer Transact-SQL-Abfrage mit [Sqlsrv_query](../../connect/php/sqlsrv-query.md) oder eine Kombination von [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[Sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Stellen Sie eine Datenzeile für das Lesen mit [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)bereit.  
  
3.  Verwenden Sie [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) , um die Felddaten einer ausgegebenen Zeile mit dem gewünschten, im dritten optionalen Parameter festgelegten PHP-Datentyp abzurufen. Wenn der optionale dritte Parameter nicht angegeben wird, werden die Daten laut den PHP-Standarddatentypen zurückgegeben. Informationen zu den PHP-Standarddatentypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
    Informationen über die Konstanten, die zur Angabe des PHP-Datentyps finden Sie unter im PHPTYPEs-Abschnitt der [Konstanten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel werden Zeilen von der *Production.ProductReview* -Tabelle der AdventureWorks-Datenbank abgerufen. Jede zurückgegebene Zeile den *ReviewDate* -Feld als Zeichenfolge abgerufen und die *Kommentare* -Feld als Stream abgerufen. Die Streamdateien werden mit der PHP [fpassthru](http://php.net/manual/en/function.fpassthru.php) -Funktion dargestellt.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
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
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Im Beispiel Abruf des zweiten Feldes (*ReviewDate*) als Zeichenfolge Millisekunden-Genauigkeit des Datentyps "DateTime" von SQL Server. Standardmäßig wird der SQL Server-Datentyp DATETIME als PHP-DateTime-Objekt abgerufen, wobei die Millisekunden-Genauigkeit verloren geht.  
  
Abrufen von das vierte Feld (*Kommentare*) wird als Stream zu Demonstrationszwecken. Standardmäßig wird der SQL Server-Datentyp „nvarchar(3850)“ als eine Zeichenfolge abgerufen. Dies ist für die meisten Situationen akzeptabel.   
  
> [!NOTE]  
> Die [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) -Funktion bietet eine Möglichkeit, Feldinformationen inklusive Feldtypinformationen zu erhalten bevor eine Abfrage durchgeführt wird.  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)

[Gewusst wie: Abrufen von Eingabe-/Ausgabeparametern mit dem SQLSRV-Treiber](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
