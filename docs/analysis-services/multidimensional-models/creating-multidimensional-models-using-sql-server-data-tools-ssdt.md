---
title: Erstellen mehrdimensionaler Modelle mit SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSAS, environments
- Analysis Services, development
- SQL Server Analysis Services, environments
- projects [Analysis Services]
- solutions [Analysis Services]
ms.assetid: 132ed779-3ec8-4734-9698-802116d1b017
caps.latest.revision: "63"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8069e4cb513ca83cd161564c6d9a0b2284890fdc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="creating-multidimensional-models-using-sql-server-data-tools-ssdt"></a>Erstellen mehrdimensionaler Modelle mit SQL Server-Datentools (SSDT)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt zwei verschiedene Umgebungen bereit, um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektmappen zu erstellen, bereitzustellen und zu verwalten: [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Beide Umgebungen implementieren ein Projektsystem. Weitere Informationen zu Visual Studio-Projekten finden Sie in der MSDN Library unter [Projekte als Container](http://go.microsoft.com/fwlink/?LinkId=63960) .  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ist eine auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2010 basierende Entwicklungsumgebung, mit der Business Intelligence-Lösungen erstellt und geändert werden können. Mithilfe von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekte erstellen, die Definitionen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekten enthalten (Cubes, Dimensionen usw.). Diese können in XML-Dateien gespeichert werden, die Elemente der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Skriptsprache (ASSL) enthalten. Diese Projekte sind in Projektmappen enthalten, die auch Projekte aus underen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]enthalten können. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekte als Teil einer Projektmappe entwickeln, die nicht von einer bestimmten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz abhängig ist. Sie können die Objekte während der Entwicklung zu Testzwecken für eine Instanz auf einem Testserver bereitstellen und anschließend dasselbe [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt verwenden, um Ihre Objekte für Instanzen auf mindestens einem Staging- oder Produktionsserver bereitzustellen. Die Projekte und Elemente in einer Projektmappe, die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] umfasst, können mit einem Quellcodeverwaltungssystem wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe integriert werden. Weitere Informationen zum Erstellen eines Projekts von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mithilfe von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]finden Sie unter [Erstellen eines Analysis Services-Projekts &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md). Sie können auch [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verwenden, um eine direkte Verbindung mit einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz herzustellen und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte zu erstellen und zu ändern, ohne ein Projekt zu verwenden und ohne Objektdefinitionen in XML-Dateien zu speichern. Weitere Informationen finden Sie unter [Mehrdimensionale Modelldatenbanken &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)und [Herstellen in Onlinemodus einer Verbindung mit einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist eine Management- und Verwaltungsumgebung, die in erster Linie zum Verwalten von Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]verwendet wird. Mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]können Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte verwalten (Sicherungen, Verarbeitungsvorgänge usw. ausführen) und außerdem mit XMLA-Skripts direkt neue Objekte für eine vorhandene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz erstellen. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] stellt ein Analysis Server-Skriptprojekt bereit, in dem Sie in Multidimensional Expressions (MDX), Data Mining Extensions (DMX) und XML for Analysis (XMLA) geschriebene Skripts entwickeln und speichern können. Normalerweise werden Analysis Server-Skriptprojekte verwendet, um Verwaltungsaufgaben auszuführen oder Objekte wie Datenbanken oder Cubes in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen neu zu erstellen. Solche Projekte können als Teil einer Lösung gespeichert werden und mit dem Quellcodeverwaltungssystem integriert werden. Weitere Informationen zum Erstellen einer Analysis Server-Skriptprojekts in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], finden Sie unter [Analysis Services-Skriptprojekt in SQL Server Management Studio](../../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="introducing-solutions-projects-and-items"></a>Einführung in Projektmappen, Projekte und Elemente  
 Sowohl [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] als auch [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] umfassen Projekte, die in Projektmappen organisiert sind. Eine Projektmappe kann viele Projekte enthalten. Ein Projekt wiederum umfasst eine Vielzahl von Elementen. Wenn Sie ein Projekt erstellen, wird automatisch eine neue Projektmappe erstellt. Außerdem können Sie einer vorhandenen Projektmappe ggf. weitere Projekte hinzufügen. Welche Objekte ein Projekt enthält, hängt vom Projekttyp ab. Die Elemente der einzelnen Projektcontainer werden in Projektordnern des Dateisystems als Dateien gespeichert.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] enthält die folgenden Projekte unter dem Projekttyp Business Intelligence-Projekte.  
  
|Projekt|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt|Enthält die Objektdefinitionen für eine einzelne [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank. Weitere Informationen zum Erstellen eines Projekts von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] finden Sie unter [Erstellen eines Analysis Services-Projekts &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md).|  
|Importieren der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2008-Datenbank|Stellt einen Assistenten bereit, mit dessen Hilfe Sie ein neues [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen können, indem Sie Objektdefinitionen aus einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank importieren.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Projekt|Enthält die Objektdefinitionen einer Gruppe von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. Weitere Informationen finden Sie unter [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).|  
|Berichtsprojekt-Assistent|Stellt einen Assistenten bereit, der Sie mithilfe von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]durch die Erstellung eines Berichtsprojekts führt. Weitere Informationen finden Sie unter [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Berichtsmodellprojekt|Enthält die Objektdefinitionen für ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsmodell. Weitere Informationen finden Sie unter [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Berichtsserverprojekt|Enthält die Objektdefinitionen für einen oder mehrere [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichte. Weitere Informationen finden Sie unter [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] umfasst einige Projekttypen, deren Schwerpunkt auf verschiedenen Abfragen oder Skripts liegt, wie in der folgenden Tabelle dargestellt.  
  
|Projekt|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Skripts|Enthält DMX-, MDX- und XMLA-Skripts für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]sowie Verbindungen zu [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen, gegen die Skripts ausgeführt werden können. Weitere Informationen finden Sie unter [Analysis Services-Skriptprojekt in SQL Server Management Studio](../../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).|  
|SQL Server Compact-Skripts|Enthält SQL-Skripts für SQL Server Compact sowie Verbindungen zu SQL Server Compact-Instanzen, für die diese Skripts ausgeführt werden können.|  
|SQL Server-Skripts|Enthält [!INCLUDE[tsql](../../includes/tsql-md.md)] - und XQuery-Skripts für eine [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz sowie Verbindungen zu [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanzen, gegen die diese Skripts ausgeführt werden können. Weitere Informationen finden Sie unter [SQL Server Database Engine](../../database-engine/configure-windows/sql-server-database-engine.md).|  
  
 Weitere Informationen zu Projektmappen und Projekten finden Sie in der Dokumentation zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET und in der MSDN Library unter "Verwalten von Projektmappen, Projekten und Dateien".  
  
## <a name="choosing-between-sql-server-management-studio-and-sql-server-data-tools"></a>Auswählen zwischen SQL Server Management Studio und SQL Server-Datentools  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist auf das Verwalten und Konfigurieren vorhandener Objekte in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ausgelegt. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ist auf die Entwicklung von Business Intelligence-Lösungen ausgelegt, die Funktionen aus [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]umfassen.  
  
 Im Folgenden sind einige der Unterschiede zwischen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aufgeführt.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] bietet eine integrierte Umgebung zum Herstellen von Verbindungen mit Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , um Objekte innerhalb einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz zu konfigurieren und zu verwalten. Durch die Verwendung von Skripts können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auch zum Erstellen oder Ändern von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekten verwenden; [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] bietet jedoch keine grafische Schnittstelle zum Entwurf und zur Definition von Objekten.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] bietet eine integrierte Entwicklungsumgebung zum Entwickeln von Business Intelligence-Lösungen. Sie können [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Projektmodus verwenden, in dem XML-basierte Definitionen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]- und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Objekten verwendet werden, die in Projekten und Projektmappen enthalten sind. Die Verwendung von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Projektmodus bedeutet, dass Änderungen an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekten in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] an diesen XML-basierten Objektdefinitionen erfolgen und erst dann direkt auf ein Objekt in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz angewendet werden, wenn die Projektmappe bereitgestellt wird. Sie können [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] auch im Onlinemodus verwenden; das bedeutet, dass eine direkte Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz hergestellt und mit Objekten in einer vorhandenen Datenbank gearbeitet wird.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verbessert die Entwicklung von Business Intelligence-Anwendungen, da Sie in einer quellcodeverwalteten Mehrbenutzerumgebung an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekten arbeiten können, ohne dass eine aktive Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz erforderlich ist. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] bietet direkten Zugriff auf vorhandene Objekte zum Abfragen und Testen und kann verwendet werden, um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken, für die zuvor ein Skript erstellt wurde, schneller zu implementieren. Nachdem ein Projekt in der Produktionsumgebung bereitgestellt wurde, ist bei der Arbeit mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank und ihren Objekten mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Vorsicht geboten. Es soll verhindert werden, dass Änderungen, die direkt an Objekten in einer vorhandenen Datenbank vorgenommen wurden, sowie Änderungen am [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt, das die bereitgestellte Projektmappe ursprünglich generiert hat, überschrieben werden. Weitere Informationen finden Sie unter [Arbeiten mit Analysis Services-Projekten und -Datenbanken während der Entwicklungsphase](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)und [Verwenden von Analysis Services-Projekten und -Datenbanken in einer Produktionsumgebung](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-production.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Erstellen eines Analysis Services-Projekts &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
-   [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
-   [Erstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
-   [Bereitstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
-   [Arbeiten mit Analysis Services-Projekten und -Datenbanken während der Entwicklungsphase](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)  
  
-   [Verwenden von Analysis Services-Projekten und -Datenbanken in einer Produktionsumgebung](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-production.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Analysis Services-Projekts &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Analysis Services-Skriptprojekt in SQL Server Management Studio](../../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md)   
 [Mehrdimensionale Modelldatenbanken &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
