---
title: Installieren von SQL Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ccbcbc7c58b940a5438cf5ff2c42d8da8da89ec5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="install-sql-server"></a>Installieren von SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 > Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Installieren von SQL Server 2014](https://msdn.microsoft.com/library/bb500395(SQL.120).aspx).

 Ab [!INCLUDE[sssql15](../../includes/sssql15-md.md)] ist [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] nur noch als 64-Bit-Anwendung verfügbar. Hier erhalten Sie wichtige Informationen zum Erhalt und zur Installation von SQL Server.

## <a name="installation-details"></a>Installationsdetails
  
*  **Optionen**: Installation mithilfe des Installations-Assistenten, einer Eingabeaufforderung oder mithilfe von SysPrep
 
*  **Anforderungen**: Nehmen Sie sich vor der Installation etwas Zeit, um die Installationsanforderungen, die Überprüfung der Systemkonfiguration und die Sicherheitsaspekte in [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Vorgehensweise**: Umfassende Anweisungen zum Installationsvorgang finden Sie unter [Installation für SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md)

* **Beispieldatenbanken und Beispielcode**: 
    * Sie sind standardmäßig nicht als Teil der SQL Server-Installation installiert. 
    * Um diese für SQL Server-Editionen außer Express Edition zu installieren, gehen Sie auf die [GitHub](http://github.com/Microsoft/sql-server-samples).
    

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]
 
|Titel|Description|  
|-----------|-----------------|  
|[Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] in Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Lesen Sie diesen Artikel, wenn Sie [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] unter Windows Server Core installieren möchten.|  
|[Überprüfen der Parameter für die Systemkonfigurationsprüfung](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Erläutert die Funktion der Systemkonfigurationsprüfung (System Configuration Checker, SCC).|  
|[Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] mit dem Installations-Assistenten (Setup)](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Artikel mit Anleitungen für eine typische [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation mit dem Installations-Assistenten.|  
|[Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Artikel mit Anleitungen, der Beispielsyntax und Installationsparameter zum Ausführen eines unbeaufsichtigten Setups bereitstellt.|  
|[Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] mithilfe einer Konfigurationsdatei](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Artikel mit Anleitungen, der Beispielsyntax und Installationsparameter zum Ausführen des Setups mithilfe einer Konfigurationsdatei bereitstellt.|  
|[Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] mit SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Artikel mit Anleitungen, der Beispielsyntax und Installationsparameter zum Ausführen des Setups mithilfe von SysPrep bereitstellt.|  
|[Hinzufügen von Funktionen in einer Instanz von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] (Setup)](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Artikel mit Anleitungen zum Aktualisieren von Komponenten einer vorhandenen [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]-Instanz.|  
|[Korrigieren einer fehlgeschlagenen Installation von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Artikel mit Anleitungen zum Reparieren einer fehlerhaften [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]-Installation.|  
|[Umbenennen eines Computers, der eine eigenständige Instanz von SQL Server hostet](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Artikel mit Anleitungen zur Aktualisierung von Systemmetadaten, die in sys.servers gespeichert sind.|  
|[Installieren von ](../../database-engine/install-windows/install-sql-server-servicing-updates.md)-Wartungsupdates[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]|Artikel mit Anleitungen zur Installation von Updates für [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Artikel mit Anleitungen zur Überprüfung von Fehlern in Setupprotokolldateien.|  
|[Überprüfen einer SQL Server-Installation](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Informieren Sie sich darüber, wie Sie mithilfe des SQL-Ermittlungsberichts die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version sowie die auf dem Computer installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen überprüfen.|  
  
  
## <a name="how-to-install-individual-components"></a>So installieren Sie einzelne Komponenten  
  
|Thema|Description|  
|-----------|-----------------|  
|[Installieren des SQL Server-Datenbankmoduls](../../database-engine/install-windows/install-sql-server-database-engine.md)|Beschreibt, wie Sie [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]installieren und konfigurieren.|  
|[Installieren der SQL Server-Replikation](../../database-engine/install-windows/install-sql-server-replication.md)|Beschreibt, wie Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation installieren und konfigurieren.|  
|[Installieren von Distributed Replay – Übersicht](../../tools/distributed-replay/install-distributed-replay-overview.md)|Enthält eine Auflistung der Artikel zur Installation der Distributed Replay-Funktion.|  
|[Installieren von SQL Server-Verwaltungstools mit SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|Beschreibt, wie Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verwaltungstools installieren und konfigurieren.|  
|[Installieren von SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Beschreibt die Überlegungen zum Installieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Komponenten.|  
  

## <a name="how-to-configure-sql-server"></a>So konfigurieren Sie SQL Server  
  
|Thema|Description|  
|-----------|-----------------|  
|[Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Dieser Artikel bietet eine Übersicht über die Konfiguration von Firewalls und sowie Anleitungen zum Konfigurieren der Windows-Firewall.|  
|[Konfigurieren eines mehrfach vernetzten Computers für SQL Server-Zugriff](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|Dieser Artikel beschreibt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und die Windows-Firewall mit erweiterter Sicherheit konfiguriert werden, um Netzwerkverbindungen zu einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer mehrfach vernetzten Umgebung bereitzustellen.|  
|[Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Sie können die in diesem Artikel beschriebenen Schritte zur Konfiguration von Port- und Firewalleinstellungen ausführen, um den Zugriff auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint zuzulassen.|  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
[Editionen und unterstützte Funktionen von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[Installation von Business Intelligence-Funktionen von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [SQL Server-Failoverclusterinstallation](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Siehe auch  

[Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Upgrade auf [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Deinstallieren von[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [Lösungen mit hoher Verfügbarkeit &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
