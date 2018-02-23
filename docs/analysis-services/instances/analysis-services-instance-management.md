---
title: Analysis Services Server Management | Microsoft Docs
ms.custom: 
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 65dbe6b6f19342db449af8c0736743d9a73000d7
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="analysis-services-server-management"></a>Analysis Services-Server-Verwaltung

  Eine Serverinstanz von Analysis Services ist eine Kopie der **msmdsrv.exe** ausführbare Datei, die als Betriebssystemdienst ausgeführt wird. Jede Instanz ist völlig unabhängig von anderen Instanzen auf dem gleichen Server. Sie hat ihre eigenen Konfigurationseinstellungen, Berechtigungen, Anschlüsse, Startkonten, Dateispeicher und Servermoduseigenschaften.  
  
 Jede Instanz wird als Windows-Dienst Msmdsrv.exe im Sicherheitskontext eines definierten Anmeldekontos ausgeführt.  
  
-   Der Dienstname der Standardinstanz lautet MSSQLServerOLAPService.  
  
-   Der Dienstname der einzelnen benannten Instanzen von lautet MSOLAP$ InstanceName.  
  
> [!NOTE]  
>  Wenn mehrere Instanzen installiert sind, installiert Setup auch einen Redirectordienst, der integriert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst. Der Redirectordienst ist für das Umleiten von Clients an die entsprechende benannte Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zuständig. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst wird immer im Sicherheitskontext des lokalen Dienstkontos ausgeführt, ein Standardbenutzerkonto, das Windows für Systemdienste verwendet, die nicht auf Ressourcen außerhalb des lokalen Computers zugreifen.  
  
 Mehrere Instanzen bedeuten, dass Sie skalieren können, indem Sie mehrere Serverinstanzen auf der gleichen Hardware installieren. Besonders für Analysis Services bedeutet dies auch, dass Sie verschiedene Servermodi unterstützen können, indem Sie mehrere Instanzen auf dem gleichen Server haben, von denen jede für die Ausführung in einem bestimmten Modus konfiguriert ist.  
  
 Der Servermodus ist eine Servereigenschaft, die bestimmt, welche Speicher- und Arbeitsspeicherarchitektur für diese Instanz verwendet wird. Ein Server, der im mehrdimensionalen Modus ausgeführt wird, verwendet die Ressourcenmanagementebene, die für mehrdimensionale Cubedatenbanken und Data Mining-Modelle erstellt wurde. Im Gegensatz dazu werden im tabellarischen Servermodus mithilfe des VertiPaq-Moduls für Datenanalyse im Arbeitsspeicher und der Datenkomprimierung wie angefordert Daten aggregiert.  
  
 Unterschiede in der Speicher- und Arbeitsspeicherarchitektur bedeuten, dass eine einzelne Instanz von Analysis Services entweder Tabellendatenbanken oder mehrdimensionale Datenbanken ausführt, aber nicht beide. Die Servermoduseigenschaft bestimmt, welcher Datenbanktyp auf der Instanz ausgeführt wird.  
  
 Der Servermodus wird während der Installation festgelegt, wenn Sie den Datenbanktyp angeben, der auf dem Server ausgeführt wird. Um alle verfügbaren Modi zu unterstützen, können Sie mehrere Instanzen von Analysis Services installieren und jeweils in einem Servermodus bereitstellen, der den von Ihnen erstellten Projekten entspricht.  
  
 Im Allgemeinen sind die meisten administrativen Aufgaben, die Sie ausführen müssen, in den einzelnen Modi dieselben. Als Analysis Services-Systemadministrator können Sie unabhängig von der Installationsart die gleichen Prozeduren und Skripte für das Verwalten aller Analysis Services-Instanzen im Netzwerk verwenden.  
  
> [!NOTE]  
>  Eine Ausnahme hiervon stellt [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint dar. Die Serververwaltung einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Bereitstellung findet immer innerhalb des Kontexts einer SharePoint-Farm statt. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] unterscheidet sich von anderen Servermodi darin, dass es sich immer um eine Einzelinstanz handelt, die immer über die SharePoint-Zentraladministration oder das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool verwaltet wird. Obwohl es möglich ist, in SQL Server Management Studio oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] eine Verbindung mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]für SharePoint in SQL Server herzustellen, ist dies nicht zu empfehlen. Eine SharePoint-Farm enthält Infrastrukturen, die den Serverstatus synchronisieren und die Serververfügbarkeit überwachen. Die Verwendung anderer Tools kann diese Vorgänge beeinträchtigen. Weitere Informationen zu [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Server-Verwaltung finden Sie unter [Power Pivot für SharePoint ](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Link|Taskbeschreibung|  
|----------|----------------------|  
|[Konfiguration nach der Installation](../../analysis-services/instances/post-install-configuration-analysis-services.md)|Beschreibt die erforderlichen und optionalen Aufgaben, durch die eine Analysis Services-Installation abgeschlossen oder geändert wird.|  
|[Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)|Beschreibt Verbindungszeichenfolgen-Eigenschaften, Clientbibliotheken, Authentifizierungsmethoden und Schritte zum Herstellen oder Löschen von Verbindungen.|  
|[Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)|Beschreibt Tools und Techniken zum Überwachen einer Serverinstanz, einschließlich der Verwendung von Systemmonitor und SQL Server Profiler.|  
|[Hohe Verfügbarkeit und Skalierbarkeit](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)|Beschreibt die am häufigsten verwendeten Techniken, um Analysis Services-Datenbanken hoch verfügbar und skalierbar zu machen. |  
|[Globalisierungsszenarien für Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)|Erläutert die Unterstützung von Sprache und Sortierung, die Schritte zum Ändern der Eigenschaften und Tipps zum Festlegen und Testen von Sprache und Sortierungsverhalten.|  
|[Protokollvorgänge in Analysis Services](../../analysis-services/instances/log-operations-in-analysis-services.md)|Beschreibt die Protokolle und erklärt, wie Sie diese konfigurieren.|  
  
  
## <a name="see-also"></a>Siehe auch  
 [Vergleichen von tabellarischen und mehrdimensionalen Lösungen ](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
