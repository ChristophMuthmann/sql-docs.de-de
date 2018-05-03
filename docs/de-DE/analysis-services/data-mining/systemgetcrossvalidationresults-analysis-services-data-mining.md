---
title: SystemGetCrossValidationResults (Analysis Services – Datamining) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- SystemGetCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: f70c3337-c930-434a-b278-caf1ef0c3b3b
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cdb80f65fcde712def73201bcfe562ac7fe92149
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults (Analysis Services – Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Partitioniert die Miningstruktur in die angegebene Anzahl an Querschnitten, trainiert ein Modell für jede Partition und gibt anschließend Genauigkeitsmetriken für jede Partition zurück.  
  
> [!NOTE]  
>  Die gespeicherte Prozedur kann nicht für die Kreuzvalidierung von Clusteringmodellen oder Modellen verwendet werden, die mithilfe des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Algorithmus oder des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus erstellt wurden. Zur Kreuzvalidierung von Clusteringmodellen können Sie die gespeicherte Prozedur [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)verwenden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argumente  
 *mining structure*  
 Name einer Miningstruktur in der aktuellen Datenbank.  
  
 (erforderlich)  
  
 *mining model list*  
 Durch Trennzeichen getrennte Liste von Miningmodellen, die überprüft werden sollen.  
  
 Wenn ein Modellname Zeichen enthält, die im Namen eines Bezeichners nicht gültig sind, muss der Name in Klammern gesetzt werden.  
  
 Wenn keine Liste mit Miningmodellen angegeben wird, erfolgt die Kreuzvalidierung für alle Clustering-Modelle, die mit der angegebenen Struktur verknüpft sind und ein vorhersagbares Attribut enthalten.  
  
> [!NOTE]  
>  Zur Kreuzvalidierung von Clusteringmodellen müssen Sie die gespeicherte Prozedur [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)verwenden.  
  
 (Optional)  
  
 *fold count*  
 Ganzzahliger Wert, der die Anzahl der Partitionen angibt, in die das Dataset aufgeteilt werden soll. Der Mindestwert beträgt 2. Die maximale Anzahl von Aufteilungen ist **maximum integer** oder die Anzahl von Fällen, wobei der jeweils niedrigere Wert gilt.  
  
 Jede Partition enthält in etwa diese Anzahl von Fällen: *max cases*/*fold count*.  
  
 Es gibt keinen Standardwert.  
  
> [!NOTE]  
>  Die Anzahl der Aufteilungen wirkt sich erheblich auf die Zeit aus, die für die Kreuzvalidierung benötigt wird. Wenn Sie eine zu hohe Zahl auswählen, kann die Ausführung der Abfrage sehr lang dauern, und in manchen Fällen reagiert der Server möglicherweise nicht mehr oder ein Timeout tritt ein.  
  
 (erforderlich)  
  
 *max cases*  
 Ganzzahliger Wert, der die maximale Anzahl von Fällen angibt, die über alle Aufteilungen hinweg getestet werden können.  
  
 Der Wert 0 gibt an, dass alle Fälle in der Datenquelle verwendet werden.  
  
 Wenn Sie einen Wert angeben, der größer ist als die tatsächliche Anzahl der Fälle im Dataset ist, werden alle Fälle in der Datenquelle verwendet.  
  
 Es gibt keinen Standardwert.  
  
 (erforderlich)  
  
 *target attribute*  
 Zeichenfolge, die den Namen des vorhersagbaren Attributs enthält. Ein vorhersagbares Attribut kann eine Spalte, eine verschachtelte Tabellenspalte oder eine Schlüsselspalte für eine geschachtelte Tabelle eines Miningmodells sein.  
  
> [!NOTE]  
>  Das Vorhandensein des Zielattributs wird nur zur Laufzeit überprüft.  
  
 (erforderlich)  
  
 *target state*  
 Formel, die den Wert angibt, der vorhergesagt werden soll. Wenn ein Zielwert angegeben ist, werden Metriken nur für den angegebenen Wert aufgelistet.  
  
 Wenn kein Wert oder **null**angegeben ist, werden die Metriken für den wahrscheinlichsten Status der einzelnen Vorhersagen berechnet.  
  
 Der Standardwert ist **null**.  
  
 Während der Überprüfung wird ein Fehler ausgelöst, wenn der angegebene Wert für das angegebene Attribut nicht gültig ist oder die Formel nicht der richtige Typ für das angegebene Attribut ist.  
  
 (Optional)  
  
 *target*  *threshold*  
 **Double** größer als 0 und kleiner als 1. Gibt das minimale Wahrscheinlichkeitsergebnis an, das für die Vorhersage des angegebenen Zielstatus erreicht werden muss, damit er als richtig gewertet wird.  
  
 Eine Vorhersage, deren Wahrscheinlichkeit niedriger als dieser Wert ist oder damit übereinstimmt, wird als falsch erachtet.  
  
 Wenn kein Wert oder **null**angegeben ist, wird der wahrscheinlichste Status unabhängig von seinem Wahrscheinlichkeitsergebnis verwendet.  
  
 Der Standardwert ist **null**.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird kein Fehler ausgelöst, wenn Sie festlegen, *statusschwellenwert* auf 0,0 ist, aber Sie sollten diesen Wert niemals verwenden. Tatsächlich bedeutet eine Schwelle von 0,0, dass Vorhersagen mit einer Wahrscheinlichkeit von 0 (null) Prozent als richtig gewertet werden.  
  
 (Optional)  
  
 *test list*  
 Eine Zeichenfolge, die Testoptionen angibt.  
  
 **Hinweis** Dieser Parameter ist für die zukünftige Verwendung reserviert.  
  
 (Optional)  
  
## <a name="return-type"></a>Rückgabetyp  
 Das Rowset, das zurückgegeben wird, enthält Bewertungen für jede Partition in jedem Modell.  
  
 In der folgenden Tabelle werden die Spalten in diesem Rowset beschrieben.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|ModelName|Name des Modells, das getestet wurde.|  
|AttributeName|Der Name der vorhersagbaren Spalte.|  
|AttributeState|Ein angegebener Zielwert in der vorhersagbaren Spalte. Wenn dieser Wert **null**ist, wurde die wahrscheinlichste Vorhersage verwendet.<br /><br /> Wenn diese Spalte einen Wert enthält, wird die Genauigkeit des Modells nur für diesen Wert bewertet.|  
|PartitionIndex|Ein 1-basierter Index, der angibt, für welche Partition die Ergebnisse gelten.|  
|PartitionSize|Ein ganzzahliger Wert, der angibt, wie viele Fälle in jeder Partition enthalten waren.|  
|Test|Kategorie des Tests, der ausgeführt wurde. Eine Beschreibung der Kategorien und der in jeder Kategorie enthaltenen Tests finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Measure|Der Name des Measures, der vom Test zurückgegeben wurde. Measures für die einzelnen Modelle richten sich nach dem Typ des vorhersagbaren Werts. Definitionen für die einzelnen Measures finden Sie unter [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Eine Liste der für die einzelnen vorhersagbaren Typen zurückgegebenen Measures finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Wert|Der Wert des angegebenen Testmeasures.|  
  
## <a name="remarks"></a>Hinweise  
 Um Genauigkeitsmetriken für das vollständige Dataset zurückzugeben, verwenden Sie [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)verwenden.  
  
 Wenn das Miningmodell bereits in Aufteilungen partitioniert wurde, können Sie die Verarbeitung umgehen und nur die Ergebnisse der Kreuzvalidierung zurückgeben, indem Sie [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)verwenden.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel veranschaulicht, wie man eine Miningstruktur zur Kreuzvalidierung in zwei Aufteilungen partitioniert und dann zwei Miningmodelle testet, die mit der Miningstruktur, `[v Target Mail]`, verknüpft sind.  
  
 In Zeile 3 des Codes sind die Miningmodelle aufgelistet, die Sie testen möchten. Wenn Sie die Liste nicht angeben, werden alle der Struktur zugeordneten Nicht-Clusteringmodelle verwendet. In Zeile 4 des Codes ist die Anzahl der Partitionen angegeben. Da für *max cases*kein Wert angegeben ist, werden alle Fälle in der Miningstruktur verwendet und gleichmäßig auf die Partitionen verteilt.  
  
 In Zeile 5 ist das vorhersehbare Attribut, Bike Buyer, angegeben, und in Zeile 6 der vorherzusagende Wert, nämlich 1 (was heißt: "Ja, will kaufen").  
  
 Der Wert NULL in Zeile 7 gibt an, dass keine minimale Wahrscheinlichkeitsschwelle erreicht werden muss. Deshalb wird die erste Vorhersage, die eine Wahrscheinlichkeit von ungleich 0 (null) hat, zur Bewertung der Genauigkeit verwendet.  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 Beispielergebnisse:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Measure|Wert|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|1|1|500|Klassifizierung|Wahr positiv|144|  
|Target Mail DT|Bike Buyer|1|1|500|Klassifizierung|Falsch positiv|105|  
|Target Mail DT|Bike Buyer|1|1|500|Klassifizierung|Wahr negativ|186|  
|Target Mail DT|Bike Buyer|1|1|500|Klassifizierung|Falsch negativ|65|  
|Target Mail DT|Bike Buyer|1|1|500|Wahrscheinlichkeit|Logarithmisches Ergebnis|-0.619042807138345|  
|Target Mail DT|Bike Buyer|1|1|500|Wahrscheinlichkeit|Lift|0.0740963734002671|  
|Target Mail DT|Bike Buyer|1|1|500|Wahrscheinlichkeit|Wurzel des mittleren quadratischen Fehlers|0.346946279977653|  
|Target Mail DT|Bike Buyer|1|2|500|Klassifizierung|Wahr positiv|162|  
|Target Mail DT|Bike Buyer|1|2|500|Klassifizierung|Falsch positiv|86|  
|Target Mail DT|Bike Buyer|1|2|500|Klassifizierung|Wahr negativ|165|  
|Target Mail DT|Bike Buyer|1|2|500|Klassifizierung|Falsch negativ|87|  
|Target Mail DT|Bike Buyer|1|2|500|Wahrscheinlichkeit|Logarithmisches Ergebnis|-0.654117781086519|  
|Target Mail DT|Bike Buyer|1|2|500|Wahrscheinlichkeit|Lift|0.038997399132084|  
|Target Mail DT|Bike Buyer|1|2|500|Wahrscheinlichkeit|Wurzel des mittleren quadratischen Fehlers|0.342721344892651|  
  
## <a name="requirements"></a>Anforderungen  
 Die Kreuzvalidierung in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] ist erst ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services – Datamining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services – Datamining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
