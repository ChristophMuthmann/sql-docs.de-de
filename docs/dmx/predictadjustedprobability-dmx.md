---
title: PredictAdjustedProbability (DMX) | Microsoft Docs
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
- PredictAdjustedProbability
dev_langs:
- DMX
helpviewer_keywords:
- PredictAdjustedProbability function
ms.assetid: 9a1e2ec5-5a37-4df6-a78e-26a495cc9301
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0ced04fb08ab3896fa535a7c11b697f85d8395a6
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="predictadjustedprobability-dmx"></a>PredictAdjustedProbability (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die angepasste Wahrscheinlichkeit für einen bestimmten Status zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictAdjustedProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Gilt für  
 Ein skalare Spalte.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert.  
  
## <a name="remarks"></a>Hinweise  
 Ist der vorhergesagte Status (predicted state) nicht angegeben, wird der Status verwendet, der die höchste vorhersagbare Wahrscheinlichkeit hat, wobei der Bucket der fehlenden Status ausgeschlossen wird. Wenn der Bucket der fehlenden Status einschließen möchten, legen die \<vorhergesagten Status > auf **INCLUDE_NULL**.  
  
 Um die angepasste Wahrscheinlichkeit für die fehlenden Status zurückzugeben, legen Sie die \<vorhergesagten Status > auf NULL.  
  
 Die **PredictAdjustedProbability** Funktion ist ein [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Erweiterung der [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB-Spezifikation für Data Mining.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine natürliche PREDICTION JOIN-Anweisung verwendet, um basierend auf dem TM Decision Tree-Miningmodell zu bestimmen, ob es wahrscheinlich ist, dass eine Person ein Fahrrad kaufen wird. Außerdem wird die angepasste Wahrscheinlichkeit für die Vorhersage bestimmt.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictAdjustedProbability([Bike Buyer]) AS [Adjusted Probability]  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

