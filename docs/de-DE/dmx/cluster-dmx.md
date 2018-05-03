---
title: Cluster (DMX) | Microsoft Docs
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
- Cluster
dev_langs:
- DMX
helpviewer_keywords:
- Cluster function
ms.assetid: 14b2942a-6dec-4dfa-98a6-697a3c89036a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: fed486ce6ec5ad2a2b0edf1f470734ae40e8c2e3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den Cluster zurück, der mit der höchsten Wahrscheinlichkeit den Eingabefall enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Gilt für  
 Diese Funktion kann nur verwendet werden, wenn das zugrunde liegende Data Mining-Modell Cluster unterstützt.  
  
## <a name="return-type"></a>Rückgabetyp  
 Die **Cluster** Funktion keine Parameter erfordert.  
  
 Die **Cluster** Funktion gibt einen Skalarwert eines Clusternamens zurück. Jedoch, wenn Sie diese Funktion als Argument einer anderen Funktion verwenden, Sie müssen unter Berücksichtigung als eine \<cluster Spaltenverweis >.  
  
## <a name="remarks"></a>Hinweise  
 **Cluster** kann auch verwendet werden, als ein `<`cluster Spaltenverweis`>` für eine **"PredictHistogram"** Funktion.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Singleton-Abfrage mit der ["PredictHistogram" &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) und -Funktionen, um die Entfernung des einzelnen Falls von jedem Cluster des Miningmodells TM Clustering zurückzugeben und die die Wahrscheinlichkeit, dass die einzelnen Groß-/Kleinschreibung in jedem Cluster vorhanden ist.  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
