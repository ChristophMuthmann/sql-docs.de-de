---
title: Beispielanwendung (SQLSRV-Treiber) | Microsoft Docs
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
- example application
ms.assetid: c0225395-3a2e-4561-a2f2-8050ad11c8e2
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: abc3fa7c4624a0de7547f961ac2a1f0886b914f4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="example-application-sqlsrv-driver"></a>Beispielanwendung (SQLSRV-Treiber)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Die Beispielanwendung „AdventureWorks Product Reviews“ ist eine Webanwendung, die den SQLSRV-Treiber von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]verwendet. Die Anwendung lässt den Benutzer durch die Eingabe eines Schlüsselwortes nach Produkten suchen, Prüfungen eines gewählten Produkts einsehen und schreiben sowie Bilder für ein gewähltes Produkt hochladen.  
  
### <a name="running-the-example-application"></a>Ausführen der Beispielanwendung  
  
1.  Installieren Sie [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Ausführliche Informationen finden Sie unter [erste Schritte mit Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md).
2.  Kopieren Sie den Code weiter unten in diesem Dokument in zwei Dateien: „adventureworks_demo.php“ und „photo.php“.  
3.  Platzieren Sie die „adventureworks_demo.php-“ und „photo.php“-Dateien im Stammverzeichnis Ihres Webservers.  
4.  Führen Sie die Anwendung durch Starten http://localhost/adventureworks_demo.php in Ihrem Browser.  
  
## <a name="requirements"></a>Anforderungen  
Um die Beispielanwendung „AdventureWorks Product Reviews“ auszuführen, muss Ihr Computer Folgendes erfüllen:  
  
-   Ihr System erfüllt die Anforderungen für [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Ausführliche Informationen finden Sie unter [System Requirements for Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
-   Die „adventureworks_demo.php“- und „photo.php“-Dateien befinden sich im Stammverzeichnis Ihres Webservers. Die Dateien müssen den weiter unten in diesem Dokument gelisteten Code enthalten.  
-   SQL Server 2005 oder SQL Server 2008 mit der [AdventureWorks2008](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) Datenbank angefügt wurde, auf dem lokalen Computer installiert ist.  
-   Ein Webbrowser ist installiert.  
  
## <a name="demonstrates"></a>Veranschaulicht  
Die Beispielanwendung „AdventureWorks Product Reviews“ demonstriert Folgendes:  
  
-   Öffnen einer Verbindung zu SQL Server mithilfe der Windows-Authentifizierung  
-   Ausführen einer parametrisierten Abfrage mit [sqlsrv_query](../../connect/php/sqlsrv-query.md)  
-   Vorbereiten und Ausführen einer parametrisierten Abfrage mithilfe der Kombination von [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) und [sqlsrv_execute](../../connect/php/sqlsrv-execute.md)  
-   Abrufen von Daten unter Verwendung von [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
-   Abrufen von Daten unter Verwendung einer Kombination von [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) und [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
-   Erhalten von Daten als Strom  
-   Senden von Datenströmen  
-   Suchen nach Fehlern  
  
## <a name="example"></a>Beispiel  
Die Beispielanwendung „AdventureWorks Product Reviews“ gibt Produktinformationen für alle Produkte, deren Namen die vom Benutzer eingegebene Zeichenfolge enthalten, von der Datenbank zurück. In der Liste der zurückgegebenen Produkte kann der Benutzer Prüfungen und Bilder sehen, ein Bild hinzufügen und eine Prüfung für ein gewähltes Produkt schreiben.  
  
Platzieren Sie den folgenden Code in einer Datei namens „adventureworks_demo.php“:  
  
```  
<!--=============  
This file is part of a Microsoft SQL Server Shared Source Application.  
Copyright (C) Microsoft Corporation.  All rights reserved.  
  
THIS CODE AND INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY  
KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE  
IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A  
PARTICULAR PURPOSE.  
============= *-->  
  
<!--Note: The presentation formatting of the example application -->  
<!-- is intentionally simple to emphasize the SQL Server -->  
<!-- data access code.-->  
<html>  
<head>  
<title>AdventureWorks Product Reviews</title>  
</head>  
<body>  
<h1 align='center'>AdventureWorks Product Reviews</h1>  
<h5 align='center'>This application is a demonstration of the   
                   procedural API (SQLSRV driver) of the Microsoft  
                   Drivers for PHP for SQL Server.</h5><br/>  
<?php  
$serverName = "(local)\sqlexpress";  
$connectionOptions = array("Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionOptions);  
if( $conn === false )  
die( FormatErrors( sqlsrv_errors() ) );  
  
if(isset($_REQUEST['action']))  
{  
switch( $_REQUEST['action'] )  
{  
/* Get AdventureWorks products by querying   
   against the product name.*/  
case 'getproducts':  
$params = array(&$_POST['query']);  
$tsql = "SELECT ProductID, Name, Color, Size, ListPrice   
FROM Production.Product   
WHERE Name LIKE '%' + ? + '%' AND ListPrice > 0.0";  
/*Execute the query with a scrollable cursor so  
  we can determine the number of rows returned.*/  
$cursorType = array("Scrollable" => SQLSRV_CURSOR_KEYSET);  
$getProducts = sqlsrv_query($conn, $tsql, $params, $cursorType);  
if ( $getProducts === false)  
die( FormatErrors( sqlsrv_errors() ) );  
  
if(sqlsrv_has_rows($getProducts))  
{  
$rowCount = sqlsrv_num_rows($getProducts);  
BeginProductsTable($rowCount);  
while( $row = sqlsrv_fetch_array( $getProducts, SQLSRV_FETCH_ASSOC))  
{  
PopulateProductsTable( $row );  
}  
EndProductsTable();  
}  
else  
{  
DisplayNoProdutsMsg();  
}  
GetSearchTerms( !null );  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $getProducts );  
sqlsrv_close( $conn );  
break;  
  
/* Get reviews for a specified productID. */  
case 'getreview':  
GetPicture( $_GET['productid'] );  
GetReviews( $conn, $_GET['productid'] );  
sqlsrv_close( $conn );  
break;  
  
/* Write a review for a specified productID. */  
case 'writereview':  
DisplayWriteReviewForm( $_POST['productid'] );  
break;  
  
/* Submit a review to the database. */  
case 'submitreview':  
/*Prepend the review so it can be opened as a stream.*/  
$comments = "data://text/plain,".$_POST['comments'];  
$stream = fopen( $comments, "r" );  
$tsql = "INSERT INTO Production.ProductReview (ProductID,  
   ReviewerName,  
   ReviewDate,  
   EmailAddress,  
   Rating,  
   Comments)   
 VALUES (?,?,?,?,?,?)";  
$params = array(&$_POST['productid'],  
&$_POST['name'],  
date("Y-m-d"),  
&$_POST['email'],  
&$_POST['rating'],   
&$stream);  
  
/* Prepare and execute the statement. */  
$insertReview = sqlsrv_prepare($conn, $tsql, $params);  
if( $insertReview === false )  
die( FormatErrors( sqlsrv_errors() ) );  
/* By default, all stream data is sent at the time of  
query execution. */  
if( sqlsrv_execute($insertReview) === false )  
die( FormatErrors( sqlsrv_errors() ) );   
sqlsrv_free_stmt( $insertReview );  
GetSearchTerms( true );  
  
/* Display a list of reviews, including the latest addition. */  
GetReviews( $conn, $_POST['productid'] );  
sqlsrv_close( $conn );  
break;  
  
        /* Display a picture of the selected product.*/  
        case 'displaypicture':  
            $tsql = "SELECT Name   
                     FROM Production.Product   
                     WHERE ProductID = ?";  
            $getName = sqlsrv_query($conn, $tsql,   
                                      array(&$_GET['productid']));  
            if( $getName === false )  
die( FormatErrors( sqlsrv_errors() ) );  
            if ( sqlsrv_fetch( $getName ) === false )  
die( FormatErrors( sqlsrv_errors() ) );  
            $name = sqlsrv_get_field( $getName, 0);  
            DisplayUploadPictureForm( $_GET['productid'], $name );  
            sqlsrv_close( $conn );  
            break;  
  
        /* Upload a new picture for the selected product. */  
        case 'uploadpicture':  
            $tsql = "INSERT INTO Production.ProductPhoto (LargePhoto)  
                     VALUES (?); SELECT SCOPE_IDENTITY() AS PhotoID";  
            $fileStream = fopen($_FILES['file']['tmp_name'], "r");  
            $uploadPic = sqlsrv_prepare($conn, $tsql, array(  
                       array(&$fileStream,   
                             SQLSRV_PARAM_IN,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY),  
                             SQLSRV_SQLTYPE_VARBINARY('max'))));  
            if( $uploadPic === false )  
die( FormatErrors( sqlsrv_errors() ) );  
            if( sqlsrv_execute($uploadPic) === false )  
die( FormatErrors( sqlsrv_errors() ) );  
  
/*Skip the open result set (row affected). */  
$next_result = sqlsrv_next_result($uploadPic);  
if( $next_result === false )  
die( FormatErrors( sqlsrv_errors() ) );  
  
/* Fetch the next result set. */  
if( sqlsrv_fetch($uploadPic) === false)  
die( FormatErrors( sqlsrv_errors() ) );  
  
/* Get the first field - the identity from INSERT. */  
$photoID = sqlsrv_get_field($uploadPic, 0);  
  
/* Associate the new photoID with the productID. */  
$tsql = "UPDATE Production.ProductProductPhoto  
 SET ProductPhotoID = ?  
 WHERE ProductID = ?";  
  
$reslt = sqlsrv_query($conn, $tsql, array(&$photoID, &$_POST['productid']));  
if($reslt === false )  
die( FormatErrors( sqlsrv_errors() ) );  
  
GetPicture( $_POST['productid']);  
DisplayWriteReviewButton( $_POST['productid'] );  
GetSearchTerms (!null);  
sqlsrv_close( $conn );  
break;  
}//End Switch  
}  
else  
{  
    GetSearchTerms( !null );  
}  
  
function GetPicture( $productID )  
{  
    echo "<table align='center'><tr align='center'><td>";  
    echo "<img src='photo.php?productId=".$productID."'   
      height='150' width='150'/></td></tr>";  
    echo "<tr align='center'><td><a href='?action=displaypicture&  
          productid=".$productID."'>Upload new picture.</a></td></tr>";  
    echo "</td></tr></table></br>";  
}  
  
function GetReviews( $conn, $productID )  
{  
    $tsql = "SELECT ReviewerName,   
             CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
 Rating,   
 Comments   
             FROM Production.ProductReview   
             WHERE ProductID = ?   
             ORDER BY ReviewDate DESC";  
/*Execute the query with a scrollable cursor so  
  we can determine the number of rows returned.*/  
$cursorType = array("Scrollable" => SQLSRV_CURSOR_KEYSET);  
$getReviews = sqlsrv_query( $conn, $tsql, array(&$productID), $cursorType);  
if( $getReviews === false )  
die( FormatErrors( sqlsrv_errors() ) );  
if(sqlsrv_has_rows($getReviews))  
{  
$rowCount = sqlsrv_num_rows($getReviews);  
echo "<table width='50%' align='center' border='1px'>";  
echo "<tr bgcolor='silver'><td>$rowCount Reviews</td></tr></table>";  
while ( sqlsrv_fetch( $getReviews ) )  
{  
$name = sqlsrv_get_field( $getReviews, 0 );  
$date = sqlsrv_get_field( $getReviews, 1 );  
$rating = sqlsrv_get_field( $getReviews, 2 );  
/* Open comments as a stream. */  
$comments = sqlsrv_get_field( $getReviews, 3,   
SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
DisplayReview($productID,  
  $name,  
              $date,  
              $rating,  
              $comments );  
}  
}  
    else  
    {   
DisplayNoReviewsMsg();  
}  
    DisplayWriteReviewButton( $productID );  
    sqlsrv_free_stmt( $getReviews );  
}  
  
/*** Presentation and Utility Functions ***/  
  
function BeginProductsTable($rowCount)  
{  
    /* Display the beginning of the search results table. */  
$headings = array("Product ID", "Product Name",  
"Color", "Size", "Price");  
    echo "<table align='center' cellpadding='5'>";   
    echo "<tr bgcolor='silver'>$rowCount Results</tr><tr>";  
    foreach ( $headings as $heading )  
    {  
        echo "<td>$heading</td>";  
    }  
    echo "</tr>";  
}  
  
function DisplayNoProdutsMsg()  
{  
    echo "<h4 align='center'>No products found.</h4>";  
}  
  
function DisplayNoReviewsMsg()  
{  
    echo "<h4 align='center'>There are no reviews for this product.</h4>";  
}  
  
function DisplayReview( $productID, $name, $date, $rating, $comments)  
{  
    /* Display a product review. */  
    echo "<table style='WORD-BREAK:BREAK-ALL' width='50%'   
                 align='center' border='1' cellpadding='5'>";   
    echo "<tr>  
            <td>ProductID</td>  
            <td>Reviewer</td>  
            <td>Date</td>  
            <td>Rating</td>  
          </tr>";  
      echo "<tr>  
              <td>$productID</td>  
              <td>$name</td>  
              <td>$date</td>  
              <td>$rating</td>  
            </tr>  
            <tr>  
              <td width='50%' colspan='4'>";  
                 fpassthru( $comments );  
     echo "</td></tr></table><br/><br/>";  
}  
  
function DisplayUploadPictureForm( $productID, $name )  
{  
    echo "<h3 align='center'>Upload Picture</h3>";  
    echo "<h4 align='center'>$name</h4>";  
    echo "<form align='center' action='adventureworks_demo.php'  
                    enctype='multipart/form-data' method='POST'>  
<input type='hidden' name='action' value='uploadpicture'/>  
<input type='hidden' name='productid' value='$productID'/>  
<table align='center'>  
         <tr>  
           <td align='center'>  
             <input id='fileName' type='file' name='file'/>  
           </td>  
         </tr>  
         <tr>  
           <td align='center'>  
            <input type='submit' name='submit' value='Upload Picture'/>  
           </td>  
         </tr>  
</table>  
</form>";  
}  
  
function DisplayWriteReviewButton( $productID )  
{  
    echo "<table align='center'><form action='adventureworks_demo.php'   
                 enctype='multipart/form-data' method='POST'>  
          <input type='hidden' name='action' value='writereview'/>  
          <input type='hidden' name='productid' value='$productID'/>  
          <input type='submit' name='submit' value='Write a Review'/>  
          </p></td></tr></form></table>";  
}  
  
function DisplayWriteReviewForm( $productID )  
{  
    /* Display the form for entering a product review. */  
    echo "<h5 align='center'>Name, E-mail, and Rating are required fields.</h5>";  
    echo "<table align='center'>  
<form action='adventureworks_demo.php'   
                enctype='multipart/form-data' method='POST'>  
<input type='hidden' name='action' value='submitreview'/>  
<input type='hidden' name='productid' value='$productID'/>  
<tr>  
<td colspan='5'>Name: <input type='text' name='name' size='50'/></td>  
</tr>  
<tr>  
<td colspan='5'>E-mail: <input type='text' name='email' size='50'/></td>  
</tr>  
<tr>  
<td>Rating: 1<input type='radio' name='rating' value='1'/></td>  
<td>2<input type='radio' name='rating' value='2'/></td>  
<td>3<input type='radio' name='rating' value='3'/></td>  
<td>4<input type='radio' name='rating' value='4'/></td>  
<td>5<input type='radio' name='rating' value='5'/></td>  
</tr>  
<tr>  
<td colspan='5'>  
<textarea rows='20' cols ='50' name='comments'>[Write comments here.]</textarea>  
</td>  
</tr>  
<tr>  
<td colspan='5'>  
                 <p align='center'><input type='submit' name='submit' value='Submit Review'/>  
</td>  
</tr>  
</form>  
          </table>";  
}  
  
function EndProductsTable()  
{   
    echo "</table><br/>";   
}  
  
function GetSearchTerms( $success )  
{  
    /* Get and submit terms for searching the database. */  
    if (is_null( $success ))  
    {  
echo "<h4 align='center'>Review successfully submitted.</h4>";}  
echo "<h4 align='center'>Enter search terms to find products.</h4>";  
echo "<table align='center'>  
            <form action='adventureworks_demo.php'   
                  enctype='multipart/form-data' method='POST'>  
            <input type='hidden' name='action' value='getproducts'/>  
            <tr>  
               <td><input type='text' name='query' size='40'/></td>  
            </tr>  
            <tr align='center'>  
               <td><input type='submit' name='submit' value='Search'/></td>  
            </tr>  
            </form>  
            </table>";  
}  
  
function PopulateProductsTable( $values )  
{  
    /* Populate Products table with search results. */  
    $productID = $values['ProductID'];  
    echo "<tr>";  
    foreach ( $values as $key => $value )  
    {  
        if ( 0 == strcasecmp( "Name", $key ) )  
        {  
            echo "<td><a href='?action=getreview&productid=$productID'>$value</a></td>";  
        }  
        elseif( !is_null( $value ) )  
        {  
            if ( 0 == strcasecmp( "ListPrice", $key ) )  
            {  
                /* Format with two digits of precision. */  
                $formattedPrice = sprintf("%.2f", $value);  
                echo "<td>$$formattedPrice</td>";  
            }  
            else  
            {  
                echo "<td>$value</td>";  
            }  
        }  
        else  
        {  
            echo "<td>N/A</td>";  
        }  
    }  
    echo "<td>  
            <form action='adventureworks_demo.php'   
                  enctype='multipart/form-data' method='POST'>  
            <input type='hidden' name='action' value='writereview'/>  
            <input type='hidden' name='productid' value='$productID'/>  
            <input type='submit' name='submit' value='Write a Review'/>  
            </td></tr>  
            </form></td></tr>";  
}  
  
function FormatErrors( $errors )  
{  
    /* Display errors. */  
    echo "Error information: <br/>";  
  
    foreach ( $errors as $error )  
    {  
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";  
        echo "Code: ".$error['code']."<br/>";  
        echo "Message: ".$error['message']."<br/>";  
    }  
}  
?>  
</body>  
</html>  
```  
  
## <a name="example"></a>Beispiel  
Das „photo.php“-Skript gibt ein Produktfoto für die angegebene **ProduktID**zurück. Das Skript wird aus dem „adventureworks_demo.php“-Skript aufgerufen.  
  
Platzieren Sie den folgenden Code in einer Datei namens „photo.php“:  
  
```  
<?php  
/*=============  
This file is part of a Microsoft SQL Server Shared Source Application.  
Copyright (C) Microsoft Corporation.  All rights reserved.  
  
THIS CODE AND INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY  
KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE  
IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A  
PARTICULAR PURPOSE.  
============= */  
  
$serverName = "(local)\sqlexpress";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Get the product picture for a given product ID. */  
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto AS p  
         JOIN Production.ProductProductPhoto AS q  
         ON p.ProductPhotoID = q.ProductPhotoID  
         WHERE ProductID = ?";  
  
$params = array(&$_REQUEST['productId']);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the image as a binary stream. */  
$getAsType = SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY);  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0, $getAsType);  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free the statement and connectin resources. */  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)

[Vergleichen von Ausführungsfunktionen](../../connect/php/comparing-execution-functions.md)

[Abrufen von Daten](../../connect/php/retrieving-data.md)

[Aktualisieren von Daten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
  
