---
title: Inhaltstypen (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], content types
- content types [DMX]
- DMX [Analysis Services], content types
ms.assetid: ab9dd887-df8d-4878-96b0-635881892573
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5641f8debd2d7dae100f8ea116b4411ea26b79d1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="content-types-dmx"></a>Inhaltstypen (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Data Mining-Algorithmen benötigen über den Datentyp hinausgehende, zusätzliche Informationen, damit sie richtig ausgewertet werden können, z. B. den Inhaltstyp. Der Inhaltstyp unterstützt dabei, für den jeweiligen Algorithmus zu ermitteln, wie die Daten in der Spalte verarbeitet werden sollen.  
  
 Jeder Algorithmus unterstützt bestimmte Inhaltstypen. Beispielsweise kann der [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes-Algorithmus keine kontinuierlichen Spalten verwenden. Wenn Sie eine kontinuierliche Spalte in einem [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes-Modell verwenden möchten, müssen Sie die Daten in der Spalte diskretisieren. Für einige Algorithmen sind bestimmte Inhaltstypen erforderlich, damit sie richtig funktionieren. Beispielsweise ist für den [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series-Algorithmus eine Schlüsselzeitspalte erforderlich, um die Zeitspanne zu kennzeichnen, in der die Daten gesammelt wurden.  
  
 Eine vollständige Beschreibung des Inhalts Datentypen [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt, finden Sie unter [Content Types &#40; Data Mining &#41;](../analysis-services/data-mining/content-types-data-mining.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datamining-Algorithmen &#40; Analysis Services – Datamining &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Understanding the DMX Select Statement (Grundlegendes zur SELECT-Anweisung)](../dmx/understanding-the-dmx-select-statement.md)  
  
  
