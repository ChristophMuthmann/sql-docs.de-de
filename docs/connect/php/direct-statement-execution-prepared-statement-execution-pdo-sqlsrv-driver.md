---
title: "Direct - Anweisung Ausführung PDO_SQLSRV-Treiber für vorbereitete Anweisungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8df460f169a1890c9e30bd2b72baa4a38fd4bf31
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Direkte Anweisungsausführung und vorbereitete Anweisungsausführung im PDO_SQLSRV-Treiber.
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema wird erläutert, wie Sie das Attribut PDO:: sqlsrv_attr_direct_query verwenden können, direkte anweisungsausführung anstelle des Standardwerts, angeben, die Ausführung der vorbereiteten Anweisung ist.  Wenn der Treiber eine Anweisung vorbereitet hat, kann dies einer verbesserten Leistung führen, wenn die Anweisung mehr als einmal mit gebundenen Parametern ausgeführt wird.  
  
## <a name="remarks"></a>Hinweise  
Wenn Sie senden möchten eine [!INCLUDE[tsql](../../includes/tsql_md.md)] Anweisung direkt an den Server ohne anweisungsvorbereitung vom Treiber, Sie können das PDO:: sqlsrv_attr_direct_query-Attribut mit festlegen [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) (oder als eine Treiberoption auf erfolgreich [PDO:: __construct](../../connect/php/pdo-construct.md)) oder beim Aufrufen [PDO:: Prepare](../../connect/php/pdo-prepare.md). Standardmäßig ist der Wert des PDO:: sqlsrv_attr_direct_query "false" (Verwendung vorbereitete anweisungsausführung).  
  
Bei Verwendung von [PDO:: Query](../../connect/php/pdo-query.md), sollten Sie die direkte Ausführung. Vor dem Aufruf [PDO:: Query](../../connect/php/pdo-query.md), rufen Sie [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) und PDO:: sqlsrv_attr_direct_query auf "true" festgelegt.  Jeder Aufruf von [PDO:: Query](../../connect/php/pdo-query.md) mit einer anderen Einstellung für PDO:: sqlsrv_attr_direct_query ausgeführt werden kann.  
  
Bei Verwendung von [PDO:: Prepare](../../connect/php/pdo-prepare.md) und [pdostatement:: Execute](../../connect/php/pdostatement-execute.md) zum Ausführen einer Abfrage mehrere Male mit gebundenen Parametern, die Ausführung der Anweisung vorbereitet werden optimiert die wiederholte Abfrage.  In diesem Fall rufen [PDO:: Prepare](../../connect/php/pdo-prepare.md) mit PDO:: sqlsrv_attr_direct_query in Treiber Optionen Arrayparameter auf "false" festgelegt. Bei Bedarf können Sie die vorbereitete Anweisungen mit PDO:: sqlsrv_attr_direct_query Wert "falsch" ausführen.  
  
Nach dem Aufruf [PDO:: Prepare](../../connect/php/pdo-prepare.md), der Wert des PDO:: sqlsrv_attr_direct_query kann nicht geändert werden, bei der Ausführung einer vorbereiteten Abfrage.  
  
Wenn eine Abfrage den Kontext, der in einer vorherigen Abfrage festgelegt wurde erfordert, sollten Sie Ihre Abfragen mit auf "true" festgelegt ist PDO:: sqlsrv_attr_direct_query ausführen. Wenn Sie temporäre Tabellen in Ihren Abfragen verwenden, muss z. B. PDO:: sqlsrv_attr_direct_query auf "true" festgelegt werden.  
  
Das folgende Beispiel zeigt, dass wenn der Kontext aus einer früheren Anweisung erforderlich ist, Sie PDO:: sqlsrv_attr_direct_query auf "true" festgelegt müssen.  Dieses Beispiel verwendet die temporäre Tabellen sind nur für nachfolgende Anweisungen in Ihrem Programm verfügbar, wenn Abfragen direkt ausgeführt werden.  
  
```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
  
