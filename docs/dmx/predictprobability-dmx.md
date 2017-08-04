---
title: PredictProbability (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictProbability
dev_langs:
- DMX
helpviewer_keywords:
- PredictProbability function
ms.assetid: 7bb7e74f-e33b-4f7b-ade8-be21ace0dbd0
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e0cdcf4b193cf1b05967fdbc5b266ebd0ca9700
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Wahrscheinlichkeit für einen bestimmten Status zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Gilt für  
 Ein skalare Spalte.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert.  
  
## <a name="remarks"></a>Hinweise  
 Ist der vorhergesagte Status (predicted state) nicht angegeben, wird der Status verwendet, der die höchste Wahrscheinlichkeit hat, wobei der Bucket der fehlenden Status ausgeschlossen wird. Wenn der Bucket der fehlenden Status einschließen möchten, legen die \<vorhergesagten Status > auf **INCLUDE_NULL**. Um die Wahrscheinlichkeit für die fehlenden Status zurückzugeben, legen die \<vorhergesagten Status > auf NULL.  
  
> [!NOTE]  
>  Einige Miningmodelle stellen keine Wahrscheinlichkeitswerte zur Verfügung und können diese Funktion daher nicht verwenden. Zudem werden Wahrscheinlichkeitswerte für jeden einzelnen Zielwert unterschiedlich berechnet, oder sie können eine in Abhängigkeit von dem abgefragten Modelltyp unterschiedliche Interpretation aufweisen. Weitere Informationen über die Berechnung der Wahrscheinlichkeit für einen bestimmten Modelltyp finden Sie unter dem spezifischen algorithmusthema unter [Miningmodellinhalt &#40; Analysis Services – Datamining &#41; ](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine natürliche PREDICTION JOIN-Anweisung verwendet, um basierend auf dem TM Decision Tree-Miningmodell zu bestimmen, ob es wahrscheinlich ist, dass eine Person ein Fahrrad kaufen wird. Außerdem wird die Wahrscheinlichkeit für die Vorhersage bestimmt. Dieses Beispiel enthält zwei PredictProbability-Funktionen, eine für jeden möglichen Wert. Wenn Sie dieses Argument auslassen, gibt die Funktion die Wahrscheinlichkeit für den wahrscheinlichsten Wert zurück.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Beispielergebnisse:  
  
|Bike Buyer|Bike Buyer = Yes|Bike Buyer = No|  
|----------------|-----------------------|----------------------|  
|1|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

