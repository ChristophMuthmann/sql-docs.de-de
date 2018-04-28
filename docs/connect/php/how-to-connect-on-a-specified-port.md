---
title: 'Vorgehensweise: Verbinden über einen angegebenen Port | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b17dd2bb8df3f7274cb8eea36faf3ee5f320f983
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-connect-on-a-specified-port"></a>Vorgehensweise: Verbinden über einen angegebenen Port
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema wird beschrieben, wie über einen angegebenen Port mit der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]eine Verbindung zu SQL Server hergestellt wird.  
  
### <a name="to-connect-on-a-specified-port"></a>Verbinden über einen angegebenen Port  
  
1.  Stellen Sie sicher, dass der Port, auf den der Server konfiguriert ist, Verbindungen akzeptiert. Informationen zum Konfigurieren eines Servers zum Akzeptieren von Verbindungen über einen angegebenen Port finden Sie unter [Vorgehensweise: konfigurieren ein Servers zur Überwachung eines bestimmten TCP-Ports (SQL Server-Konfigurations-Manager)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Fügen Sie den gewünschten Port dem *$serverName* Parameter von der [Sqlsrv_connect](../../connect/php/sqlsrv-connect.md) Funktion. Trennen Sie den Servernamen und den Port durch ein Komma. Beispielsweise verwenden die folgenden Codezeilen die SQLSRV-Treiber, um zu veranschaulichen, wie die Verbindung mit einem Server namens *myServer* über Port 1521 hergestellt wird:  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    Die folgenden Codezeilen verwenden den PDO_SQLSRV-Treiber zu um zeigen, wie die Verbindung mit einem Server mit dem Namen *"EigenerServer"* über Port 1521 hergestellt:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)

[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[Erste Schritte mit Microsoft-Treiber für PHP für SQLServer](../../connect/php/getting-started-with-the-php-sql-driver.md)

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Referenz zum Treiber PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
