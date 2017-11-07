---
title: Definieren von Cubeattributeigenschaften | Microsoft Docs
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
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fe36e6ba9ff002706260e2e195adb292ba19b085
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="define-cube-attribute-properties"></a>Definieren von Cubeattributeigenschaften
  Durch Cubeattributeigenschaften können Sie eindeutige Einstellungen für Dimensionsattribute in Cubedimensionen angeben, die auf derselben Datenbankdimension basieren. In der folgenden Tabelle werden die Eigenschaften eines Cubeattributs beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AggregationUsage**|Gibt an, wie der Aggregationsentwurfs-Assistent Aggregationen für das Attribut entwirft. Der Standardwert lautet **Default**. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **Default:**<br />                    Der Aggregationsentwurfs-Assistent wendet eine Standardregel basierend auf dem Typ des Attributs an (Vollständig für Schlüssel, Uneingeschränkt für andere Attribute).<br /><br /> **None:**<br />                    Keine Aggregation für den Cube darf dieses Attribut enthalten.<br /><br /> **Unrestricted:**<br />                    Für den Aggregationsentwurfs-Assistenten gelten keine Einschränkungen.<br /><br /> **Full:**<br />                    Jede Aggregation für den Cube muss dieses Attribut enthalten.|  
|**AttributeHierarchyEnabled**|Identifiziert, ob die Attributhierarchie für diese Cubedimension aktiviert ist. Hierdurch ist es möglich, Attributhierarchien für bestimmte Cubes oder Dimensionsrollen zu deaktivieren. Diese Einstellung hat keine Wirkung, wenn die zugrunde liegende Attributhierarchie deaktiviert ist. Der Standardwert ist **True**.|  
|**OptimizedState**|Zeigt an, ob die Attributhierarchie für diese Cubedimension optimiert ist. Hierdurch ist es möglich, Attributhierarchien für bestimmte Cubes oder Dimensionsrollen zu optimieren. Diese Einstellung hat keine Wirkung, wenn die zugrunde liegende Attributhierarchie nicht optimiert ist. Der Standardwert lautet **FullyOptimized**. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **FullyOptimized**: Von der Instanz werden Indizes zum Verbessern der Abfrageleistung für die Hierarchie erstellt. Dies ist der Standardwert.<br /><br /> **NotOptimized:**<br />                    Durch die Instanz werden keine zusätzlichen Indizes erstellt.|  
|**AttributeHierarchyVisible**|Zeigt an, ob die Attributhierarchie für diese Cubedimension sichtbar ist. Hierdurch ist es möglich, dass Attributhierarchien für bestimmte Cubes oder Dimensionsrollen sichtbar gemacht werden. Diese Einstellung hat keine Wirkung, wenn die zugrunde liegende Attributhierarchie nicht sichtbar ist. Der Standardwert lautet **True**.|  
|**AttributeID**|Enthält den eindeutigen Bezeichner (ID) des Attributs.|  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren von Cubedimensionseigenschaften](../../analysis-services/multidimensional-models/define-cube-dimension-properties.md)   
 [Definieren von Cubehierarchieeigenschaften](../../analysis-services/multidimensional-models/define-cube-hierarchy-properties.md)  
  
  

