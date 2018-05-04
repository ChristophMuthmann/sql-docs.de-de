---
title: Neuronale Netzwerkmodellabfragen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b900cf7799baf78234127d52ab064e31f3699f86
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="neural-network-model-query-examples"></a>Neuronale Beispiele für Netzwerkmodellabfragen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Beim Schreiben einer Abfrage für ein Data Mining-Modell können Sie eine Inhaltsabfrage erstellen, die Details über die bei der Analyse ermittelten Muster liefert. Alternativ dazu können Sie auch eine Vorhersageabfrage erstellen, die Vorhersagen für neue Daten anhand der im Modell befindlichen Muster vornimmt. Eine Inhaltsabfrage für ein neuronales Netzwerkmodell ruft beispielsweise Modellmetadaten wie die Anzahl der verborgenen Ebenen ab. Alternativ schlägt eine Vorhersageabfrage Klassifikationen basierend auf einer Eingabe vor und stellt wahlweise Wahrscheinlichkeiten für jede Klassifikation zur Verfügung.  
  
 In diesem Abschnitt wird erklärt, wie Abfragen für Modelle erstellt werden, die auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus basieren.  
  
 **Inhaltsabfragen**  
  
 [Abrufen von Modellmetadaten mithilfe von DMX](#bkmk_Query1)  
  
 [Abrufen von weiteren Modellmetadaten aus dem Schemarowset](#bkmk_Query2)  
  
 [Abrufen von Eingabeattributen für das Modell](#bkmk_Query3)  
  
 [Abrufen von Gewichtungen von der verborgenen Ebene](#bkmk_Query4)  
  
 **Vorhersageabfragen**  
  
 [Erstellen einer Singleton-Vorhersage](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>Suchen nach Informationen über ein neuronales Netzwerkmodell  
 Alle Miningmodelle machen den vom Algorithmus erfassten Inhalt nach einem standardisierten Schema verfügbar. Dieses Schema wird als Miningmodell-Schemarowset bezeichnet. Diese Information bietet Details über das Modell und umfasst grundlegende Metadaten, bei der Analyse ermittelte Strukturen und für die Verarbeitung verwendete Parameter. Abfragen für den Modellinhalt können Sie mithilfe von DMX-Anweisungen (Data Mining-Erweiterungen) erstellen.  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Abrufen von Modellmetadaten mit DMX  
 Die folgende Abfrage gibt einige grundlegende Metadaten über ein Modell zurück, das mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus erstellt wurde. In einem neuronalen Netzwerkmodell enthält der übergeordnete Knoten des Modells nur den Namen des Modells, den Namen der Datenbank, in der das Modell gespeichert ist, und die Anzahl der untergeordneten Knoten. Der Knoten für Randstatistik (NODE_TYPE = 24) stellt sowohl diese grundlegenden Metadaten als auch einige abgeleitete statistische Daten über die in dem Modell verwendeten Eingabespalten zur Verfügung.  
  
 Die folgende Beispielabfrage basiert auf dem Miningmodell mit dem Namen ,das Sie im [Data Mining-Lernprogramm für Fortgeschrittene](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b) `Call Center Default NN`erstellen. Das Modell verwendet Daten von einem Callcenter, um mögliche Korrelationen zwischen Personalbesetzung, Anzahl der Anrufe, Bestellungen und Problemen zu untersuchen. Mit der DMX-Anweisung werden Daten vom Knoten für Randstatistik des neuronalen Netzwerkmodells abgerufen. Die Abfrage umfasst das FLATTENED-Schlüsselwort, da die statistischen Eingabeattributwerte, die von Interesse sind, in einer geschachtelten Tabelle, NODE_DISTRIBUTION, gespeichert sind. Wenn der Abfrageanbieter hierarchische Rowsets unterstützt, muss das FLATTENED-Schlüsselwort nicht verwendet werden.  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  Der Name der geschachtelten Tabellenspalten SUPPORT und PROBABILITY muss in Klammern eingeschlossen werden, um ihn vom reservierten Schlüsselwort mit dem gleichen Namen unterscheiden zu können.  
  
 Beispielergebnisse:  
  
|MODEL_CATALOG|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|Nicht vorhanden|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|< 64.7094100096|11|0.407407407|5|  
  
 Eine Definition der Bedeutung der Spalten im Schemarowset im Kontext eines neuronalen Netzwerkmodells finden Sie unter [Miningmodellinhalt von neuronalen Netzwerkmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)erstellen.  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Abrufen von weiteren Modellmetadaten aus dem Schemarowset  
 Durch Abfragen des Data Mining-Schemarowsets erhalten Sie dieselben Informationen wie bei einer DMX-Inhaltsabfrage. Das Schemarowset stellt jedoch weitere Spalten bereit. Die folgende Beispielabfrage gibt das jeweilige Datum zurück, an dem das Modell erstellt, geändert und zuletzt verarbeitet wurde. Die Abfrage gibt außerdem die vorhersagbaren Spalten zurück, die nicht einfach im Modellinhalt verfügbar sind, sowie die Parameter, die zum Erstellen des Modells verwendet wurden. Diese Informationen können zum Dokumentieren des Modells nützlich sein.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Average Time Per Issue<br /><br /> Grade Of Service<br /><br /> Number Of Orders|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Abrufen von Eingabeattributen für das Modell  
 Sie können die eingegebenen Attribut-Wert-Paare, die zum Erstellen des Modells verwendet wurden, durch Abfragen der untergeordneten Knoten (NODE_TYPE = 20) der Eingabeebene (NODE_TYPE = 18) abrufen. Die folgende Abfrage gibt eine Liste von Eingabeattributen aus den Knotenbeschreibungen zurück.  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Beispielergebnisse:  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Average Time Per Issue=64.7094100096 - 77.4002099712|  
|Day Of Week=Fri.|  
|Level 1 Operators|  
  
 Es werden nur einige repräsentative Zeilen der Ergebnisse angezeigt. Sie können allerdings erkennen, dass NODE_DESCRIPTION abhängig vom Datentyp des Eingabeattributs leicht abweichende Informationen liefert.  
  
-   Wenn es sich bei dem Attribut um einen diskreten oder diskretisierten Wert handelt, werden das Attribut sowie entweder der zugehörige Wert oder der diskretisierte Bereich zurückgegeben.  
  
-   Wenn das Attribut ein kontinuierlicher numerischer Datentyp ist, enthält NODE_DESCRIPTION nur den Attributnamen. Sie können jedoch die geschachtelte NODE_DISTRIBUTION-Tabelle abrufen, um den Mittelwert zu erhalten, oder NODE_RULE zurückgeben, um den Mindest- und Höchstwert des numerischen Bereichs zu erhalten.  
  
 Die folgende Abfrage zeigt, wie mit der geschachtelten NODE_DISTRIBUTION-Tabelle die Attribute in einer Spalte und ihre entsprechenden Werte in einer anderen Spalte zurückgegeben werden. Für kontinuierliche Attribute wird der Wert des Attributs durch seinen Mittelwert dargestellt.  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 Beispielergebnisse:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Average Time Per Issue|64.7094100096 - 77.4002099712|  
|Day Of Week|Fri.|  
|Level 1 Operators|3.2962962962963|  
  
 Der Mindest- und Höchstwert des Bereichs werden in der NODE_RULE-Spalte gespeichert und als XML-Fragment dargestellt, wie im folgenden Beispiel gezeigt:  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> Beispielabfrage 4: Abrufen von Gewichtungen von der verborgenen Ebene  
 Der Modellinhalt eines neuronalen Netzwerkmodells ist so strukturiert, dass das Abrufen von Details zu jedem beliebigen Knoten im Netzwerk erleichtert wird. Darüber hinaus bieten die ID-Nummern der Knoten hilfreiche Informationen zur Identifizierung des Beziehungsgefüges der Knotentypen.  
  
 Die folgende Abfrage demonstriert, wie die unter einem bestimmten Knoten der verborgenen Ebene gespeicherten Koeffizienten abgerufen werden. Die verborgene Ebene besteht aus einem Planerknoten (NODE_TYPE = 19), der nur Metadaten enthält, sowie mehreren untergeordneten Knoten (NODE_TYPE = 22), die Koeffizienten für verschiedene Kombinationen aus Attributen und Werten enthalten. Diese Abfrage gibt nur die Koeffizientenknoten zurück.  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 Beispielergebnisse:  
  
|NODE_UNIQUE_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 Die hier aufgeführten Teilergebnisse zeigen, wie der verborgene Knoten durch den Inhalt des neuronalen Netzwerkmodells mit den Eingabeknoten in Beziehung gesetzt wird.  
  
-   Die eindeutigen Namen von Knoten auf der verborgenen Ebene beginnen immer mit 70000000.  
  
-   Die eindeutigen Namen von Knoten auf der Eingabeebene beginnen immer mit 60000000.  
  
 Diese Ergebnisse zeigen, dass an den Knoten mit der ID 70000000200000000 sechs verschiedene Koeffizienten (VALUETYPE = 7) übergeben wurden. Die Werte der Koeffizienten sind in der ATTRIBUTE_VALUE-Spalte enthalten. Mit der Knoten-ID in der ATTRIBUTE_NAME-Spalte können Sie genau bestimmen, für welches Eingabeattribut der Koeffizient bestimmt ist. Die Knoten-ID 6000000000000000a verweist beispielsweise auf das Eingabeattribut und den Wert `Day of Week = 'Tue.'` . Mit der Knoten-ID können Sie eine Abfrage erstellen, oder Sie können den Knoten mit dem [Microsoft Generic Content Tree Viewer](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)durchsuchen.  
  
 Entsprechend können Sie bei Abfrage der NODE_DISTRIBUTION-Tabelle der Knoten in der Ausgabeebene (NODE_TYPE = 23) die Koeffizienten für jeden Ausgabewert sehen. In der Ausgabeebene verweisen die Zeiger jedoch zurück auf die Knoten der verborgenen Ebene. Weitere Informationen finden Sie unter [Miningmodellinhalt von neuronalen Netzwerkmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)erstellen.  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>Verwenden eines neuronalen Netzwerkmodells zum Erstellen von Vorhersagen  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus unterstützt sowohl Klassifikation als auch Regression. Sie können Vorhersagefunktionen mit diesen Modellen verwenden, um neue Daten zur Verfügung zu stellen und entweder SINGLETON- oder Batchvorhersagen zu erstellen.  
  
###  <a name="bkmk_Query5"></a> Beispielabfrage 5: Erstellen einer SINGLETON-Vorhersage  
 Die einfachste Methode, eine Vorhersageabfrage in einem neuronalen Netzwerkmodell zu erstellen, stellt der Generator für Vorhersageabfragen dar. Dieser ist auf der Registerkarte **Miningvorhersage** des Data Mining Designer sowohl in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] als auch in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verfügbar. Sie können das Modell im [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für neuronale Netzwerke durchsuchen, um Attribute von Interesse zu filtern und Trends anzuzeigen. Anschließend können Sie auf die Registerkarte **Miningvorhersage** wechseln, um eine Abfrage zu erstellen und neue Werte für diese Trends vorherzusagen.  
  
 Sie können beispielsweise das Callcentermodell durchsuchen, um Korrelationen zwischen der Anzahl der Bestellungen und anderen Attributen anzuzeigen. Zu diesem Zweck öffnen Sie das Modell im Viewer, und für **Eingabe**Option  **\<alle >**.  Wählen Sie anschließend für **Ausgabe**die Option **Anzahl der Bestellungen**aus. Wählen Sie für **Wert 1**den Bereich aus, der die meisten Bestellungen repräsentiert, und für **Wert 2**den Bereich, der die wenigsten Bestellungen darstellt. Sie können dann auf einen Blick alle Attribute sehen, die das Modell mit der Anzahl der Bestellungen korreliert.  
  
 Durch Durchsuchen der Ergebnisse im Viewer können Sie feststellen, dass einige Tage der Woche niedrige Bestellzahlen aufweisen und dass ein Anstieg der Anzahl der Operatoren anscheinend mit höheren Umsätzen korreliert. Anschließend können Sie mit einer Vorhersageabfrage für das Modell eine "Was-wäre-wenn"-Hpyothese testen und untersuchen, ob eine Erhöhung der Anzahl von Operatoren auf Ebene 2 an einem Tag mit niedriger Bestellmenge zu einem Anstieg der Bestellungen führen würde. Erstellen Sie dazu beispielsweise folgende Abfrage:  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 Beispielergebnisse:  
  
|Predicted Orders|Wahrscheinlichkeit|  
|----------------------|-----------------|  
|364|0.9532…|  
  
 Die vorhergesagte Absatzmenge ist größer als der aktuelle Absatzbereich für Dienstag, und die Wahrscheinlichkeit für die Vorhersage ist sehr hoch. Sie können jedoch auch mehrere Vorhersagen erstellen, indem Sie einen Batchprozess verwenden, um verschiedene Hypothesen für das Modell zu testen.  
  
> [!NOTE]  
>  Die Data Mining Add-Ins für Excel 2007 stellen einen Logistic Regression-Assistenten bereit, mit dem komplexe Fragen einfach beantwortet werden können, beispielsweise wie viele Operatoren auf Ebene 2 benötigt werden, um die Dienstqualität für die Zielebene einer bestimmten Schicht zu verbessern. Die Data Mining-Add-Ins können kostenlos heruntergeladen werden und enthalten Assistenten, die auf dem neuronalen Netzwerk und/oder den Logistic Regression-Algorithmen basieren. Weitere Informationen finden Sie unter [Data Mining-Add-Ins für Office 2007](http://go.microsoft.com/fwlink/?LinkID=117790) .  
  
## <a name="list-of-prediction-functions"></a>Liste der Vorhersagefunktionen  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Es gibt keine für den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus spezifischen Vorhersagefunktionen. Der Algorithmus unterstützt jedoch die Funktionen, die in der folgenden Tabelle aufgeführt sind.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|Bestimmt, ob ein Knoten ein untergeordnetes Element eines anderen Knotens im Diagramm für neuronale Netzwerke ist.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|Gibt die gewichtete Wahrscheinlichkeit zurück.|  
|["PredictHistogram" & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|Gibt eine Tabelle mit Werten zurück, die sich auf den aktuellen vorhergesagten Wert beziehen.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Gibt die Varianz für den vorhergesagten Wert zurück.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für den vorhergesagten Wert zurück.|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|Gibt die Standardabweichung für den vorhergesagten Wert zurück.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|Für neuronale Netzwerk- und logistische Regressionsmodelle wird ein einzelner Wert zurückgegeben, der die Größe des Trainingssatzes für das gesamte Modell darstellt.|  
  
 Eine Liste der Funktionen, die allen [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Algorithmen gemeinsam sind, finden Sie in der [Algorithmusreferenz (Analysis Services – Data Mining)](https://technet.microsoft.com/library/bb895228\(v=sql.105\).aspx). Die Syntax einzelner Funktionen finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Funktionsreferenz](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Technische Referenz zu Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Miningmodellinhalt, neuronale Netzwerkmodelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Lektion 5: Erstellen von neuronalen Netzwerk und logistischen Regressionsmodellen & #40; Datamining-Lernprogramm für fortgeschrittene & #41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
