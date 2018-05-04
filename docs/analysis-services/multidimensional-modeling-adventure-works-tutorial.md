---
title: Mehrdimensionale Modellierung (Adventure Works-Lernprogramm) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [Analysis Services]
- Analysis Services, tutorials
ms.assetid: db55e226-601a-4026-8651-573195555a59
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ec76d00ee0c2c63a65db9e1c96d8ba6764edcd63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>Mehrdimensionale Modellierung (Adventure Works-Lernprogramm)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Willkommen beim [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Lernprogramm. In diesem Lernprogramm wird beschrieben, wie [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] zum Entwickeln und Bereitstellen eines [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekts verwendet wird, wobei das fiktive Unternehmen [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] für alle Beispiele verwendet wird.  
  
## <a name="what-you-learn"></a>Was Sie lernen  
In diesem Lernprogramm lernen Sie Folgendes:  
  
-   Definieren von Datenquellen, Datenquellensichten, Dimensionen, Attributen, Attributbeziehungen, Hierarchien und Cubes in einem [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekt innerhalb von [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Anzeigen von Cube- und Dimensionsdaten durch Bereitstellen des [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekts für eine Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]und anschließendes Verarbeiten der bereitgestellten Objekte, um sie mit Daten aus der zugrunde liegenden Datenquelle aufzufüllen.  
  
-   Ändern von Measures, Dimensionen, Hierarchien, Attributen und Measuregruppen im [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekt und anschließendes Bereitstellen von inkrementellen Änderungen für den bereitgestellten Cube auf dem Entwicklungsserver.  
  
-   Definieren von Berechnungen, Key Performance Indicators (KPIs), Aktionen, Perspektiven, Übersetzungen und Sicherheitsrollen innerhalb eines Cubes.  
  
Dieses Lernprogramm wird mit einer Szenariobeschreibung bereitgestellt, damit Sie den Kontext dieser Lektionen besser verstehen können. Weitere Informationen finden Sie unter [Analysis Services Tutorial Scenario](../analysis-services/analysis-services-tutorial-scenario.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Sie benötigen Beispieldaten, Beispielprojektdateien und Software, um alle Lektionen in diesem Lernprogramm abzuschließen. Anweisungen zum Suchen und Installieren der erforderlichen Komponenten für dieses Lernprogramm finden Sie unter [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](../analysis-services/install-sample-data-and-projects.md).  
  
Darüber hinaus müssen die folgenden Berechtigungen vorhanden sein, um das Lernprogramm erfolgreich abzuschließen:  
  
-   Sie müssen ein Mitglied der lokalen Administratorgruppe auf dem [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Computer oder ein Mitglied der Serveradministratorrolle in der [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Instanz sein.  
  
-   Sie benötigen Leseberechtigungen in der **AdventureWorksDW** -Beispieldatenbank. Diese Beispieldatenbank ist für die [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Version geeignet.  
  
## <a name="lessons"></a>Lektionen  
Dieses Lernprogramm umfasst die folgenden Lektionen:  
  
|Lektion|Für den Abschluss voraussichtlich benötigte Zeit|  
|----------|------------------------------|  
|[Lektion 1: Definieren einer Datenquellensicht innerhalb eines Analysis Services-Projekts](../analysis-services/lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 Minuten|  
|[Lektion 2: Definieren und Bereitstellen eines Cubes](../analysis-services/lesson-2-defining-and-deploying-a-cube.md)|30 Minuten|  
|[Lektion 3: Ändern von Maßen, Attributen und Hierarchien](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 Minuten|  
|[Lektion 4: Definieren von erweiterten Attributen und Dimensionseigenschaften](../analysis-services/lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 Minuten|  
|[Lektion 5: Definieren von Beziehungen zwischen Dimensionen und Measuregruppen](../analysis-services/lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 Minuten|  
|[Lektion 6: Definieren von Berechnungen](../analysis-services/lesson-6-defining-calculations.md)|45 Minuten|  
|[Lektion 7: Definieren von Key Performance Indicators & #40; KPIs & #41;](../analysis-services/lesson-7-defining-key-performance-indicators-kpis.md)|30 Minuten|  
|[Lektion 8: Definieren von Aktionen](../analysis-services/lesson-8-defining-actions.md)|30 Minuten|  
|[Lektion 9: Defining Perspectives and Translations](../analysis-services/lesson-9-defining-perspectives-and-translations.md)|30 Minuten|  
|[Lektion 10: Definieren von Administratorrollen](../analysis-services/lesson-10-defining-administrative-roles.md)|15 Minuten|  
  
> [!NOTE]  
> Die Cubedatenbank, die Sie in diesem Lernprogramm erstellte Cubedatenbank ist eine vereinfachte Version von den [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] mehrdimensionale Modellprojekt, die Teil der Adventure Works-Beispieldatenbanken, die zum Download auf GitHub verfügbar ist. Die Lernprogrammversion der mehrdimensionalen Adventure Works-Datenbank ist vereinfacht, um den Fokus auf die Fähigkeiten zu richten, die Sie vorrangig erwerben möchten. Nachdem Sie das Lernprogramm abgeschlossen haben, können Sie das mehrdimensionale Modellprojekt selbst untersuchen, um Ihr Verständnis der mehrdimensionalen [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Modellierung zu vertiefen.  
  
## <a name="next-step"></a>Nächster Schritt  
Um das Lernprogramm zu starten, gehen Sie zur ersten Lektion über: [Lesson 1: Defining a Data Source View within an Analysis Services Project](../analysis-services/lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md).  
  
  
  
