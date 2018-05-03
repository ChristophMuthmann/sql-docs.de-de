---
title: IsTestCase (DMX) | Microsoft Docs
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
- IsTestCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTestCase function
ms.assetid: 7ff4b895-9bb4-4e26-ab1b-c9049cfc2291
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 8754f92f96740c02470081b12b8fe1056c2fe04a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt an, ob ein Fall als Testfall für ein bestimmtes Data Mining-Modell oder eine bestimmte Data Mining-Struktur verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>Ergebnistyp  
 Gibt **"true"** ist der Fall ein Teil des testdatasets; andernfalls **"false"**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie eine Miningstruktur und ein damit verknüpftes Miningmodell mit dem Data Mining-Assistenten erstellen, werden standardmäßig 30 Prozent der Fälle zur Verwendung als Testdataset zurückgehalten. Die übrigen Fälle werden zum Trainieren des Data Mining-Modells verwendet. Dasselbe Testdataset kann mit allen Modellen verwendet werden, die auf der Struktur basieren. Wenn Sie das Miningmodell jedoch mithilfe von DMX erstellen, werden standardmäßig alle Daten zum Trainieren des Modells verwendet, und es wird kein Testsatz erstellt. Um die Erstellung eines Test-Datasets zu aktivieren, müssen Sie die Parameter der WITH HOLDOUT-Klausel festlegen.  
  
 Sie können ermitteln, ob ein Testsatz für eine bestimmte Miningstruktur erstellt wurde, indem Sie den Wert der Eigenschaften von <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> und <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> anzeigen.  
  
> [!NOTE]  
>  Drillthrough muss für das Modell aktiviert werden, wenn die IsTrainingCase oder IsTestCase-Funktion zu verwenden, um Details zu den Fällen in einem bestimmten Modell zurückgegeben werden sollen. Weitere Informationen finden Sie unter [Aktivieren von Drillthrough für ein Miningmodell](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Um Fälle zurückzugeben, die Teil des trainingsdatasets sind, verwenden Sie die Funktion [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `Targeted Mailing` Miningstruktur, die in erstellt haben, wird die [Data Mining-Grundlagen](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Die Abfrage gibt alle Fälle der Struktur zurück, die für Tests verwendet werden.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 Weitere Informationen zum Abfragen von Fällen in Datamining verwendet, finden Sie unter [SELECT FROM &#60;Modell&#62;. Fällen &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) und [SELECT FROM &#60;Struktur&#62;. Fällen](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Datamining-Abfragen](../analysis-services/data-mining/data-mining-queries.md)   
 [Trainings- und Testdatasets](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
