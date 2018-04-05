---
title: PredictSupport (DMX) | Microsoft Docs
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
- PredictSupport
dev_langs:
- DMX
helpviewer_keywords:
- PredictSupport function
ms.assetid: 325437d6-7cb5-4ae0-8abe-edb58fe5e90d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 51f5e9d8c479944b59bc93bd0f97af1a7c2cd1ac
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den Unterstützungswert für einen bestimmten Status zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Gilt für  
 Ein skalare Spalte.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert des Typs, der angegebenen  *\<* skalarspaltenverweis*>*.  
  
## <a name="remarks"></a>Remarks  
 Ist der vorhergesagte Status (predicted state) nicht angegeben, wird der Status verwendet, der die höchste vorhersagbare Wahrscheinlichkeit hat, wobei der Bucket der fehlenden Status ausgeschlossen wird. Wenn der Bucket der fehlenden Status einschließen möchten, legen die \<vorhergesagten Status > auf **INCLUDE_NULL**.  
  
 Um die Unterstützung für die fehlenden Status zurückzugeben, legen Sie die \<vorhergesagten Status > auf NULL.  
  
> [!NOTE]  
>  Die Unterstützungswerte werden abweichend berechnet oder können in Abhängigkeit von dem abgefragten Modelltyp eine abweichende Interpretation aufweisen. Weitere Informationen über die Berechnung der Unterstützung für bestimmte Modelltypen finden Sie unter dem spezifischen Algorithmustyp unter [Miningmodellinhalt &#40; Analysis Services – Datamining &#41; ](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine SINGLETON-Abfrage verwendet, um vorherzusagen, ob eine Person ein Fahrrad kaufen wird. Außerdem wird die Unterstützung der Vorhersage basierend auf dem TM Decision Tree-Miningmodell bestimmt.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
