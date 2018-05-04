---
title: Konfigurieren die Ebene (alle) für Attributhierarchien | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dff6197f4bad933ee4e5abaf5e83e65125df3596
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>Datenbankdimensionen – Konfigurieren der Ebene (alle) für Attributhierarchien
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Die Alle-Ebene in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist eine optionale, vom System generierte Ebene. Sie enthält nur ein Element, dessen Wert die Aggregation der Werte aller Elemente in der direkt untergeordneten Ebene ist. Dieses Element wird als Alle-Element bezeichnet. Das vom System erzeugte Element ist nicht in der Dimensionstabelle enthalten. Da sich das Element in der Gesamtergebnisebene an oberster Stelle in der Hierarchie befindet, ist der Wert des Elements die konsolidierte Aggregation der Werte aller Elemente in der Hierarchie. Das Alle-Element dient häufig als Standardelement einer Hierarchie.  
  
 Ob eine Alle-Ebene in einer Attributhierarchie vorhanden ist, hängt von der Einstellung der **IsAggregatable** -Eigenschaft für das Attribut ab. Ob eine Alle-Ebene in einer benutzerdefinierten Hierarchie vorhanden ist, hängt von der **IsAggregatable** -Eigenschaft des Attributs auf der obersten Ebene der benutzerdefinierten Hierarchie ab. Wenn die **IsAggregatable** -Eigenschaft auf **TRUE**festgelegt ist, ist eine Alle-Ebene vorhanden. In einer Hierarchie ist keine Alle-Ebene vorhanden, wenn die **IsAggregatable** -Eigenschaft auf **FALSE**festgelegt ist.  
  
## <a name="establishing-the-topmost-level"></a>Einrichten der obersten Ebene  
 Wenn die **IsAggregatable** -Eigenschaft für das Quellattribut einer Ebene in einer Hierarchie auf **False** festgelegt ist, kann in der Hierarchie über dieser Ebene keine Aggregatebene vorkommen. Eine Nichtaggregatebene muss die oberste Ebene jeder Hierarchie sein, oder die **IsAggregatable** -Eigenschaft der Quellattribute für alle Ebenen darüber müssen ebenfalls auf **FALSE**festgelegt sein.  
  
## <a name="all-member-and-all-level"></a>Alle-Element und Alle-Ebene  
 Das einzige Element der Alle-Ebene wird als Alle-Element bezeichnet. Die **AttributeAllMemberName**-Eigenschaft einer Dimension gibt den Namen des Elements „Alle“ für Attribute in einer Dimension an. Die **AllMemberName** -Eigenschaft in einer Hierarchie gibt den Namen des Alle-Elements für die Hierarchie an.  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren eines Standardelements](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
