---
title: "Verwaltung von Datamining-Lösungen und-Objekten | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], managing
- managing mining models
ms.assetid: 06fc61dd-925c-4347-8677-7046ee5d2f6f
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4154a0e542ed8e2bc6799dbc3f3c9ecb25ad5f4e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="management-of-data-mining-solutions-and-objects"></a>Verwaltung von Data Mining-Lösungen und -Objekten
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] stellt Clienttools bereit, mit denen Sie vorhandene Miningstrukturen und Miningmodelle verwalten können. In diesem Abschnitt werden die Verwaltungsvorgänge beschrieben, die Sie mit der jeweiligen Umgebung ausführen können.  
  
 Außer mit diesen Tools können Data Mining-Objekte auch programmgesteuert mithilfe von AMO oder mit anderen Clients verwaltet werden, die eine Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank herstellen können, wie etwa mit den Data Mining Add-Ins für [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Verschieben von Data Mining-Objekten](../../analysis-services/data-mining/moving-data-mining-objects.md)  
  
 [Anforderungen und Überlegungen zur Verarbeitung &#40;Data Mining&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
 [Verwenden von SQL Server Profiler zum Überwachen von Data Mining &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/using-sql-server-profiler-to-monitor-data-mining-analysis-services-data-mining.md)  
  
## <a name="location-of-data-mining-objects"></a>Speicherort von Data Mining-Objekten  
 Verarbeitete Miningstrukturen und -modelle werden in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]gespeichert.  
  
 Wenn zur Entwicklung von Data Mining-Objekten eine Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank im **Sofort** -Modus erstellt wird, werden alle neu erstellten Objekte sofort dem Server hinzugefügt. Wenn Data Mining-Objekte im **Offline** -Modus erstellt werden, dem Standardmodus bei der Arbeit in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], dann sind die erstellten Miningobjekte so lange nur Metadatencontainer, bis sie auf einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereitgestellt werden. Jedes Mal, wenn ein Objekt verändert wird, muss es daher erneut auf dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server bereitgestellt werden. Weitere Informationen zur Datamining-Architektur finden Sie unter [Physische Architektur &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Einige Clients, z.B. die Data Mining Add-Ins für [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007, ermöglichen auch die Erstellung von Miningmodellen und -strukturen als Sitzungsobjekte, für die eine Verbindung mit einer Instanz verwendet wird, deren Miningstrukturen und -modelle jedoch auf dem Server nur für die Dauer der Sitzung gespeichert werden. Diese Modelle können ebenso mit dem Client verwaltet werden wie die in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank gespeicherten Strukturen und Modelle, aber die Objekte werden nicht persistent gespeichert, nachdem die Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz getrennt wurde.  
  
## <a name="managing-data-mining-objects-in-sql-server-data-tools"></a>Verwalten von Data Mining-Objekten in SQL Server-Datentools  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] bietet Funktionen, die das Erstellen, Durchsuchen und Bearbeiten von Data Mining-Objekten erleichtern.  
  
 Die folgenden Links enthalten Informationen darüber, wie Sie Data Mining-Objekte mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ändern können:  
  
-   [Bearbeiten der für eine Miningstruktur verwendeten Datenquellensicht](../../analysis-services/data-mining/edit-the-data-source-view-used-for-a-mining-structure.md)  
  
-   [Ändern der Eigenschaften einer Miningstruktur](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)  
  
-   [Ändern der Eigenschaften eines Miningmodells](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)  
  
-   [Anzeigen oder Ändern von Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)  
  
-   [Anzeigen oder Ändern von Algorithmusparametern](../../analysis-services/data-mining/view-or-change-algorithm-parameters.md)  
  
 In der Regel verwenden Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] als Tool zum Entwickeln von neuen Projekten und zum Hinzufügen zu vorhandenen Projekten. Sie verwalten dann Projekte und Objekte, die mit Tools wie z. B. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bereitgestellt wurden.  
  
 Sie können Objekte, die bereits auf einer Instanz von ssASnoversion mit der **Immediate** -Option bereitgestellt werden, und das Herstellen einer Verbindung mit dem Server im Onlinemodus jedoch direkt ändern. Weitere Informationen finden Sie unter [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
> [!WARNING]  
>  Alle Änderungen an einer Miningstruktur oder einem Miningmodell, selbst Änderungen an Metadaten wie Name oder Beschreibung, machen es erforderlich, dass die Miningstruktur bzw. das -modell erneut verarbeitet wird.  
  
 Wenn Sie die Projektmappendatei nicht haben, die verwendet wurde, um das Data Mining-Projekt oder die -Objekte zu erstellen, können Sie das vorhandene Projekt vom Server importieren, der den Analysis Services-Import-Assistenten verwendet. Außerdem können Sie Änderungen an den Objekten vornehmen und diese dann mit der **Incremental** -Option erneut bereitstellen. Weitere Informationen finden Sie unter [Importieren eines Data Mining-Projekts mithilfe des Analysis Services-Import-Assistenten](../../analysis-services/data-mining/import-a-data-mining-project-using-the-analysis-services-import-wizard.md).  
  
## <a name="managing-data-mining-objects-in-sql-server-management-studio"></a>Verwalten von Data Mining-Objekten in SQL Server Management Studio  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]können Sie Skripts für Miningstrukturen und -modelle schreiben, Miningstrukturen und -modelle verarbeiten oder löschen. Im Objektexplorer wird nur ein eingeschränkter Satz an Eigenschaften angezeigt. Sie können jedoch zusätzliche Metadaten zu Miningmodellen anzeigen, indem Sie das Fenster **DMX-Abfrage** öffnen und eine Miningstruktur auswählen.  
  
-   [Erstellen einer DMX-Abfrage in SQL Server Management Studio](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="managing-data-mining-objects-programmatically"></a>Programmgesteuertes Verwalten von Data Mining-Objekten  
 Mit den folgenden Programmiersprachen können Data Mining-Objekte erstellt, geändert, verarbeitet und gelöscht werden. Jede Sprache wurde für verschiedene Tasks entwickelt. Daher kann es Beschränkungen hinsichtlich des Typs der ausführbaren Vorgänge geben. Einige Eigenschaften der Data Mining-Objekte können z. B. nicht mit DMX (Data Mining Extensions) geändert werden. Sie müssen stattdessen XMLA oder AMO verwenden.  
  
### <a name="analysis-management-objects-amo"></a>Analysis Management Objects (AMO)  
 Analysis Management Object (AMO) ist ein Objektmodell, das auf XMLA aufsetzt und Ihnen einen Vollzugriff auf Data Mining-Objekte erlaubt. Durch die Verwendung von AMO können Sie Miningstrukturen und Miningmodelle erstellen, bereitstellen und überwachen.  
  
-   [AMO-Konzepte und -Objektmodell](../../analysis-services/multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)  
  
-   <xref:Microsoft.AnalysisServices>  
  
 **Einschränkungen:** Keine.  
  
### <a name="data-mining-extensions-dmx"></a>Data Mining-Erweiterungen (DMX)  
 Data Mining-Erweiterungen (DMX) können in Kombination mit anderen Befehlsschnittstellen wie [!INCLUDE[vstecado](../../includes/vstecado-md.md)] oder ADOMD.NET verwendet werden, um Miningstrukturen und Miningmodelle zu erstellen, zu löschen und abzufragen.  
  
-   [Data Mining-Erweiterungen &#40;DMX&#41; – Datendefinitionsanweisungen](../../dmx/dmx-statements-data-definition.md)  
  
 **Einschränkungen:** Einige Eigenschaften können mit DMX nicht geändert werden.  
  
### <a name="xml-for-analysis-xmla"></a>XML for Analysis (XMLA)  
 XML for Analysis (XMLA) ist die Datendefinitionssprache für sämtliche Analysis Services. XMLA ermöglicht es Ihnen, die meisten der Data Mining-Objekte und Servervorgänge zu steuern. Alle Verwaltungsvorgänge zwischen Client und Server können mit XMLA ausgeführt werden. Zur Vereinfachung können Sie die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Skriptsprache (ASSL) verwenden, um das XML einzubinden.  
  
 **Einschränkungen:** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] generiert einige XMLA-Anweisungen, die nur für die interne Verwendung unterstützt werden und in XML DDL-Skripts nicht verwendet werden können.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwicklerhandbuch (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md)  
  
  

