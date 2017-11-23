---
title: Erstellen von benannten Mengen in MDX (Multidimensional Expressions) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
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
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 382c4f44f40ad89266a26695109111a185719b2d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-named-sets---building-named-sets"></a>MDX benannte Mengen - Erstellen von benannten Mengen
  Ein Mengenausdruck kann aus einer langen und komplexen und deshalb schwer verständlichen Deklaration bestehen. Wenn ein Mengenausdruck häufig verwendet wird, kann das wiederholte Definieren der Menge lästig werden. Um das Verwenden längerer, komplexer oder häufig verwendeter Ausdrücke zu vereinfachen, ermöglicht MDX (Multidimensional Expressions) die Definition eines solchen Ausdrucks als *benannte Menge*.  
  
 Grundsätzlich handelt es sich bei einer benannten Menge um einen Mengenausdruck, dem ein Alias zugewiesen wurde. Eine benannte Menge kann alle Elemente oder Funktionen enthalten, die normalerweise in eine Menge aufgenommen werden können. Da der Alias der benannten Menge von MDX als Mengenausdruck behandelt wird, können Sie den Alias überall verwenden, wo ein Mengenausdruck zulässig ist.  
  
 Sie können eine benannte Menge in einem der folgenden Kontexte definieren:  
  
-   **Im Bereich einer Abfrage** Mit dem WITH-Schlüsselwort können Sie eine benannte Menge erstellen, die als Teil einer MDX-Abfrage definiert ist und deren Bereich daher auf die Abfrage beschränkt ist. Anschließend können Sie die benannte Menge in einer SELECT-Anweisung von MDX verwenden. Bei dieser Vorgehensweise kann die mit dem WITH-Schlüsselwort erstellte benannte Menge geändert werden, ohne dass die SELECT-Anweisung davon beeinflusst wird.  
  
     Weitere Informationen zum Erstellen benannter Mengen mithilfe des WITH-Schlüsselworts finden Sie unter [Erstellen benannter Mengen im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **Im Bereich einer Sitzung** Mit der CREATE SET-Anweisung können Sie eine benannte Menge erstellen, deren Bereich über den Kontext der Abfrage hinausgeht, d.h., deren Bereich die Dauer der MDX-Sitzung ist. Eine mit der CREATE SET-Anweisung definierte benannte Menge ist für alle MDX-Abfragen in dieser Sitzung verfügbar. Die CREATE SET-Anweisung ist z. B. in einer Clientanwendung sinnvoll, die die gleiche Menge in unterschiedlichen Abfragen wiederverwendet.  
  
     Weitere Informationen zum Erstellen benannter Mengen in einer Sitzung mithilfe der CREATE SET-Anweisung finden Sie unter [Erstellen benannter Mengen im Bereich einer Sitzung &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Erstellen Sie die SET-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-set.md)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
