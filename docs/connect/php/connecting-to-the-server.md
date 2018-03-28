---
title: Herstellen einer Verbindung mit dem Server | Microsoft Docs
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
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 818a71b8e0bc60168602e7fc0228c21319d08a21
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="connecting-to-the-server"></a>Verbinden mit dem Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Die Themen in diesem Abschnitt beschreiben die Optionen und Verfahren, um mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Verbindung zu [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]herzustellen.  

Mittels der Windows-Authentifizierung oder der SQL Server-Authentifizierung können sich die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verbinden. Standardmäßig versuchen die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] sich mit dem Server zu verbinden, in dem sie die Windows-Authentifizierung verwenden.  

## <a name="in-this-section"></a>In diesem Abschnitt  

|Thema|Description|  
|---------|---------------|  
|[Vorgehensweise: Herstellen einer Verbindung mithilfe der Windows-Authentifizierung](../../connect/php/how-to-connect-using-windows-authentication.md)|Beschreibt, wie eine Verbindung mittels der Windows-Authentifizierung hergestellt wird|  
|[Vorgehensweise: Herstellen einer Verbindung mithilfe der SQL Server-Authentifizierung](../../connect/php/how-to-connect-using-sql-server-authentication.md)|Beschreibt wie eine Verbindung mittels der SQL Server-Authentifizierung hergestellt wird|  
|[Gewusst wie: Herstellen einer Verbindung mithilfe der Azure Active Directory-Authentifizierung](../../connect/php/azure-active-directory.md)|Beschreibt, wie Sie den Authentifizierungsmodus festlegen und Herstellen einer Verbindung mithilfe von Azure Active Directory-Identitäten.|  
|[Gewusst wie: Verbinden über einen angegebenen Port](../../connect/php/how-to-connect-on-a-specified-port.md)|Beschreibt wie eine Verbindung zum Server über einen angegebenen Port hergestellt wird|  
|[Verbindungspooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|Bietet Informationen zum Verbindungspooling im Treiber|  
|[Gewusst wie: Deaktivieren von Multiple Active Resultsets (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|Beschreibt wie die MARS-Funktion beim Herstellen einer Verbindung deaktiviert wird|  
|[Verbindungsoptionen](../../connect/php/connection-options.md)|Listet die erlaubten Optionen im assoziativen Array auf, das Verbindungsattribute enthält.|  
|[Unterstützung für LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|Beschreibt [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] -Unterstützung für die „LocalDB“-Funktion die in [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]hinzugefügt wurde.|  
|[Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|Erläutert, wie die Anwendung konfiguriert werden kann, um die hohe Verfügbarkeit und notfallwiederherstellung nutzen Funktionen, in hinzugefügt [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)].|  
|[Herstellen einer Verbindung mit einer Microsoft Azure SQL-Datenbank](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Erläutert, wie eine Verbindung mit einer Azure SQL-Datenbank herstellen.|  
|[Verbindungsstabilität](../../connect/php/connection-resiliency.md)|Erläutert das verbindungsstabilitätsfeature, das unterbrochene Verbindungen erneut herstellt.|  

## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[Beispielanwendung &#40;SQLSRV-Treiber&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
