---
title: "Data Mining-Eigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "ClusterCount (Eigenschaft)"
  - "AllowedProvidersInOpenRowset (Eigenschaft)"
  - "MinimumSeriesValue (Eigenschaft)"
  - "ScoreMethod (Eigenschaft)"
  - "MinimumImportance (Eigenschaft)"
  - "ModellingCardinality (Eigenschaft)"
  - "BrentTolerance (Eigenschaft)"
  - "ComplexityPenalty (Eigenschaft)"
  - "MaximumItemsetCount (Eigenschaft)"
  - "MinimumSupport (Eigenschaft)"
  - "AllowSessionMiningModels (Eigenschaft)"
  - "HoldoutPercentage (Eigenschaft)"
  - "ClusterCountPrior (Eigenschaft)"
  - "MaximumSequenceStates (Eigenschaft)"
  - "OptimizedPredictionCount (Eigenschaft)"
  - "Data Mining [Analysis Services], Eigenschaften"
  - "MaximumStates (Eigenschaft)"
  - "MaximumContinuousInputAttributes (Eigenschaft)"
  - "MaximumOutputAttributes (Eigenschaft)"
  - "AllowAdHocOpenRowsetQueries (Eigenschaft)"
  - "Enabled-Eigenschaft"
  - "HistoricModelGap (Eigenschaft)"
  - "SampleSize (Eigenschaft)"
  - "MaximumInputAttributes (Eigenschaft)"
  - "PeriodicityHint (Eigenschaft)"
  - "MissingValueSubstitution (Eigenschaft)"
  - "SplitMethod (Eigenschaft)"
  - "ForceRegressor (Eigenschaft)"
  - "MaximumBucketsForContinuousSplit (Eigenschaft)"
  - "MaxConcurrentPredictionQueries (Eigenschaft)"
  - "MinimumItemsetSize (Eigenschaft)"
  - "AcyclicGraph (Eigenschaft)"
  - "HoldoutMethod (Eigenschaft)"
  - "StoppingTolerance (Eigenschaft)"
  - "Eigenschaften [Data Mining]"
  - "AutoDetectPeriodicity (Eigenschaft)"
  - "HoldoutTolerance (Eigenschaft)"
  - "MinimumLeafCases (Eigenschaft)"
  - "HoldoutSeed (Eigenschaft)"
  - "MinimumClusterCases (Eigenschaft)"
  - "ClusterCountDeviation (Eigenschaft)"
  - "MinimumDependencyProbability (Eigenschaft)"
  - "ClusteringMethod (Eigenschaft)"
  - "MaximumItemsetSize (Eigenschaft)"
  - "HiddenNodeRatio (Eigenschaft)"
  - "MaximumSeriesValue (Eigenschaft)"
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Data Mining-Eigenschaften
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] werden die in den folgenden Tabellen aufgeführten Data Mining-Eigenschaften unterstützt. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** Nur mehrdimensionaler Servermodus  
  
## Nicht spezifische Kategorie  
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
  
## Algorithmus-Kategorie  
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
  
## Siehe auch  
 [Physische Architektur &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  