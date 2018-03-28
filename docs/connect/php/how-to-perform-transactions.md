---
title: 'Vorgehensweise: Ausführen von Transaktionen | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
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
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15f4ba792e7657125c6964f098c6c1f7a9fe83f0
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-perform-transactions"></a>Vorgehensweise: Ausführen von Transaktionen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Der SQLSRV-Treiber des [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] bietet drei Funktionen zur Durchführung von Transaktionen:  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [Sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
Der PDO_SQLSRV-Treiber bietet drei Funktionen zur Durchführung von Transaktionen:  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
Ein Beispiel hierzu finden Sie unter [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) .  
  
Im weiteren Verlauf dieses Themas wird erläutert und veranschaulicht, wie Sie Transaktionen mit dem SQLSRV-Treiber durchführen können.  
  
## <a name="remarks"></a>Hinweise  
Die Schritte zum Ausführen einer Transaktion können wie folgt zusammengefasst werden:  
  
1.  Starten Sie die Transaktion mit **sqlsrv_begin_transaction**.  
  
2.  Überprüfen Sie jede Abfrage, die Teil der Transaktion ist, auf Erfolg oder Fehlschlagen.  
  
3.  Committen Sie die Transaktion gegebenenfalls mit **Sqlsrv_commit**. Andernfalls können Sie mit **sqlsrv_rollback**. Nach dem Aufruf **Sqlsrv_commit** oder **Sqlsrv_rollback**, wird der Treiber in den Autocommit-Modus zurückgegeben.  
  
    Wird standardmäßig der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] befindet sich im Autocommit-Modus. Dies bedeutet, dass alle Abfragen bei Erfolg automatisch committet werden, es sei denn, sie wurden durch **sqlsrv_begin_transaction**.  
  
    Wenn eine explizite Transaktion nicht mit übernommen wird **Sqlsrv_commit**, wird ein Rollback beim Trennen der Verbindung oder bei Beendigung des Skripts.  
  
    Verwenden Sie eingebettetes Transact-SQL nicht zum Durchführen von Transaktionen. Führen Sie z. B. keine Anweisung mit "BEGIN TRANSACTION" als Transact-SQL-Abfrage aus, um eine Transaktion zu beginnen. Das erwartete Transaktionsverhalten kann nicht garantiert werden, wenn Sie eingebettetes Transact-SQL zum Durchführen von Transaktionen verwenden.  
  
    Für die Durchführung von Transaktionen sollten die oben aufgelisteten **sqlsrv** -Funktionen verwendet werden.  
  
## <a name="example"></a>Beispiel  
  
### <a name="description"></a>Description  
Im folgenden Beispiel werden mehrere Abfragen im Rahmen einer Transaktion ausgeführt. Wenn alle Abfragen erfolgreich sind, wird die Transaktion committet. Wenn eine der Abfragen fehlschlägt, wird für die Transaktion ein Rollback ausgeführt.  
  
Das Beispiel versucht, einen Verkaufsauftrag aus der *Sales.SalesOrderDetail* -Tabelle zu löschen und die Lagerbestände der Produkte in der *Product.ProductInventory* -Tabelle für jedes Produkt im Verkaufsauftrag anzupassen. Diese Abfragen werden in eine Transaktion aufgenommen, weil alle Abfragen erfolgreich ausgeführt werden müssen, damit die Datenbank den Status der Aufträge und die Verfügbarkeit von Produkten korrekt widerspiegelt.  
  
Die erste Abfrage im Beispiel ruft die Produkt-IDs und Mengen für eine bestimmte Verkaufsauftrags-ID ab. Diese Abfrage ist nicht Teil der Transaktion. Das Skript wird jedoch beendet, wenn diese Abfrage fehlschlägt, da die Produkt-IDs und Mengen zur Durchführung von Abfragen erforderlich sind, die Teil der nachfolgenden Transaktion sind.  
  
Die anschließenden Abfragen (Löschen des Verkaufsauftrags und Aktualisieren der Lagerbestände der Produkte) sind Teil der Transaktion.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
### <a name="code"></a>Code  
  
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
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>Kommentare  
Für die Überwachung des Transaktionsverhaltens ist eine empfohlene Fehlerbehandlung im vorherigen Beispiel nicht enthalten. Für eine produktionsanwendung empfehlen wir überprüfen jeden Aufruf eine **Sqlsrv** Funktion auf Fehler, und diese entsprechend zu behandeln.
  
## <a name="see-also"></a>Siehe auch  
[Aktualisieren von Daten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Transaktionen (Datenbankmodul)](https://msdn.microsoft.com/library/ms190612.aspx)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
