---
title: "Bereitstellung von Datamining-Lösungen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], deploying
- deploying [Analysis Services], production environments
- deploying [Analysis Services - data mining]
- solutions [Analysis Services], deploying
- models [Analysis Services], data mining
ms.assetid: d83effc7-437d-42e9-8ac3-b65f79e27043
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aa037f7ff155df158ba2967c5e7c31989ace887d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deployment-of-data-mining-solutions"></a>Bereitstellen von Data Mining-Lösungen
  Der letzte Schritt im Data Mining-Prozess besteht darin, die Modelle in einer Produktionsumgebung bereitzustellen. Die Bereitstellung ist wichtig, da dadurch die Modelle Benutzern zur Verfügung gestellt werden, damit Sie irgendeine der folgenden Aufgaben ausführen können:  
  
-   Verwenden Sie die Modelle, um Vorhersagen und Geschäftsentscheidungen zu treffen. Weitere Informationen zu den Tools, mit denen Sie Abfragen erstellen können, finden Sie unter [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
-   Data Mining-Funktionen in eine Anwendung integrieren. Sie können Analysis Management Objects (AMO) hinzufügen oder ein Assembly mit mehreren Objekten einbetten. Mit diesen Objekten kann Ihre Anwendung Miningstrukturen und -modelle erstellen, ändern, verarbeiten und löschen.  
  
-   Erstellen Sie Berichte, mit denen Benutzer Vorhersagen anfordern, Trends anzeigen oder Modelle vergleichen können.  
  
 Dieser Abschnitt enthält ausführliche Informationen über Bereitstellungsoptionen.  
  
 [Anforderungen für die Bereitstellung von Data Mining-Projektmappen](#bkmk_Reqs)  
  
 [Bereitstellen von relationalen Projektmappen](#bkmk_RelationalSltn)  
  
 [Bereitstellen von mehrdimensionalen Projektmappen](#bkmk_MDSltn)  
  
 [Verwandte Ressourcen](#bkmk_Resources)  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Bereitstellen von Data Mining-Lösungen für frühere Versionen von SQL Server](../../analysis-services/data-mining/deploy-a-data-mining-solution-to-previous-versions-of-sql-server.md)  
  
 [Exportieren und Importieren von Data Mining-Objekten](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
##  <a name="bkmk_Reqs"></a> Anforderungen für die Bereitstellung von Data Mining-Projektmappen  
 Die Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , für die Sie die Projektmappe bereitstellen, muss in einem Modus ausgeführt werden, der mehrdimensionale Objekte und Data Mining-Objekte unterstützt. Sie können daher Data Mining-Objekte nicht in einer Instanz bereitstellen, die tabellarische Modelle oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten hostet.  
  
 Wenn Sie in Visual Studio eine Data Mining-Projektmappe erstellen, müssen Sie demzufolge die Vorlage für multidimensionale Projekte bzw. Data Mining-Projekte von Analysis Services ****verwenden.  
  
 Wenn Sie die Projektmappe bereitstellen, werden die für Data Mining verwendeten Objekte in der angegebenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz erstellt, und zwar in einer Datenbank mit dem gleichen Namen wie die Projektmappendatei.  
  
###  <a name="bkmk_RelationalSltn"></a> Bereitstellen von relationalen Projektmappen  
 Wenn Sie eine relationale Data Mining-Projektmappe bereitstellen, werden die erforderlichen Data Mining-Objekte innerhalb einer neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank erstellt, und die Objekte werden standardmäßig verarbeitet. Sie können die Verarbeitungsoptionen mithilfe der Konfigurationseigenschaft für die Verarbeitungsoption ****ändern. Weitere Informationen finden Sie unter [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
 Standardmäßig werden nur inkrementelle Änderungen jedes Mal bereitgestellt. Sie können demnach ein Miningmodell ändern, und wenn Sie das Projekt erneut bereitstellen, wird nur das Miningmodell aktualisiert. Wenn jedoch mehrere Clients die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bearbeiten, kann dies zu Fehlern führen. Ändern Sie die Eigenschaft **Bereitstellungsmodus** , um den Standardbereitstellungsmodus zu ändern, damit die gesamte Datenbank aktualisiert wird, wenn Sie die Projektmappe bereitstellen.  
  
 In einer relationalen Data Mining-Projektmappe sind die einzigen bereitzustellenden Objekte die Datenquellendefinition, sämtliche verwendeten Datenquellensichten, die Miningstrukturen und alle abhängigen Miningmodelle.  
  
###  <a name="bkmk_MDSltn"></a> Bereitstellen von mehrdimensionalen Projektmappen  
 Wenn Sie eine mehrdimensionale Data Mining-Projektmappe bereitstellen, erstellt diese Projektmappe die Data Mining-Objekte in der gleichen Datenbank wie die des Quellcubes.  
  
 Wenn Sie die Miningstruktur oder das Miningmodell verarbeiten, müssen Sie auch den Quellcube verarbeiten. Daher kann es länger dauern, eine Projektmappe bereitzustellen, die OLAP-Miningmodelle verwendet, als eine relationale Data Mining-Projektmappe.  
  
 In der Regel verwenden Data Mining-Objekte auch die gleichen Datenquellen und die Datenquellensichten, die für den Cube verwendet werden. Sie können jedoch auch Datenquellen und Datenquellenansichten hinzufügen, die speziell auf Data Mining abzielen. Ein Cube würde beispielsweise in der Regel keine Daten über potenzielle Kunden oder externe Daten enthalten, die in mehrdimensionalen Objekten nicht verwendete Daten.  
  
##  <a name="bkmk_Resources"></a> Verwandte Ressourcen  
 [Verschieben von Data Mining-Objekten](../../analysis-services/data-mining/moving-data-mining-objects.md)  
  
 Wenn das Modell nur auf relationalen Daten basiert, ist das Exportieren und Importieren von Objekten mit DMX die einfachste Möglichkeit, Modelle zu verschieben.  
  
 [Verschieben einer Analysis Services Datenbank](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 Wenn Modelle einen Cube als Datenquelle verwenden, sind weitere Informationen über das Verschieben von Modellen und deren Cubedatenunterstützung diesem Thema zu entnehmen.  
  
 [Bereitstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
 Bietet allgemeine Informationen über die Bereitstellungen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekten und beschreibt die Eigenschaften, die als Teil der Projektkonfiguration festgelegt werden können.  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Anforderungen und Überlegungen zur Verarbeitung &#40;Data Mining&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  

