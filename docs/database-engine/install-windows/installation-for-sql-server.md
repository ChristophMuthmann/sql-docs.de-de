---
title: "Installation für SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f3053d9238af0112dfb41be2eb0f2972f24a34ce
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="installation-for-sql-server"></a>Installation für SQL Server

Der Installations-Assistent für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält eine einzelne Funktionsstruktur für die Installation aller [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   Konnektivitätskomponenten  
  
Ab [!INCLUDE[ss2016](../../includes/sssql15-md.md)] werden die SQL Server-Verwaltungstools nicht mehr aus der Hauptfunktionsstruktur installiert. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md).  
  
Sie können jede Komponente einzeln installieren oder eine Kombination der oben aufgelisteten Komponenten auswählen. Informationen, die Ihnen beim Treffen der bestmöglichen Auswahl in Bezug auf die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbaren Editionen und Komponenten helfen, finden Sie in den von Ihrer Version von SQL Server unterstützten Funktionen:

- [Editionen und unterstützte Funktionen von [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md)  
- [Editionen und unterstützte Funktionen von [!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md)  
- [Von den SQL Server 2016-Editionen unterstützte Funktionen[!INCLUDE[ss2014](../../includes/sssql14-md.md)]](http://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>In diesem Abschnitt  
Unabhängig davon, ob Sie die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oder über die Eingabeaufforderung vornehmen, umfasst das Setup immer folgende Schritte:  
  
[Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)  
Beschreibt, wie der Computer auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]vorbereitet wird:  
  
-   Hardware- und Softwareanforderungen  
-   Anforderungen für die Systemkonfigurationsprüfung sowie Blockadefaktoren.  
-   Überlegungen zur Sicherheit.  
  
[Installieren von SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 Beschreibt Installationsoptionen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Informationen zur Benutzeroberfläche des SQL Server-Setups](http://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 Beschreibt die Installationsoptionen, die vom Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geboten werden.  
  
[Aktualisieren von SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 Beschreibt Optionen zum Aktualisieren auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Deinstallieren von SQL Server](../../sql-server/install/uninstall-sql-server.md)  
 Beschreibt Verfahren zum Deinstallieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
[SQL Server-Failoverclusterinstallation](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In diesem Abschnitt der Dokumentation zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup wird die Installation und Konfiguration von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclustern beschrieben.  
  
[Installieren von SQL Server Business Intelligence-Funktionen](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funktionen, die Teil der Microsoft BI-Plattform darstellen, sind [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]sowie mehrere Clientanwendungen, die zum Erstellen von oder Arbeiten mit analytischen Daten verwendet werden. In diesem Abschnitt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setupdokumentation wird erläutert, wie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]installiert werden.  
  
## <a name="more-information"></a>Weitere Informationen
[Installieren der BI-Funktionen von SQL Server mit SharePoint &#40;Power Pivot und Reporting Services&#41;](http://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 In diesem Abschnitt wird erläutert, wie Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen in einer SharePoint-Umgebung installieren. Es wird angegeben, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen für eine bestimmte Version oder Edition von SharePoint verfügbar sind. Außerdem umfasst der Abschnitt Installationsschritte für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint und Reporting Services im SharePoint-Modus.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Installieren der neuen Beispieldatenbank, [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx). 
  
[Zusätzliche SQL Server-Beispiele und -Beispieldatenbanken](http://sqlserversamples.codeplex.com/)  
 Beschreibt, wie Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Beispiele und -Beispieldatenbanken installieren und konfigurieren.  
  
Links und Informationen für alle unterstützten Versionen von [finden Sie im](https://msdn.microsoft.com/library/ff803383.aspx) SQL Server-Update Center [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
[Neuigkeiten in der SQL Server-Installation](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[Hardware- und Softwareanforderungen für die Installation von SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
