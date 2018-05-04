---
title: Bewirkt, dass (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEAVES
dev_langs:
- kbMDX
helpviewer_keywords:
- Leaves function
ms.assetid: 09f908aa-1b2d-4af9-8c8d-c023915241b2
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c9ac580c71d1c82876a41953d6f8b5411dc7dd55
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="leaves-mdx"></a>Leaves (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Menge mit allen Attribute zurück (kann optional auf die Attribute einer bestimmten Dimension beschränkt werden) Für alle Attribute x in der zurückgegebenen Menge gilt: Wenn x das Granularitätsattribut ist oder direkt oder indirekt mit diesem verknüpft ist, wird die Granularität ohne Auswirkung auf den Slice für das Attribut x festgelegt. Die **verlässt** Funktion für die Verwendung innerhalb einer SCOPE-Anweisung oder auf der linken Seite einer Zuweisung vorgesehen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Dimension_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Dimension zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Blattelemente sind Tupel, die durch der Cross Join der niedrigsten Ebene aller Attributhierarchien gebildet werden. Berechnete Elemente sind ausgeschlossen.  
  
-   Wenn ein Dimensionsname angegeben wird, die **verlässt** Funktion gibt eine Menge mit die Blattelementen des Schlüsselattributs für die angegebene Dimension zurück.  
  
-   Wenn die Dimension mit mehreren Measuregruppen verknüpft ist, wird die des Measure im aktuellen Geltungsbereich verwendet.  
  
-   Wenn kein Dimensionsname angegeben wird, gibt die Funktion eine Menge mit den Blattelementen des gesamten Cubes zurück.  
  
    > [!NOTE]  
    >  Wenn der Dimensionsname in eine Hierarchie aufgelöst wird und der eindeutige Name der Hierarchie mit dem eindeutigen Dimensionsnamen identisch ist (Cubedimensionseigenschaft HierarchyUniqueNameStyle=ExcludeDimensionName und hierarchy name=dimension name), wird die Dimension verwendet.  
  
    > [!IMPORTANT]  
    >  Wenn nicht alle Attribute die gleiche Granularität für die Measuregruppe im aktuellen Bereich haben, wird ein Fehler erzeugt.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
