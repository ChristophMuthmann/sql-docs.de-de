---
title: Definieren von Cubedimensionseigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f4f83f8225cc233b45bb3f4299a700992902995
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="define-cube-dimension-properties"></a>Definieren von Cubedimensionseigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Eine Cubedimension handelt es sich um eine Instanz einer Datenbankdimension in einem Cube. Eine Datenbankdimension kann in mehreren Cubes verwendet werden, und mehrere Cubedimensionen können auf einer einzigen Datenbankdimension basieren. In der folgenden Tabelle werden die Eigenschaften einer Cubedimension beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|Steuert, wie Aggregationen vom Aggregations-Designer in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]entworfen werden. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **Full:**Jede Aggregation für den Cube muss das Alle-Element enthalten.<br /><br /> **None:**Keine Aggregation für den Cube darf das Alle-Element enthalten. Dies ist der Standardwert.<br /><br /> **Unrestricted:**Keine Einschränkungen für den Aggregations-Designer.<br /><br /> **Default:**Dieselbe Funktion wie Unbeschränkt.|  
|**Description**|Stellt einen aussagekräftigen Namen für die Ebene bereit.|  
|**DimensionID**|Enthält den eindeutigen Bezeichner (ID) für die Datenbankdimension.|  
|**HierarchyUniqueNameStyle**|Bestimmt, wie eindeutige Namen für Hierarchien generiert werden, die in der Cubedimension enthalten sind. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **IncludeDimensionName**:<br />                    Der Name der Dimension ist im Namen der Hierarchie enthalten. Dies ist der Standardwert.<br /><br /> **ExcludeDimensionName**:<br />                    Der Name der Dimension ist nicht im Namen der Hierarchie enthalten.|  
|**ID**|Enthält den eindeutigen Bezeichner für die Cubedimension.|  
|**MemberUniqueNameStyle**|Bestimmt, wie eindeutige Namen für Elemente in Hierarchien generiert werden, die in der Cubedimension enthalten sind. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **Native:**<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] legt die eindeutigen Namen von Elementen automatisch fest. Dies ist der Standardwert.<br /><br /> **NamePath:** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generiert einen zusammengesetzten Namen, der aus dem Namen den einzelnen Ebenen und der Beschriftung des Elements besteht.|  
|**Name**|Enthält den Anzeigename für die Cubedimension. Der Name einer Cubedimension ist standardmäßig derselbe wie der Name der Datenbankdimension, sofern nicht bereits eine andere Cubedimension mit demselben Namen definiert ist.|  
|**Visible**|Bestimmt, ob die Cubedimension sichtbar ist. Der Standardwert lautet **True**.|  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
