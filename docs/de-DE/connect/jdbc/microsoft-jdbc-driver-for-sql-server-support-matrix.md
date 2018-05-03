---
title: Microsoft JDBC Driver für SQL Server-Supportmatrix | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07eebb2ef5464109b3d363d521744f4342c8d578
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Supportmatrix für den Microsoft JDBC-Treiber für SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Auf dieser Seite finden Sie die Unterstützungsmatrix und die Support Lifecycle-Richtlinie für den Microsoft JDBC-Treiber für SQL Server.  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Unterstützungsmatrix und Support Lifecycle-Richtlinie für Microsoft JDBC-Treiber  
 Die Microsoft Support Lifecycle-Richtlinie (MLS) bietet transparente, vorhersagbare Informationen hinsichtlich der Supportdauer bei Microsoft-Produkten. JDBC Driver, Version 3.0, 4.x und 6.x haben Veröffentlichungsdatum fünf Jahre grundlegender Support aus dem Treiber. Die Definition für Mainstream-Support finden Sie auf der Website der Microsoft Support Lifecycle-Richtlinie.  
  
 Erweiterte und benutzerdefinierte Support-Optionen sind für den Microsoft JDBC-Treiber nicht verfügbar.  
    
 Die folgenden Microsoft JDBC-Treiber werden bis zum angegebenen Supportende unterstützt.  
  
|Treibername|Paket-Treiberversion|Zutreffend JAR(s)|Ende der Mainstream-Support|
|-|-|-|-|  
|Microsoft JDBC-Treiber 6.4 für SQL Server|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|22 Januar 2023|    
|Microsoft JDBC-Treiber 6.2 für SQL Server|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|30 Juni 2022|    
|Microsoft JDBC-Treiber 6.0 für SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|14 Juli 2021|    
|Der Microsoft JDBC-Treiber 4.2 für SQL Server|4.2|sqljdbc42.jar<br>sqljdbc41.jar|24. August 2020|  
|Microsoft JDBC-Treiber 4.1 für SQL Server|4.1|sqljdbc41.jar|12. Dezember 2019|  
  
 Die folgenden Microsoft JDBC-Treiber werden nicht länger unterstützt.  
 
|Treibername|Paket-Treiberversion|Ende der Mainstream-Support|  
|-|-|-|
|Microsoft JDBC-Treiber 4.0 für SQL Server|4.0|6. März 2017|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|23. April 2015|  
|Microsoft SQL Server JDBC Driver 2.2|2.0|31. Dezember 2012|  
|Microsoft SQL Server 2005 JDBC Driver 1.2|1.2|25. Juni 2011|  
|Microsoft SQL Server 2005 JDBC Driver 1.1|1.1|25. Juni 2011|  
|Microsoft SQL Server 2005 JDBC Driver 1.0|1,0|25. Juni 2011|  
|Microsoft SQL Server 2000 JDBC Driver|2000|9. Juli 2010|  
  
## <a name="sql-version-compatibility"></a>SQL-Versionskompatibilität  
  
