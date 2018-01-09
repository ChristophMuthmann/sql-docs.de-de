---
title: Erstellen von Zellenberechnungen in MDX (Multidimensional Expressions) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8e2e963c47746a85e760b3b4464edd5cbe39f1fe
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-cell-calculations---build-cell-calculations"></a>MDX-Zellenberechnungen - Build Zellenberechnungen
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]MDX (Multidimensional Expressions) bietet Ihnen eine Reihe von Tools zum Generieren berechneter Werte, z. B. berechnete Elemente, benutzerdefinierte Rollups und benutzerdefinierte Elemente. Allerdings ist es schwierig, mithilfe dieser Funktionen eine bestimmte Menge von Zellen oder eine einzelne Zelle zu beeinflussen.  
  
 Wenn Sie berechnete Werte für bestimmte Zellen generieren möchten, sollten Sie die Funktion für berechnete Zellen in MDX verwenden. Mit berechneten Zellen können Sie einen bestimmten Slice von Zellen definieren, der als *Berechnungsteilcube*bezeichnet wird, und eine Formel auf jede einzelne Zelle im Berechnungsteilcube anwenden, wobei eine optionale Bedingung zugrunde liegt, die auf jede Zelle angewendet werden kann.  
  
 Berechnete Zellen stellen außerdem eine komplexe Funktionalität bereit, z. B. zielsuchende Formeln (wie sie in KPIs verwendet werden) oder Formeln für spekulative Analysen. Dieses Maß an Funktionalität ergibt sich aus der Funktion der Durchlaufreihenfolge in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , die es ermöglicht, dass rekursive Durchläufe mit berechneten Zellen ausgeführt werden, wobei Berechnungsformeln auf bestimmte Durchläufe in der Durchlaufreihenfolge angewendet werden. Weitere Informationen zur Durchlaufreihenfolge finden Sie unter [Grundlegendes zu Durchlauf- und Lösungsreihenfolge &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 In Bezug auf den Gültigkeitsbereich sind berechnete Zellen sowohl mit benannten Mengen als auch mit berechneten Elementen vergleichbar, da berechnete Zellen temporär für die Dauer einer Sitzung oder einer einzelnen Abfrage erstellt oder global als Teil eines Cubes zur Verfügung gestellt werden können.  
  
-   **Im Bereich einer Abfrage** Mit dem WITH-Schlüsselwort können Sie eine berechnete Zelle erstellen, die als Teil einer MDX-Abfrage definiert ist und deren Bereich somit auf die Abfrage beschränkt ist. Anschließend können Sie die berechnete Zelle in einer MDX-SELECT-Anweisung verwenden. Bei dieser Vorgehensweise kann die mit dem **WITH** -Schlüsselwort erstellte berechnete Zelle geändert werden, ohne dass die SELECT-Anweisung davon beeinflusst wird.  
  
     Weitere Informationen zum Erstellen berechneter Elemente mithilfe des WITH-Schlüsselworts finden Sie unter [Erstellen von Zellenberechnungen im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md).  
  
-   **Im Bereich einer Sitzung** Mit der CREATE CELL CALCULATION- oder der ALTER CUBE-Anweisung können Sie ein berechnetes Element erstellen, dessen Bereich mehr als den Kontext der Abfrage umfasst, dessen Bereich nämlich die Dauer der MDX-Sitzung ist.  
  
     Weitere Informationen zum Erstellen berechneter Elemente in einer Sitzung mithilfe der CREATE CELL CALCULATION- oder der ALTER CUBE-Anweisung finden Sie unter [Erstellen berechneter Zellen im Bereich einer Sitzung](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER CUBE-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-alter-cube.md)   
 [Erstellen Sie CELL CALCULATION-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Erstellen von Zellenberechnungen im Bereich einer Abfrage &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
