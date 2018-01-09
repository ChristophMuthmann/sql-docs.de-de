---
title: Klassifizierte Spalten [Datamining] | Microsoft Docs
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
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 02792608fce3f2cca0c1bf78e5215b1a0b607a1e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="classified-columns-data-mining"></a>Klassifizierte Spalten [Data Mining]
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn Sie eine klassifizierte Spalte definieren, erstellen Sie eine Beziehung zwischen der aktuellen Spalte und eine andere Spalte in der Miningstruktur an. Die Daten in der Miningstrukturspalte, die Sie als klassifizierte Spalte festlegen, enthält Kategorieinformationen zur Beschreibung der Werte in einer anderen Spalte der Miningstruktur.  
  
 Angenommen, Sie verfügen über zwei Spalten mit numerischen Daten: die Spalte [Jährliche Käufe] enthält die gesamten jährlichen Käufe pro Kunde für ein bestimmtes Kalenderjahr, und die andere Spalte [Standardabweichungen] enthält die Standardabweichungen für diese Werte. In diesem Fall könnten Sie die Spalte [Jährliche Käufe] als klassifizierte Spalte festlegen, und das Modell wäre in der Lage, diese Beziehung in der Analyse zu verwenden.  
  
> [!NOTE]  
>  Von den in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellten Algorithmen werden klassifizierte Spalten nicht unterstützt. Diese Funktion wird für die Erstellung benutzerdefinierter Algorithmen bereitgestellt.  
  
## <a name="defining-a-classified-column"></a>Definieren einer klassifizierten Spalte  
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
  
## <a name="see-also"></a>Siehe auch  
 [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Datentypen &#40;Data Mining&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  
