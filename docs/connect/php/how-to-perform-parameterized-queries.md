---
title: 'Vorgehensweise: Ausführen von parametrisierten Abfragen | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
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
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23660f3d7ddbaf45ac39674c4eba23092e3ae2d2
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-perform-parameterized-queries"></a>Vorgehensweise: Ausführen von parametrisierten Abfragen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema fasst zusammen und veranschaulicht, wie die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] verwendet werden, um eine parametrisierte Abfrage auszuführen.  
  
Die Schritte zur Durchführung einer parametrisierten Abfrage können in vier Schritten zusammengefasst werden:  
  
1.  Setzen Sie Fragezeichen (?) als Platzhalter für Parameter in der Transact-SQL-Zeichenfolge, die die auszuführende Abfrage darstellt.  
  
2.  Initialisieren oder aktualisieren Sie PHP-Variablen, die den Platzhaltern in der Transact-SQL-Abfrage entsprechen.  
  
3.  Verwenden Sie PHP-Variablen aus Schritt 2 erstellt oder aktualisiert ein Array von Parameterwerten entsprechen Parameterplatzhalter in der Transact-SQL-Zeichenfolge. Die Parameterwerte im Array muss sich in derselben Reihenfolge wie die Platzhalter vorgesehen, die sie darstellen.
  
4.  Führen Sie die Abfrage aus:  
  
    -   Wenn Sie den SQLSRV-Treiber verwenden, verwenden Sie [sqlsrv_query](../../connect/php/sqlsrv-query.md) oder [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
    -   Wenn Sie den PDO_SQLSRV-Treiber verwenden, führen Sie die Abfrage mit [PDO:: Prepare](../../connect/php/pdo-prepare.md) und [pdostatement:: Execute](../../connect/php/pdostatement-execute.md). Die Themen für [PDO::prepare](../../connect/php/pdo-prepare.md) und [PDOStatement::execute](../../connect/php/pdostatement-execute.md) enthalten Codebeispiele.  
  
Im weiteren Verlauf dieses Themas werden parametrisierte Abfragen erläutert, die SQLSRV-Treiber verwenden.  
  
> [!NOTE]  
> Parameter sind implizit gebunden, wenn Sie **sqlsrv_prepare**. Dies bedeutet, dass wenn eine parametrisierte Abfrage mit **sqlsrv_prepare** vorbereitet wird und Werte im Parameterarray aktualisiert werden, bei der nächsten Ausführung der Abfrage die aktualisierten Werte verwendet werden. Weitere Informationen finden Sie im zweiten Beispiel dieses Themas.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel aktualisiert die Menge für eine angegebene Produkt-ID in der *Production.ProductInventory* -Tabelle der AdventureWorks-Datenbank. Die Menge und die Produkt-ID sind Parameter in der UPDATE-Abfrage.  
  
Das Beispiel fragt dann die Datenbank ab, um sicherzustellen, dass die Menge korrekt aktualisiert wurde. Die Produkt-ID ist ein Parameter in der SELECT-Abfrage.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
Das vorhergehende Beispiel verwendet die Funktion **sqlsrv_query** , um Abfragen ausführen. Diese Funktion eignet sich zum Ausführen von einmaligen Abfragen, da sie jeweils die Anweisungsvorbereitung als auch die -Ausführung durchführt. Die Kombination von **Sqlsrv_prepare**/**Sqlsrv_execute** eignet sich am besten für die erneute Ausführung einer Abfrage mit verschiedenen Parameterwerten. Ein Beispiel für die erneute Ausführung einer Abfrage mit anderen Parameterwerten finden Sie im nächsten Beispiel.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel veranschaulicht die implizite Bindung von Variablen bei Verwendung der **sqlsrv_prepare** -Funktion. Das Beispiel fügt mehrere Verkaufsaufträge in die *Sales.SalesOrderDetail* -Tabelle ein Die *$params* Array an die Anweisung gebunden ist (*$stmt*) beim **Sqlsrv_prepare** aufgerufen wird. Vor jeder Ausführung einer Abfrage, die einen neuen Verkaufsauftrag in die Tabelle einfügt, wird das *$params* -Array mit neuen Werten entsprechend der Auftragsdetails aktualisiert. Die Ausführung der nachfolgenden Abfrage verwendet die neuen Parameterwerte.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Konvertieren von Datentypen](../../connect/php/converting-data-types.md)

[Sicherheitsüberlegungen für die Microsoft-Treiber für PHP für SQLServer](../../connect/php/security-considerations-for-php-sql-driver.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
