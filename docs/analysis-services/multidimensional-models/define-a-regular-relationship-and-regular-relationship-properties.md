---
title: "Definieren einer regulären Beziehung und reguläre Beziehungseigenschaften | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- granularity attribute
- relationships [Analysis Services], regular relationships
ms.assetid: 840280d8-20c3-46c0-99ea-62479469c36b
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 640b8197e37773249cb9afd53cbcad46d33754f9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>Definieren einer regulären Beziehung und von Eigenschaften einer regulären Beziehung
  Wenn Sie eine neue Cubedimension oder eine neue Measuregruppe definieren, versucht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zu erkennen, ob eine reguläre Beziehung vorhanden ist, und legt dann die Einstellung für die Dimensionsverwendung auf **Regulär**fest. Sie können eine reguläre Dimensionsbeziehung im Cube-Designer auf der Registerkarte **Dimensionsverwendung** anzeigen oder bearbeiten.  
  
 Beim Definieren der Beziehung einer Cubedimension zu einer Measuregruppe geben Sie auch das Granularitätsattribut für die Beziehung an. Das Granularitätsattribut definiert die niedrigste Detailstufe, die im Cube für die entsprechende Dimension verfügbar ist. Im Allgemeinen ist dies das Schlüsselattribut für die Dimension. Mitunter kann es jedoch gewünscht sein, die Granularität einer bestimmten Cubedimension in einer bestimmten Measuregruppe auf eine andere Einheit festzulegen. So könnte es beispielsweise gewünscht sein, das Granularitätsattribut für die Time-Dimension auf das Month-Attribut anstatt auf das Day-Attribut festzulegen, wenn Sie eine Sales Quotas- oder Budget-Measuregruppe verwenden. Wenn Sie ein anderes als das Schlüsselattribut als Granularitätsattribut festlegen, müssen Sie sicherstellen, dass alle anderen Attribute in der Dimension über Attributbeziehungen direkt oder indirekt mit diesem anderen Attribut verknüpft sind. Andernfalls ist [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nicht in der Lage, Daten ordnungsgemäß zu aggregieren.  
  
  

