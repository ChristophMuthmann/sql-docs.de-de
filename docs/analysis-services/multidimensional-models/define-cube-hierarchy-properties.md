---
title: "Definieren von Cubehierarchieeigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "Hierarchien [Analysis Services], mit mehreren Ebenen"
  - "Hierarchien [Analysis Services], Cubes"
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# Definieren von Cubehierarchieeigenschaften
  Durch Cubehierarchieeigenschaften können Sie eindeutige Einstellungen für benutzerdefinierte Hierarchien in Cubedimensionen angeben, die auf denselben Datenbankdimensionen basieren. In der folgenden Tabelle werden die Eigenschaften einer Cubehierarchie beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Aktiviert**|Bestimmt, ob die Hierarchie für die Cubedimension aktiviert ist.|  
|**HierarchyID**|Enthält den eindeutigen Bezeichner (ID) der Hierarchie.|  
|**OptimizedState**|Bestimmt die Optimierungsebene, die auf die Hierarchie angewendet wird. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> **FullyOptimized:**<br />                    Durch die Instanz werden Indizes zum Verbessern der Abfrageleistung für die Hierarchie erstellt. Dies ist der Standardwert.<br /><br /> **NotOptimized:**<br />                    Durch die Instanz werden keine zusätzlichen Indizes erstellt.|  
|**Visible**|Beschreibt die Sichtbarkeit der Cubehierarchie. Der Standardwert lautet **True**.|  
  
## Siehe auch  
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  