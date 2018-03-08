---
title: Definieren von Cubehierarchieeigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 13934070e4121913b82a2604acf26581cf27796f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="define-cube-hierarchy-properties"></a>Definieren von Cubehierarchieeigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Durch Cubehierarchieeigenschaften können Sie eindeutige Einstellungen für benutzerdefinierte Hierarchien in Cubedimensionen angeben, die auf denselben Datenbankdimensionen basieren. In der folgenden Tabelle werden die Eigenschaften einer Cubehierarchie beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Aktiviert**|Bestimmt, ob die Hierarchie für die Cubedimension aktiviert ist.|  
|**HierarchyID**|Enthält den eindeutigen Bezeichner (ID) der Hierarchie.|  
|**OptimizedState**|Bestimmt die Optimierungsebene, die auf die Hierarchie angewendet wird. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **FullyOptimized:**<br />                    Durch die Instanz werden Indizes zum Verbessern der Abfrageleistung für die Hierarchie erstellt. Dies ist der Standardwert.<br /><br /> **NotOptimized:**<br />                    Durch die Instanz werden keine zusätzlichen Indizes erstellt.|  
|**Visible**|Beschreibt die Sichtbarkeit der Cubehierarchie. Der Standardwert lautet **True**.|  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
