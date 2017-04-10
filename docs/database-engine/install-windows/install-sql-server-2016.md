---
title: "Installieren von SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "AdventureWorks-Beispieldatenbank"
  - "Installieren von SQL Server, Vorbereiten der Installation"
  - "Installation [SQL Server]"
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
ms.author: "mikeray"
manager: "jhubbard"
---
# Installieren von SQL Server 2016
  SQL Server 2016 ist eine 64-Bit-Anwendung. Hier erhalten Sie wichtige Informationen zum Erhalt und zur Installation von SQL Server.

## <a name="installation-details"></a>Installationsdetails
  
*  **Optionen**: Installation mithilfe des Installations-Assistenten, einer Eingabeaufforderung oder mithilfe von SysPrep
 
*  **Anforderungen**: Nehmen Sie sich vor der Installation etwas Zeit, um die Installationsanforderungen, die Überprüfung der Systemkonfiguration und die Sicherheitsaspekte in [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md) durchzuarbeiten 

* **Vorgehensweise**: Umfassende Anweisungen zum Installationsvorgang finden Sie unter [Installation für SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md)

* **Beispieldatenbanken und Beispielcode**: 
    * Sie sind standardmäßig nicht als Teil der SQL Server-Installation installiert. 
    * Um diese für SQL Server-Editionen außer Express Edition zu installieren, gehen Sie auf die [CodePlex-Website](http://go.microsoft.com/fwlink/?LinkId=87843).
    * Supportinformationen zu SQL Server-Beispieldatenbanken und Beispielcode für SQL Server Express finden Sie unter [Databases and Samples Overview (in englischer Sprache)](http://go.microsoft.com/fwlink/?LinkId=110391).
    

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

Der Downloadspeicherort für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ist abhängig von der Edition.

- **SQL Server Enterprise-, Standard- und Express-Editionen** werden für die Verwendung in einer Produktionsumgebung lizenziert. Wenden Sie sich für die Installation von Medien für Enterprise- und Standard-Editionen an Ihren Softwareanbieter. Einkaufsinformationen und ein Verzeichnis mit Microsoft-Partner finden Sie auf der [Einkaufswebsite von Microsoft](https://www.microsoft.com/en-us/server-cloud/products/sql-server/overview.aspx). 

- **Kostenlose Editionen** sind unter den folgenden Links verfügbar:

| Edition | Description
|---------|--------
|[Developer Edition](http://myprodscussu1.app.vssubscriptions.visualstudio.com/Downloads?q=SQL%20Server%20Developer) | Kostenloser, voll funktionsfähiger Satz der SQL Server 2016 Enterprise Edition-Software, die Entwicklern das Erstellen, Testen und Demonstrieren von Anwendungen in einer Nichtproduktionsumgebung ermöglicht. 
|[Express Edition](http://www.microsoft.com/download/details.aspx?id=52679)|  Eine kostenlose Datenbank für den Einstieg, die ideal für das Bereitstellen kleiner Datenbanken in Produktionsumgebungen ist. Erstellen Sie Desktops, kleine Server und datengesteuerte Anwendungen bis zu einer Datenträgergröße von 10 GB. 
| [Evaluation Edition](http://technet.microsoft.com/evalcenter/mt130694) | Vollständige Funktionsgruppe der SQL Server Enterprise Edition-Software mit einem Evaluierungszeitraum von 180 Tagen.
   
 
  

## <a name="how-to-install-sql-server"></a>So installieren Sie SQL Server
 
|Title|Description|  
|-----------|-----------------|  
|[Installieren von SQL Server 2016 unter Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md)|Lesen Sie dieses Thema, wenn Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unter Windows Server Core installieren möchten.|  
|[Überprüfen der Parameter für die Systemkonfigurationsprüfung](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Erläutert die Funktion der Systemkonfigurationsprüfung (System Configuration Checker, SCC).|  
|[Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)|Thema mit Anleitungen für eine typische [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation mit dem Installations-Assistenten.|  
|[Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Thema mit Anleitungen, das Beispielsyntax und Installationsparameter zum Ausführen eines unbeaufsichtigten Setups bereitstellt.|  
|[Installieren von SQL Server 2016 mithilfe einer Konfigurationsdatei](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Thema mit Anleitungen, das Beispielsyntax und Installationsparameter zum Ausführen einer unbeaufsichtigten Installation mithilfe einer Konfigurationsdatei bereitstellt.|  
|[Installieren von SQL Server 2016 mit SysPrep](../../database-engine/install-windows/install-sql-server-2016-using-sysprep.md)|Thema mit Anleitungen, das Beispielsyntax und Installationsparameter zum Ausführen des Setups mithilfe von SysPrep bereitstellt.|  
|[Hinzufügen von Funktionen zu einer Instanz von SQL Server 2016 &#40;Setup&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Thema mit Anleitungen zum Update von Komponenten einer vorhandenen Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|[Reparieren von Fehlern bei einer SQL Server 2016-Installation](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)|Thema mit Anleitungen zum Reparieren einer fehlerhaften [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Installation.|  
|[Umbenennen eines Computers, der eine eigenständige Instanz von SQL Server hostet](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Thema mit Anleitungen zur Aktualisierung von Systemmetadaten, die in sys.servers gespeichert werden.|  
|[Installieren von SQL Server 2016-Wartungsupdates](../../database-engine/install-windows/install-sql-server-2016-servicing-updates.md)|Thema mit Anleitungen zur Installation von Updates für SQL Server 2016.|  
|[Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Thema mit Anleitungen zur Überprüfung von Fehlern in Setupprotokolldateien.|  
|[Überprüfen einer SQL Server-Installation](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Informieren Sie sich darüber, wie Sie mithilfe des SQL-Ermittlungsberichts die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version sowie die auf dem Computer installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen überprüfen.|  
  
  
## <a name="how-to-install-individual-components"></a>So installieren Sie einzelne Komponenten  
  
|Thema|Description|  
|-----------|-----------------|  
|[Installieren des SQL Server-Datenbankmoduls](../../database-engine/install-windows/install-sql-server-database-engine.md)|Beschreibt, wie Sie [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] installieren und konfigurieren.|  
|[Installieren der SQL Server-Replikation](../../database-engine/install-windows/install-sql-server-replication.md)|Beschreibt, wie Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation installieren und konfigurieren.|  
|[Installieren von Distributed Replay – Übersicht](../../tools/distributed-replay/install-distributed-replay-overview.md)|Enthält eine Auflistung der Themen zur Installation der Distributed Replay-Funktion.|  
|[Installieren von SQL Server-Verwaltungstools mit SSMS](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md)|Beschreibt, wie Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verwaltungstools installieren und konfigurieren.|  
|[Installieren von SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Beschreibt die Überlegungen zum Installieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Komponenten.|  
  

## <a name="how-to-configure-sql-server"></a>So konfigurieren Sie SQL Server  
  
|Thema|Description|  
|-----------|-----------------|  
|[Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|Dieses Thema bietet einen Überblick über die Firewallkonfiguration und wie Windows-Firewall konfiguriert wird.|  
|[Konfigurieren eines mehrfach vernetzten Computers für SQL Server-Zugriff](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|In diesem Thema wird beschrieben, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Windows-Firewall mit erweiterter Sicherheit konfiguriert werden, um Netzwerkverbindungen zu einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer mehrfach vernetzten Umgebung bereitzustellen.|  
|[Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Sie können die in diesem Thema beschriebenen Schritte zur Konfiguration von Port- und Firewalleinstellungen ausführen, um den Zugriff auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint zuzulassen.|  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
[Von der SQL Server 2016-Edition unterstützte Funktionen](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
[Installieren von SQL Server 2016 Business Intelligence-Funktionen](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
  [SQL Server-Failoverclusterinstallation](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Siehe auch  

[Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Aktualisieren auf SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Deinstallieren von SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)   
 [Lösungen mit hoher Verfügbarkeit &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  