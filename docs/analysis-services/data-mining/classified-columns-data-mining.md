---
title: "Klassifizierte Spalten [Data Mining] | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Inhaltstypen [Data Mining]"
  - "STDEV (Spalte)"
  - "VARIANCE (Spalte)"
  - "PROBABLILITY (Spalte)"
  - "PROBABILITY_STDEV (Spalte)"
  - "Spalten [Data Mining], klassifiziert"
  - "Klassifizierte Spalten [Data Mining]"
  - "PROBABILITY_VARIANCE (Spalte)"
  - "SUPPORT (Spalte)"
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 26
---
# Klassifizierte Spalten [Data Mining]
  Wenn Sie eine klassifizierte Spalte definieren, erstellen Sie eine Beziehung zwischen der aktuellen Spalte und eine andere Spalte in der Miningstruktur. Die Daten in der Miningstrukturspalte, die Sie als klassifizierte Spalte festlegen, enthält Kategorieinformationen zur Beschreibung der Werte in einer anderen Spalte der Miningstruktur.  
  
 Angenommen, Sie verfügen über zwei Spalten mit numerischen Daten: die Spalte [Jährliche Käufe] enthält die gesamten jährlichen Käufe pro Kunde für ein bestimmtes Kalenderjahr, und die andere Spalte [Standardabweichungen] enthält die Standardabweichungen für diese Werte. In diesem Fall könnten Sie die Spalte [Jährliche Käufe] als klassifizierte Spalte festlegen, und das Modell wäre in der Lage, diese Beziehung in der Analyse zu verwenden.  
  
> [!NOTE]  
>  Von den in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellten Algorithmen werden klassifizierte Spalten nicht unterstützt. Diese Funktion wird für die Erstellung benutzerdefinierter Algorithmen bereitgestellt.  
  
## Definieren einer klassifizierten Spalte  
 Der Datentyp für eine klassifizierte Spalte muss entweder **Long** oder **Double**sein.  
  
 In der folgenden Liste werden die Inhaltstypen beschrieben, die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für klassifizierte Spalten unterstützt.  
  
 **PROBABILITY**  
 Der Wert in der Spalte entspricht der Wahrscheinlichkeit des zugeordneten Wertes und ist eine Zahl zwischen 0 und 1.  
  
 **VARIANCE**  
 Der Wert in der Spalte entspricht der Varianz des zugeordneten Wertes.  
  
 **STDEV**  
 Der Wert in der Spalte entspricht der Standardabweichung des zugeordneten Wertes.  
  
 **PROBABILITY_VARIANCE**  
 Der Wert in der Spalte entspricht der Varianz der Wahrscheinlichkeit des zugeordneten Wertes.  
  
 **PROBABILITY_STDEV**  
 Der Wert in der Spalte entspricht der Standardabweichung der Wahrscheinlichkeit des zugeordneten Wertes.  
  
 **Alias**  
 Der Wert in der Spalte entspricht der Gewichtung oder dem Fallreplikationsfaktor des zugeordneten Wertes.  
  
## Siehe auch  
 [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Datentypen &#40;Data Mining&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  