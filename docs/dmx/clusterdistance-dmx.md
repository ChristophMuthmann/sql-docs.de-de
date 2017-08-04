---
title: ClusterDistance (DMX) | Microsoft Docs
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
- ClusterDistance
dev_langs:
- DMX
helpviewer_keywords:
- ClusterDistance function
ms.assetid: a13152b3-4cd1-4c79-8a3e-207624198330
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ba8bb17dbd5e443a56b4eb218fae814f8fbcff4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **ClusterDistance** -Funktion gibt den Abstand des eingabefalls von dem angegebenen Cluster, oder wenn kein Cluster, den Abstand des eingabefalls von dem wahrscheinlichsten Cluster angegeben wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>Gilt für  
 Diese Funktion kann nur verwendet werden, wenn das zugrunde liegende Data Mining-Modell Cluster unterstützt. Die Funktion kann mit jedem Clusteringmodell verwendet werden (EM, K-Means usw.), die Ergebnisse unterscheiden sich jedoch in Abhängigkeit von dem Algorithmus.  
  
## <a name="return-type"></a>Rückgabetyp  
 Ein Skalarwert.  
  
## <a name="remarks"></a>Hinweise  
 Die **ClusterDistance** Funktion gibt den Abstand zwischen dem Eingabefall und dem Cluster, die für die höchste Wahrscheinlichkeit hat, den Eingabefall zurück.  
  
 Im Fall von K-Means-Clustering, bei dem jeder Fall nur zu einem Cluster gehören kann und die Mitgliedschaftsgewichtung 1,0 beträgt, ist der Clusterabstand immer 0. In K-Means wird jedoch davon ausgegangen, dass jeder Cluster einen Schwerpunkt besitzt. Sie können den Wert des Schwerpunkts abrufen, indem Sie im Miningmodellinhalt die geschachtelte Tabelle NODE_DISTRIBUTION abfragen oder durchsuchen. Weitere Informationen zu diesem Algorithmus finden Sie unter [Mining Model Content for Clustering Models &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
 Im Fall der standardmäßigen EM-Clusteringmethode werden alle Punkte innerhalb des Clusters als gleich wahrscheinlich betrachtet, daher ist programmbedingt kein Schwerpunkt für den Cluster vorhanden. Der Wert der **ClusterDistance** zwischen einem bestimmten Fall und einem bestimmten Cluster *N* wird wie folgt berechnet:  
  
 ClusterDistance(N) =1–(membershipWeight(N))  
  
 Oder:  
  
 ClusterDistance(N) = 1 – ClusterProbability (N))  
  
## <a name="related-prediction-functions"></a>Zugehörige Vorhersagefunktionen  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] stellt folgende zusätzliche Funktionen für die Abfrage von Clusteringmodellen bereit:  
  
-   Verwenden der [Cluster &#40; DMX &#41;](../dmx/cluster-dmx.md) Funktion, um die wahrscheinlichsten Cluster zurückzugeben.  
  
-   Verwenden der [ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md) Funktion zum Abrufen von der Wahrscheinlichkeit, dass ein Fall zu einem bestimmten Cluster gehört. Dieser Wert stellt die Umkehrung des Clusterabstands dar.  
  
-   Verwenden der ["PredictHistogram" &#40; DMX &#41;](../dmx/predicthistogram-dmx.md) Funktion, um ein Histogramm, der die Wahrscheinlichkeit, dass der Eingabefall in jedem Cluster des Modells zurückzugeben.  
  
-   Verwenden der [PredictCaseLikelihood &#40; DMX &#41;](../dmx/predictcaselikelihood-dmx.md) -Funktion zurückgibt, ein Measure von 0 bis 1, der gibt an, wie wahrscheinlich ein Eingabefall unter Berücksichtigung des Modells vorhanden ist, die vom Algorithmus erfassten.  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>Beispiel 1: Abrufen des Clusterabstands zum wahrscheinlichsten Cluster  
 Im folgenden Beispiel wird der Abstand von dem angegebenen Fall zu dem Cluster angegeben, zu dem der Fall höchstwahrscheinlich gehört.  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Beispielergebnisse:  
  
|expression|  
|----------------|  
|0.0477390930705145|  
  
 Sie können im vorstehenden Beispiel `Cluster` durch `ClusterDistance` ersetzen, um festzustellen, um welchen Cluster es sich handelt.  
  
 Beispielergebnisse:  
  
|$CLUSTER|  
|--------------|  
|Cluster 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>Beispiel 2: Abrufen des Abstands zu einem bestimmten Cluster  
 In der folgenden Syntax wird das Schemarowset für den Inhalt eines Miningmodells verwendet, um eine Liste mit Knoten-IDs und Knotenbeschriftungen für die Cluster zurückzugeben, die im Miningmodell vorhanden sind. Anschließend können Sie die knotenbeschriftung als clusterbezeichnerargument in der **ClusterDistance** Funktion.  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 Beispielergebnisse:  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|Cluster 1|  
|002|Cluster 2|  
  
 Im folgenden Syntaxbeispiel wird der Abstand zwischen dem angegebenen Fall und dem Cluster mit der Bezeichnung Cluster 2 zurückgeben.  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Beispielergebnisse:  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>Siehe auch  
 [Cluster &#40; DMX &#41;](../dmx/cluster-dmx.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funktionen &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Miningmodellinhalt, für das Clustering-Modelle &#40; Analysis Services – Datamining &#41;](../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  

