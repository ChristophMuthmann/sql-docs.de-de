---
title: RangeMin (DMX) | Microsoft Docs
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
- RangeMin
dev_langs:
- DMX
helpviewer_keywords:
- RangeMin function
ms.assetid: 64159bbe-7016-4f67-91d9-5c5f6ceb6c25
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 03595b718b2381bd9cb8849d57c2e68400a6db82
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="rangemin-dmx"></a>RangeMin (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das untere Ende des vorhergesagten Buckets zurück, der für eine diskretisierte Spalte ermittelt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RangeMin(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Skalare Spalten.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert.  
  
## <a name="remarks"></a>Hinweise  
 Die **RangeMin** Funktion kann verwendet werden, [SELECT DISTINCT FROM &#60; Modell &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md) Abfragen. Wird der Verweis auf skalare Spalten mit diesem Abfragetyp verwendet, kann er kontinuierliche oder diskrete Spalten enthalten, die entweder vorhersagbar oder Eingabe sind.  
  
 Bei Verwendung mit [SELECT FROM &#60; Modell &#62; PREDICTION JOIN-Abfrage &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), **RangeMin**, **RangeMid**, und **RangeMax** Funktionen geben die tatsächlichen Begrenzungswerte des angegebenen Buckets zurück. Wenn Sie z. B. eine Vorhersage für eine diskretisierte Spalte ausführen, gibt die Abfrage die vorhergesagte Bucketnummer in der diskretisierten Spalte zurück. Die **RangeMin**, **RangeMid**, und **RangeMax** Funktionen beschreiben den Bucket, der die Vorhersage angibt. Wenn die **RangeMin** Funktion mit einer PREDICTION JOIN-Anweisung verwendet wird, Verweis auf skalare Spalten kann nur diskrete vorhersagbare Spalten enthalten.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Mindest-, Höchst- und Durchschnittswerte für die kontinuierliche Spalte Yearly Income im Decision Tree-Miningmodell zurückgegeben.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)   
 [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)  
  
  

