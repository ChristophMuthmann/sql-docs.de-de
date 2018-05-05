---
title: Microsoft Drivers for PHP for SQLServer-Support Matrix | Microsoft Docs
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
ms.topic: conceptual
caps.latest.revision: 1
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: 448a770c8b95f437c981eff2c4d6edcebb44d442
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP-Treiber für SQL Server-Supportmatrix
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  Diese Seite enthält Unterstützung Matrix und Support Lifecycle-Richtlinie für die Microsoft-Treiber für PHP für SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP Treiber Unterstützungsmatrix und Support Lifecycle-Richtlinie
 Die Microsoft Support Lifecycle-Richtlinie (MLS) bietet transparente, vorhersagbare Informationen hinsichtlich der Supportdauer bei Microsoft-Produkten. PHP-Treibern die Versionen 3.x, 4.x und 5.x fünf Jahre grundlegender Support nach dem Veröffentlichungsdatum Treiber haben. Der Mainstream-Support wird definiert, auf die [Microsoft Support Lifecycle-Website](https://support.microsoft.com/lifecycle).

 Erweiterte und benutzerdefinierte Support-Optionen sind nicht verfügbar für die Microsoft-Treiber für PHP.

 Die folgenden Microsoft PHP-Treiber werden bis zu der angegebenen Supportende unterstützt.

|Treibername|Paket-Treiberversion|Ende der Mainstream-Support|
|-|-|-|
|Microsoft PHP-Treibern 5.2 für SQLServer|5.2|9 Februar 2023|
|Microsoft PHP-Treibern 4.3 für SQLServer|4.3|6 Juli 2022|
|Microsoft PHP-Treiber 4.0 für SQLServer|4.0|11 Juli 2021|
|Microsoft PHP Drivers 3.2 for SQLServer|3.2|9 März 2020|
|Microsoft PHP Drivers 3.1 for SQLServer|3.1|12. Dezember 2019|

 Die folgenden Microsoft PHP-Treiber werden nicht mehr unterstützt.

|Treibername|Paket-Treiberversion|Ende der Mainstream-Support|
|-|-|-|
|Microsoft PHP-Treiber 3.0 für SQLServer|3.0|6. März 2017|
|Microsoft PHP-Treibern 2.0 für SQLServer|2.0|10 August 2015|
|Microsoft PHP-Treiber 1.0 für SQLServer|1,0|28. April 2014|

## <a name="sql-server-version-certified-compatibility"></a>SQL Server-Version zertifizierte Kompatibilität
 Die folgende Matrix führt SQL Server-Versionen, die getestet und als kompatibel mit der entsprechenden Treiberversion zertifiziert wurden. Wir bemühen uns, die Abwärtskompatibilität mit früheren Treiberversionen, aber nur der neueste unterstützte Treiber getestet und zertifiziert mit neuen SQL Server-Versionen als SQL Server freigegeben wird.

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;SQL Server-version|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Verwaltete Azure SQL-Instanz<br/> (Erweiterte privater Ansicht)|J|J| | | | | |
|Azure SQL Data Warehouse|J|J| | | | | |
|SQL Server 2017   |J|J| | | | | |
|SQL Server 2016   |J|J|J| | | | |
|SQL Server 2014   |J|J|J|J|J| | |
|SQL Server 2012   |J|J|J|J|J|J| |
|SQL Server 2008 R2|J|J|J|J|J|J|J|
|SQL Server 2008   | | |J|J|J|J|J|

## <a name="php-version-support"></a>Unterstützung für PHP-Version
 Die folgenden Versionen von PHP sind mit die aufgeführte Version von Microsoft PHP-Treiber unterstützt:

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;PHP-version|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|7.2.1+ unter Windows<br/>7.2.0+ auf anderen Plattformen| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4 +  |        |        |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme
 Die folgenden Windows-Betriebssystemversionen werden mit die aufgeführte Version von Microsoft PHP-Treiber unterstützt:

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;Betriebssystem|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Windows Server 2016                 |J  |J  |   |   |   |   |   |
|Windows Server 2012 R2              |J  |J  |J  |J  |J  |   |   |
|Windows Server 2012                 |J  |J  |J  |J  |J  |   |   |
|Windows Server 2008 R2 SP1          |   |   |J  |J  |J  |J  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |J  |
|Windows Server 2008 SP2             |   |   |J  |J  |J  |J  |   |
|Windows Server 2008                 |   |   |   |   |   |   |J  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |J  |
|Windows 10                          |J  |J  |J  |   |   |   |   |
|Windows 8.1                         |J  |J  |J  |J  |J  |   |   |
|Windows 8                           |   |J  |J  |J  |J  |   |   |
|Windows 7 SP1                       |   |   |J  |J  |J  |J  |   |
|Windows Vista SP2                   |   |   |J  |J  |J  |J  |J  |
|Windows XP SP3                      |   |   |   |   |   |   |J  |

 Die folgenden Linux und Macintosh-Betriebssystemversionen (nur 64-Bit) werden mit die aufgeführte Version von Microsoft PHP-Treiber unterstützt:

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;Betriebssystem|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Ubuntu 17.10 (64-Bit)               |J  |   |   |   |   |   |   |
|Ubuntu 16.04 (64-Bit)               |J  |J  |J  |   |   |   |   |
|Ubuntu 15.10 (64-Bit)               |   |J  |   |   |   |   |   |
|Ubuntu 15.04 (64-Bit)               |   |   |J  |   |   |   |   |
|Debian 9 (64-Bit)                   |J  |   |   |   |   |   |   |
|Debian 8 (64-Bit)                   |J  |J  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64-Bit) |J  |J  |J  |   |   |   |   |
|Enterprise SuSE Linux 12 (64-Bit)   |J  |   |   |   |   |   |   |
|MacOS Sierra (64-Bit)               |J  |J  |   |   |   |   |   |
|MacOS El Capitan (64-Bit)           |J  |J  |   |   |   |   |   |

## <a name="see-also"></a>Siehe auch  
[Anmerkungen zu dieser Version](../../connect/php/release-notes-for-the-php-sql-driver.md)

[Supportressourcen](../../connect/php/support-resources-for-the-php-sql-driver.md)

[Systemanforderungen](../../connect/php/system-requirements-for-the-php-sql-driver.md)
