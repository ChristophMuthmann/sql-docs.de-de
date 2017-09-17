---
title: Sqlsrv_cancel | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_cancel
apitype: NA
helpviewer_keywords:
- sqlsrv_cancel
- API Reference, sqlsrv_cancel
ms.assetid: 75798c9b-f711-445d-9b8f-ba4d405ca50a
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f69d5a11e4edd726479c48918f9a332f2279ed7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvcancel"></a>sqlsrv_cancel
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Bricht eine Anweisung ab. Dies bedeutet, dass alle ausstehenden Ergebnisse für die Anweisung verworfen werden. Nachdem diese Funktion aufgerufen wird, die Anweisung kann erneut ausgeführt werden, wenn er mit vorbereitet wurde [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Das Aufrufen dieser Funktion ist nicht erforderlich, wenn alle Ergebnisse, die der Anweisung zugeordnet sind, verwendet wurden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_cancel( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Die Anweisung, die abgebrochen werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
Ein boolescher Wert: **true** , wenn der Vorgang erfolgreich war. Andernfalls lautet der Wert **false**.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel nimmt die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank als Ziel zur Ausführung einer Abfrage. Es werden dann Ergebnisse verarbeitet und gezählt, bis die Variable *$salesTotal* einen angegebenen Betrag erreicht. Die verbleibenden Abfrageergebnisse werden anschließend verworfen. Das Beispiel setzt voraus, dass SQL Server und die AdventureWorks-Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Prepare and execute the query. */  
$tsql = "SELECT OrderQty, UnitPrice FROM Sales.SalesOrderDetail";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
if( sqlsrv_execute( $stmt ) === false)  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Initialize tracking variables. */  
$salesTotal = 0;  
$count = 0;  
  
/* Count and display the number of sales that produce revenue  
of $100,000. */  
while( ($row = sqlsrv_fetch_array( $stmt)) && $salesTotal <=100000)  
{  
     $qty = $row[0];  
     $price = $row[1];  
     $salesTotal += ( $price * $qty);  
     $count++;  
}  
echo "$count sales accounted for the first $$salesTotal in revenue.\n";  
  
/* Cancel the pending results. The statement can be reused. */  
sqlsrv_cancel( $stmt);  
?>  
```  
  
## <a name="comments"></a>Kommentare  
Eine Anweisung, die vorbereitet und ausgeführt wird, mit der Kombination von wird [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) und [Sqlsrv_execute](../../connect/php/sqlsrv-execute.md) kann erneut ausgeführt, mit **Sqlsrv_execute** nach dem Aufrufen von **Sqlsrv_cancel**. Eine Anweisung, die ausgeführt wird, mit [Sqlsrv_query](../../connect/php/sqlsrv-query.md) kann nicht erneut ausgeführt werden, nach dem Aufruf **Sqlsrv_cancel**.  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)  
  

