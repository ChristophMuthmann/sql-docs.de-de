---
title: Sqlsrv_begin_transaction | Microsoft Docs
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
apiname:
- sqlsrv_begin_transaction
apitype: NA
helpviewer_keywords:
- sqlsrv_begin_transaction
- transaction support
- API Reference, sqlsrv_begin_transaction
ms.assetid: 0b223bc8-4047-4329-9cbf-d350ab0fb886
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd05e98f7068229867626c518a29ca3782e79002
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sqlsrvbegintransaction"></a>sqlsrv_begin_transaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Beginnt eine Transaktion für eine angegebene Verbindung Die aktuelle Transaktion enthält alle Anweisungen für die angegebene Verbindung, die nach dem Aufruf von **sqlsrv_begin_transaction** und vor allen Aufrufen von [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md) oder [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)ausgeführt wurden.  
  
> [!NOTE]  
> Die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] befindet sich im Autocommit-Modus in der Standardeinstellung. Dies bedeutet, dass alle Abfragen bei Erfolg automatisch committet werden, es sei denn, sie wurden durch **sqlsrv_begin_transaction**.  
  
> [!NOTE]  
> Wenn **sqlsrv_begin_transaction** aufgerufen wird, nachdem eine Transaktion bereits für die Verbindung initiiert, aber nicht durch Aufrufen von entweder **sqlsrv_commit** oder **sqlsrv_rollback**abgeschlossen wurde, gibt der Aufruf **false** zurück, und der Fehlerauflistung wird ein *Already in Transaction* -Fehler hinzugefügt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_begin_transaction( resource $conn)  
```  
  
#### <a name="parameters"></a>Parameter  
*$conn*: Die Verbindung, der die Transaktion zugeordnet ist.  
  
## <a name="return-value"></a>Rückgabewert  
Ein boolescher Wert: **true** , wenn die Transaktion erfolgreich gestartet wurde. Andernfalls lautet der Wert **false**.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel werden zwei Abfragen im Rahmen einer Transaktion ausgeführt. Wenn beide Abfragen erfolgreich sind, wird die Transaktion committet. Wenn eine oder beide Abfragen fehlschlagen, wird für die Transaktion ein Rollback ausgeführt.  
  
Die erste Abfrage im Beispiel fügt einen neuen Verkaufsauftrag in die *Sales.SalesOrderDetail* -Tabelle der AdventureWorks-Datenbank ein. Der Auftrag umfasst fünf Einheiten des Produkts, das die Produkt-ID 709 besitzt. In der zweiten Abfrage wird der Lagerbestand des Produkts mit der ID 709 um fünf Einheiten reduziert. Diese Abfragen werden in eine Transaktion aufgenommen, weil beide Abfragen erfolgreich ausgeführt werden müssen, damit die Datenbank den Status von Aufträgen und die Verfügbarkeit von Produkten korrekt widerspiegelt.  
  
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
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if ( sqlsrv_begin_transaction( $conn ) === false )  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and execute the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
Da wir uns auf die Überwachung des Transaktionsverhaltens konzentrieren, sind Teile der empfohlenen Fehlerbehandlung im vorherigen Beispiel nicht enthalten. Für eine Produktionsanwendung wird empfohlen, dass jeder Aufruf einer **sqlsrv** -Funktion auf Fehler überprüft und entsprechend behandelt wird.  
  
> [!NOTE]  
> Verwenden Sie eingebettetes Transact-SQL nicht zum Durchführen von Transaktionen. Führen Sie z. B. keine Anweisung mit "BEGIN TRANSACTION" als Transact-SQL-Abfrage aus, um eine Transaktion zu beginnen. Das erwartete Transaktionsverhalten kann nicht garantiert werden, wenn eingebettetes Transact-SQL zum Durchführen von Transaktionen verwendet wird.  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Gewusst wie: Ausführen von Transaktionen](../../connect/php/how-to-perform-transactions.md)

[Übersicht über die Microsoft-Treiber für PHP für SQLServer](../../connect/php/overview-of-the-php-sql-driver.md) 
  
