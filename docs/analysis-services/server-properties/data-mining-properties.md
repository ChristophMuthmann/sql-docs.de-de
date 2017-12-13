---
title: Datamining-Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4eec8a71e71f63b970ea8615ff3aca1a53ccdfe1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-properties"></a>Data Mining-Eigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data mining in den folgenden Tabellen aufgeführten Servereigenschaften unterstützt. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** Nur mehrdimensionaler Servermodus  
  
## <a name="non-specific-category"></a>Nicht spezifische Kategorie  
 **AllowSessionMiningModels**  
 Eine boolesche Eigenschaft, die anzeigt, ob Sitzungsminingmodelle erstellt werden können.  
  
 Der Standardwert für diese Eigenschaft ist FALSE. Dies bedeutet, dass keine Sitzungsminingmodelle erstellt werden können.  
  
 **AllowAdHocOpenRowsetQueries**  
 Eine boolesche Eigenschaft, die anzeigt, ob Ad-hoc-Abfragen für geöffnete Rowsets zulässig sind.  
  
 Der Standardwert für diese Eigenschaft ist FALSE. Dies bedeutet, dass während einer Sitzung keine Abfragen für geöffnete Rowsets zugelassen sind.  
  
 **AllowedProvidersInOpenRowset**  
 Eine Zeichenfolge, die die in einem geöffneten Rowset zulässigen Anbieter identifiziert. Die Zeichenfolge kann aus einer durch Kommas bzw. Semikolons getrennten Liste von Anbieter-ProgIDs oder aus dem Wert [All] bestehen.  
  
 **MaxConcurrentPredictionQueries**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die maximale Anzahl von gleichzeitigen Vorhersageabfragen definiert.  
  
## <a name="algorithms-category"></a>Algorithmus-Kategorie  
 **Microsoft_Association_Rules\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Association_Rules-Algorithmus aktiviert ist.  
  
 **Microsoft_Clustering\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Clustering-Algorithmus aktiviert ist.  
  
 **Microsoft_Decision_Trees\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_DecisionTrees-Algorithmus aktiviert ist.  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_ Naive_Bayes-Algorithmus aktiviert ist.  
  
 **Microsoft_Neural_Network\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Neural_Network-Algorithmus aktiviert ist.  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Sequence_Clustering-Algorithmus aktiviert ist.  
  
 **Microsoft_Time_Series\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Time_Series-Algorithmus aktiviert ist.  
  
 **Microsoft_Linear_Regression\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Linear_Regression-Algorithmus aktiviert ist.  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob der Microsoft_Logistic_Regression-Algorithmus aktiviert ist.  
  
> [!NOTE]  
>  Zusätzlich zu den Data Mining-Diensten, die auf dem Server verfügbar sind, sind Data Mining-Eigenschaften vorhanden, die das Verhalten bestimmter Algorithmen definieren. Sie konfigurieren diese Eigenschaften, wenn Sie ein einzelnes Data Mining-Modell erstellen, nicht auf Serverebene. Weitere Informationen finden Sie unter [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Physische Architektur &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
