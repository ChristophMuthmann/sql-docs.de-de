---
title: "Erstellen von Zellenberechnungen in MDX (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Berechnete Zellen [MDX]"
  - "Abfragen [MDX], Zellenberechnungen"
  - "Zellen [MDX]"
  - "MDX [Analysis Services], Berechnungen"
  - "Berechnungsteilcubes [MDX]"
  - "Berechnete Werte [MDX]"
  - "Mehrdimensionale Ausdrücke [Analysis Services], Zellenberechnungen"
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Erstellen von Zellenberechnungen in MDX (MDX)
  MDX (Multidimensional Expressions) stellt eine Reihe von Tools zum Generieren berechneter Werte bereit, wie z. B. berechnete Elemente, benutzerdefinierte Rollups und benutzerdefinierte Elemente. Allerdings ist es schwierig, mithilfe dieser Funktionen eine bestimmte Menge von Zellen oder eine einzelne Zelle zu beeinflussen.  
  
 Wenn Sie berechnete Werte für bestimmte Zellen generieren möchten, sollten Sie die Funktion für berechnete Zellen in MDX verwenden. Mit berechneten Zellen können Sie einen bestimmten Slice von Zellen definieren, der als *Berechnungsteilcube*bezeichnet wird, und eine Formel auf jede einzelne Zelle im Berechnungsteilcube anwenden, wobei eine optionale Bedingung zugrunde liegt, die auf jede Zelle angewendet werden kann.  
  
 Berechnete Zellen stellen außerdem eine komplexe Funktionalität bereit, z. B. zielsuchende Formeln (wie sie in KPIs verwendet werden) oder Formeln für spekulative Analysen. Dieses Maß an Funktionalität ergibt sich aus der Funktion der Durchlaufreihenfolge in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , die es ermöglicht, dass rekursive Durchläufe mit berechneten Zellen ausgeführt werden, wobei Berechnungsformeln auf bestimmte Durchläufe in der Durchlaufreihenfolge angewendet werden. Weitere Informationen zur Durchlaufreihenfolge finden Sie unter [Grundlegendes zu Durchlauf- und Lösungsreihenfolge &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/understanding-pass-order-and-solve-order-mdx.md).  
  
 In Bezug auf den Gültigkeitsbereich sind berechnete Zellen sowohl mit benannten Mengen als auch mit berechneten Elementen vergleichbar, da berechnete Zellen temporär für die Dauer einer Sitzung oder einer einzelnen Abfrage erstellt oder global als Teil eines Cubes zur Verfügung gestellt werden können.  
  
-   **Im Bereich einer Abfrage** Mit dem WITH-Schlüsselwort können Sie eine berechnete Zelle erstellen, die als Teil einer MDX-Abfrage definiert ist und deren Bereich somit auf die Abfrage beschränkt ist. Anschließend können Sie die berechnete Zelle in einer MDX-SELECT-Anweisung verwenden. Bei dieser Vorgehensweise kann die mit dem **WITH** -Schlüsselwort erstellte berechnete Zelle geändert werden, ohne dass die SELECT-Anweisung davon beeinflusst wird.  
  
     Weitere Informationen zum Erstellen berechneter Elemente mithilfe des WITH-Schlüsselworts finden Sie unter [Erstellen von Zellenberechnungen im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-cell-calculations-mdx.md).  
  
-   **Im Bereich einer Sitzung** Mit der CREATE CELL CALCULATION- oder der ALTER CUBE-Anweisung können Sie ein berechnetes Element erstellen, dessen Bereich mehr als den Kontext der Abfrage umfasst, dessen Bereich nämlich die Dauer der MDX-Sitzung ist.  
  
     Weitere Informationen zum Erstellen berechneter Elemente in einer Sitzung mithilfe der CREATE CELL CALCULATION- oder der ALTER CUBE-Anweisung finden Sie unter [Erstellen berechneter Zellen im Bereich einer Sitzung](../../../analysis-services/multidimensional-models/mdx/creating-session-scoped-calculated-cells.md).  
  
## Siehe auch  
 [ALTER CUBE-Anweisung &#40;MDX&#41;](../Topic/ALTER%20CUBE%20Statement%20\(MDX\).md)   
 [CREATE CELL CALCULATION-Anweisung &#40;MDX&#41;](../Topic/CREATE%20CELL%20CALCULATION%20Statement%20\(MDX\).md)   
 [Erstellen von Zellenberechnungen im Bereich einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-cell-calculations-mdx.md)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  