---
title: Systemanforderungen (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 53d9262fcac1329374393c6ee1275d9caf7ec688
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="system-requirements"></a>Systemanforderungen
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In diesem Thema werden die Anforderungen aufgelistet, die für die Verwendung von [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 (Vorschau) und 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] on Linux erforderlich sind


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13, 13.1 for SQL Server

Die Treiber für Linux und MacOS stehen nur für die 64-Bit-Versionen der folgenden Betriebssysteme:

|Betriebssystem|Unterstützte Treiberversion|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Apple MacOS 10.12 (Sierra)|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Apple MacOS 10,13 (hohe Sierra)|17| 
|Debian Linux 8|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Debian Linux 9|17|
|Red Hat Enterprise Linux|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Red Hat Enterprise Linux|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|SUSE Linux Enterprise Server|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17 <br /><br /> **Hinweis:** 17 der ODBC-Treiber unterstützt nur die SuSE Linux Enterprise Server 11 SP4|
|SUSE Linux Enterprise Server|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Ubuntu Linux 14.04|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Ubuntu Linux 15.10|13|
|Ubuntu Linux 16.04|%13, 13.1, 17 %2 %3 %4 %5 %6 %7 [%8]%9 %10 %11 %12 %13 %14 %15 %16 %17|
|Ubuntu Linux 16.10|13|
|Ubuntu Linux 17.10|17|

Die Installationspakete für die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber 13 13.1 und 17 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS der Treiber-Abhängigkeiten automatisch bei der Installation mithilfe der Paket-Verwaltungssystem Ihrer Verteilung, wie beschrieben in Auflösen[ Installieren des Treibers](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   64-Bit UnixODBC 2.3.0 Treiber-Manager, der für 64-Bit SQLLEN/SQLULEN erstellt wurde. Höhere Versionen des 64-Bit UnixODBC-Treiber-Managers werden nicht vom ODBC-Treiber unter Linux unterstützt. Weitere Informationen finden Sie unter [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) .  
  
-   Der ODBC-Treiber für  **Red Hat Enterprise Linux 5 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 (Preview) and 11 for SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   Der ODBC-Treiber für  **Red Hat Enterprise Linux 6 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 (Preview) and 11 for SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   Der ODBC-Treiber für **SUSE Linux Enterprise 11 Service Pack 2 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 and 11 Previews for SQL Server - SUSE Linux](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter
[Installieren des Treiber-Managers](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Bekannte Probleme in dieser Version des Treibers](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)  
