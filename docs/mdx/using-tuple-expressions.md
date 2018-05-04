---
title: Verwenden von Tupelausdrücken | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- single-member tuples [MDX]
- expressions [MDX], tuples
- one-member tuples
- tuples
- implicit tuples
ms.assetid: 0b802b76-9123-405e-ae43-d438754724ba
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: fba6675213e513806f27c85fe881fc3efdeb0166
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-tuple-expressions"></a>Verwenden von Tupelausdrücken
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ein Tupel besteht aus einem Mitglied aus jeder Dimension, die in einem Cube enthalten ist. Daher kennzeichnet ein Tupel eine einzelne Zelle im Cube eindeutig.  
  
> [!NOTE]  
>  Ein Tupel, das auf ein oder mehrere Elemente verweist, die nicht gültig sind, wird als leeres Tupel bezeichnet.  
  
 Der vollständige Ausdruck eines Tupelbezeichners besteht aus einem oder mehreren explizit angegebenen Elementen, die in Klammern stehen:  
  
 (*Member_expression* [,*Member_expression* ...])  
  
 Ein Tupel kann vollqualifiziert sein, kann implizite Elemente enthalten oder kann ein einzelnes Element enthalten.  
  
## <a name="tuples-and-implicit-members"></a>Tupel und implizite Elemente  
 Ein Tupel, das explizit ein einzelnes Element aus jeder Dimension angibt, die in einem Cube enthalten ist, wird als vollqualifiziertes Tupel bezeichnet. Ein Tupel muss aber nicht vollqualifiziert sein.  
  
 Auf jede Dimension, auf die in einem Tupel nicht explizit verwiesen wird, wird implizit verwiesen. Das Element der Dimension, auf die implizit verwiesen wird, hängt von der Struktur der Dimension und den darin definierten Attributbeziehungen ab. Wenn es in der gleichen Dimension des impliziten Hierarchiebezugs einen expliziten Hierarchiebezug gibt und zwischen den beiden Hierarchien eine direkte oder indirekte Beziehung definiert ist, verhält sich das Tupel, als enthielte es das Element in der Hierarchie, auf die implizit verwiesen wird, die mit dem Element in der Hierarchie vorhanden ist, auf die explizit verwiesen wird.  Wenn z. B. ein Cube eine Kundendimension mit Stadt- und Landattributen enthält und eine Beziehung zwischen beiden Attributen definiert ist, so dass eine Stadt zu genau einem Land gehört, ein Land jedoch mehrere Städte haben kann, stellt die explizite Einbeziehung der Stadt „London“ in ein Tupel einen impliziten Bezug für das Land „England“ her. Wenn jedoch keine Attributbeziehung definiert ist, die Beziehung umgekehrt ist (obwohl Stadt und Land in Beziehung stehen, können Sie z.  B. aus dem Land, in dem jemand lebt, nicht ableiten, in welcher Stadt er lebt) oder keine direkte Beziehung zwischen den beiden Attributen definiert ist (eine Beziehung kann zwischen Kunde und Stadt sowie zwischen Kunde und Land bestehen, ohne dass eine Beziehung zwischen Stadt und Land definiert ist), gelten folgende Regeln:  
  
-   Hat die Hierarchie, auf die implizit verwiesen wird, ein Standardelement, wird dem Tupel das Standardelement hinzugefügt.  
  
-   Wenn die Hierarchie implizit verwiesen wird, kein Standardelement, hat die **(alle)** Mitglied der Standardhierarchie verwendet wird.  
  
-   Hat die Hierarchie, auf die implizit verwiesen wird, kein Standardelement, wird das erste Element der obersten Ebene der Hierarchie verwendet.  
  
## <a name="one-member-tuples"></a>Tupel mit einem Element  
 Wenn der Tupelausdruck nur ein Element hat, konvertiert MDX das Element zum Auswerten des Ausdrucks in ein Tupel mit einem Element. Anders formuliert heißt das, der Elementausdruck `[Measures].[TestMeasure]` ist, wird er statt eines Tupelausdrucks bereitgestellt, funktional identisch mit dem Tupelausdruck `( [Measures].[TestMeasure] ).`  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40;MDX&#41;](../mdx/expressions-mdx.md)   
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
