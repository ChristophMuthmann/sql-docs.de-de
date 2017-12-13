---
title: Miningmodellspalten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0acbc12c9aa0d553bfee5e9e11dcb098547288c7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mining-model-columns"></a>Miningmodellspalten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Datamining-Modell wendet einen Miningmodellalgorithmus auf die Daten, die durch eine Miningstruktur dargestellt wird. Wie die Miningstruktur enthält das Miningmodell Spalten. Ein Miningmodell ist in der Miningstruktur enthalten und erbt alle Werte der Eigenschaften, die von der Miningstruktur definiert werden. Das Modell kann alle Spalten aus der Miningstruktur oder nur eine Teilmenge der Spalten verwenden.  
  
 Sie können für eine Miningmodellspalte zwei weitere Informationen definieren: Verwendung und Modellierungsflags.  
  
-   Bei der**Verwendung** handelt es sich um eine Eigenschaft, die definiert, wie das Modell die Spalte verwendet. Spalten können als Eingabespalten, Schlüsselspalten oder vorhersagbare Spalten verwendet werden.  
  
-   **Modellierungsflags** stellen weitere Informationen zu den in der Falltabelle definierten Daten für den Algorithmus bereit, sodass der Algorithmus ein genaueres Modell erstellen kann. Modellierungsflags können programmgesteuert in der Sprache Data Mining-Erweiterungen (DMX) oder in **mit dem** Data Mining-Designer [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]definiert werden.  
  
 In der folgenden Liste werden die Modellierungsflags beschrieben, die Sie für eine Miningmodellspalte definieren können.  
  
 **MODEL_EXISTENCE_ONLY**  
 Gibt an, dass das Vorhandensein der Attributs wichtiger ist als die Werte in der Attributspalte. Stellen Sie sich z. B. eine Falltabelle mit einer Bestellelementenliste vor, die einem bestimmten Kunden zugeordnet ist. Die Tabellendaten enthalten für jedes Element Produkttyp, Bezeichner und Kosten. Für die Modellierung kann die Tatsache, dass der Kunde einen bestimmtes Bestellelement erworben hat, wichtiger sein als die Kosten des Bestellelements selbst. In diesem Fall sollte die Cost-Spalte mit **MODEL_EXISTENCE_ONLY**gekennzeichnet werden.  
  
 **REGRESSOR**  
 Zeigt an, dass der Algorithmus die angegebene Spalte in der Regressionsformel von Regressionsalgorithmen verwenden kann. Dieses Flag wird von den Algorithmen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series unterstützt.  
  
 Weitere Informationen zum Festlegen der Verwendungseigenschaft und zum programmgesteuerten Definieren des Modellierungsflags mit DMX finden Sie unter [CREATE MINING MODEL &#40;DMX&#41;](../../dmx/create-mining-model-dmx.md). Weitere Informationen zum Festlegen der Verwendungseigenschaft und zum Definieren des Modellierungsflags in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] finden Sie unter [Verschieben von Data Mining-Objekten](../../analysis-services/data-mining/moving-data-mining-objects.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Ändern der Eigenschaften eines Miningmodells](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [Ausschließen einer Spalte aus einem Miningmodell](../../analysis-services/data-mining/exclude-a-column-from-a-mining-model.md)   
 [Miningstrukturspalten](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
