---
title: zu Sqlsrv_has_rows | Microsoft Docs
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
helpviewer_keywords:
- API Reference, sqlsrv_has_rows
- sqlsrv_has_rows
ms.assetid: 4da7f640-cf12-409f-9e00-95b30a8d5e17
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eeabad44fa452c78e1dbf056f15486b4719757b8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvhasrows"></a>sqlsrv_has_rows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Zeigt an, ob das Resultset eine oder mehrere Zeilen enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_has_rows( resource $stmt )  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: ausgeführte Anweisung.  
  
## <a name="return-value"></a>Rückgabewert  
Falls das Resultset Zeilen enthält, wird der zurückgegebene Wert **true**sein. Falls es keine Zeilen gibt oder der Funktionsaufruf fehlschlägt, ist der zurückgegebene Wert **false**.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
   $server = "server_name";  
   $conn = sqlsrv_connect( $server, array( 'Database' => 'Northwind' ) );  
  
   $stmt = sqlsrv_query( $conn, "select * from orders where CustomerID = 'VINET'" , array());  
  
   if ($stmt !== NULL) {  
      $rows = sqlsrv_has_rows( $stmt );  
  
      if ($rows === true)  
         echo "\nthere are rows\n";  
      else   
         echo "\nno rows\n";  
   }  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
  

