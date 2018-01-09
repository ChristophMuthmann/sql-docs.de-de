---
title: RangeMax (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: RangeMax
dev_langs: DMX
helpviewer_keywords: RangeMax function
ms.assetid: 6798d9d7-c3dc-40fb-bd8e-56cb1a6d0e5f
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 24559ff09a5791897a41627941d0cf98c7c3cabf
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="rangemax-dmx"></a>RangeMax (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das obere Ende des vorhergesagten Buckets zurück, der für eine diskretisierte Spalte ermittelt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RangeMax(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Skalare Spalten.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert.  
  
## <a name="remarks"></a>Hinweise  
 Die **RangeMax** Funktion kann verwendet werden, [SELECT DISTINCT FROM &#60; Modell &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md) Abfragen. Wird der Verweis auf skalare Spalten mit diesem Abfragetyp verwendet, kann er kontinuierliche oder diskrete Spalten enthalten, die entweder vorhersagbar oder Eingabe sind.  
  
 Bei Verwendung mit [SELECT FROM &#60; Modell &#62; PREDICTION JOIN-Abfrage &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), **RangeMin**, **RangeMid**, und **RangeMax** Funktionen geben die tatsächlichen Begrenzungswerte des angegebenen Buckets zurück. Wenn Sie z. B. eine Vorhersage für eine diskretisierte Spalte ausführen, gibt die Abfrage die vorhergesagte Bucketnummer in der diskretisierten Spalte zurück. Die **RangeMin**, **RangeMid**, und **RangeMax** Funktionen beschreiben den Bucket, der die Vorhersage angibt. Wenn die **RangeMax** Funktion mit einer PREDICTION JOIN-Anweisung verwendet wird, Verweis auf skalare Spalten kann nur diskrete vorhersagbare Spalten enthalten.  
  
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
 [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)   
 [RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)  
  
  
