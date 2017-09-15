---
title: Versionshinweise - Microsoft ODBC Driver for SQL Server unter Linux und MacOS | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fe65ff49f5618634517b612c2430a3489ac11141
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Anmerkungen zu dieser Version für den Microsoft ODBC Driver for SQL Server unter Linux und macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>What's New in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS  

Odbcdriver 13.1 for [! INCLUDEssNoVersion] fügt Unterstützung für Always Encrypted und Azure Active Directory in Verbindung mit Microsoft SQL Server 2016. 

**Neue Verteilungen unterstützt**: OS X 10.11 und MacOS 10.12 werden in der ersten Version des ODBC-Treibers auf MacOS unterstützt. Ubuntu 16.10 wird nun ebenfalls unterstützt, zusammen mit Red Hat-6, 7 und SUSE 12. Jede Plattform gibt es eine Plattform entsprechende Paket (RPM oder DEB), um die Installation und Konfiguration zu vereinfachen.  Finden Sie unter [Installieren des Treibers](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) installationsanweisungen.

**UnixODBC 2.3.1-Treiber-Manager-Unterstützungsänderungen**: die ODBC-Treiber hängt benutzerdefinierte Packen für den UnixODBC Treiber-Manager nicht mehr (außer RedHat 6), und verlässt sich stattdessen auf die Verteilung-Paket-Manager zum Auflösen der UnixODBC-Abhängigkeit aus der Verteilung Repositorys.

**BCP-API-Unterstützung**: die Linux und MacOS ODBC-Treiber unterstützt jetzt die Verwendung von der [BCP-API-Funktionen (**Bcp_init**usw..)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>Neuigkeiten in Microsoft ODBC Driver 13.0 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Linux  
Microsoft ODBC Driver 13.0 für SQL Server werden SQL Server 2014 und SQL Server 2016 nun ebenfalls unterstützt.  
  
**Neue Verteilungen unterstützt**:

Ubuntu wird jetzt zusammen mit Red Hat und SUSE unterstützt. Jede Plattform gibt es eine Plattform entsprechende Paket (RPM oder DEB), um die Installation und Konfiguration zu vereinfachen.  Finden Sie unter [Installieren des Treibers](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) installationsanweisungen.
  
**UnixODBC 2.3.1-Treiber-Manager-Unterstützung**: Zusätzlich zu einer neueren-Treiber-Manager ist außerdem ein Paket für die Installation dieser Abhängigkeit, die die Installation und Konfiguration vereinfacht.  

**Transparentes Netzwerk-IP-Auflösung**: transparentes Netzwerk-IP-Auflösung ist eine Version der vorhandenen Multisubnetz-Failover-Funktion, die die Verbindungssequenz des Treibers in die Groß-/Kleinschreibung wirkt sich auf, in dem die erste aufgelöst IP-Adresse des dem Hostnamen nicht, reagieren, und es sind mehrere IP-Adressen, die den Hostnamen zugeordnet.

**TLS 1.2-Unterstützung**: der Microsoft ODBC-Treiber 13.0 für SQL Server unter Linux unterstützt jetzt TLS 1.2 bei der sichere der Kommunikation mit SQL Server verwendet werden.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>Neuigkeiten in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Odbcdriver 11 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Linux  
Der ODBC-Treiber unter SUSE Linux (Preview) unterstützt das 64-Bit-SUSE Linux Enterprise 11 Service Pack 2. Weitere Informationen finden Sie unter [Systemanforderungen](../../../connect/odbc/linux-mac/system-requirements.md).  
  
Der ODBC-Treiber unter Linux unterstützt [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Weitere Informationen finden Sie unter [ODBC-Treiber unter Linux-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
Der ODBC-Treiber unter Linux unterstützt Verbindungen mit Microsoft Azure SQL-Datenbanken. Weitere Informationen finden Sie unter [Gewusst wie: Verbinden mit Microsoft Azure SQL-Datenbank mithilfe von ODBC](http://msdn.microsoft.com/library/hh974312.aspx).  
  
Die `-l` Option (Anmeldungstimeout) wurde um `bcp`. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit **Bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
  

