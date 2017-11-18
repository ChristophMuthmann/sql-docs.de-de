---
title: Cursortypen (SQLSRV-Treiber) | Microsoft Docs
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
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92fa89c2f477b867930d1b53da7e6fa318a3d39d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-types-sqlsrv-driver"></a>Cursortypen (SQLSRV-Treiber)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Der SQLSRV-Treiber können Sie erstellen ein Resultset mit Zeilen, die Sie in beliebiger Reihenfolge, abhängig vom Cursortyp zugreifen können.  In diesem Thema wird erläutert, clientseitigen (gepufferten) und (ungepufferten) serverseitige Cursor.  
  
## <a name="cursor-types"></a>Cursortypen  
Beim Erstellen eines Resultsets mit [Sqlsrv_query](../../connect/php/sqlsrv-query.md) oder mit [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md), können Sie den Typ des Cursors angeben. Standardmäßig wird ein Vorwärtscursor verwendet, sodass Sie eine Zeile zu einem Zeitpunkt gestartet, bei der ersten Zeile des Resultsets, bis das Ende des Resultsets erreicht verschieben können.  
  
Sie können ein Resultset mit einem bildlauffähigen Cursor, in der Sie eine beliebige Zeile im Resultset in beliebiger Reihenfolge zugreifen kann, erstellen. Die folgende Tabelle enthält die Werte, die übergeben werden können die **Scrollable** Option Sqlsrv_query oder Sqlsrv_prepare.  
  
|Option|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|Ermöglicht Ihnen das Verschieben einer Zeile zu einem Zeitpunkt ab, die bei der ersten Zeile des Resultsets, bis das Ende des Resultsets erreicht ist.<br /><br />Dies ist der Standardcursortyp.<br /><br />[zu Sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) gibt einen Fehler für diesen Cursortyp erstellt Resultsets zurück.<br /><br />**Vorwärts** ist die abgekürzte Form der SQLSRV_CURSOR_FORWARD.|  
|SQLSRV_CURSOR_STATIC|Können Sie Zeilen in beliebiger Reihenfolge zuzugreifen, aber Änderungen in der Datenbank nicht widerspiegelt.<br /><br />**statische** ist die abgekürzte Form der SQLSRV_CURSOR_STATIC.|  
|SQLSRV_CURSOR_DYNAMIC|Können Sie Zeilen in beliebiger Reihenfolge zuzugreifen und Änderungen in der Datenbank widerspiegelt.<br /><br />[zu Sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) gibt einen Fehler für diesen Cursortyp erstellt Resultsets zurück.<br /><br />**dynamische** ist die abgekürzte Form der SQLSRV_CURSOR_DYNAMIC.|  
|SQLSRV_CURSOR_KEYSET|Können Sie die Zeilen in beliebiger Reihenfolge zugreifen. Ein Keysetcursor aktualisiert jedoch nicht die Anzahl der Zeilen, wenn eine Zeile aus der Tabelle gelöscht wird (eine gelöschte Zeile wird ohne Werte zurückgegeben).<br /><br />**Keyset** ist die abgekürzte Form der SQLSRV_CURSOR_KEYSET.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|Können Sie die Zeilen in beliebiger Reihenfolge zugreifen. Erstellt eine Cursorabfrage für die clientseitige.<br /><br />**gepuffert** ist die abgekürzte Form der SQLSRV_CURSOR_CLIENT_BUFFERED.|  
  
Wenn eine Abfrage mehrere Resultsets generiert die **Scrollable** Option gilt für alle Resultsets.  
  
## <a name="selecting-rows-in-a-result-set"></a>Auswählen von Zeilen in einem Resultset  
Nachdem Sie ein Resultset erstellen, können Sie [Sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [Sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md), oder [Sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) Zeile angeben.  
  
Die folgende Tabelle beschreibt die Werte Sie, in angeben können der *Zeile* Parameter.  
  
|Parameter|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|Gibt die nächste Zeile an. Dies ist der Standardwert, wenn Sie keinen angeben der *Zeile* Parameter für einen Satz scrollfähigen Resultsets.|  
|SQLSRV_SCROLL_PRIOR|Gibt die Zeile vor der aktuellen Zeile.|  
|SQLSRV_SCROLL_FIRST|Gibt die erste Zeile im Resultset.|  
|SQLSRV_SCROLL_LAST|Gibt die letzte Zeile im Resultset.|  
|SQLSRV_SCROLL_ABSOLUTE|Gibt an, der Zeile angegeben wird, mit der *Offset* Parameter.|  
|SQLSRV_SCROLL_RELATIVE|Gibt an, der Zeile angegeben wird, mit der *Offset* Parameter aus der aktuellen Zeile.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>Serverseitige Cursor und den SQLSRV-Treiber  
Das folgende Beispiel zeigt die Auswirkungen der verschiedenen Cursor. Zeile 33 des Beispiels sehen Sie die erste von drei abfrageanweisungen, die verschiedene Cursor angeben.  Zwei der abfrageanweisungen sind kommentiert. Bei jedem des Programms ausführen verwenden eines anderen Cursortyps, die Auswirkung des-Datenbankupdates in Zeile 47 anzuzeigen.  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>Die clientseitige Cursor und den SQLSRV-Treiber  
Die clientseitige Cursor sind eine Funktion, die in Version 3.0 des hinzugefügten der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] , mit der Sie ein komplettes Resultset im Arbeitsspeicher zwischengespeichert. Anzahl der Zeilen ist verfügbar, nachdem die Abfrage ausgeführt wird, wenn Sie einen clientseitigen Cursor verwenden.  
  
Die clientseitige Cursor sollte für kleine-mittelständische Resultsets verwendet werden. Verwenden Sie serverseitige Cursor für große Resultsets.  
  
Eine Abfrage wird "false" ist der Puffer nicht groß genug für das gesamte Resultset zurück. Sie können die Größe des Puffers bis hin zur PHP-Speichergrenze erhöhen.  
  
Die SQLSRV-Treiber verwenden, können Sie konfigurieren, die Größe des Puffers, das Resultset mit der Einstellung ClientBufferMaxKBSize für enthält [Sqlsrv_configure](../../connect/php/sqlsrv-configure.md). [Sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) gibt den Wert der ClientBufferMaxKBSize zurück. Sie können auch die maximale Puffergröße in der Datei "PHP.ini" mit Sqlsrv festlegen. ClientBufferMaxKBSize (z. B. Sqlsrv. ClientBufferMaxKBSize = 1024).  
  
Das folgende Beispiel zeigt:  
  
-   Zeilenanzahl ist immer mit einem clientseitigen Cursor verfügbar.  
  
-   Verwendung von clientseitigen Cursorn und Batchanweisungen.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
Das folgende Beispiel zeigt einen clientseitigen Cursor verwenden [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable"=>SQLSRV_CURSOR_CLIENT_BUFFERED));  
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  

