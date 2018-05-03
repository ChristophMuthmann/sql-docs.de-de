---
title: Definieren von Cubedimensionseigenschaften | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 16c95ce4fd05f40e1dc9ebde1fed566add96b7d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="define-cube-dimension-properties"></a>Definieren von Cubedimensionseigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine Cubedimension ist eine Instanz einer Datenbankdimension in einem Cube. Eine Datenbankdimension kann in mehreren Cubes verwendet werden, und mehrere Cubedimensionen können auf einer einzigen Datenbankdimension basieren. In der folgenden Tabelle werden die Eigenschaften einer Cubedimension beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|Steuert, wie Aggregationen vom Aggregations-Designer in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]entworfen werden. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **Full:** Jede Aggregation für den Cube muss das Alle-Element enthalten.<br /><br /> **None:** Keine Aggregation für den Cube darf das Alle-Element enthalten. Dies ist der Standardwert.<br /><br /> **Unrestricted:** Keine Einschränkungen für den Aggregations-Designer.<br /><br /> **Default:** Dieselbe Funktion wie Unbeschränkt.|  
|**Description**|Stellt einen aussagekräftigen Namen für die Ebene bereit.|  
|**DimensionID**|Enthält den eindeutigen Bezeichner (ID) für die Datenbankdimension.|  
|**HierarchyUniqueNameStyle**|Bestimmt, wie eindeutige Namen für Hierarchien generiert werden, die in der Cubedimension enthalten sind. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **IncludeDimensionName**:<br />                    Der Name der Dimension ist im Namen der Hierarchie enthalten. Dies ist der Standardwert.<br /><br /> **ExcludeDimensionName**:<br />                    Der Name der Dimension ist nicht im Namen der Hierarchie enthalten.|  
|**ID**|Enthält den eindeutigen Bezeichner für die Cubedimension.|  
|**MemberUniqueNameStyle**|Bestimmt, wie eindeutige Namen für Elemente in Hierarchien generiert werden, die in der Cubedimension enthalten sind. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **Native:**<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] legt die eindeutigen Namen von Elementen automatisch fest. Dies ist der Standardwert.<br /><br /> **NamePath:** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generiert einen zusammengesetzten Namen, der aus dem Namen den einzelnen Ebenen und der Beschriftung des Elements besteht.|  
|**Name**|Enthält den Anzeigename für die Cubedimension. Der Name einer Cubedimension ist standardmäßig derselbe wie der Name der Datenbankdimension, sofern nicht bereits eine andere Cubedimension mit demselben Namen definiert ist.|  
|**Visible**|Bestimmt, ob die Cubedimension sichtbar ist. Der Standardwert lautet **True**.|  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionen & #40; Analysis Services – mehrdimensionale Daten & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
