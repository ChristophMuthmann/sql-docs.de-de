---
title: "Datenbankobjekte (Analysis Services – mehrdimensionale Daten) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], about objects
- SQL Server Analysis Services, objects
- Analysis Services objects, about Analysis Services objects
- SSAS, objects
- Analysis Services objects
- objects [Analysis Services]
ms.assetid: f76d869b-fc1d-4807-9f28-da09c7be382d
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ace461fd29f5c1a1176ddab2f41056df939592e8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="database-objects-analysis-services---multidimensional-data"></a>Datenbankobjekte (Analysis Services - Mehrdimensionale Daten)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Ein [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz enthält Datenbankobjekte und Assemblys für die Verwendung mit online analytical Processing (OLAP) und Datamining.  
  
-   Datenbanken enthalten OLAP- und Data Mining-Objekte, z.&#160;B. Datenquellen, Datenquellensichten, Cubes, Measures, Measuregruppen, Dimensionen, Attribute, Hierarchien, Miningstrukturen, Miningmodelle und Rollen.  
  
-   Assemblys enthalten benutzerdefinierte Funktionen, die die Funktionalität der mit den Sprachen Multidimensional Expressions (MDX) und Data Mining Extensions (DMX) bereitgestellten systeminternen Funktionen erweitern.  
  
 Die <xref:Microsoft.AnalysisServices.Database> Objekt ist der Container für alle Datenobjekte, die für ein Business Intelligence-Projekt (z. B. OLAP-Cubes, Dimensionen und Datamining-Strukturen) erforderlich sind, sowie deren Unterstützungsobjekte (z. B. <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Account>, und <xref:Microsoft.AnalysisServices.Role>).  
  
 Ein <xref:Microsoft.AnalysisServices.Database>-Objekt bietet u. a. Zugriff auf folgende Objekte und Attribute:  
  
-   Eine Auflistung aller Cubes, auf die Sie Zugriff haben.  
  
-   Eine Auflistung aller Dimensionen, auf die Sie Zugriff haben.  
  
-   Eine Auflistung aller Miningstrukturen, auf die Sie Zugriff haben.  
  
-   Alle Datenquellen und Datenquellensichten in zwei Auflistungen.  
  
-   Alle Rollen und Datenbankberechtigungen in zwei Auflistungen.  
  
-   Der Sortierungswert der Datenbank.  
  
-   Die geschätzte Größe der Datenbank.  
  
-   Der Sprachwert der Datenbank.  
  
-   Die sichtbare Einstellung der Datenbank.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den folgenden Themen werden die Objekte beschrieben, die sowohl von OLAP- als auch von Data Mining-Funktionen in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verwendet werden.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Datenquellen in mehrdimensionalen Modellen](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)|Beschreibt eine Datenquelle in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Datenquellsichten in mehrdimensionalen Modellen](../../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)|Beschreibt ein logisches Datenmodell, das basierend auf eine oder mehrere Datenquellen in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Cubes in mehrdimensionalen Modellen](../../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)|Beschreibt Cubes und Cubeobjekte, einschließlich Measures, Measuregruppen, Dimensionsverwendungbeziehungen, Berechnungen, Key Performance Indicators (KPIs), Aktionen, Übersetzungen, Partitionen und Perspektiven.|  
|[Dimensionen &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|Beschreibt Dimensionen und Dimensionsobjekte, einschließlich Attribute, Attributbeziehungen, Hierarchien, Ebenen und Elemente.|  
|[Miningstrukturen &#40; Analysis Services – Datamining &#41;](../../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)|Beschreibt Miningstrukturen und Miningobjekte, einschließlich Miningmodellen.|  
|[Sicherheitsrollen &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)|Beschreibt eine Rolle, den Sicherheitsmechanismus, der zum Steuern des Zugriffs auf Objekte in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Mehrdimensionales Modell Assemblys-Verwaltung](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)|Beschreibt eine Assembly, eine Auflistung von benutzerdefinierten Funktionen, die zum Erweitern der Sprachen MDX und DMX in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verwendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützte Datenquellen &#40; SSAS – mehrdimensional &#41;](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [Mehrdimensionale Modelllösungen &#40; SSAS &#41;](../../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Datamining-Lösungen](../../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
