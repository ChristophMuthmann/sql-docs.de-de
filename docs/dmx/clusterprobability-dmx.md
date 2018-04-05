---
title: ClusterProbability (DMX) | Microsoft Docs
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
- ClusterProbability
dev_langs:
- DMX
helpviewer_keywords:
- ClusterProbability function
ms.assetid: a6447b3c-94ce-4122-a3eb-6f3827598d8f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d4b85f18478d1cc34050804845f62e2283b57462
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Wahrscheinlichkeit zurück, mit der der Eingabefall zum angegebenen Cluster gehört.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>Gilt für  
 Diese Funktion kann nur verwendet werden, wenn das zugrunde liegende Data Mining-Modell Cluster unterstützt.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert.  
  
## <a name="remarks"></a>Remarks  
 In der folgenden Syntax wird das Schemarowset für den Inhalt eines Miningmodells verwendet, um die Knotenbeschriftungen zurückzugeben, die im Miningmodell vorhanden sind.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 Weitere Informationen zum Verwenden dieser Syntax finden Sie unter [SELECT FROM &#60; Modell &#62;. Inhalt &#40; DMX &#41; ](../dmx/select-from-model-content-dmx.md). Weitere Informationen über Mining Model Content-Schemarowset finden Sie unter [DMSCHEMA_MINING_MODEL_CONTENT-Rowset](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md).  
  
 Wenn eine \<knotenbeschriftung > nicht angegeben ist, wird die Funktion gibt die Wahrscheinlichkeit, dass die eingabefälle zum wahrscheinlichsten Cluster gehören. Verwenden der **Cluster** Funktion, um die wahrscheinlichsten Cluster zurückzugeben.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Wahrscheinlichkeit dafür zurückgegeben, dass der angegebene Fall im Cluster mit der Bezeichnung Cluster 2 enthalten ist.  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Cluster &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
