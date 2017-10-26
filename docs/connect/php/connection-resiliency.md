---
title: "Verbindungsstabilität im Leerlauf"
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38d51492d488db404786a60b8ab73576d0a1acb4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="idle-connection-resiliency"></a>Verbindungsstabilität im Leerlauf
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Verbindungsresilienz](https://msdn.microsoft.com/library/dn632678.aspx) ist das Prinzip, dass eine unterbrochene Verbindung im Leerlauf kann, in bestimmten Einschränkungen hergestellt werden. Wenn eine Verbindung mit Microsoft SQL Server ein Fehler auftritt, kann verbindungsstabilität den Client automatisch versucht wird, um die Verbindung wiederherzustellen. Verbindungsresilienz ist eine Eigenschaft der Datenquelle. nur SQLServer 2014 und höher und Azure SQL-Datenbank resilienz von Verbindungen zu unterstützen.

Verbindungsresilienz wird implementiert, mit zwei Schlüsselwörter, die Verbindungszeichenfolgen hinzugefügt werden können: **ConnectRetryCount** und **Connectionretryinterval**.

|Schlüsselwort|Werte|Standardwert|Description|
|-|-|-|-|
|**ConnectRetryCount**| Ganze Zahl zwischen 0 und 255 (inklusiv)|1|Die maximale Anzahl der Versuche vor dem Allgemeinheit eine unterbrochene Verbindung her. Standardmäßig wird ein einzelner Versuch unternommen, bei unterteilt eine Verbindung her. Der Wert 0 bedeutet, dass keine erneute Verbindung erneut versucht wird.|
|**Connectionretryinterval**| Ganze Zahl zwischen 1 und 60 (inklusiv)|1| Die Zeit in Sekunden zwischen den versuchen, eine Verbindung wiederherzustellen. Die Anwendung versucht, die sofort erneut eine Verbindung herzustellen, eine unterbrochene Verbindung wird erkannt, und wartet dann **Connectionretryinterval** Sekunden, bevor Sie es erneut zu versuchen. Dieses Schlüsselwort wird ignoriert, wenn **ConnectRetryCount** gleich 0 ist.

Wenn das Produkt der **ConnectRetryCount** multipliziert **Connectionretryinterval** ist größer als **LoginTimeout**, und klicken Sie dann der Client eingestellt wird einmal eine Verbindung herstellen möchten ** LoginTimeout** erreicht wird; andernfalls ist sie weiterhin für die Verbindung erst versuchen **ConnectRetryCount** erreicht ist.

#### <a name="remarks"></a>Hinweise

Verbindungsresilienz gilt, wenn die Verbindung im Leerlauf befindet. Fehler, die auftreten, während der erneuten Herstellen einer Verbindung versucht – Ausführen einer Transaktions, z. B. nicht ausgelöst wird, schlagen sie fehl, als sonst zu erwarten wäre. Erneute Verbindung versucht, die folgenden Situationen als nicht wiederherstellbar Sitzungszustände bezeichnet werden nicht ausgelöst:

* Temporäre Tabellen 
* Globale und lokale Cursor
* Bereits verwendeten Transaktionskontext und Sitzung Ebene Transaktionssperren
* Anwendungssperren
* EXECUTE AS / Sicherheitskontext wiederherstellen
* OLE-Automatisierung-handles
* Vorbereitete XML-handles
* Ablaufverfolgungsflags

## <a name="example"></a>Beispiel

Der folgende Code eine Verbindung mit einer Datenbank her und führt eine Abfrage. Die Verbindung wird durch das Entfernen der Sitzungs unterbrochen, und die unterbrochene Verbindung mit eine neue Abfrage versucht. Dieses Beispiel verwendet die [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) -Beispieldatenbank.

In diesem Beispiel geben wir einen zwischengespeicherten Cursor vor dem Unterbrechen der Verbindungs an. Wenn wir einen zwischengespeicherten Cursor nicht angeben, würde die Verbindung nicht hergestellt werden, da gäbe es keinen aktiven serverseitige Cursor und somit die Verbindung nicht im Leerlauf, wenn unterteilt. Allerdings wird in diesem Fall könnten wir vor dem Unterbrechen der Verbindung, um den Cursor vacate sqlsrv_free_stmt() aufrufen und würde die Verbindung erfolgreich hergestellt.

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
Erwartete Ausgabe:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>Siehe auch
[Verbindungsresilienz im Windows ODBC-Treiber](https://docs.microsoft.com/en-us/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)

