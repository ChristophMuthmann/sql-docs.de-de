---
title: SystemGetClusterAccuracyResults (Analysis Services – Datamining) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetClusterAccuracyResults
- cross-validation [data mining]
ms.assetid: e1701738-50d5-46b4-b406-f1e800545abb
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0c86e85ec2eaf375b939150a30fc3d85c1bc2834
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults (Analysis Services – Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Gibt Genauigkeitsmetriken einer Kreuzvalidierung für eine Miningstruktur und zugehörige Clustering-Modelle zurück.  
  
 Diese gespeicherte Prozedur gibt Metriken für das ganze Dataset als einzelne Partition zurück. Um das Dataset in Querschnitte zu partitionieren und Metriken für jede Partition zurückzugeben, verwenden Sie [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Diese gespeicherte Prozedur funktioniert nur bei Clustering-Modellen. Verwenden Sie für Nicht-Clustermodelle [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>Argumente  
 *mining structure*  
 Name einer Miningstruktur in der aktuellen Datenbank.  
  
 (Erforderlich)  
  
 *Miningmodellliste*  
 Durch Trennzeichen getrennte Liste von Modellen, die überprüft werden sollen.  
  
 Der Standardwert beträgt **null**, was heißt, dass alle anwendbaren Modelle verwendet werden. Bei Verwendung des Standardwerts werden Nicht-Clustermodelle automatisch aus der Liste der Kandidaten für die Verarbeitung ausgeschlossen.  
  
 (Optional)  
  
 *Dataset*  
 Ein ganzzahliger Wert, der angibt, welche Partition in der Miningstruktur zum Testen verwendet werden soll. Der Wert wird von einer Bitmaske abgeleitet, die die Summe der folgenden Werte darstellt, wobei jeder einzelne Wert optional ist:  
  
|||  
|-|-|  
|Trainingsfälle|0x0001|  
|Testfälle|0x0002|  
|Modellfilter|0x0004|  
  
 Eine vollständige Liste der möglichen Werte finden Sie in diesem Thema im Abschnitt mit den Hinweisen.  
  
 (Erforderlich)  
  
 *Testliste*  
 Eine Zeichenfolge, die Testoptionen angibt. Dieser Parameter ist für die zukünftige Verwendung reserviert.  
  
 (Optional)  
  
## <a name="return-type"></a>Rückgabetyp  
 Eine Tabelle mit Bewertungen für jede einzelne Partition und Aggregaten für alle Modelle.  
  
 In der folgenden Tabelle sind die Spalten aufgeführt, die von **SystemGetClusterAccuracyResults**zurückgegeben werden. Weitere Informationen zum Interpretieren der durch die gespeicherte Prozedur zurückgegebenen Informationen finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|ModelName|Name des Modells, das getestet wurde. **Alles** gibt an, dass das Ergebnis ein Aggregat für alle Modelle ist.|  
|AttributeName|Nicht anwendbar auf Clustering-Modelle.|  
|AttributeState|Nicht anwendbar auf Clustering-Modelle.|  
|PartitionIndex|Eine Zahl, die die Partition angibt.<br /><br /> Für diese gespeicherte Prozedur ist die Zahl immer 0.|  
|PartitionCases|Ein ganzzahliger Wert, der angibt, wie viele Fälle getestet wurden.|  
|Test|Der Typ von Test, der ausgeführt wurde.|  
|Measure|Der Name des Measures, der vom Test zurückgegeben wurde. Measures für die einzelnen Modelle richten sich nach dem Modelltyp und dem Typ des vorhersagbaren Werts.<br /><br /> Eine Liste der für die einzelnen vorhersagbaren Typen zurückgegebenen Measures finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Definitionen für die einzelnen Measures finden Sie unter [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Wert|Ein Wahrscheinlichkeitsergebnis, das die Wahrscheinlichkeit des Clusterfalls angibt.|  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Tabelle enthält Beispiele für die Werte, mit denen Sie die Daten in der für die Kreuzvalidierung verwendeten Miningstruktur angeben können. Wenn Sie Testfälle für die Kreuzvalidierung verwenden möchten, muss die Miningstruktur bereits ein Testdataset enthalten. Informationen zum Definieren eines Testdatasets bei der Erstellung einer Miningstruktur finden Sie unter [Trainings- und Testdatasets](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
|Ganzzahliger Wert|Description|  
|-------------------|-----------------|  
|1|Nur Trainingsfälle werden verwendet.|  
|2|Nur Testfälle werden verwendet.|  
|3|Sowohl die Trainingsfälle als auch Testfälle werden verwendet.|  
|4|Ungültige Kombination.|  
|5|Nur Trainingsfälle werden verwendet, und der Modellfilter wird angewendet.|  
|6|Nur Testfälle werden verwendet, und der Modellfilter wird angewendet.|  
|7|Sowohl die Trainingsfälle als auch Testfälle werden verwendet, und der Modellfilter wird angewendet.|  
  
 Weitere Informationen über die Szenarien, in denen Sie Kreuzvalidierung verwenden würden, finden Sie unter [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel werden Genauigkeitsmeasures für zwei Clustering-Modelle namens `Cluster 1` und `Cluster 2`zurückgegeben, die mit der vTargetMail-Miningstruktur verknüpft sind. Der Code in Zeile 4 gibt an, dass die Ergebnisse nur auf den Testfällen basieren sollen, ohne dass möglicherweise mit den einzelnen Modellen verknüpfte Filter verwendet werden.  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 Beispielergebnisse:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Measure|Wert|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Cluster 1|||0|5545|Clustering|Fallwahrscheinlichkeit|0.796514342249313|  
|Cluster 2|||0|5545|Clustering|Fallwahrscheinlichkeit|0.732122471228572|  
  
## <a name="requirements"></a>Anforderungen  
 Die Kreuzvalidierung in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ist erst ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services – Datamining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services – Datamining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
