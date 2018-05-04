---
title: Cubes in mehrdimensionalen Modellen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71db68e9283e1dffd463928aac5437f21e668b2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cubes-in-multidimensional-models"></a>Cubes in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein Cube ist eine mehrdimensionale Struktur, die Informationen für analytische Zwecke enthält. Die Hauptbestandteile eines Cubes sind Dimensionen und Measures. Dimensionen definieren die Struktur des Cubes, den Sie für Aufteilungen verwenden, während Measures dem Endbenutzer numerische Werte zur Verfügung stellen, die für ihn von Interesse sind. Als logische Struktur ermöglicht ein Cube einer Clientanwendung das Abrufen von Werten von Measures, so als ob sie in Zellen im Cube enthalten wären. Zellen werden für jeden möglichen zusammengefassten Wert definiert. Eine Zelle im Cube wird von der Schnittmenge von Dimensionselementen definiert und enthält die aggregierten Werte der Measures an dieser speziellen Schnittmenge.  
  
## <a name="benefits-of-using-cubes"></a>Vorteile der Verwendung von Cubes  
 Ein Cube bietet eine einzelne Position, an der alle verknüpften Daten für die Analyse gespeichert werden.  
  
## <a name="components-of-cubes"></a>Komponenten von Cubes  
 Ein Cube besteht aus den folgenden Elementen:  
  
|Element|Description|  
|-------------|-----------------|  
|Dimensionen|[Dimensionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)|  
|Measures und Measuregruppen|[Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Partitionen|[Partitionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)|  
|Perspektiven|[Perspektiven in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|  
|Hierarchien|[Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)|  
|Aktionen|[Aktionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|  
|Key Performance Indicators (KPI)|[Key Performance Indicators & #40; KPIs & #41; In mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Berechnungen|[Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|  
|Übersetzungen|[Übersetzungen in mehrdimensionalen Modellen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen eines Cubes mithilfe des Cube-Assistenten](../../analysis-services/multidimensional-models/create-a-cube-using-the-cube-wizard.md)|Beschreibt das Definieren von Cubes, Dimensionen, Dimensionsattributen und benutzerdefinierten Hierarchien mithilfe des Cube-Assistenten.|  
|[Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Beschreibt das Definieren von Measuregruppen.|  
|[Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|Beschreibt das Definieren und Konfigurieren einer Berechnung in einem MDX-Skript.|  
|[Aktionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|Beschreibt das Definieren und Konfigurieren einer Aktion.|  
|[Perspektiven in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|Beschreibt das Definieren und Konfigurieren einer Perspektive.|  
|[Definieren von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Beschreibt das Verwenden von gespeicherten Prozeduren.|  
  
  
