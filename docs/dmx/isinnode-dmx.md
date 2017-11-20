---
title: IsInNode (DMX) | Microsoft Docs
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
f1_keywords:
- IsInNode
dev_langs:
- DMX
helpviewer_keywords:
- IsInNode function
ms.assetid: 47b2114f-9ad6-45cc-9498-193ad6fa5288
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d10cc8b335fa47eee2932da7805f97fb42ed6711
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Zeigt an, ob der angegebene Knoten den aktuellen Fall enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein boolescher Typ.  
  
## <a name="remarks"></a>Hinweise  
 **IsInNode** dient lediglich [SELECT FROM &#60; Modell &#62;. Fällen &#40; DMX &#41; ](../dmx/select-from-model-cases-dmx.md) und [SELECT FROM &#60; Modell &#62;. SAMPLE_CASES &#40; DMX &#41; ](../dmx/select-from-model-sample-cases-dmx.md) Abfragen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Fälle zurückgegeben, die zum Erstellen des Modells verwendet wurden, das mit dem in der IsInNode-Funktion angegebenen Knoten verknüpft ist.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

