---
title: Definieren von Cubehierarchieeigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dad968995a91d8a163a8ba067925e4dcb07848cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="define-cube-hierarchy-properties"></a>Definieren von Cubehierarchieeigenschaften
  Durch Cubehierarchieeigenschaften können Sie eindeutige Einstellungen für benutzerdefinierte Hierarchien in Cubedimensionen angeben, die auf denselben Datenbankdimensionen basieren. In der folgenden Tabelle werden die Eigenschaften einer Cubehierarchie beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Aktiviert**|Bestimmt, ob die Hierarchie für die Cubedimension aktiviert ist.|  
|**HierarchyID**|Enthält den eindeutigen Bezeichner (ID) der Hierarchie.|  
|**OptimizedState**|Bestimmt die Optimierungsebene, die auf die Hierarchie angewendet wird. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **FullyOptimized:**<br />                    Durch die Instanz werden Indizes zum Verbessern der Abfrageleistung für die Hierarchie erstellt. Dies ist der Standardwert.<br /><br /> **NotOptimized:**<br />                    Durch die Instanz werden keine zusätzlichen Indizes erstellt.|  
|**Visible**|Beschreibt die Sichtbarkeit der Cubehierarchie. Der Standardwert lautet **True**.|  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
