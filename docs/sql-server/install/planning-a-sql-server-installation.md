---
title: Planen einer SQL Server-Installation | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 03/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 72117bfd62b37633e2b815fb1c8014b48c63d2ab
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="planning-a-sql-server-installation"></a>Planen einer SQL Server-Installation
  Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu installieren, führen Sie folgende Schritte aus:  
  
-   Überprüfen Sie die Installationsanforderungen, Systemkonfigurationsprüfungen und Sicherheitsaspekte für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation.  
  
-   Führen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup aus, um eine höhere Version zu installieren bzw. darauf zu aktualisieren. Lesen Sie vor dem Upgrade [Upgrade to SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md).  
  
-   Verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramme, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu konfigurieren.  
  
 Unabhängig von der Installationsmethode ist es erforderlich, dass Sie den Softwarelizenzbedingungen als Einzelperson oder im Auftrag einer juristischen Person zustimmen, sofern die Verwendung der Software in keiner separaten Vereinbarung geregelt ist, z. B. einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Volumenlizenzvertrag oder einem Vertrag eines Drittanbieters mit einem ISV oder OEM.  
  
 Die Lizenzbedingungen werden in der Setup-Benutzeroberfläche angezeigt, damit Sie diese lesen und akzeptieren können. Unbeaufsichtigte Installationen (mit dem /Q-Parameter oder /QS-Parameter) müssen den /IAcceptSQLServerLicenseTerms-Parameter enthalten. Sie können die Lizenzbedingungen unter [Microsoft-Software-Lizenzbedingungen](http://go.microsoft.com/fwlink/?LinkID=148209)in einer separaten Kopie lesen.  
  
> [!NOTE]  
>  Abhängig davon, wie Sie die Software erworben haben (z. B. durch [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Volumenlizenzierung), unterliegt die Verwendung der Software möglicherweise zusätzlichen Bestimmungen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Neuigkeiten in der SQL Server-Installation](../../sql-server/install/what-s-new-in-sql-server-installation.md)  
 In diesem Thema werden die Details zu den neuen oder verbesserten Installationsfunktionen in dieser Version von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]beschrieben.  
  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
 In diesem Thema sind die Mindestanforderungen an die Hardware und Software aufgeführt, um eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zu installieren und auszuführen.  
  
 [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 In diesem Thema werden einige bewährte Sicherheitsmethoden beschrieben, die Sie vor dem Installieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und nach dem Installieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]berücksichtigen sollten.  
  
 [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 In diesem Thema werden die Standardkonfiguration von Diensten in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]und die Konfigurationsoptionen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste beschrieben, die Sie während und nach der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation festlegen können.  
  
 [Netzwerkprotokolle und Netzwerkbibliotheken](../../sql-server/install/network-protocols-and-network-libraries.md)  
 In diesem Thema werden die Standardkonfiguration von Netzwerkprotokollen in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]und die verfügbaren Konfigurationsoptionen beschrieben.  
  
 [Verwenden mehrerer Versionen und Instanzen von SQL Server](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 In diesem Thema werden die Überlegungen zum Installieren mehrerer Versionen und Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]beschrieben.  
  
 [Lokale Sprachversionen in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md)  
 In diesem Thema werden die lokalisierten Versionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]erläutert.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Installieren von SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
 Dieser Abschnitt bietet eine Übersicht über andere Installationsoptionen, die zur Installation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zur Verfügung stehen.  
  
 [Installieren von SQL Server 2016 Business Intelligence-Funktionen](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 In diesem Abschnitt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setupdokumentation wird erläutert, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen, die Teil der Microsoft BI-Plattform sind, installiert werden.  
  
 [Upgrade to SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)  
 Der Abschnitt bietet eine Übersicht über das Aktualisieren von Instanzen früherer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Deinstallieren von SQL Server 2016](../../sql-server/install/uninstall-sql-server.md)  
 Lesen Sie diesen Abschnitt, wenn Sie eine vorhandene Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] vollständig deinstallieren und das System für die Neuinstallation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]vorbereiten möchten.  
  
 [SQL Server-Failoverclusterinstallation](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In diesem Abschnitt der Dokumentation zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup wird die Installation und Konfiguration von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclustern beschrieben.  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Lösungen mit hoher Verfügbarkeit &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Vor dem Installieren des Failoverclusterings](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [Aktualisieren auf SQL Server 2016 mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

