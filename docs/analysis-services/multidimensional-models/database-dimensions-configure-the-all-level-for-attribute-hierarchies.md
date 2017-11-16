---
title: "Konfigurieren die Ebene (alle) für Attributhierarchien | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2378dafcda0d9eca8786fb81cadfd44b22d0998b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>Datenbankdimensionen – Konfigurieren der Ebene (alle) für Attributhierarchien
  Die Alle-Ebene in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist eine optionale, vom System generierte Ebene. Sie enthält nur ein Element, dessen Wert die Aggregation der Werte aller Elemente in der direkt untergeordneten Ebene ist. Dieses Element wird als Alle-Element bezeichnet. Das vom System erzeugte Element ist nicht in der Dimensionstabelle enthalten. Da sich das Element in der Gesamtergebnisebene an oberster Stelle in der Hierarchie befindet, ist der Wert des Elements die konsolidierte Aggregation der Werte aller Elemente in der Hierarchie. Das Alle-Element dient häufig als Standardelement einer Hierarchie.  
  
 Ob eine Alle-Ebene in einer Attributhierarchie vorhanden ist, hängt von der Einstellung der **IsAggregatable** -Eigenschaft für das Attribut ab. Ob eine Alle-Ebene in einer benutzerdefinierten Hierarchie vorhanden ist, hängt von der **IsAggregatable** -Eigenschaft des Attributs auf der obersten Ebene der benutzerdefinierten Hierarchie ab. Wenn die **IsAggregatable** -Eigenschaft auf **TRUE**festgelegt ist, ist eine Alle-Ebene vorhanden. In einer Hierarchie ist keine Alle-Ebene vorhanden, wenn die **IsAggregatable** -Eigenschaft auf **FALSE**festgelegt ist.  
  
## <a name="establishing-the-topmost-level"></a>Einrichten der obersten Ebene  
 Wenn die **IsAggregatable** -Eigenschaft für das Quellattribut einer Ebene in einer Hierarchie auf **False** festgelegt ist, kann in der Hierarchie über dieser Ebene keine Aggregatebene vorkommen. Eine Nichtaggregatebene muss die oberste Ebene jeder Hierarchie sein, oder die **IsAggregatable** -Eigenschaft der Quellattribute für alle Ebenen darüber müssen ebenfalls auf **FALSE**festgelegt sein.  
  
## <a name="all-member-and-all-level"></a>Alle-Element und Alle-Ebene  
 Das einzige Element der Alle-Ebene wird als Alle-Element bezeichnet. Die **AttributeAllMemberName**-Eigenschaft einer Dimension gibt den Namen des Elements „Alle“ für Attribute in einer Dimension an. Die **AllMemberName** -Eigenschaft in einer Hierarchie gibt den Namen des Alle-Elements für die Hierarchie an.  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren eines Standardelements](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  

