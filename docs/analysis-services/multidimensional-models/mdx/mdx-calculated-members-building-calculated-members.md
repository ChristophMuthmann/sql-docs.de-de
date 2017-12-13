---
title: Erstellen von berechneten Elementen in MDX (Multidimensional Expressions) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 46d11311159db821d44c8999f9f71ba40c82451c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-calculated-members---building-calculated-members"></a>MDX berechnete Elemente - erstellen von berechneten Elementen
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]In MDX (Multidimensional Expressions), ist ein berechnetes Element ein Element, das aufgelöst wird, indem Sie berechnen einen MDX-Ausdruck, um einen Wert zurückzugeben. Diese einfach klingende Definition hat immense Auswirkungen. Die Erstellung und Verwendung von berechneten Elementen in einer MDX-Abfrage eröffnet umfassende Änderungsmöglichkeiten für mehrdimensionale Daten.  
  
 Sie können berechnete Elemente an jedem beliebigen Punkt in einer Hierarchie erstellen. Sie können außerdem berechnete Elemente erstellen, die nicht nur von vorhandenen Elementen in einem Cube abhängen, sondern auch von anderen berechneten Elementen, die in demselben MDX-Ausdruck definiert sind.  
  
 Sie können berechnete Elemente in einem der folgenden Kontexte definieren:  
  
-   **Im Bereich einer Abfrage** : Mit dem WITH-Schlüsselwort können Sie ein berechnetes Element erstellen, das als Teil einer MDX-Abfrage definiert ist und dessen Bereich somit auf die Abfrage beschränkt ist. Anschließend können Sie das berechnete Element in einer SELECT-Anweisung von MDX verwenden. Bei dieser Vorgehensweise kann das mit dem WITH-Schlüsselwort erstellte berechnete Element geändert werden, ohne dass die SELECT-Anweisung davon beeinflusst wird.  
  
     Weitere Informationen zum Erstellen berechneter Elemente mithilfe des WITH-Schlüsselworts finden Sie unter [Erstellen berechneter Elemente im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Im Bereich einer Sitzung**: Mit der CREATE MEMBER-Anweisung können Sie ein berechnetes Element erstellen, dessen Bereich umfangreicher als der Kontext der Abfrage ist, d.h. der Dauer der MDX-Sitzung entspricht. Ein mit der CREATE MEMBER-Anweisung definiertes berechnetes Element ist für alle MDX-Abfragen in dieser Sitzung verfügbar. Die CREATE MEMBER-Anweisung ist z. B. in einer Clientanwendung sinnvoll, die die gleiche Menge in unterschiedlichen Abfragen wiederverwendet.  
  
     Weitere Informationen zum Erstellen berechneter Elemente in einer Sitzung mithilfe der CREATE MEMBER-Anweisung finden Sie unter [Erstellen berechneter Elemente im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE MEMBER-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [MDX-Funktionsreferenz &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
