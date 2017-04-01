---
title: "Erstellen von benutzerdefinierten Hierarchien | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "Benutzerdefinierte Hierarchien [Analysis Services]"
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Erstellen von benutzerdefinierten Hierarchien
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] In können Sie benutzerdefinierte Hierarchien erstellen. Eine Hierarchie ist eine Auflistung von Ebenen, die auf Attributen basiert. So kann beispielsweise eine Zeithierarchie die Ebenen Jahr, Quartal, Monat, Woche und Tag enthalten. In einigen Hierarchien impliziert jedes Elementattribut das jeweils übergeordnete Elementattribut. Dies wird auch als natürliche Hierarchie bezeichnet. Eine Hierarchie kann von Endbenutzern verwendet werden, um Cubedaten zu durchsuchen. Zum Definieren von Hierarchien verwenden Sie den Bereich Hierarchien des Dimensions-Designers in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Wenn Sie eine benutzerdefinierte Hierarchie erstellen, kann die Hierarchie *unregelmäßig* werden. In einer unregelmäßigen Hierarchie befindet sich das logisch übergeordnete Element mindestens eines Elements nicht auf der Ebene unmittelbar über dem betreffenden Element. Wenn Sie über eine unregelmäßige Hierarchie verfügen, können Sie festlegen, ob die fehlenden Elemente sichtbar sind und wie sie angezeigt werden sollen. Weitere Informationen finden Sie unter [Unregelmäßige Hierarchien](../../analysis-services/multidimensional-models/ragged-hierarchies.md).  
  
> [!NOTE]  
>  Weitere Informationen zu Leistungsproblemen im Zusammenhang mit dem Design und der Konfiguration von benutzerdefinierten Hierarchien finden Sie im [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## Siehe auch  
 [Eigenschaften der Benutzerhierarchie](../Topic/User%20Hierarchy%20Properties.md)   
 [Ebeneneigenschaften [Erneuert]](../Topic/Level%20Properties%20-%20user%20hierarchies.md)   
 [Über- und untergeordnete Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimensions.md)  
  
  