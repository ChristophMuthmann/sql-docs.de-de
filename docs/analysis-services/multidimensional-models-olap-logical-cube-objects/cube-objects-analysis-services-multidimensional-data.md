---
title: Cubeobjekte (Analysis Services – mehrdimensionale Daten) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 27fab4d1fb52df03991db9559f54f6d829e3256d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Cubeobjekte (Analysis Services – Mehrdimensionale Daten)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
    
## <a name="introducing-cube-objects"></a>Einführung in Cubeobjekte  
 Ein einfaches <xref:Microsoft.AnalysisServices.Cube>-Objekt besteht aus grundlegenden Informationen, Dimensionen und Measuregruppen. Grundlegende Informationen beinhalten den Namen des Cubes, das Standardmeasure des Cubes, die Datenquelle, den Speichermodus usw.  
  
 Die Dimensionsauflistung enthält den eigentlichen Dimensionssatz, der im Cube aus der Dimensionsauflistung der Datenbank verwendet wird. Alle Dimensionen müssen in der Dimensionsauflistung der Datenbank definiert werden, bevor im Cube auf sie verwiesen wird. Private Dimensionen sind nicht verfügbar in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Measuregruppen sind Sätze von Measures im Cube. Eine Measuregruppe ist eine Auflistung von Measures, die eine gemeinsame Datenquellensicht und einen gemeinsamen Satz von Dimensionen besitzen. Eine Measuregruppe ist die Verarbeitungseinheit für Measures. Measuregruppen können einzeln verarbeitet und dann durchsucht werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|||  
|-|-|  
|Thema||  
|[Aktionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Aggregationen und Aggregationsentwürfe](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)||  
|[Berechnungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)||  
|[Cubezellen &#40; Analysis Services – mehrdimensionale Daten &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-cells-analysis-services-multidimensional-data.md)||  
|[Cubeeigenschaften – Mehrdimensionale Modellprogrammierung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-properties-multidimensional-model-programming.md)||  
|[Speicherung von Cubes &#40; Analysis Services – mehrdimensionale Daten &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)||  
|[Cubeübersetzungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)||  
|[Dimensionsbeziehungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)||  
|[Leistungskennzahlen &#40;Key Performance Indicators, KPIs&#41; in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Measures und Measuregruppen](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)||  
|[Partitionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)||  
|[Perspektiven](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)||  
  
  
