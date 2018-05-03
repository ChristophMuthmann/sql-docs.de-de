---
title: PredictCaseLikelihood (DMX) | Microsoft Docs
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
f1_keywords:
- PredictCaseLikelihood
dev_langs:
- DMX
helpviewer_keywords:
- PredictCaseLikelihood function
ms.assetid: b00180e5-b2eb-49e2-891d-e39fb378f50a
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 06300993d36eb81c6db93e656a7d9ea4cf6e9ff9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Diese Funktion gibt die Wahrscheinlichkeit zurück, mit der ein Eingabefall in ein vorhandenes Modell passt. Wird nur mit Clustermodellen verwendet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>Argumente  
 NORMALIZED  
 Der Rückgabewert enthält die Wahrscheinlichkeit des Falls im Modell geteilt durch die Wahrscheinlichkeit des Falls ohne Modell.  
  
 NONNORMALIZED  
 Der Rückgabewert enthält die interne Wahrscheinlichkeit des Falls, bei der es sich um das Produkt aus den Wahrscheinlichkeiten der Fallattribute handelt.  
  
## <a name="applies-to"></a>Gilt für  
 Modelle, die mit basieren die [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering und [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering-Algorithmus.  
  
## <a name="return-type"></a>Rückgabetyp  
 Eine Gleitkommazahl doppelter Genauigkeit zwischen 0 und 1. Bei einer Zahl, die näher an 1 liegt, steigt die Wahrscheinlichkeit, dass der Fall in diesem Modell auftritt. Bei einer Zahl, die näher an 0 liegt, sinkt die Wahrscheinlichkeit, dass der Fall in diesem Modell auftritt.  
  
## <a name="remarks"></a>Hinweise  
 Standardmäßig ist das Ergebnis der **PredictCaseLikelihood** Funktion normalisiert wird. Normalisierte Werte sind in der Regel nützlicher, weil die Anzahl von Attributen in einem Fall zunimmt und die Unterschiede zwischen den internen Wahrscheinlichkeiten zweier Fälle erheblich geringer werden.  
  
 Die folgende Gleichung dient zur Berechnung der normalisierten Werte, wobei X und Y gegeben sind:  
  
-   x = Wahrscheinlichkeit für den Fall auf Grundlage des Clusteringmodells  
  
-   y = Marginale Fallwahrscheinlichkeit, berechnet als logarithmische Wahrscheinlichkeit des Falls auf Grundlage der Zählung der Trainingsfälle  
  
-   Z = Exp(log(x) – Log(Y))  
  
 Normalisiert = (Z / (1 + Z))  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Wahrscheinlichkeit zurückgegeben, mit der der angegebene Fall innerhalb des Clustermodells auftritt, das auf der [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW-Datenbank basiert.  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Erwartete Ergebnisse:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6,30672792729321E-08|6,30672792729321E-08|9,5824454056846E-48|  
  
 Der Unterschied zwischen diesen Ergebnissen veranschaulicht den Effekt der Normalisierung. Der Rohwert für **CaseLikelihood** schlägt vor, dass die Wahrscheinlichkeit des Falles ungefähr 20 Prozent; Wenn Sie die Ergebnisse normalisieren, es jedoch ersichtlich ist wird, dass die Wahrscheinlichkeit des Falls gering ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Algorithmen & #40; Analysis Services – Datamining & #41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
