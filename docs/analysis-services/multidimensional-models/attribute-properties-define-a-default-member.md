---
title: Definieren eines Standardelements | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 642c8ceb45d5a756f8fad396d0fb1bf48138afb0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---define-a-default-member"></a>Attributeigenschaften – Definieren eines Standardelements
  Das Standardelement einer Attributhierarchie wird zum Auswerten von Ausdrücken verwendet, wenn eine Attributhierarchie nicht in einer Abfrage enthalten ist. Das Standardelement wird ignoriert, wenn eine Abfrage eine Attributhierarchie oder eine benutzerdefinierte Hierarchie einschließt, die das Quellattribut der Attributhierarchie enthält. Der Grund dafür ist, dass hier das in der Abfrage angegebene Element verwendet wird.  
  
 Das Standardelement einer Attributhierarchie wird festgelegt, indem ein Attributelement als **DefaultMember** -Eigenschaftswert der Attributhierarchie angegeben wird. Diese Eigenschaft legen Sie auf der Registerkarte Dimensionsstruktur des Dimensions-Designers oder im Kalkulationsskript auf der Registerkarte Berechnung des Cube-Designers in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fest. Sie können die **DefaultMember** -Eigenschaft auch für eine Sicherheitsrolle angeben (und damit das für die Dimension festgelegte Standardelement überschreiben). Öffnen Sie dazu während der Definition der Dimensionssicherheit die Registerkarte „Dimensionsdaten“. Wenn Sie Namensauflösungsprobleme in folgenden Situationen vermeiden möchten, definieren Sie das Standardelement im MDX-Skript des Cubes: wenn der Cube mehr als einmal auf eine Datenbankdimension verweist; wenn die Dimension im Cube einen anderen Namen aufweist als die Dimension in der Datenbank; wenn Sie in verschiedenen Cubes verschiedene Standardelemente verwenden möchten.  
  
 Das Standardelement eines Attributs wird zum Auswerten von Ausdrücken verwendet, wenn ein Attribut nicht in einer Abfrage enthalten ist. Das Standardelement eines Attributs wird durch die **DefaultMember** -Eigenschaft des Attributs angegeben. Wenn eine Hierarchie aus einer Dimension in einer Abfrage enthalten ist, werden alle Standardelemente von Attributen ignoriert, die Ebenen in der Hierarchie entsprechen. Ist keine Hierarchie aus einer Dimension in einer Abfrage enthalten, werden für alle Attribute in der Dimension Standardelemente verwendet.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Auflösen des Standardelements, wenn kein Standardelement angegeben ist  
 Wird für eine Attributhierarchie kein Standardelement angegeben, und kann die Attributhierarchie aggregiert werden (die **IsAggregatable** -Eigenschaft des Attributs ist auf **TRUE**festgelegt), ist das (Alle)-Element das Standardelement. Wird kein Standardelement angegeben, und kann die Attributhierarchie nicht aggregiert werden (die **IsAggregatable** -Eigenschaft des Attributs ist auf **FALSE**festgelegt), wird ein Standardelement aus der obersten Ebene der Attributhierarchie ausgewählt.  
  
## <a name="specifying-the-default-member"></a>Festlegen des Standardelements  
 Jedes Attribut in einer Dimension von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] besitzt ein Standardelement, das Sie mithilfe der **DefaultMember** -Eigenschaft für ein Attribut angeben können. Diese Einstellung wird zum Auswerten von Ausdrücken verwendet, wenn ein Attribut nicht in einer Abfrage enthalten ist. Legt eine Abfrage eine Hierarchie in einer Dimension fest, werden die Standardelemente für die Attribute in der Hierarchie ignoriert. Legt eine Abfrage keine Hierarchie in einer Dimension fest, treten die **DefaultMember** -Einstellungen für Dimensionsattribute in Kraft.  
  
 Ist die **DefaultMember** -Einstellung für ein Attribut leer und die **IsAggregatable** -Eigenschaft ist auf **True**festgelegt, gilt das Alle-Element als Standardelement. Wird die **Is Aggregatable** -Eigenschaft auf **False**festgelegt, ist das Standardelement das erste Element der ersten sichtbaren Ebene.  
  
 Die **DefaultMember** -Einstellung für ein Attribut gilt für jede Hierarchie, an der das Attribut beteiligt ist. Sie können für verschiedene Hierarchien in einer Dimension keine unterschiedlichen Einstellungen verwenden. Wenn beispielsweise das Element [1998] das Standardelement für ein [Year]-Attribut ist, gilt diese Einstellung für jede Hierarchie in der Dimension. Die **DefaultMember** -Einstellung kann in diesem Fall nicht [1998] in einer Hierarchie und [1997] in einer anderen Hierarchie sein.  
  
 Wenn Sie ein Standardelement für eine bestimmte Ebene in einer Hierarchie definieren, das nicht auf natürliche Weise aggregiert, müssen Sie in allen Ebenen über dieser Ebene in der Hierarchie Standardelemente definieren. So können Sie beispielsweise in der Hierarchie All-Countries–Climate nur dann ein Standardelement für Climate festlegen, wenn Sie auch ein Standardelement für Countries definieren. Tun Sie dies nicht, führt dies zu Abfragezeitfehlern.  
  
 Wenn Ebenen in einer Hierarchie natürlich aggregieren, können Sie ein Standardelement für ein beliebiges Attribut in der Hierarchie definieren, ohne andere Attribute in der Hierarchie berücksichtigen zu müssen. In der Hierarchie Country-Province-City können Sie beispielsweise ein Standardelement für City wie [City].[Montreal] definieren, ohne das Standardelement für State oder für Country definieren zu müssen.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren der Ebene &#40;Alle&#41; für Attributhierarchien](../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
