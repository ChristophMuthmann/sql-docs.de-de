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
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb3ccdb0348cc05146bdadbccb8ce26d733cea79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements"></a>Systemanforderungen
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Dieses Thema listet die Anforderungen der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13 13.1 und 17 für SQLServer

Die Treiber für Linux und MacOS stehen nur für die 64-Bit-Versionen der folgenden Betriebssysteme:

|Betriebssystem|Unterstützte Treiberversion|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|13, 13.1, 17|
|Apple MacOS 10.12 (Sierra)|13, 13.1, 17|
|Apple MacOS 10,13 (hohe Sierra)|17| 
|Debian Linux 8|13, 13.1, 17|
|Debian Linux 9|17|
|Red Hat Enterprise Linux 6|13, 13.1, 17|
|Red Hat Enterprise Linux 7|13, 13.1, 17|
|SuSE Linux Enterprise Server 11|13, 13.1, 17 <br /><br /> **Hinweis:** 17 der ODBC-Treiber unterstützt nur die SuSE Linux Enterprise Server 11 SP4|
|SuSE Linux Enterprise Server 12|13, 13.1, 17|
|Ubuntu Linux 14.04|13, 13.1, 17|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17|
|Ubuntu Linux 16.10|13, 13.1|
|Ubuntu Linux 17.10|17|

Die Installationspakete für die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber 13 13.1 und 17 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS der Treiber-Abhängigkeiten automatisch bei der Installation mithilfe der Paket-Verwaltungssystem Ihrer Verteilung, wie beschrieben in Auflösen[ Installieren des Treibers](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   64-Bit UnixODBC 2.3.0 Treiber-Manager, der für 64-Bit SQLLEN/SQLULEN erstellt wurde. Höhere Versionen des 64-Bit UnixODBC-Treiber-Managers werden nicht vom ODBC-Treiber unter Linux unterstützt. Weitere Informationen finden Sie unter [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) .  
  
-   ODBC-Treiber für **Red Hat Enterprise Linux 5 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   ODBC-Treiber für **Red Hat Enterprise Linux 6 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   ODBC-Treiber für **SUSE Linux Enterprise 11 Service Pack 2 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11-Vorschau für SQL Server - SUSE Linux](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Siehe auch
[Installieren des Treiber-Managers](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Bekannte Probleme in dieser Version des Treibers](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Anmerkungen zu dieser Version](../../../connect/odbc/linux-mac/release-notes.md)  
