---
title: "Vergleichen von Ausführungsfunktionen | Microsoft Docs"
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
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e74c7433ab2e3a831d6aa800a2a1a9abbbda5863
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="comparing-execution-functions"></a>Vergleichen von Ausführungsfunktionen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] bietet mehrere Optionen zum Ausführen von Funktionen.  
  
Wenn Sie den SQLSRV-Treiber verwenden, verwenden Sie [sqlsrv_query](../../connect/php/sqlsrv-query.md) zum Ausführen einer einzelnen Abfrage und [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) mit [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) zur mehrfachen Ausführung einer vorbereiteten Anweisung mit verschiedenen Parameterwerten für jede Ausführung.  
  
Wenn Sie den PDO_SQLSRV-Treiber verwenden, können Sie eine Abfrage mit einer der folgenden Methoden ausführen:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) und [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referenz zum Treiber PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
  