|Treiberversion|SQL Server 2008|SQL Server 2008R2|SQL Server 2012|Azure SQL Database|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|SQL Azure verwaltete Instanz (Extended privaten Ansicht)|  
|-|-|-|-|-|-|-|-|-|-|
|6.4|N|J|J|J|J|J|J|J|J|  
|6.2|J|J|J|J|J|J|J|J|N|
|6.1|J|J|J|J|J|J|J|N|N|
|6.0|J|J|J|J|J|J|J|N|N|
|4.2|J|J|J|J|J|J|J|N|N|
|4.1|J|J|J|J|J|J|J|N|N|
|4.0|J|J|J|J|J|J|J|N|N|
|3.0|J|J|Y<sup>1</sup>|Y<sup>2</sup>|N|Y<sup>5</sup>|N|N|N|
|2.0|Y<sup>3</sup>|Y<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|Y<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|  
|1,0|N|N|N|N|N|N|N|N|N|  
|2000|N|N|N|N|N|N|N|N|N|  
  
 <sup>1</sup>Microsoft SQL Server JDBC Driver, Version 3.0 können auf SQL Server 2012 als ein downlevelclient eine Verbindung herstellen.  
  
 <sup>2</sup>Unterstützung für Azure SQL-Datenbank wurde in Version 3.0 als Hotfix eingeführt. Es wird empfohlen, dass Azure SQL-Datenbank-Kunden die neuesten Treiber verwenden.  
  
 <sup>3</sup>Microsoft SQL Server JDBC Driver, Version 2.0 und Microsoft SQL Server 2005 JDBC Driver, Version 1.2 können auf SQL Server 2008 als ein downlevelclient eine Verbindung herstellen. Sind abwärtskompatible Konvertierungen erlaubt, kann die Anwendung Abfragen ausführen und Aktualisierungen auf die neuen Datentypen von SQL Server 2008 durchführen, wie z. B. „time“, „date“, „datetime2“, „datetimeoffset“ und FILESTREAM. Weitere Informationen zur Verwendung dieser neuen Datentypen mit dem JDBC-Treiber finden Sie unter  [Verwenden der Date/Time-Datentypen in SQL Server 2008 mithilfe eines JDBC-Treibers](http://go.microsoft.com/fwlink/?LinkId=145198) und unter  [Verwenden von Filestream in SQL Server 2008 mithilfe eines JDBC-Treibers](http://go.microsoft.com/fwlink/?LinkId=145199). Weitere Informationen zur Abwärtskompatibilität dieser neuen Datentypen finden Sie in den Themen  [Verwenden von Datums- und Zeitdaten](http://go.microsoft.com/fwlink/?LinkId=145211)und  [FILESTREAM-Unterstützung](http://go.microsoft.com/fwlink/?LinkId=145212) in der SQL Server-Onlinedokumentation  
  
 <sup>4</sup>Unterstützung für Verbindungen zwischen dem Microsoft JDBC-Treiber und Parallel Data Warehouse wurde erstmals in Microsoft JDBC Driver 4.0 für SQL Server und Microsoft SQL Server 2008 R2 Parallel Data Warehouse Appliance Update 3.  
  
 <sup>5</sup>Microsoft SQL Server JDBC Driver, Version 3.0 können mit SQL Server 2014 als ein downlevelclient eine Verbindung herstellen.  
  
## <a name="java-and-jdbc-specification-support"></a>Unterstützung der Java- und JDBC-Spezifikation  
  
|Version des JDCB-Treibers|JRE-Version|JDBC-API-Version| 
|-|-|-|  
|6.4|1.7, 1.8, 1.9|4.1, 4.2, 4.3 (teilweise)|  
|6.2|1.7, 1.8|4.1, 4.2|  
|6.1|1.7, 1.8|4.1, 4.2|  
|6.0|1.7, 1.8|4.1, 4.2|  
|4.2|1.7, 1.8|4.1, 4.2|  
|4.1|1.7|4.0|  
|4.0|1.5, 1.6, 1.7|3.0, 4.0|  
|3.0|1.5, 1.6,|3.0, 4.0|  
|2.0|1.5, 1.6|3.0, 4.0|  
|1.2|1.4, 1.5, 1.6|3.0|  
|1.1|1.4|3.0|  
|1,0|1.4|3.0|  
|2000|1.4|3.0|  
  
## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 Der JDBC-Treiber ist für die Verwendung mit allen Betriebssystemen konzipiert, die die Java Virtual Machine (JVM) unterstützen. Einige weitverbreitete Plattformen enthalten Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2008 R2, Windows Vista, Linux, Unix, AIX, Mac OS und andere.  
  
 Das JDBC-Produktteam testet unsern Treiber unter Windows, Sun Solaris, SUSE Linux und RedHat Linux.  Der Kundendienst steht dem Kunden auf allen Plattformen zur Verfügung. Jedoch kann es vorkommen, dass Sie gebeten werden, Ihr Problem auf einer anderen Plattform, z. B. auf Windows, zu reproduzieren.  
  
## <a name="application-server-support"></a>Support für Anwendungsserver  
 Der Microsoft JDBC-Treiber für SQL Server wird mit verschiedenen Anwendungsservern getestet.  Wenden Sie sich an den Anbieter Ihres Anwendungsserver, um detaillierte Informationen über die zu seinem Produkt kompatible Treiberversion zu erhalten.  
  
  
