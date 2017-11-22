---
title: "Vergleichen von Ausführungsfunktionen | Microsoft Docs"
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
helpviewer_keywords: executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59523326f9eedb07742fa67dc85026a1570e3bea
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
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
  
