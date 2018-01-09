---
title: "SystemGetAccuracyResults (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetAccuracyResults
- cross-validation [data mining]
ms.assetid: 54ff584c-c6ce-4c31-9515-0a645719bd1a
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1f6cc8a8bc3e35f6072e5998faed8fb9d51b768f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Gibt genauigkeitsmetriken einer kreuzvalidierung für eine Miningstruktur und alle zugehörigen Modelle, mit Ausnahme der clustering-Modelle zurück.  
  
 Diese gespeicherte Prozedur gibt Metriken für das ganze Dataset als einzelne Partition zurück. Um das Dataset in Querschnitte zu partitionieren und Metriken für jede Partition zurückzugeben, verwenden Sie [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Diese gespeicherte Prozedur wird nicht bei Modellen unterstützt, die mithilfe des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Algorithmus oder des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus erstellt werden. Verwenden Sie bei Clusteringmodellen die separate gespeicherte Prozedur [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argumente  
 *mining structure*  
 Name einer Miningstruktur in der aktuellen Datenbank.  
  
 (Erforderlich)  
  
 *Modellliste*  
 Durch Trennzeichen getrennte Liste von Modellen, die überprüft werden sollen.  
  
 Der Standardwert ist **null**. Dies heißt, dass alle anwendbaren Modelle verwendet werden. Bei Verwendung des Standardwerts werden Clustering-Modelle automatisch aus der Liste der Kandidaten für die Verarbeitung ausgeschlossen.  
  
 (Optional)  
  
 *Dataset*  
 Ein ganzzahliger Wert, der angibt, welche Partition in der Miningstruktur zum Testen verwendet wird. Der Wert wird von einer Bitmaske abgeleitet, die die Summe der folgenden Werte darstellt, wobei jeder einzelne Wert optional ist:  
  
|||  
|-|-|  
|Trainingsfälle|0x0001|  
|Testfälle|0x0002|  
|Modellfilter|0x0004|  
  
 Eine vollständige Liste der möglichen Werte finden Sie in diesem Thema im Abschnitt mit den Hinweisen.  
  
 (erforderlich)  
  
 *Zielattribut*  
 Zeichenfolge, die den Namen eines vorhersagbaren Objekts enthält. Ein vorhersagbares Objekt kann eine Spalte, eine verschachtelte Tabellenspalte oder eine Schlüsselspalte für eine geschachtelte Tabelle eines Miningmodells sein.  
  
 (erforderlich)  
  
 *Zielstatus*  
 Zeichenfolge, die einen bestimmten vorherzusagenden Wert enthält.  
  
 Wenn ein Wert angegeben ist, werden die Metriken für diesen bestimmten Status aufgelistet.  
  
 Wenn kein Wert oder Null angegeben ist, werden die Metriken für den wahrscheinlichsten Status der einzelnen Vorhersagen berechnet.  
  
 Der Standardwert ist **null**.  
  
 (Optional)  
  
 *Zielschwellenwert*  
 Zahl zwischen 0,0 und 1, die die Mindestwahrscheinlichkeit angibt, mit der Vorhersagewert als richtig gewertet wird.  
  
 Der Standardwert ist **null**. Das heißt, dass alle Vorhersagen als richtig gewertet werden.  
  
 (Optional)  
  
 *test list*  
 Eine Zeichenfolge, die Testoptionen angibt. Dieser Parameter ist für die zukünftige Verwendung reserviert.  
  
 (Optional)  
  
## <a name="return-type"></a>Rückgabetyp  
 Das Rowset, das zurückgegeben wird, enthält Bewertungen für jede Partition und Aggregate für alle Modelle.  
  
 In der folgenden Tabelle sind die Spalten aufgeführt, die von **GetValidationResults**zurückgegeben werden.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|Model|Name des Modells, das getestet wurde. **Alles** gibt an, dass das Ergebnis ein Aggregat für alle Modelle ist.|  
|AttributeName|Der Name der vorhersagbaren Spalte.|  
|AttributeState|Ein Zielwert in der vorhersagbaren Spalte.<br /><br /> Wenn diese Spalte einen Wert enthält, werden Metriken nur für den angegebenen Status aufgelistet.<br /><br /> Wenn kein Wert oder Null angegeben ist, werden die Metriken für den wahrscheinlichsten Status der einzelnen Vorhersagen berechnet.|  
|PartitionIndex|Bezeichnet die Partition, für die das Ergebnis gilt.<br /><br /> Bei dieser Prozedur ist das immer 0.|  
|PartitionCases|Eine ganze Zahl, die die Anzahl der Zeilen in der Groß-/Kleinschreibung auf Grundlage der  *\<DataSet >* Parameter.|  
|Test|Der Typ von Test, der ausgeführt wurde.|  
|Measure|Der Name des Measures, der vom Test zurückgegeben wurde. Measures für die einzelnen Modelle richten sich nach dem Modelltyp und dem Typ des vorhersagbaren Werts.<br /><br /> Eine Liste der für die einzelnen vorhersagbaren Typen zurückgegebenen Measures finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Definitionen für die einzelnen Measures finden Sie unter [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|value|Der Wert für das angegebene Measure.|  
  
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
 In diesem Beispiel werden Genauigkeitsmeasures für ein einzelnes Entscheidungsstrukturmodell, `v Target Mail DT`, zurückgegeben, das mit der `vTargetMail` -Miningstruktur verknüpft ist. Der Code auf Zeile vier gibt an, dass die Ergebnisse auf den Testfällen basieren müssen, die für jedes Modell mit dem jeweils modellspezifischen Filter gefiltert wurden.  `[Bike Buyer]` gibt die zu vorherzusagende Spalte an, und die 1 auf der folgenden Zeile gibt an, dass das Modell nur für den bestimmten Wert 1 ("Yes, will buy") ausgewertet werden soll.  
  
 Die letzte Zeile des Codes gibt an, dass der Statusschwellenwert 0,5 beträgt. Das heißt, dass Vorhersagen mit einer Wahrscheinlichkeit über 50 Prozent bei der Genauigkeitsberechnung als "gute" Vorhersagen bewertet werden sollen.  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 Beispielergebnisse:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Measure|value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|1|0|1638|Klassifizierung|Wahr positiv|605|  
|v Target Mail DT|Bike Buyer|1|0|1638|Klassifizierung|Falsch positiv|177|  
|v Target Mail DT|Bike Buyer|1|0|1638|Klassifizierung|Wahr negativ|501|  
|v Target Mail DT|Bike Buyer|1|0|1638|Klassifizierung|Falsch negativ|355|  
|v Target Mail DT|Bike Buyer|1|0|1638|Wahrscheinlichkeit|Logarithmisches Ergebnis|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|1|0|1638|Wahrscheinlichkeit|Lift|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|1|0|1638|Wahrscheinlichkeit|Wurzel des mittleren quadratischen Fehlers|0.361630800104946|  
  
## <a name="requirements"></a>Anforderungen  
 Die Kreuzvalidierung in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ist erst ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services – Datamining &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
