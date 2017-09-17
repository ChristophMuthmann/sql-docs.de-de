---
title: Abrufen von Datums- und Uhrzeitangabe Geben Sie als Zeichenfolgen mit dem SQLSRV-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9638bc7ec31f4631b2938a61f2470a057a4465db
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver"></a>Vorgehensweise: Datums- und Uhrzeittypen mittels des SQLSRV-Treibers als Zeichenfolgen abrufen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Diese Funktion wurde der Version 1.1 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] hinzugefügt und ist nur zulässig, wenn der SQLSRV-Treiber für die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]verwendet wird. Es ist ein Fehler die Verbindungsoption „ReturnDatesAsStrings“  mit dem PDO_SQLSRV-Treiber zu verwenden.  
  
Sie können Datums- und Uhrzeittypen abrufen (**"DateTime"**, **Datum**, **Zeit**, **datetime2**, und **"DateTimeOffset"**) als Zeichenfolgen durch eine Option in der Verbindungszeichenfolge angeben.  
  
### <a name="to-retrieve-date-and-time-types-as-strings"></a>Datums- und Uhrzeittypen als Zeichenfolgen abrufen  
  
-   Verwenden Sie die folgende Verbindungsoption:  
  
    ```  
    'ReturnDatesAsStrings'=>true  
    ```  
  
    Der Standardwert ist **false**, d. h. dass **datetime**, **Date**, **Time**, **DateTime2**und **DateTimeOffset** -Typen als PHP- **Datetime** -Typen ausgegeben werden.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel zeigt die Syntax, welche festlegt, dass die Datums- und Uhrzeittypen als Zeichenfolgen abgerufen werden.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel zeigt, dass Sie Datumsangaben als Zeichenfolgen abrufen können, indem Sie UTF-8 angeben, wenn Sie die Zeichenfolge abrufen, selbst wenn die Verbindung hergestellt wurde, mit `"ReturnDatesAsStrings" => false`.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));  
  
if( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
echo $date;  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Im folgende Beispiel wird gezeigt, wie Datumsangaben als Zeichenfolgen abgerufen werden UTF-8 spezifizieren und `"ReturnDatesAsStrings" => true` in der Verbindungszeichenfolge angegeben.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8' );  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0 );  
  
if ( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
echo $date;  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel zeigt, wie das Datum als PHP-Typ abgerufen wird. `'ReturnDatesAsStrings'=> false` ist standardmäßig aktiviert.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0 );  
  
if ( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$date_string = date_format( $date, 'jS, F Y' );  
echo "Date = $date_string\n";  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
  

