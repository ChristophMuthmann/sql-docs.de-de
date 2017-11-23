---
title: "Systemanforderungen für den PHP-SQL-Treiber | Microsoft Docs"
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
helpviewer_keywords: requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: "93"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: abff6843dbf1b8f1362f10dbf2fe52fa5f686515
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="system-requirements-for-the-php-sql-driver"></a>Systemanforderungen für den PHP_SQL-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Für den Datenzugriff in einer SQL Server oder Azure SQL-Datenbank mit der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], müssen die folgenden Komponenten auf Ihrem Computer installiert sein:  
  
-   PHP ist erforderlich. Informationen zum Herunterladen und Installieren von stabilen Binärdateien finden Sie unter [http://php.net](http://go.microsoft.com/fwlink/?LinkId=101876).  Microsoft Drivers for PHP for SQL Server erfordern die folgenden Versionen:
  
|Version von Microsoft Drivers for PHP for SQL Server|Unterstützte PHP-Versionen|  
|----------------------------------------------------|--------------------------|  
|4.3|PHP 7.0 und PHP 7.1| 
|4.0|PHP 7.0|  
|3.2|PHP 5.6.4+ oder<br /><br />PHP 5.5.16+ oder<br /><br />PHP 5.4.32|  
|3.1|PHP 5.5.16+ oder<br /><br />PHP 5.4.32|  
|3.0|PHP 5.4.32 oder<br /><br />PHP 5.3.0|  
|2.0|PHP 5.3.0 oder<br /><br />PHP 5.2.4 oder<br /><br />PHP 5.2.13|  
  
-   Eine Version der Treiberdatei muss sich in Ihrem PHP-Erweiterungsverzeichnis befinden. Weiter unten in diesem Text finden Sie unter „Treiberversionen“ weitere Informationen zu den verschiedenen Treiberdateien. Unter [Laden des PHP-SQL-Treibers](../../connect/php/loading-the-php-sql-driver.md)  finden Sie weitere Informationen zur Konfiguration der Treiber für die PHP-Laufzeit. Zum Herunterladen der Treiber, gehen Sie zu [Microsoft Drivers for PHP for SQL Server](http://www.microsoft.com/download/details.aspx?id=20098).  
  
-   Ein Webserver ist erforderlich. Ihr Webserver muss für die Ausführung von PHP konfiguriert sein. Informationen zum Hosten von PHP-Anwendungen mit Internet Information Services (IIS) 6.0 finden Sie unter [FastCGI zum Hosten von PHP-Anwendungen auf IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=117131). Informationen zum Hosten von PHP-Anwendungen mit IIS 7.0 finden Sie unter [FastCGI zum Hosten von PHP-Anwendungen auf IIS 7.0 verwenden](http://go.microsoft.com/fwlink/?LinkId=117132).  
  
    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] wurde auf IIS 6 und IIS 7 mit FastCGI getestet.  
  
    > [!NOTE]  
    > Microsoft bietet lediglich für IIS Support.  
  
-   Die richtige Version von Microsoft ODBC Driver für SQL Server oder SQL Server Native Client muss auf dem Computer, auf dem PHP ausgeführt wird.  Wenn Sie eine 64-Bit-Betriebssystem verwenden, installiert der ODBC-64-Bit-Installationsprogramm 32-Bit und 64-Bit-ODBC-Treiber. Wenn Sie eine 32-Bit-Betriebssystem verwenden, verwenden Sie die ODBC-X86 Installer.

|Version von Microsoft Drivers for PHP for SQL Server|Version von Microsoft ODBC Driver for SQLServer oder SQL Server Native Client|  
|----------------------------------------------------|--------------------------|
|4.3|Microsoft ODBC Driver 11 für SQLServer oder Microsoft ODBC Driver 13.1 for SqlServer. Informationen zum Herunterladen von Microsoft ODBC-Treiber finden Sie unter der [Microsoft ODBC Driver 11 für SQL Server-Seite](http://www.microsoft.com/download/details.aspx?id=36434) oder [Microsoft ODBC Driver 13.1 für SQL Server-Seite](https://www.microsoft.com/en-us/download/details.aspx?id=53339)|    
|4.0|Microsoft ODBC Driver 11 für SQLServer oder Microsoft ODBC Driver 13 for SqlServer. Informationen zum Herunterladen von Microsoft ODBC-Treiber finden Sie unter der [Microsoft ODBC Driver 11 für SQL Server-Seite](http://www.microsoft.com/download/details.aspx?id=36434) oder [Microsoft ODBC Driver 13 für SQL Server-Seite](https://www.microsoft.com/download/details.aspx?id=50420)|  
|3.2 oder <br><br> 3.1|Microsoft ODBC Driver 11 für SqlServer. Informationen zum Herunterladen von Microsoft ODBC-Treiber finden Sie unter der [Microsoft ODBC Driver 11 für SQL Server-Seite](http://www.microsoft.com/download/details.aspx?id=36434)|   
|3.0|Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client. Sie können den Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client von der [SQL Server 2012 Feature Pack-Seite](http://go.microsoft.com/fwlink/?LinkID=236805)| 
|2.0|Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro_md.md)] Native Client:<br /><br />[Die X86 Downloadpaket](http://go.microsoft.com/fwlink/?LinkID=188400&clcid=0x409) für 32-Bit-Betriebssysteme <br /><br />[Die X64 Downloadpaket](http://go.microsoft.com/fwlink/?LinkID=188401&clcid=0x409) für 64-Bit-Betriebssysteme|  

  
Bei Verwendung des SQLSRV-Treibers [Sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) gibt Informationen über die Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird von Native Client oder Microsoft ODBC Driver for SQL Server verwendet die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Wenn Sie den PDO_SQLSRV-Treiber verwenden, können Sie [GetAttribute](../../connect/php/pdo-getattribute.md) zum Ermitteln der Version.  



## <a name="database-versions"></a>Datenbank-Versionen
-   Azure SQL-Datenbanken werden unterstützt. Informationen finden Sie unter [Herstellen einer Verbindung mit Microsoft Azure SQL-Datenbank](../../connect/php/connecting-to-microsoft-azure-sql-database.md). 

- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]Version 4.3 unterstützt SQL Server 2008 R2 und höher
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]Version 4.0 unterstützt SQLServer 2008 und höher
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]Unterstützung für Version 3.1 SQLServer 2008 und höher
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]Version 2.0 und 3.0 unterstützt SQLServer 2005 und höher


## <a name="driver-versions"></a>Treiberversionen  
Dieser Abschnitt listet die Treiber, die mit jeder Version von enthalten sind die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Um die Treiber für die Verwendung mit der PHP-Laufzeit zu konfigurieren, führen Sie die installationsanweisungen im [Laden des PHP-SQL-Treibers](../../connect/php/loading-the-php-sql-driver.md).  
  
**Microsoft Drivers 4.3 for PHP for SQLServer:**  

Unter Windows werden für 4.3 die folgenden Versionen des Treibers installiert:
  
|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|Nein|32-Bit-php7.dll| 
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|Ja|32-Bit-php7ts.dll| 
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|Nein|64-Bit-php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|Ja|64-Bit-php7ts.dll| 
|php_sqlsrv_71_nts_x86.dll<br /><br />php_pdo_sqlsrv_71_nts_x86.dll|7.1|Nein|32-Bit-php7.dll|  
|php_sqlsrv_71_ts_x86.dll<br /><br />php_pdo_sqlsrv_71_ts_x86.dll|7.1|Ja|32-Bit-php7ts.dll|  
|php_sqlsrv_71_nts_x64.dll<br /><br />php_pdo_sqlsrv_71_nts_x64.dll|7.1|Nein|64-Bit-php7.dll|  
|php_sqlsrv_71_ts_x64.dll<br /><br />php_pdo_sqlsrv_71_ts_x64.dll|7.1|Ja|64-Bit-php7ts.dll|   
  
**Microsoft-Treiber 4.0 für PHP für SQLServer:**  

Unter Windows werden für 4.0 die folgenden Versionen des Treibers installiert:
  
|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|Nein|32-Bit-php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|Ja|32-Bit-php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|Nein|64-Bit-php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|Ja|64-Bit-php7ts.dll|   
  
Zu den unterstützten Versionen von Linux kann die entsprechende Version von Sqlsrv und/oder Pdo_sqlsrv mithilfe PHPs-PECL Paket System installiert werden. 
  
**Microsoft Drivers 3.2 for PHP for SQL Server installiert die folgenden Versionen des Treibers:**  
  
|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|nein|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|ja|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|nein|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|ja|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br /><br />php_pdo_sqlsrv_56_nts.dll|5.6|nein|php5.dll|  
|php_sqlsrv_56_ts.dll<br /><br />php_pdo_sqlsrv_56_ts.dll|5.6|ja|php5ts.dll|  
  
**Microsoft Drivers 3.1 for PHP for SQL Server installiert die folgenden Versionen des Treibers:**  
  
|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|nein|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|ja|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|nein|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|ja|php5ts.dll|  
  
**Microsoft Drivers 3.0 for PHP for SQL Server installiert die folgenden Versionen des Treibers:**  
  
|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts.dll<br /><br />php_pdo_sqlsrv_53_nts.dll|5.3|nein|php5.dll|  
|php_sqlsrv_53_ts.dll<br /><br />php_pdo_sqlsrv_53_ts.dll|5.3|ja|php5ts.dll|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|nein|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|ja|php5ts.dll|  
  
**Microsoft Drivers 2.0 for PHP for SQL Server installiert die folgenden Versionen des Treibers:**  
  
|Treiberdatei|PHP-Version|Threadsicher?|Zu verwendende PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts_vc6.dll<br /><br />php_pdo_sqlsrv_53_nts_vc6.dll|5.3|nein|php5.dll|  
|php_sqlsrv_53_nts_vc9.dll<br /><br />php_pdo_sqlsrv_53_nts_vc9.dll|5.3|nein|php5.dll|  
|php_sqlsrv_53_ts_vc6.dll<br /><br />php_pdo_sqlsrv_53_ts_vc6.dll|5.3|ja|php5ts.dll|  
|php_sqlsrv_53_ts_vc9.dll<br /><br />php_pdo_sqlsrv_53_ts_vc9.dll|5.3|ja|php5ts.dll|  
|php_sqlsrv_52_nts_vc6.dll<br /><br />php_pdo_sqlsrv_52_nts_vc6.dll|5.2|nein|php5.dll|  
|php_sqlsrv_52_ts_vc6.dll<br /><br />php_pdo_sqlsrv_52_ts_vc6.dll|5.2|ja|php5ts.dll|  
  
Wenn der Name der Treiberdatei „vc9“ enthält, sollte er mit einer PHP-Version, die mit Visual C++ 9.0 kompiliert wurde, verwendet werden.  
## <a name="operating-systems"></a>Betriebssysteme 
Unterstützter Betriebssysteme für die Versionen des Treibers lauten wie folgt:

-   4.3:
    -   Windows Server 2012  
    -   Windows Server 2012 R2
    -   Windows Server 2016 
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10
    -   Ubuntu 15.10 (64-Bit)
    -   Ubuntu 16.04 (64-Bit)
    -   Debian 8 (64-Bit)
    -   Red Hat Enterprise Linux 7 (64-Bit)
    -   Mac OS Sierra (64-Bit)
    -   Mac OS El Capitan (64-Bit)
    
-   4.0:  
    -   Windows Server 2008 SP2
    -   Windows Server 2008 R2 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows Vista SP2  
    -   Windows 7 SP1  
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10 
    -   Ubuntu 15.04 (64-Bit)
    -   Ubuntu 16.04 (64-Bit)
    -   Red Hat Enterprise Linux 7 (64-Bit)

 
-   3.2 und 3.1:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows 8  
    -   Windows 8.1  
  
  
-   3.0:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  


-   2.0:
    -   [!INCLUDE[winxpsvr](../../includes/winxpsvr_md.md)] Service Pack 1  
    -   Windows XP Service Pack 3  
    -   Windows Vista Service Pack 1 oder neuer  
    -   Windows Server 2008  
    -   Windows Server 2008 R2  
    -   Windows 7  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit dem PHP-SQL-Treiber](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV-Treiber – API-Referenz](../../connect/php/sqlsrv-driver-api-reference.md)  
  
