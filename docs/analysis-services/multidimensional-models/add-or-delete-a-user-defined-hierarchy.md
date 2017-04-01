---
title: "Hinzuf&#252;gen oder L&#246;schen einer benutzerdefinierten Hierarchie | Microsoft Docs"
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
  - "Hierarchien [Analysis Services], hinzufügen"
  - "Entfernen von Hierarchien"
  - "Hinzufügen von Hierarchien"
  - "Löschen von Hierarchien"
  - "Hierarchien [Analysis Services], entfernen"
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
caps.latest.revision: 51
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Hinzuf&#252;gen oder L&#246;schen einer benutzerdefinierten Hierarchie
  Zum Hinzufügen oder Entfernen einer benutzerdefinierten Hierarchie zu bzw. aus einer Dimension verwenden Sie die Registerkarte **Dimensionsstruktur** im Dimensions-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Wenn Sie eine benutzerdefinierte Hierarchie hinzufügen, steht diese den Benutzern erst dann zur Verfügung, wenn sie in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz instanziiert und die Dimension verarbeitet wurde. Weitere Informationen finden Sie unter [Mehrdimensionale Modelldatenbanken &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) und [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### So fügen Sie einer Dimension eine benutzerdefinierte Hierarchie hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das entsprechende [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt und danach die Dimension, mit der Sie arbeiten möchten.  
  
     Die Dimension wird im Dimensions-Designer auf der Registerkarte **Dimensionsstruktur** geöffnet.  
  
2.  Ziehen Sie das Attribut, das Sie in der benutzerdefinierten Hierarchie verwenden möchten, aus dem Bereich **Attribute** in den Bereich **Hierarchien**.  
  
3.  Ziehen Sie zusätzliche Attribute in den Bereich, um Ebenen in der benutzerdefinierten Hierarchie zu bilden.  
  
     Die Reihenfolge, in der Attribute in der Hierarchie aufgeführt sind, spielt eine wichtige Rolle. Beispielsweise sollten in einer Zeithierarchie Jahre in der Hierarchieliste höher angezeigt werden als Tage.  
  
4.  Wahlweise können Sie die Ebenen in der benutzerdefinierten Hierarchie auch neu anordnen, indem Sie sie an die jeweils gewünschte Position ziehen.  
  
5.  Sie haben auch die Möglichkeit, Eigenschaften der benutzerdefinierten Hierarchie oder deren Ebenen zu ändern.  
  
     So empfiehlt es sich beispielsweise, einen Namen für die benutzerdefinierte Hierarchie anzugeben, eine oder mehrere Ebenen umzubenennen und einen benutzerdefinierten Namen für die Alle-Ebene zu definieren. Weitere Informationen finden Sie unter [Eigenschaften der Benutzerhierarchie](../Topic/User%20Hierarchy%20Properties.md), und [Ebeneneigenschaften [Erneuert]](../Topic/Level%20Properties%20-%20user%20hierarchies.md).  
  
    > [!NOTE]  
    >  Standardmäßig ist eine benutzerdefinierte Hierarchie lediglich ein Pfad, in dem Benutzer nach Informationen suchen können. Wenn jedoch Beziehungen zwischen Ebenen vorhanden sind, können Sie die Abfrageleistung verbessern, indem Sie Attributbeziehungen zwischen Ebenen konfigurieren. Weitere Informationen finden Sie unter [Attributbeziehungen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) und [Definieren von Attributbeziehungen](../../analysis-services/multidimensional-models/define-attribute-relationships.md).  
  
### So entfernen Sie eine benutzerdefinierte Hierarchie aus einer Dimension  
  
-   Klicken Sie auf der Registerkarte **Dimensionsstruktur** im Bereich **Hierarchien** auf die benutzerdefinierte Hierarchie, die Sie entfernen möchten. Klicken Sie auf der Symbolleiste auf **Löschen**.  
  
     – oder –  
  
-   Klicken Sie im Bereich **Hierarchien** mit der rechten Maustaste auf die benutzerdefinierte Hierarchie, die Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
     – oder –  
  
-   Ziehen Sie die benutzerdefinierte Hierarchie von der Entwurfsoberfläche weg.  
  
## Siehe auch  
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/create-user-defined-hierarchies.md)  
  
  