---
title: Klassifizierte Spalten [Datamining] | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9fcd5aac5f5384f62b4fe4cd53f480ac70f69a63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="classified-columns-data-mining"></a>Klassifizierte Spalten [Data Mining]
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Wenn Sie eine klassifizierte Spalte definieren, erstellen Sie eine Beziehung zwischen der aktuellen Spalte und eine andere Spalte in der Miningstruktur. Die Daten in der Miningstrukturspalte, die Sie als klassifizierte Spalte festlegen, enthält Kategorieinformationen zur Beschreibung der Werte in einer anderen Spalte der Miningstruktur.  
  
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
 [Content-Arten & #40; Datamining & #41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Miningstrukturen & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Datentypen & #40; Datamining & #41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  
