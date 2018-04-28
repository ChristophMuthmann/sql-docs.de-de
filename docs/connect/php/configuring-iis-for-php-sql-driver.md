---
title: Konfigurieren von IIS für die Microsoft-Treiber für PHP für SQLServer | Microsoft Docs
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
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 047a1af6d22d7f28f27ccc2b8f6172964d8d831d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>Konfigurieren von IIS für die Microsoft-Treiber für PHP für SQLServer
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema enthält Links zu Ressourcen, auf die [Website (Internet Information Services, IIS)](https://www.iis.net/) für die Konfiguration von IIS zum Hosten von PHP-Anwendungen relevant sind. Die hier aufgelisteten Ressourcen sind spezifisch für die Verwendung von FastCGI mit IIS. FastCGI ist ein Standardprotokoll, das den ausführbaren Dateien der gemeinsamen Gatewayschnittstelle (CGI) eines Anwendungsframeworks die Kommunikation mit dem Webserver ermöglicht. FastCGI unterscheidet sich vom CGI-Standardprotokoll, insofern, dass FastCGI die CGI-Prozesse für mehrere Anforderungen wiederverwendet.  
  
## <a name="tutorials"></a>Lernprogramme  
Die folgenden Links führen zu Tutorials zum Einrichten von FastCGI für PHP und zum Hosten von PHP-Anwendungen in IIS 6.0 und IIS 7.0:  
  
-   [FastCGI mit PHP](https://docs.microsoft.com/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [Die Verwendung von FastCGI zum Hosten von PHP-Anwendungen unter IIS 7.0](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [Die Verwendung von FastCGI zum Hosten von PHP-Anwendungen auf IIS 6.0](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [Konfigurieren einer FastCGI-Erweiterung für IIS 6.0](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>Videopräsentationen  
Die folgenden Links führen zu Videopräsentationen zum Einrichten von FastCGI für PHP und zur Verwendung von IIS 7.0-Features zum Hosten von PHP-Anwendungen:  
  
-   [Einrichten von FastCGI für PHP](https://docs.microsoft.com/en-us/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [Partying mit PHP für Microsoft-Internetinformationsdienste 7](https://docs.microsoft.com/en-us/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>Supportressourcen  
Die folgenden Foren bieten Communityunterstützung für FastCGI unter IIS:  
  
-   [FastCGI-Handler](https://forums.iis.net/1103.aspx)  
-   [IIS 7 – FastCGI-Modul](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit Microsoft-Treiber für PHP für SQLServer](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
