---
title: Sqlsrv_execute | Microsoft Docs
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
apiname:
- sqlsrv_execute
apitype: NA
helpviewer_keywords:
- sqlsrv_exclude
- executing queries
- API Reference, sqlsrv_execute
ms.assetid: 38331bc2-4391-4f9f-aa83-9873dad605a0
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d9326e49d0fd22440fe8d974d7d0b66800e04cdc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvexecute"></a>sqlsrv_execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Führt eine zuvor vorbereitete Anweisung aus. Weitere Informationen zum Vorbereiten einer Anweisung für die Ausführung finden Sie unter [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) .  
  
> [!NOTE]  
> Diese Funktion ist ideal  zum mehrfachen Ausführen einer vorbereiteten Anweisung mit verschiedenen Parameterwerten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_execute( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Ressource, die die auszuführende Anweisung angibt. Weitere Informationen zum Erstellen einer Anweisungsressource finden Sie unter [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
## <a name="return-value"></a>Rückgabewert  
Ein boolescher Wert: **true** wenn die Anweisung erfolgreich ausgeführt wurde. Andernfalls lautet der Wert **false**.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel führt eine Anweisung durch, die ein Feld in der *Sales.SalesOrderDetail* -Tabelle in der [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank aktualisiert. Das Beispiel setzt voraus, dass SQL Server und die AdventureWorks-Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ( ?)   
         WHERE SalesOrderDetailID = ( ?)";  
  
/* Set up the parameters array. Parameters correspond, in order, to  
question marks in $tsql. */  
$params = array( 5, 10);  
  
/* Create the statement. */  
$stmt = sqlsrv_prepare( $conn, $tsql, $params);  
if( $stmt )  
{  
     echo "Statement prepared.\n";  
}  
else  
{  
     echo "Error in preparing statement.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute the statement. Display any errors that occur. */  
if( sqlsrv_execute( $stmt))  
{  
      echo "Statement executed.\n";  
}  
else  
{  
     echo "Error in executing statement.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
[sqlsrv_query](../../connect/php/sqlsrv-query.md)  
  

