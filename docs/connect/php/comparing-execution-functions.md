---
title: Vergleichen von Ausführungsfunktionen | Microsoft Docs
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
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a906ec1a197cb6ede1570c9202cc955f8432ff79
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="comparing-execution-functions"></a>Vergleichen von Ausführungsfunktionen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] bietet mehrere Optionen zum Ausführen von Funktionen.  

## <a name="sqlsrv-execution-functions"></a>SQLSRV Ausführungsfunktionen  
Wenn Sie den SQLSRV-Treiber verwenden, verwenden Sie [sqlsrv_query](../../connect/php/sqlsrv-query.md) zum Ausführen einer einzelnen Abfrage und [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) mit [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) zur mehrfachen Ausführung einer vorbereiteten Anweisung mit verschiedenen Parameterwerten für jede Ausführung.  

## <a name="pdosqlsrv-execution-functions"></a>PDO_SQLSRV Execution Functions 
Wenn Sie den PDO_SQLSRV-Treiber verwenden, können Sie eine Abfrage mit einer der folgenden Methoden ausführen:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) und [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Referenz zum Treiber PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)
  
