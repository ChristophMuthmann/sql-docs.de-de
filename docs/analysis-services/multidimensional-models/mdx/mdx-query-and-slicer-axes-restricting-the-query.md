---
title: "Einschränken der Abfrage mit Abfrage- und Slicerachse (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
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
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b0efaa9f791e125cb6a2b9b139a318a120f969c9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>MDX Abfrage- und Slicerachsen - Einschränken der Abfrage
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Wenn eine SELECT-Anweisung von MDX (Multidimensional Expressions) formulieren durchsucht, werden von einer Anwendung in der Regel r. einen Cube und unterteilt die Menge der Hierarchien in zwei Teilbereiche:  
  
-   **Abfrageachsen**– die Menge der Hierarchien, aus denen Daten für mehrere Elemente abgerufen werden. Weitere Informationen zu den Abfrageachsen finden Sie unter [Angeben des Inhalts einer Abfrageachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   **Slicerachsen**- die Menge der Hierarchien, aus denen Daten für ein einzelnes Element abgerufen werden. Weitere Informationen zu den Slicerachsen finden Sie unter [Angeben des Inhalts einer Slicerachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
 Da Abfrage- und Slicerachsen aus mehreren Hierarchien des abzufragenden Cubes erstellt werden können, wird mit diesen Begriffen unterschieden zwischen den Hierarchien, die im abzufragenden Cube verwendet werden, und den Hierarchien, die im von einer MDX-Abfrage zurückgegebenen Cube erstellt werden.  
  
 Ein einfaches Beispiel mit Verwendung von Abfrage- und Slicerachsen finden Sie unter [Verwenden von Abfrage- und Slicerachsen in einem einfachen Beispiel &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Elementen, Tupeln und Mengen &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
