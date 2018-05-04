---
title: Erstellen von benannten Mengen in MDX (Multidimensional Expressions) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1890c1965299ba0f7318c7bfa9b47935e3b85fc8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-named-sets---building-named-sets"></a>MDX benannte Mengen - Erstellen von benannten Mengen
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Ein Mengenausdruck kann aus einer langen und komplexen und deshalb schwer verständlichen Deklaration bestehen. Wenn ein Mengenausdruck häufig verwendet wird, kann das wiederholte Definieren der Menge lästig werden. Um das Verwenden längerer, komplexer oder häufig verwendeter Ausdrücke zu vereinfachen, ermöglicht MDX (Multidimensional Expressions) die Definition eines solchen Ausdrucks als *benannte Menge*.  
  
 Grundsätzlich handelt es sich bei einer benannten Menge um einen Mengenausdruck, dem ein Alias zugewiesen wurde. Eine benannte Menge kann alle Elemente oder Funktionen enthalten, die normalerweise in eine Menge aufgenommen werden können. Da der Alias der benannten Menge von MDX als Mengenausdruck behandelt wird, können Sie den Alias überall verwenden, wo ein Mengenausdruck zulässig ist.  
  
 Sie können eine benannte Menge in einem der folgenden Kontexte definieren:  
  
-   **Im Bereich einer Abfrage** Mit dem WITH-Schlüsselwort können Sie eine benannte Menge erstellen, die als Teil einer MDX-Abfrage definiert ist und deren Bereich daher auf die Abfrage beschränkt ist. Anschließend können Sie die benannte Menge in einer SELECT-Anweisung von MDX verwenden. Bei dieser Vorgehensweise kann die mit dem WITH-Schlüsselwort erstellte benannte Menge geändert werden, ohne dass die SELECT-Anweisung davon beeinflusst wird.  
  
     Weitere Informationen zum Erstellen benannter Mengen mithilfe des WITH-Schlüsselworts finden Sie unter [Erstellen benannter Mengen im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **Im Bereich einer Sitzung** Mit der CREATE SET-Anweisung können Sie eine benannte Menge erstellen, deren Bereich über den Kontext der Abfrage hinausgeht, d.h., deren Bereich die Dauer der MDX-Sitzung ist. Eine mit der CREATE SET-Anweisung definierte benannte Menge ist für alle MDX-Abfragen in dieser Sitzung verfügbar. Die CREATE SET-Anweisung ist z. B. in einer Clientanwendung sinnvoll, die die gleiche Menge in unterschiedlichen Abfragen wiederverwendet.  
  
     Weitere Informationen zum Erstellen benannter Mengen in einer Sitzung mithilfe der CREATE SET-Anweisung finden Sie unter [Erstellen benannter Mengen im Bereich einer Sitzung &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT-Anweisung & #40; MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Erstellen Sie die SET-Anweisung & #40; MDX & #41;](../../../mdx/mdx-data-definition-create-set.md)   
 [Grundlegendes zu MDX-Abfrage & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
