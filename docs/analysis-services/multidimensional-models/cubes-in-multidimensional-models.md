---
title: "Cubes in mehrdimensionalen Modellen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OLAP-Objekte [Analysis Services], Cubes"
  - "Cubes [Analysis Services], Informationen zu Cubes"
  - "Cubes [Analysis Services]"
  - "OLAP [Analysis Services], Cubes"
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 33
---
# Cubes in mehrdimensionalen Modellen
  Ein Cube ist eine mehrdimensionale Struktur, die Informationen für analytische Zwecke enthält. Die Hauptbestandteile eines Cubes sind Dimensionen und Measures. Dimensionen definieren die Struktur des Cubes, den Sie für Aufteilungen verwenden, während Measures dem Endbenutzer numerische Werte zur Verfügung stellen, die für ihn von Interesse sind. Als logische Struktur ermöglicht ein Cube einer Clientanwendung das Abrufen von Werten von Measures, so als ob sie in Zellen im Cube enthalten wären. Zellen werden für jeden möglichen zusammengefassten Wert definiert. Eine Zelle im Cube wird von der Schnittmenge von Dimensionselementen definiert und enthält die aggregierten Werte der Measures an dieser speziellen Schnittmenge.  
  
## Vorteile der Verwendung von Cubes  
 Ein Cube bietet eine einzelne Position, an der alle verknüpften Daten für die Analyse gespeichert werden.  
  
## Komponenten von Cubes  
 Ein Cube besteht aus den folgenden Elementen:  
  
|Element|Description|  
|-------------|-----------------|  
|Dimensionen|[Dimensionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)|  
|Measures und Measuregruppen|[Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Partitionen|[Partitionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)|  
|Perspektiven|[Perspektiven in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|  
|Hierarchien|[Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/create-user-defined-hierarchies.md)|  
|Aktionen|[Aktionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|  
|Key Performance Indicators (KPI)|[Leistungskennzahlen &#40;Key Performance Indicators, KPIs&#41; in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Berechnungen|[Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|  
|Übersetzungen|[Übersetzungen in mehrdimensionalen Modellen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|  
  
## Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen eines Cubes mit dem Cube-Assistenten](../../analysis-services/multidimensional-models/create-a-cube-using-the-cube-wizard.md)|Beschreibt das Definieren von Cubes, Dimensionen, Dimensionsattributen und benutzerdefinierten Hierarchien mithilfe des Cube-Assistenten.|  
|[Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Beschreibt das Definieren von Measuregruppen.|  
|[Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|Beschreibt das Definieren und Konfigurieren einer Berechnung in einem MDX-Skript.|  
|[Aktionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|Beschreibt das Definieren und Konfigurieren einer Aktion.|  
|[Perspektiven in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|Beschreibt das Definieren und Konfigurieren einer Perspektive.|  
|[Definieren von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Beschreibt das Verwenden von gespeicherten Prozeduren.|  
  
  