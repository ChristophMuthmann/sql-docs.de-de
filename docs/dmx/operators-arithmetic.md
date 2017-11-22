---
title: Arithmetische Operatoren (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
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
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords: arithmetic operators
ms.assetid: befe4f0c-e5dd-4ae1-b88e-6ac7aab2181a
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2e376910297723821351570d76c076c15748e0a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="operators---arithmetic"></a>Operatoren – arithmetische Operationen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sie können arithmetische Operatoren in Data Mining Extensions (DMX) für arithmetische Berechnungen in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], z. B. Addition, Subtraktion, Multiplikation und Division.  
  
 In der folgenden Tabelle sind die arithmetischen Operatoren aufgeführt, die DMX unterstützt.  
  
|Operator|Description|  
|--------------|-----------------|  
|[+ &#40; Hinzufügen &#41; &#40; DMX &#41;](../dmx/add-dmx.md)|Addiert zwei Zahlen.|  
|[-&#40; Subtrahieren &#41; &#40; DMX &#41;](../dmx/subtract-dmx.md)|Subtrahiert eine Zahl von einer anderen Zahl.|  
|[&#42; &#40; Multiplizieren Sie &#41; &#40; DMX &#41;](../dmx/multiply-dmx.md)|Multipliziert eine Zahl mit einer anderen Zahl.|  
|[&#40; aufgrund einer Division &#41; &#40; DMX &#41;](../dmx/divide-dmx.md)|Dividiert eine Zahl durch eine andere Zahl.|  
  
 Die folgenden Regeln bestimmen die Rangfolge, die arithmetische Operatoren in einem DMX-Ausdruck haben.  
  
-   Sind in einem Ausdruck mehrere arithmetische Operatoren vorhanden, werden Multiplikationen und Divisionen vor Subtraktionen und Additionen berechnet.  
  
-   Wenn alle arithmetischen Operatoren in einem Ausdruck in der Rangfolge gleichwertig sind, werden sie von links nach rechts ausgewertet.  
  
-   Ausdrücke, die in Klammern stehen, erhalten Vorrang vor allen anderen Operationen.  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Ausdrücke &#40; DMX &#41;](../dmx/expressions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operatoren &#40; DMX &#41;](../dmx/operators-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Understanding the DMX Select Statement (Grundlegendes zur SELECT-Anweisung)](../dmx/understanding-the-dmx-select-statement.md)  
  
  
