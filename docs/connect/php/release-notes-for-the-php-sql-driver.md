---
title: "Versionshinweise für den PHP-SQL-Treiber | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: "37"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7614ac9453d6021503ac6f5c86ef852269df30fd
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="release-notes-for-the-php-sql-driver"></a>Versionshinweise für den PHP-SQL-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema wird erläutert, was in jeder Version von hinzugefügt wurde die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="whats-new-in-version-43"></a>Was ist neu in Version 4.3

- Unterstützung für PHP 7.1
- Unterstützung für Mac OS Sierra und Mac OS El Capitan
- Unterstützung für Ubuntu 15.10 sowie Debian 8
- Keine Unterstützung mehr für Ubuntu 15.04
- Unterstützung für Verfügbarkeit mit AlwaysOn-Gruppen über transparenten Netzwerk-IP-Auflösung. Weitere Informationen finden Sie unter [Connection Options](../../connect/php/connection-options.md). 
- Unterstützung für Sql_variant-Datentyp mit der Einschränkung hinzugefügt.
- Idle Connection Resiliency-Unterstützung in Windows. Weitere Informationen finden Sie unter [Connection Options](../../connect/php/connection-options.md).
- Unterstützung für Linux und MacOS für Verbindungspooling. Weitere Informationen finden Sie unter [Verbindungspooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Unterstützung für Azure Active Directory-Authentifizierung mit ActiveDirectoryPassword und SqlPassword. Weitere Informationen finden Sie unter [Connection Options](../../connect/php/connection-options.md).
  
## <a name="whats-new-in-version-40"></a>Was ist neu in Version 4.0 

- Unterstützung für PHP 7.0  
- 64-Bit-Unterstützung
- Unterstützung für Ubuntu 15.04, Ubuntu 16.04 und RedHat 7

## <a name="whats-new-in-version-32"></a>Neuerungen in Version 3.2 

- Unterstützung für PHP 5.6   
- Enthält die neuesten Updates für vorherige PHP-Versionen 5.5 und 5.4   
- Erfordert Microsoft ODBC Driver 11 für SQLServer  
  
## <a name="whats-new-in-version-31"></a>Neuerungen in Version 3.1
 
- Unterstützung für PHP 5.5  
- Erfordert Microsoft ODBC Driver 11 für SqlServer. Frühere Versionen benötigten SQL Native Client.  
  
## <a name="whats-new-in-version-30"></a>Neuerungen in Version 3.0  

- Unterstützung für PHP 5.4  PHP 5.2 wird in Version 3 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]nicht unterstützt.  
- Verbindungsoption AttachDBFileName wurde hinzugefügt. Weitere Informationen finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
- Unterstützung für LocalDB, (ab [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]). Weitere Informationen finden Sie unter [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- Verbindungsoption AttachDBFileName wurde hinzugefügt. Weitere Informationen finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
- Unterstützung für die Funktionen für die hohe Verfügbarkeit und notfallwiederherstellung. Weitere Informationen finden Sie unter [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(Unterstützung für hohe Verfügbarkeit im PHP-Treiber für SQL Server, Notfallwiederherstellung).
- Unterstützung für clientseitige Cursor (Zwischenspeichern eines Resultsets im Arbeitsspeicher). Weitere Informationen finden Sie unter [Cursortypen &#40; SQLSRV-Treiber &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md) und [Cursortypen &#40; PDO_SQLSRV-Treiber &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- Das Attribut PDO::ATTR_EMULATE_PREPARES- wurde hinzugefügt. Weitere Informationen finden Sie unter [PDO:: Prepare](../../connect/php/pdo-prepare.md).  
  
## <a name="whats-new-in-version-20"></a>Neuerungen in Version 2.0  
In Version 2.0 wurde Unterstützung für den PDO_SQLSRV-Treiber hinzugefügt. Weitere Informationen finden Sie in der [PDO_SQLSRV-Treiberreferenz](../../connect/php/pdo-sqlsrv-driver-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
[Übersicht zum PHP-SQL-Treiber](../../connect/php/overview-of-the-php-sql-driver.md)
  
