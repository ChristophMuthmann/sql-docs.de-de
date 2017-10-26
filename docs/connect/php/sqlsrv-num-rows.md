---
title: zu Sqlsrv_num_rows | Microsoft Docs
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
- API Reference, sqlsrv_num_rows
- sqlsrv_num_rows
ms.assetid: c832210e-bb2a-47b5-a505-160b02d1d95e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1739cdd1632ec9d7bbc191e30d09252ab014e536
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvnumrows"></a>sqlsrv_num_rows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Berichtet über die Anzahl der Zeilen in einem Resultset.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_num_rows( resource $stmt )  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Das Resultset für das die Zeilen gezählt werden sollen.  
  
## <a name="return-value"></a>Rückgabewert  
Falls es bei der Berechnung der Anzahl der Zeilen einen Fehler gab, wird**false** zurückgegeben. Ansonsten gibt der Befehl die Anzahl der Zeilen im Resultset zurück.  
  
## <a name="remarks"></a>Hinweise  
erfordert eine clientseitigen, statischen oder Keysetcursor und gibt zurück zu Sqlsrv_num_rows **"false"** Wenn Sie einen Vorwärtscursor oder einen dynamischen Cursor verwenden. (Standard ist der Vorwärtscursor.) Weitere Informationen zu Cursorn finden Sie unter [Sqlsrv_query](../../connect/php/sqlsrv-query.md) und [Cursortypen &#40; SQLSRV-Treiber &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
   $server = "server_name";  
   $conn = sqlsrv_connect( $server, array( 'Database' => 'Northwind' ) );  
  
   $stmt = sqlsrv_query( $conn, "select * from orders where CustomerID = 'VINET'" , array(), array( "Scrollable" => SQLSRV_CURSOR_KEYSET ));  
  
   $row_count = sqlsrv_num_rows( $stmt );  
  
   if ($row_count === false)  
      echo "\nerror\n";  
   else if ($row_count >=0)  
      echo "\n$row_count\n";  
?>  
```  
  
Das folgende Beispiel zeigt, das, wenn es mehr als ein Resultset gibt, (eine Batchabfrage) die Anzahl der Zeilen nur verfügbar ist, wenn Sie einen clientseitigen Cursor verwenden.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
$tsql = "select * from HumanResources.Department";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
// works  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
  
// fails  
// $stmt = sqlsrv_query($conn, $tsql);  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"forward"));  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"static"));  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"keyset"));  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"dynamic"));  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
  

