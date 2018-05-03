---
title: PredictHistogram (DMX) | Microsoft Docs
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
- PredictHistogram
dev_langs:
- DMX
helpviewer_keywords:
- PredictHistogram function
ms.assetid: 85ffc542-96e7-4f58-aaa3-34d76befcedf
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2c06d117d2abd0fc988f5d5b497e588910bd744a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Tabelle zurück, die einem Histogramm für die Vorhersage einer bestimmten Spalte entspricht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>Gilt für  
 Einen Verweis auf eine skalare Spalte oder eine Clusterspalte. Kann mit allen Algorithmentypen außer dem [!INCLUDE[msCoName](../includes/msconame-md.md)] Association-Algorithmus verwendet werden.  
  
## <a name="return-type"></a>Rückgabetyp  
 Tabelle  
  
## <a name="remarks"></a>Hinweise  
 Ein Histogramm generiert Statistikspalten. Die Spaltenstruktur des zurückgegebenen Histogramms hängt vom Typ des Spaltenverweises, die mit der **"PredictHistogram"** Funktion.  
  
## <a name="scalar-columns"></a>Skalare Spalten  
 Für eine \<skalarspaltenverweis >, das Histogramm, das **"PredictHistogram"** Funktionsrückgaben besteht aus den folgenden Spalten:  
  
-   Der Wert, der vorhergesagt wird.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] Datamining-Algorithmen unterstützen keine **$ProbabilityVariance**. Diese Spalte enthält für [!INCLUDE[msCoName](../includes/msconame-md.md)]-Algorithmen immer 0.  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] Datamining-Algorithmen unterstützen keine **$ProbabilityStdev**. Diese Spalte enthält für [!INCLUDE[msCoName](../includes/msconame-md.md)]-Algorithmen immer 0.  
  
-   **$AdjustedProbability**  
  
     Die **$AdjustedProbability** Spalte ist eine [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Erweiterung der [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB-Spezifikation für Data Mining.  
  
## <a name="cluster-columns"></a>Clusterspalten  
 Das Histogramm, das **"PredictHistogram"** idatabasebackupreadstream für eine \<cluster Spaltenverweis > besteht aus den folgenden Spalten:  
  
-   **$Cluster** (entspricht dem Clusternamen)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der vorhergesagte Status der Bike Buyer-Spalte in einer SINGLETON-Abfrage zurückgegeben. Die Abfrage gibt auch die oberen beiden wahrscheinlichsten Statuswerte des Bike Buyer-Attributs basierend auf der angepassten Wahrscheinlichkeit abgerufen werden, mithilfe der **"PredictHistogram"** Funktion.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
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
 [Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [Datamining-Algorithmen & #40; Analysis Services – Datamining & #41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Verweis-Funktion](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
