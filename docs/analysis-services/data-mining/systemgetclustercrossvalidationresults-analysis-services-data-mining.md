---
title: "SystemGetClusterCrossValidationResults (Analysis Services – Datamining) | Microsoft Docs"
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
- SystemGetClusterCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: 79de9b81-9f2e-4f20-ace9-e3b19d6a9759
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 54b91c7abf3f9abe366d45d2579818aee1c121a5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="systemgetclustercrossvalidationresults-analysis-services---data-mining"></a>SystemGetClusterCrossValidationResults (Analysis Services – Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Partitioniert die Miningstruktur in die angegebene Anzahl an Querschnitten, trainiert ein Modell für jede Partition, und gibt anschließend genauigkeitsmetriken für jede Partition.  
  
 **Hinweis** Diese gespeicherte Prozedur kann nur mit einer Miningstruktur verwendet werden, die mindestens ein Clustering-Modell enthält. Zur Kreuzvalidierung von Nichtclusteringmodellen müssen Sie [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)verwenden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## <a name="arguments"></a>Argumente  
 *mining structure*  
 Name einer Miningstruktur in der aktuellen Datenbank.  
  
 (erforderlich)  
  
 *mining model list*  
 Durch Trennzeichen getrennte Liste von Miningmodellen, die überprüft werden sollen.  
  
 Wenn keine Liste mit Miningmodellen angegeben wird, erfolgt die Kreuzvalidierung für alle Clustering-Modelle, die mit der angegebenen Struktur verknüpft sind.  
  
> [!NOTE]  
>  Zur Kreuzvalidierung von Modellen, die keine Clusteringmodelle sind, müssen Sie eine separate gespeicherte Prozedur verwenden: [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)verwenden.  
  
 (Optional)  
  
 *fold count*  
 Ganzzahliger Wert, der die Anzahl der Partitionen angibt, in die das Dataset aufgeteilt werden soll. Der Mindestwert beträgt 2. Die maximale Anzahl von Aufteilungen ist **maximum integer** oder die Anzahl von Fällen, wobei der jeweils niedrigere Wert gilt.  
  
 Jede Partition enthält in etwa diese Anzahl von Fällen: *max cases*/*fold count*.  
  
 Es gibt keinen Standardwert.  
  
> [!NOTE]  
>  Die Anzahl der Aufteilungen wirkt sich erheblich auf die Zeit aus, die für die Kreuzvalidierung benötigt wird. Wenn Sie eine zu hohe Zahl auswählen, kann die Ausführung der Abfrage sehr lang dauern, und in manchen Fällen reagiert der Server möglicherweise nicht mehr oder ein Timeout tritt ein.  
  
 (erforderlich)  
  
 *max cases*  
 Ganzzahliger Wert, der die maximale Anzahl von Fällen angibt, die getestet werden können.  
  
 Der Wert 0 gibt an, dass alle Fälle in der Datenquelle verwendet werden.  
  
 Wenn Sie eine Zahl angeben, die größer ist als die tatsächliche Anzahl der Fälle im Dataset ist, werden alle Fälle in der Datenquelle verwendet.  
  
 (erforderlich)  
  
 *Testliste*  
 Eine Zeichenfolge, die Testoptionen angibt.  
  
 **Hinweis** Dieser Parameter ist für die zukünftige Verwendung reserviert.  
  
 (Optional)  
  
## <a name="return-type"></a>Rückgabetyp  
 Die Tabelle mit den Rückgabetypen enthält Bewertungen für jede einzelne Partition und Aggregate für alle Modelle.  
  
 In der folgenden Tabelle werden diese zurückgegebenen Spalten beschrieben.  
  
|Spaltenname|Beschreibung|  
|-----------------|-----------------|  
|ModelName|Name des Modells, das getestet wurde.|  
|AttributeName|Der Name der vorhersagbaren Spalte. Bei Clustermodellen immer **null**.|  
|AttributeState|Ein angegebener Zielwert in der vorhersagbaren Spalte. Bei Clustermodellen immer **null.**|  
|PartitionIndex|Ein 1-basierter Index, der angibt, für welche Partition die Ergebnisse gelten.|  
|PartitionSize|Ein ganzzahliger Wert, der angibt, wie viele Fälle in jeder Partition enthalten waren.|  
|Test|Der Typ von Test, der ausgeführt wurde.|  
|Measure|Der Name des Measures, der vom Test zurückgegeben wurde. Measures für die einzelnen Modelle richten sich nach dem Typ des vorhersagbaren Werts. Definitionen für die einzelnen Measures finden Sie unter [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Eine Liste der für die einzelnen vorhersagbaren Typen zurückgegebenen Measures finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Wert|Der Wert des angegebenen Testmeasures.|  
  
## <a name="remarks"></a>Hinweise  
 Um Genauigkeitsmetriken für das gesamte Dataset zurückzugeben, verwenden Sie [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)verwenden.  
  
 Auch wenn das Miningmodell bereits in Aufteilungen partitioniert wurde, können Sie die Verarbeitung umgehen und nur die Ergebnisse der Kreuzvalidierung zurückgeben, indem Sie [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)verwenden.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel veranschaulicht, wie man eine Miningstruktur in drei Aufteilungen partitioniert und dann zwei Clustering-Modelle testet, die mit der Miningstruktur verknüpft sind.  
  
 In Zeile 3 des Codes sind die spezifischen Miningmodelle aufgelistet, die Sie testen möchten. Wenn Sie die Liste nicht angeben, werden alle der Struktur zugeordneten Clustering-Modelle verwendet.  
  
 In Zeile 4 des Codes ist die Anzahl der Aufteilungen und in Zeile 5 die Höchstzahl der zu verwendenden Fälle angegeben.  
  
 Da es sich hierbei um Clustering-Modelle handelt, brauchen Sie kein vorhersagbares Attribut oder Wert anzugeben.  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 Beispielergebnisse:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Measure|Wert|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Cluster 1|||1|3025|Clustering|Fallwahrscheinlichkeit|0.930524511864121|  
|Cluster 1|||2|3025|Clustering|Fallwahrscheinlichkeit|0.919184178430778|  
|Cluster 1|||3|3024|Clustering|Fallwahrscheinlichkeit|0.929651120490248|  
|Cluster 2|||1|1289|Clustering|Fallwahrscheinlichkeit|0.922789726933607|  
|Cluster 2|||2|1288|Clustering|Fallwahrscheinlichkeit|0.934865535691068|  
|Cluster 2|||3|1288|Clustering|Fallwahrscheinlichkeit|0.924724595688798|  
  
## <a name="requirements"></a>Anforderungen  
 Die Kreuzvalidierung in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ist erst ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40; Analysis Services – Datamining &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
