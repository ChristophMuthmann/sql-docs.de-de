---
title: "Installation f&#252;r SQLServer 2016 | Microsoft Docs"
ms.custom: ""
ms.date: "04/13/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.portal.Installation.f1"
helpviewer_keywords: 
  - "Installieren von SQL Server, Erstinstallation"
  - "Installation [SQL Server]"
  - "Erstinstallation [SQL Server]"
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 34
---
# Installation f&#252;r SQLServer 2016
  Der Installations-Assistent für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält eine einzelne Funktionsstruktur für die Installation aller [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   Konnektivitätskomponenten  
  
 Ab SQL Server 2016 werden die SQL Server-Verwaltungstools nicht mehr aus der Hauptfunktionsstruktur installiert. Weitere Informationen finden Sie unter [Installieren von SQL Server-Verwaltungstools mit SSMS](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md).  
  
 Sie können jede Komponente einzeln installieren oder eine Kombination der oben aufgelisteten Komponenten auswählen. Informationen, die Ihnen beim Treffen der bestmöglichen Auswahl in Bezug auf die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbaren Editionen und Komponenten helfen, finden Sie unter [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) und [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
## In diesem Abschnitt  
 Unabhängig davon, ob Sie die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder über die Eingabeaufforderung vornehmen, umfasst das Setup immer folgende Schritte:  
  
 [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)  
 Beschreibt, wie der Computer auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorbereitet wird:  
  
-   Hardware- und Softwareanforderungen  
  
-   Anforderungen für die Systemkonfigurationsprüfung sowie Blockadefaktoren.  
  
-   Überlegungen zur Sicherheit.  
  
 [Installieren von SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)  
 Beschreibt Installationsoptionen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Informationen zur Benutzeroberfläche des SQL Server-Setups](../Topic/SQL%20Server%20Setup%20User%20Interface%20Reference.md)  
 Beschreibt die Installationsoptionen, die vom Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geboten werden.  
  
 [Aktualisieren auf SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)  
 Beschreibt Optionen zum Aktualisieren auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Deinstallieren von SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)  
 Beschreibt Verfahren zum Deinstallieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
 [SQL Server-Failoverclusterinstallation](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In diesem Abschnitt der Dokumentation zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup wird die Installation und Konfiguration von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclustern beschrieben.  
  
 [Installieren von SQL Server 2016 Business Intelligence-Funktionen](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funktionen, die Teil der Microsoft BI-Plattform darstellen, sind [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sowie mehrere Clientanwendungen, die zum Erstellen von oder Arbeiten mit analytischen Daten verwendet werden. In diesem Abschnitt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setupdokumentation wird erläutert, wie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installiert werden.  
  
## Weitere Informationen  
 [Installieren der BI-Funktionen von SQL Server mit SharePoint &#40;Power Pivot und Reporting Services&#41;](../Topic/Install%20SQL%20Server%20BI%20Features%20with%20SharePoint%20\(Power%20Pivot%20and%20Reporting%20Services\).md)  
 In diesem Abschnitt wird erläutert, wie Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen in einer SharePoint-Umgebung installieren. Es wird angegeben, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen für eine bestimmte Version oder Edition von SharePoint verfügbar sind. Außerdem umfasst der Abschnitt Installationsschritte für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint und Reporting Services im SharePoint-Modus.  
  
 ![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Installieren der neuen Beispieldatenbank, [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx). 
  
 [Zusätzliche SQL Server-Beispiele und -Beispieldatenbanken](http://sqlserversamples.codeplex.com/)  
 Beschreibt, wie Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Beispiele und -Beispieldatenbanken installieren und konfigurieren.  
  
Links und Informationen für alle unterstützten Versionen von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] finden Sie im [SQL Server-Update Center](https://msdn.microsoft.com/library/ff803383.aspx).  
  
## Siehe auch  
 [Neuigkeiten in der SQL Server-Installation](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)  
  
  