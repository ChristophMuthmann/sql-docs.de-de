---
title: Erstellen von benutzerdefinierten Hierarchien | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a188eb62eb80e23ef5f20bc054653891958377f6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="user-defined-hierarchies---create"></a>Erstellen von benutzerdefinierten Hierarchien-
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ermöglicht die Erstellung von benutzerdefinierten Hierarchien. Eine Hierarchie ist eine Auflistung von Ebenen, die auf Attributen basiert. So kann beispielsweise eine Zeithierarchie die Ebenen Jahr, Quartal, Monat, Woche und Tag enthalten. In einigen Hierarchien impliziert jedes Elementattribut das jeweils übergeordnete Elementattribut. Dies wird auch als natürliche Hierarchie bezeichnet. Eine Hierarchie kann von Endbenutzern verwendet werden, um Cubedaten zu durchsuchen. Zum Definieren von Hierarchien verwenden Sie den Bereich Hierarchien des Dimensions-Designers in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Wenn Sie eine benutzerdefinierte Hierarchie erstellen, kann die Hierarchie *unregelmäßig*werden. In einer unregelmäßigen Hierarchie befindet sich das logisch übergeordnete Element mindestens eines Elements nicht auf der Ebene unmittelbar über dem betreffenden Element. Wenn Sie über eine unregelmäßige Hierarchie verfügen, können Sie festlegen, ob die fehlenden Elemente sichtbar sind und wie sie angezeigt werden sollen. Weitere Informationen finden Sie unter [Unregelmäßige Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Weitere Informationen zu Leistungsproblemen im Zusammenhang mit dem Design und der Konfiguration von benutzerdefinierten Hierarchien finden Sie im [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenschaften der Benutzerhierarchie](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Ebeneneigenschaften - Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Über-und untergeordneten Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
