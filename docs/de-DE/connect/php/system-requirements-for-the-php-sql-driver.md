---
title: Systemanforderungen für die Microsoft-Treiber für PHP für SQLServer | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
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
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23b8c2e8fe5545f19848f589a2a830c1d402c8d5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Systemanforderungen für die Microsoft-Treiber für PHP für SQLServer
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Dokument aufgeführt, die Komponenten, die auf den Zugriff auf Daten in einer SQL Server oder Azure SQL-Datenbank mit dem System installiert werden, müssen die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

Versionen 3.1 und höher die Microsoft PHP-Treiber für SQL Server werden offiziell unterstützt. Vollständige Informationen zu Supportlebenszyklen und Anforderungen, einschließlich früherer Versionen von PHP-Treibern, finden Sie unter der [Unterstützungsmatrix](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Informationen zum Herunterladen und installieren die neueste stabilen PHP-Binärdateien finden Sie unter [der PHP-Website](http://php.net).  Microsoft Drivers for PHP for SQL Server erfordern die folgenden Versionen von PHP:

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;PHP-version|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|7.2.1+ unter Windows<br/>7.2.0+ auf anderen Plattformen | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4 +  |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   Eine Version der Treiberdatei muss sich in Ihrem PHP-Erweiterungsverzeichnis befinden. Finden Sie unter [Treiberversionen](#driver-versions) Informationen zu den verschiedenen Treiberdateien.  Zum Herunterladen der Treiber finden Sie unter [Herunterladen von Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md). Informationen zur Konfiguration der Treiber für PHP finden Sie unter [Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md).

-   Ein Webserver ist erforderlich. Ihr Webserver muss für die Ausführung von PHP konfiguriert sein. Informationen zum Hosten von PHP-Anwendungen mit IIS finden Sie unter der [Lernprogramm auf PHPs-Website](http://php.net/manual/fa/install.windows.iis.php).  

    Die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 10 IIS mit FastCGI getestet wurde.  

    > [!NOTE]  
    > Microsoft bietet lediglich für IIS Support.  

## <a name="odbc-driver"></a>ODBC-Treiber

Die richtige Version von Microsoft ODBC Driver für SQL Server muss auf dem Computer, auf dem PHP ausgeführt wird. Die folgenden Links herunterladen:
- [Microsoft ODBC Driver 17 für SQLServer](https://www.microsoft.com/en-us/download/details.aspx?id=56567)
- [Microsoft ODBC Driver 13.1 for SQLServer](https://www.microsoft.com/en-us/download/details.aspx?id=53339)
- [Microsoft ODBC Driver 13 for SQLServer](https://www.microsoft.com/download/details.aspx?id=50420)
- [Microsoft ODBC Driver 11 für SQLServer](http://www.microsoft.com/download/details.aspx?id=36434)

Wenn Sie eine 64-Bit-Betriebssystem verwenden, installiert der ODBC-64-Bit-Installationsprogramm 32-Bit und 64-Bit-ODBC-Treiber. Wenn Sie eine 32-Bit-Betriebssystem verwenden, verwenden Sie die ODBC-X86 Installer.

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;ODBC-Treiberversion|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|ODBC-Treiber 17  |J| | | | |
|Odbcdriver 13.1|J|J|J| | |
|ODBC-Treiber 13  | | |J| | |
|ODBC-Treiber 11  |J|J|J|J|J|

Bei Verwendung des SQLSRV-Treibers [Sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) gibt Informationen über die Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird von Microsoft ODBC Driver for SQL Server verwendet die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Wenn Sie den PDO_SQLSRV-Treiber verwenden, können Sie [GetAttribute](../../connect/php/pdo-getattribute.md) zum Ermitteln der Version.  

## <a name="sql-server"></a>SQL Server

Azure SQL-Datenbanken werden unterstützt. Informationen finden Sie unter [Herstellen einer Verbindung mit Microsoft Azure SQL-Datenbank](../../connect/php/connecting-to-microsoft-azure-sql-database.md).

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;SQL Server-version|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Verwaltete Azure SQL-Instanz<br/> (Erweiterte privater Ansicht)|J|J| | | |
|Azure SQL Data Warehouse|J|J| | | |
|SQL Server 2017   |J|J| | | |
|SQL Server 2016   |J|J|J| | |
|SQL Server 2014   |J|J|J|J|J|
|SQL Server 2012   |J|J|J|J|J|
|SQL Server 2008 R2|J|J|J|J|J|
|SQL Server 2008   | | |J|J|J|

## <a name="operating-systems"></a>Betriebssysteme
Unterstützter Betriebssysteme für die Versionen des Treibers lauten wie folgt:

|PHP für SQL Server-Treiberversion&#8594;<br />&#8595;Betriebssystem|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Windows Server 2016                      |J|J| | | |
|Windows Server 2012 R2                   |J|J|J|J|J|
|Windows Server 2012                      |J|J|J|J|J|
|Windows Server 2008 R2 SP1               | | |J|J|J|
|Windows Server 2008 SP2                  | | |J|J|J|
|Windows 10                               |J|J|J| | |
|Windows 8.1                              |J|J|J|J|J|
|Windows 8                                | |J|J|J|J|
|Windows 7 SP1                            | | |J|J|J|
|Windows Vista SP2                        | | |J|J|J|
|Ubuntu 17.10 (64-Bit)                    |J| | | | |
|Ubuntu 16.04 (64-Bit)                    |J|J|J| | |
|Ubuntu 15.10 (64-Bit)                    | |J| | | |
|Ubuntu 15.04 (64-Bit)                    | | |J| | |
|Debian 9 (64-Bit)                        |J| | | | |
|Debian 8 (64-Bit)                        |J|J| | | |
|Red Hat Enterprise Linux 7 (64-Bit)      |J|J|J| | |
|Enterprise SuSE Linux 12 (64-Bit)        |J| | | | |
|MacOS Sierra (64-Bit)                    |J|J| | | |
|MacOS El Capitan (64-Bit)                |J|J| | | |

## <a name="driver-versions"></a>Treiberversionen  
Dieser Abschnitt listet die Treiberdateien, die mit jeder Version von enthalten sind die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Jedem Installationspaket enthält die SQLSRV- und PDO_SQLSRV-Treiber-Dateien in Threads und nicht-threaded Varianten. Unter Windows sind auch verfügbar in 32-Bit und 64-Bit-Varianten. Um die Treiber für die Verwendung mit der PHP-Laufzeit zu konfigurieren, führen Sie die installationsanweisungen im [Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md).

Auf unterstützten Versionen von Linux und MacOS geeignete Treiber installiert werden können mithilfe PHPs-PECL Paket System nach dem [installationsanweisungen für Linux und MacOS](../../connect/php/installation-tutorial-linux-mac.md). Alternativ können Sie herunterladen vorgefertigte Binärdateien für Ihre Plattform aus der [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github-Projektseite--die folgenden Tabellen enthalten die Dateien in binäre vorgefertigten Pakete gefunden.

**Microsoft Drivers 5.2 for PHP for SQLServer:**  

Unter Windows werden die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|32-Bit-php_sqlsrv_7_nts.dll <br />32-Bit-php_pdo_sqlsrv_7_nts.dll |7.0|nein |32-Bit-php7.dll|
|32-Bit-php_sqlsrv_7_ts.dll  <br />32-Bit-php_pdo_sqlsrv_7_ts.dll  |7.0|ja|32-Bit-php7ts.dll|
|64-Bit-php_sqlsrv_7_nts.dll <br />64-Bit-php_pdo_sqlsrv_7_nts.dll |7.0|nein |64-Bit-php7.dll|  
|64-Bit-php_sqlsrv_7_ts.dll  <br />64-Bit-php_pdo_sqlsrv_7_ts.dll  |7.0|ja|64-Bit-php7ts.dll|
|32-Bit-php_sqlsrv_71_nts.dll<br />32-Bit-php_pdo_sqlsrv_71_nts.dll|7.1|nein |32-Bit-php7.dll|  
|32-Bit-php_sqlsrv_71_ts.dll <br />32-Bit-php_pdo_sqlsrv_71_ts.dll |7.1|ja|32-Bit-php7ts.dll|  
|64-Bit-php_sqlsrv_71_nts.dll<br />64-Bit-php_pdo_sqlsrv_71_nts.dll|7.1|nein |64-Bit-php7.dll|  
|64-Bit-php_sqlsrv_71_ts.dll <br />64-Bit-php_pdo_sqlsrv_71_ts.dll |7.1|ja|64-Bit-php7ts.dll|   
|32-Bit-php_sqlsrv_72_nts.dll<br />32-Bit-php_pdo_sqlsrv_72_nts.dll|7.2|nein |32-Bit-php7.dll|  
|32-Bit-php_sqlsrv_72_ts.dll <br />32-Bit-php_pdo_sqlsrv_72_ts.dll |7.2|ja|32-Bit-php7ts.dll|  
|64-Bit-php_sqlsrv_72_nts.dll<br />64-Bit-php_pdo_sqlsrv_72_nts.dll|7.2|nein |64-Bit-php7.dll|  
|64-Bit-php_sqlsrv_72_ts.dll <br />64-Bit-php_pdo_sqlsrv_72_ts.dll |7.2|ja|64-Bit-php7ts.dll|  

Unter Linux sind die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|nein |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|ja|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|nein |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|ja|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|nein |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|ja|

**Microsoft Drivers 4.3 for PHP for SQLServer:**  

Unter Windows werden die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|32-Bit-php_sqlsrv_7_nts.dll <br />32-Bit-php_pdo_sqlsrv_7_nts.dll |7.0|nein |32-Bit-php7.dll|
|32-Bit-php_sqlsrv_7_ts.dll  <br />32-Bit-php_pdo_sqlsrv_7_ts.dll  |7.0|ja|32-Bit-php7ts.dll|
|64-Bit-php_sqlsrv_7_nts.dll <br />64-Bit-php_pdo_sqlsrv_7_nts.dll |7.0|nein |64-Bit-php7.dll|  
|64-Bit-php_sqlsrv_7_ts.dll  <br />64-Bit-php_pdo_sqlsrv_7_ts.dll  |7.0|ja|64-Bit-php7ts.dll|
|32-Bit-php_sqlsrv_71_nts.dll<br />32-Bit-php_pdo_sqlsrv_71_nts.dll|7.1|nein |32-Bit-php7.dll|  
|32-Bit-php_sqlsrv_71_ts.dll <br />32-Bit-php_pdo_sqlsrv_71_ts.dll |7.1|ja|32-Bit-php7ts.dll|  
|64-Bit-php_sqlsrv_71_nts.dll<br />64-Bit-php_pdo_sqlsrv_71_nts.dll|7.1|nein |64-Bit-php7.dll|  
|64-Bit-php_sqlsrv_71_ts.dll <br />64-Bit-php_pdo_sqlsrv_71_ts.dll |7.1|ja|64-Bit-php7ts.dll|   

Unter Linux sind die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|nein |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|ja|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|nein |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|ja|  

**Microsoft-Treiber 4.0 für PHP für SQLServer:**  

Unter Windows werden die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|nein|32-Bit-php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|ja|32-Bit-php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|nein|64-Bit-php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|ja|64-Bit-php7ts.dll|   

Unter Linux sind die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|nein |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|ja|

**Microsoft Drivers 3.2 for PHP for SQLServer:**  

Unter Windows werden die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|nein|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|ja|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|nein|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|ja|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|nein|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|ja|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQLServer:**  

Unter Windows werden die folgenden Versionen des Treibers enthalten:

|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|nein|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|ja|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|nein|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|ja|php5ts.dll|  

## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit Microsoft-Treiber für PHP für SQLServer](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[API-Referenz zum Treiber PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
