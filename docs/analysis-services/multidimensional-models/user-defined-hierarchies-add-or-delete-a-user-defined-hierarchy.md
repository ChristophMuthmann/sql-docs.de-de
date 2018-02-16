---
title: "Hinzufügen oder Löschen einer benutzerdefinierten Hierarchie | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: efa987972b10642f176e96bd93a9deee58aa06ec
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="user-defined-hierarchies---add-or-delete-a-user-defined-hierarchy"></a>Benutzerdefinierte Hierarchien - hinzufügen oder Löschen einer benutzerdefinierten Hierarchie
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Zum Hinzufügen oder Entfernen einer benutzerdefinierten Hierarchie zu bzw. aus einer Dimension verwenden Sie die Registerkarte **Dimensionsstruktur** im Dimensions-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Wenn Sie eine benutzerdefinierte Hierarchie hinzufügen, steht diese den Benutzern erst dann zur Verfügung, wenn sie in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz instanziiert und die Dimension verarbeitet wurde. Weitere Informationen finden Sie unter [Mehrdimensionale Modelldatenbanken &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) und [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>So fügen Sie einer Dimension eine benutzerdefinierte Hierarchie hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das entsprechende [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt und danach die Dimension, mit der Sie arbeiten möchten.  
  
     Die Dimension wird im Dimensions-Designer auf der Registerkarte **Dimensionsstruktur** geöffnet.  
  
2.  Ziehen Sie das Attribut, das Sie in der benutzerdefinierten Hierarchie verwenden möchten, aus dem Bereich **Attribute** in den Bereich **Hierarchien** .  
  
3.  Ziehen Sie zusätzliche Attribute in den Bereich, um Ebenen in der benutzerdefinierten Hierarchie zu bilden.  
  
     Die Reihenfolge, in der Attribute in der Hierarchie aufgeführt sind, spielt eine wichtige Rolle. Beispielsweise sollten in einer Zeithierarchie Jahre in der Hierarchieliste höher angezeigt werden als Tage.  
  
4.  Wahlweise können Sie die Ebenen in der benutzerdefinierten Hierarchie auch neu anordnen, indem Sie sie an die jeweils gewünschte Position ziehen.  
  
5.  Sie haben auch die Möglichkeit, Eigenschaften der benutzerdefinierten Hierarchie oder deren Ebenen zu ändern.  
  
     So empfiehlt es sich beispielsweise, einen Namen für die benutzerdefinierte Hierarchie anzugeben, eine oder mehrere Ebenen umzubenennen und einen benutzerdefinierten Namen für die Alle-Ebene zu definieren. Weitere Informationen finden Sie unter [Eigenschaften der Benutzerhierarchie](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md), und [Ebeneneigenschaften [Erneuert]](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md).  
  
    > [!NOTE]  
    >  Standardmäßig ist eine benutzerdefinierte Hierarchie lediglich ein Pfad, in dem Benutzer nach Informationen suchen können. Wenn jedoch Beziehungen zwischen Ebenen vorhanden sind, können Sie die Abfrageleistung verbessern, indem Sie Attributbeziehungen zwischen Ebenen konfigurieren. Weitere Informationen finden Sie unter [Attributbeziehungen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) und [Definieren von Attributbeziehungen](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>So entfernen Sie eine benutzerdefinierte Hierarchie aus einer Dimension  
  
-   Klicken Sie auf der Registerkarte **Dimensionsstruktur** im Bereich **Hierarchien** auf die benutzerdefinierte Hierarchie, die Sie entfernen möchten. Klicken Sie auf der Symbolleiste auf **Löschen**.  
  
     – oder –  
  
-   Klicken Sie im Bereich **Hierarchien** mit der rechten Maustaste auf die benutzerdefinierte Hierarchie, die Sie entfernen möchten, und klicken Sie anschließend auf **Löschen**.  
  
     – oder –  
  
-   Ziehen Sie die benutzerdefinierte Hierarchie von der Entwurfsoberfläche weg.  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
  
  
