---
title: "Systemanforderungen für | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 75c8c9daea3f26dc694ae66597649f399a986456
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="system-requirements"></a>Systemanforderungen
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Dieses Thema listet die Anforderungen der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS.

## <a name="microsoft-odbc-driver-13-and-131-for-sql-server"></a>Microsoft ODBC Driver 13 und 13.1 for SQLServer

Die Treiber für Linux und MacOS stehen nur für die 64-Bit-Versionen der folgenden Betriebssysteme:

- Apple MacOS 10.12 (Sierra)
- Apple OS X 10.11 (El Capitan)
- Debian Linux 8
- Red Hat Enterprise Linux 6
- Red Hat Enterprise Linux 7
- SuSE Linux Enterprise Server 11
- SuSE Linux Enterprise Server 12
- Ubuntu Linux 14.04
- Ubuntu Linux 15.10
- Ubuntu Linux 16.04
- Ubuntu Linux 16.10

Die Installationspakete für die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 and 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS Auflösen des Treibers Abhängigkeiten automatisch bei der Installation mithilfe der Paket-Verwaltungssystem Ihrer Verteilung, wie beschrieben in [Installieren des Treibers](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 for SQL Server  
  
-   64-Bit UnixODBC 2.3.0 Treiber-Manager, der für 64-Bit SQLLEN/SQLULEN erstellt wurde. Höhere Versionen des 64-Bit UnixODBC-Treiber-Managers werden nicht vom ODBC-Treiber unter Linux unterstützt. Weitere Informationen finden Sie unter [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) .  
  
-   ODBC-Treiber für **Red Hat Enterprise Linux 5 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   e2fsprogs-libs  
    -   krb5-libs  
    -   openssl  
  
-   ODBC-Treiber für **Red Hat Enterprise Linux 6 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   libuuid  
    -   krb5-libs  
    -   openssl  
  
-   ODBC-Treiber für **SUSE Linux Enterprise 11 Service Pack 2 (64-Bit)** erfordert die folgenden Pakete und kann hier heruntergeladen werden: [Microsoft ODBC Driver 11-Vorschau für SQL Server - SUSE Linux](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   glibc  
    -   libstdc++46  
    -   libgcc46  
    -   libuuid1  
    -   krb5  
    -   libopenssl0_9_8  
  
## <a name="see-also"></a>Siehe auch
[Installieren des Treiber-Managers](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Bekannte Probleme in dieser Version des Treibers](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)  

