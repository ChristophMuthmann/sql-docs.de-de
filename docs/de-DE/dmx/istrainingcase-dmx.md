---
title: IsTrainingCase (DMX) | Microsoft Docs
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
- IsTrainingCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTrainingCase function
ms.assetid: 63eab315-e743-470d-9c4c-edfc3f4058a3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 980d214f31a955e73cd2362f41b8d3b84f1f4726
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt an, ob ein Fall als Trainingsfall für ein bestimmtes Data Mining-Modell oder eine bestimmte Data Mining-Struktur verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>Ergebnistyp  
 Gibt **"true"** ist der Fall ein Teil des trainingsdatasets; andernfalls **"false"**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie eine Miningstruktur und ein damit verknüpftes Miningmodell mit dem Data Mining-Assistenten erstellen, werden standardmäßig 30 Prozent der Fälle zur Verwendung als Testdataset zurückgehalten. Die verbleibenden Fälle in der angegebenen Datenquelle werden zum Trainieren des Modells verwendet. Wenn Sie das Miningmodell jedoch mithilfe von DMX-Anweisungen (Data Mining-Erweiterungen) erstellen, werden standardmäßig alle Daten zum Trainieren des Modells verwendet, und es wird kein Testsatz erstellt. Damit ein Testdataset erstellt werden kann, müssen Sie die Parameter der WITH HOLDOUT-Klausel festlegen.  
  
 Sie können ermitteln, ob die Daten in einer bestimmten Miningstruktur in Test- und Trainingssätze geteilt wurden, indem Sie den Wert der Eigenschaften von <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> und <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> anzeigen.  
  
> [!NOTE]  
>  Drillthrough muss für das Modell aktiviert werden, wenn Sie die IsTrainingCase oder IsTestCase-Funktion zu verwenden, um die Details der Fälle im Modell zurückgeben möchten. Weitere Informationen finden Sie unter [Aktivieren von Drillthrough für ein Miningmodell](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Um Fälle zurückzugeben, die Teil des testdatasets sind, verwenden Sie die Funktion [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird clustering Datamining-Modell aus der targeted mailing-Szenario, in dem [Data Mining-Grundlagen](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Die Abfrage gibt nur die Fälle zurück, die zum Trainieren des Miningmodells verwendet wurden. Darüber hinaus werden die Trainingsfälle auf Kunden unter 40 eingeschränkt.  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 Weitere Beispiele zum Abfragen von Fällen in Datamining verwendet, finden Sie unter [SELECT FROM &#60;Modell&#62;. Fällen &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) und [SELECT FROM &#60;Struktur&#62;. Fällen](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Trainings- und Testdatasets](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Datamining-Abfragen](../analysis-services/data-mining/data-mining-queries.md)  
  
  
