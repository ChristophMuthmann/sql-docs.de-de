---
title: Clusteringmodellabfragen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustering [Data Mining]
- content queries [DMX]
- clustering algorithms [Analysis Services]
ms.assetid: bf2ba332-9bc6-411a-a3af-b919c52432c8
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34300c8642dcc48aff1b470a0b027a0e85cf8076
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="clustering-model-query-examples"></a>Beispiele für Clustermodellabfragen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Wenn Sie eine Abfrage für ein Data Mining-Modell erstellen, können Sie Metadaten über das Modell abrufen oder eine Inhaltsabfrage erstellen, die Details über die in der Analyse erkannten Muster bereitstellt. Sie können auch eine Vorhersageabfrage erstellen, die anhand der Muster des Modells Vorhersagen für neue Daten generiert. Jeder Abfragetyp stellt andere Informationen bereit. Eine Inhaltsabfrage stellt beispielsweise zusätzliche Details über die gefundenen Cluster zur Verfügung, während eine Vorhersageabfrage Aufschluss darüber gibt, zu welchem Cluster ein neuer Datenpunkt höchstwahrscheinlich gehört.  
  
 In diesem Abschnitt wird erklärt, wie die Abfragen für Modelle erstellt werden, die auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus basieren.  
  
 **Inhaltsabfragen**  
  
 [Abrufen von Modellmetadaten mithilfe von DMX](#bkmk_Query1)  
  
 [Abrufen von weiteren Modellmetadaten aus dem Schemarowset](#bkmk_Query2)  
  
 [Zurückgeben eines Clusters oder einer Liste von Clustern](#bkmk_Query3)  
  
 [Zurückgeben von Attributen für einen Cluster](#bkmk_Query4)  
  
 [Zurückgeben eines Clusterprofils mit gespeicherten Systemprozeduren](#bkmk_Query5)  
  
 [Suchen von kritischen Faktoren für einen Cluster](#bkmk_Query6)  
  
 [Zurückgeben von Fällen, die zu einem Cluster gehören](#bkmk_Query7)  
  
 **Vorhersageabfragen**  
  
 [Vorhersagen von Ergebnissen eines Clustermodells](#bkmk_Query8)  
  
 [Bestimmen der Clustermitgliedschaft](#bkmk_Query9)  
  
 [Zurückgeben aller möglichen Cluster mit Wahrscheinlichkeit und Entfernung](#bkmk_Query10)  
  
##  <a name="bkmk_top2"></a> Suchen nach Informationen über das Modell  
 Alle Miningmodelle machen den vom Algorithmus erfassten Inhalt nach einem standardisierten Schema verfügbar. Dieses Schema wird als Miningmodell-Schemarowset bezeichnet. Abfragen für das Miningmodell-Schemarowset können Sie mithilfe von DMX-Anweisungen (Data Mining-Erweiterungen) erstellen. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie die Schemarowsets auch direkt als Systemtabellen abfragen.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Abrufen von Modellmetadaten mit DMX  
 Die folgende Abfrage gibt grundlegende Metadaten über das Clustermodell `TM_Clustering`zurück, das Sie im Rahmen des Lernprogramms zu Data Mining-Grundlagen erstellt haben. Die im übergeordneten Knoten eines Clustermodells verfügbaren Metadaten umfassen den Namen des Modells, die Datenbank, in der das Modell gespeichert ist, und die Anzahl der untergeordneten Knoten im Modell. Diese Abfrage ruft die Metadaten mithilfe einer DMX-Inhaltsabfrage vom übergeordneten Knoten des Modells ab:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  Setzen Sie den Namen der Spalte CHILDREN_CARDINALITY in Klammern, um ihn von dem gleichnamigen reservierten Schlüsselwort für mehrdimensionale Ausdrücke (MDX) zu unterscheiden.  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Clustermodell|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|Alle|  
  
 Eine Definition der Bedeutung dieser Spalten in einem Clustermodell finden Sie unter [Miningmodellinhalt von Clustermodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Abrufen von weiteren Modellmetadaten aus dem Schemarowset  
 Durch Abfragen des Data Mining-Schemarowsets erhalten Sie dieselben Informationen wie bei einer DMX-Inhaltsabfrage. Das Schemarowset stellt jedoch weitere Spalten bereit. Dazu gehören die Parameter, die beim Erstellen des Modells verwendet wurden, Datum und Uhrzeit der letzten Modellverarbeitung sowie der Besitzer des Modells.  
  
 Mit dem folgenden Beispiel wird das Datum zurückgegeben, an dem das Modell erstellt, geändert und zuletzt verarbeitet wurde, ferner die Clustering-Parameter, die zum Erstellen des Modells verwendet wurden, und die Größe des Trainingssatzes. Diese Informationen können zum Dokumentieren des Modells oder zur Bestimmung der Clustering-Optionen, die zum Erstellen eines vorhandenen Modells verwendet wurden, nützlich sein.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>Suchen nach Informationen über Cluster  
 Die nützlichsten Inhaltsabfragen für Clustermodelle geben im Allgemeinen dieselben Informationen zurück, die Sie über das Durchsuchen des **Cluster-Viewers**finden können. Dies schließt Clusterprofile, Clustermerkmale und Clusterunterscheidung ein. Dieser Abschnitt enthält Beispiele für Abfragen, die diese Informationen abrufen.  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Zurückgeben eines Clusters oder einer Liste von Clustern  
 Da alle Cluster den Knotentyp 5 besitzen, können Sie einfach eine Liste der Cluster abrufen, indem Sie den Modellinhalt nur für diesen Knotentyp abfragen. Sie können auch die Knoten, die zurückgegeben werden, nach Wahrscheinlichkeit oder Unterstützung filtern, wie in diesem Beispiel dargestellt.  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|Cluster 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree, 32 <=Age <=48, Number Cars Owned=0, 35964.0771121808 <=Yearly Income <=97407.7163393957, English Occupation=Professional, Commute Distance=2-5 Miles, Region=North America, Bike Buyer=1, Number Children At Home=0, Number Cars Owned=1, Commute Distance=0-1 Miles, English Education=Bachelors, Total Children=1, Number Children At Home=2, English Occupation=Skilled Manual, Marital Status=S, Total Children=0, House Owner Flag=0, Gender=F, Total Children=2, Region=Pacific|  
  
 Die Attribute, die den Cluster definieren, befinden sich in zwei Spalten des Data Mining-Schemarowsets.  
  
-   Die Spalte NODE_DESCRIPTION enthält eine durch Trennzeichen getrennte Liste von Attributen. Beachten Sie, dass die Liste der Attribute möglicherweise für Anzeigezwecke gekürzt wird.  
  
-   Die geschachtelte Tabelle in der Spalte NODE_DISTRIBUTION enthält die vollständige Liste der Attribute für den Cluster. Wenn Ihr Client keine hierarchischen Rowsets unterstützt, können Sie die geschachtelte Tabelle zurückgeben, indem Sie vor der Spaltenliste SELECT das Schlüsselwort FLATTENED hinzufügen. Weitere Informationen zum FLATTENED-Schlüsselwort finden Sie unter [SELECT FROM &#60;Modell&#62;.CONTENT &#40;DMX&#41;](../../dmx/select-from-model-content-dmx.md).  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query4"></a> Beispielabfrage 4: Zurückgeben von Attributen für einen Cluster  
 Für jeden Cluster zeigt der **Cluster-Viewer** ein Profil an, das die Attribute und ihre Werte auflistet. Im Viewer wird außerdem ein Histogramm angezeigt, das die Verteilung der Werte für die Gesamtauffüllung der Fälle im Modell zeigt. Wenn Sie das Modell im Viewer durchsuchen, können Sie das Histogramm einfach aus der Mininglegende kopieren und in ein Excel- oder Word-Dokument einfügen. Außerdem können Sie mithilfe des Viewerbereichs Clustermerkmale die Attribute der verschiedenen Cluster grafisch vergleichen.  
  
 Wenn Sie allerdings Werte für mehr als jeweils einen Cluster abrufen müssen, ist eine Abfrage des Modells einfacher. Wenn Sie das Modell beispielsweise durchsuchen, stellen Sie möglicherweise fest, dass sich die beiden oberen Cluster in Bezug auf ein Attribut, `Number Cars Owned`, unterscheiden. Daher empfiehlt es sich, die Werte für jeden Cluster zu extrahieren.  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 Die erste Zeile des Codes gibt an, dass nur die oberen zwei Cluster berücksichtigt werden sollen.  
  
> [!NOTE]  
>  Standardmäßig sind die Cluster nach Unterstützung sortiert. Daher kann die Spalte NODE_SUPPORT weggelassen werden.  
  
 Die zweite Codezeile fügt eine untergeordnete SELECT-Anweisung hinzu, mit der bestimmte Spalten der geschachtelten Tabellenspalte zurückgegeben werden. Außerdem beschränkt sie die Zeilen der geschachtelten Tabelle auf diejenigen, die sich auf das Zielattribut `Number Cars Owned`beziehen. Zur Vereinfachung der Anzeige wird die geschachtelte Tabelle als Alias verwendet.  
  
> [!NOTE]  
>  Die geschachtelte Tabellenspalte `PROBABILITY`muss in Klammern gesetzt werden, da sie dem Namen eines reservierten MDX-Schlüsselworts entspricht.  
>   
>  Beispielergebnisse:  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Nicht vorhanden|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1.60E-05|  
|002|4|0|  
|002|Nicht vorhanden|0|  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> Beispielabfrage 5: Zurückgeben eines Clusterprofils mit gespeicherten Systemprozeduren  
 Statt eigene Abfragen mit DMX zu erstellen, können Sie auch die gespeicherten Systemprozeduren aufrufen, die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zur Arbeit mit Clustern verwendet. Im folgenden Beispiel wird veranschaulicht, wie anhand intern gespeicherter Prozeduren das Profil für einen Cluster mit der ID 002 zurückgegeben wird.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 Entsprechend können Sie eine gespeicherte Systemprozedur dazu verwenden, die Merkmale eines bestimmten Clusters zurückzugeben, wie im folgenden Beispiel veranschaulicht:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 Beispielergebnisse:  
  
|Attribute|Werte|Häufigkeit|Support|  
|----------------|------------|---------------|-------------|  
|Anzahl der zu Hause lebenden Kinder|0|0.999999829076798|899|  
|Region|North America|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  Die gespeicherten Data Mining-Systemprozeduren sind nur für die interne Verwendung bestimmt, und [!INCLUDE[msCoName](../../includes/msconame-md.md)] behält sich das Recht vor, sie bei Bedarf zu ändern. Für die Verwendung in einer Produktionsumgebung wird empfohlen, Abfragen mit DMX, AMO oder XMLA zu erstellen.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query6"></a> Beispielabfrage 6: Suchen von kritischen Faktoren für einen Cluster  
 Auf der Registerkarte **Clusterunterscheidung** im **Cluster-Viewer** können Sie bequem einen Cluster mit einem anderen Cluster vergleichen oder einen Cluster mit allen übrigen Fällen (Komplement des Clusters) vergleichen.  
  
 Das Erstellen von Abfragen zum Zurückgeben dieser Informationen kann ein komplexer Vorgang sein. Unter Umständen ist eine zusätzliche Verarbeitung auf dem Client erforderlich, um die temporären Ergebnisse und die Ergebnisse von zwei oder mehreren Abfragen zu speichern. Um das Verfahren abzukürzen, können Sie die gespeicherten Systemprozeduren verwenden.  
  
 Die folgende Abfrage gibt eine einzelne Tabelle zurück, die die primären kritischen Faktoren der beiden Cluster mit den Knoten-IDs 009 und 007 angibt. Attribute mit positiven Werten begünstigen Cluster 009, wohingegen Attribute mit negativen Werten Cluster 007 begünstigen.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 Beispielergebnisse:  
  
|Attribute|Werte|Ergebnis|  
|----------------|------------|-----------|  
|Region|North America|100|  
|English Occupation|Skilled Manual|94.9003803898654|  
|Region|Europe|-72.5041051379789|  
|English Occupation|Manuell|-69.6503163202722|  
  
 Diese Informationen werden auch im Diagramm des Viewers **Clusterunterscheidung** dargestellt, wenn Sie in der ersten Dropdownliste Cluster 9 und in der zweiten Dropdownliste Cluster 7 auswählen. Um Cluster 9 mit dem entsprechenden Komplement zu vergleichen, verwenden Sie die leere Zeichenfolge im zweiten Parameter, wie im folgenden Beispiel dargestellt.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  Die gespeicherten Data Mining-Systemprozeduren sind nur für die interne Verwendung bestimmt, und [!INCLUDE[msCoName](../../includes/msconame-md.md)] behält sich das Recht vor, sie bei Bedarf zu ändern. Für die Verwendung in einer Produktionsumgebung wird empfohlen, Abfragen mit DMX, AMO oder XMLA zu erstellen.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> Beispielabfrage 7: Zurückgeben von Fällen, die zu einem Cluster gehören  
 Wenn Sie Drillthrough für ein Miningmodell aktiviert haben, können Sie Abfragen erstellen, die detaillierte Informationen über die im Modell verwendeten Fälle zurückgeben. Wenn darüber hinaus in der Miningstruktur ebenfalls Drillthrough aktiviert wurde, können Sie mit der Funktion [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md) Spalten aus der zugrunde liegenden Struktur einbeziehen.  
  
 Im folgenden Beispiel werden zwei Spalten, Age und Region, zurückgegeben, die im Modell verwendet wurden, sowie eine Spalte, First Name, die nicht im Modell verwendet wurde. Die Abfrage gibt nur Fälle zurück, die in Cluster 1 klassifiziert wurden.  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 Um die Fälle zurückzugeben, die zu einem Cluster gehören, müssen Sie die ID des Clusters kennen. Sie können die ID des Clusters erhalten, indem Sie das Modell in einem der Viewer durchsuchen. Oder Sie können einen Cluster der Einfachheit halber umbenennen. Anschließend können Sie den Namen statt der ID verwenden. Die einem Cluster zugewiesenen Namen gehen allerdings verloren, wenn das Modell erneut verarbeitet wird.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Treffen von Vorhersagen mit dem Modell  
 Auch wenn Clustering in der Regel zum Beschreiben und zum Verstehen von Daten verwendet wird, können Sie mit der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Implementierung Vorhersagen über die Clustermitgliedschaft treffen und Wahrscheinlichkeiten im Zusammenhang mit der Vorhersage zurückgeben. Dieser Abschnitt enthält Beispiele für das Erstellen von Vorhersageabfragen für Clustermodelle. Sie können Vorhersagen für mehrere Fälle treffen, indem Sie eine tabellarische Datenquelle angeben, oder Sie können durch Erstellen einer SINGLETON-Abfrage jeweils neue Werte bereitstellen. Der Deutlichkeit halber handelt es sich bei den Beispielen in diesem Abschnitt nur um SINGLETON-Abfragen.  
  
 Weitere Informationen zum Erstellen von Vorhersageabfragen mit DMX finden Sie unter [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query8"></a> Beispielabfrage 8: Vorhersagen von Ergebnissen eines Clustermodells  
 Wenn das von Ihnen erstellte Clustermodell ein vorhersagbares Attribut enthält, können Sie anhand des Modells Vorhersagen über Ergebnisse treffen. Das Modell behandelt das vorhersagbare Attribut jedoch unterschiedlich, abhängig davon, ob Sie die vorhersagbare Spalte auf **Predict** oder **PredictOnly**festlegen. Wenn Sie die Verwendung der Spalte auf **Predict**festlegen, werden die Werte für dieses Attribut zum Clustermodell hinzugefügt und erscheinen im fertig gestellten Modell als Attribute. Legen Sie jedoch die Verwendung der Spalte auf **PredictOnly**fest, werden die Werte nicht zum Erstellen von Clustern verwendet. Stattdessen erstellt der Clustering-Algorithmus neue Werte für das Attribut **PredictOnly** auf Basis der Cluster, zu denen der jeweilige Fall gehört.  
  
 Die folgende Abfrage stellt einen einzelnen neuen Fall für das Modell bereit, wobei die einzigen Informationen über den Fall Alter und Geschlecht sind. Die SELECT-Anweisung gibt das vorhersagbare Attribut/Wert-Paar an, für das Sie sich interessieren, und die Funktion [PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md) gibt Aufschluss über die Wahrscheinlichkeit, dass ein Fall mit diesen Attributen das gewünschte Ergebnis aufweist.  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Beispiel für Ergebnisse, wenn die Verwendung auf **Predict**festgelegt wird:  
  
|Bike Buyer|expression|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 Beispiel für Ergebnisse, wenn die Verwendung auf **PredictOnly** festgelegt und das Modell erneut verarbeitet wird:  
  
|Bike Buyer|expression|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 In diesem Beispiel besteht kein signifikanter Unterschied im Modell. Mitunter kann es jedoch wichtig sein, Unterschiede zwischen der tatsächlichen Verteilung der Werte und den Vorhersageergebnissen des Modells zu erkennen. Auf der Registerkarte [PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md) ist in diesem Szenario nützlich, da sie anhand des Modells Aufschluss darüber gibt, wie wahrscheinlich ein Fall ist.  
  
 Die von der PredictCaseLikelihood-Funktion zurückgegebene Zahl stellt die Wahrscheinlichkeit dar und bewegt sich daher stets zwischen 0 und 1. Der Wert 0,5 repräsentiert ein willkürliches Ergebnis. Ein Ergebnis kleiner als 0,5 bedeutet, dass der vorhergesagte Fall angesichts des Modells unwahrscheinlich ist. Ein Ergebnis größer als 0,5 gibt an, dass es wahrscheinlicher ist, dass der vorhergesagte Fall dem Modell entspricht, als dass er dem Modell nicht entspricht.  
  
 Die folgende Abfrage gibt beispielsweise zwei Werte zurück, die die Wahrscheinlichkeit für einen neuen Beispielfall charakterisieren. Der nicht normalisierte Wert stellt die Wahrscheinlichkeit in Bezug auf das aktuelle Modell dar. Wenn Sie das NORMALIZED-Schlüsselwort verwenden, wird das von der Funktion zurückgegebene Wahrscheinlichkeitsergebnis durch Division der "Wahrscheinlichkeit mit dem Modell" durch die "Wahrscheinlichkeit ohne Modell" angepasst.  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Beispielergebnisse:  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5.56438372679893E-11|8.65459953145182E-68|  
  
 Beachten Sie, dass die Zahlen in diesen Ergebnissen in wissenschaftlicher Schreibweise ausgedrückt werden.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query9"></a> Beispielabfrage 9: Bestimmen der Clustermitgliedschaft  
 In diesem Beispiel wird die Funktion [Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md) verwendet, um den Cluster, zu dem der neue Fall höchstwahrscheinlich gehört, zurückzugeben. Mit der Funktion [ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md) wird die Wahrscheinlichkeit für die Mitgliedschaft in diesem Cluster zurückgegeben.  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 Beispielergebnisse:  
  
|$CLUSTER|expression|  
|--------------|----------------|  
|Cluster 2|0.397918596951617|  
  
 **Hinweis:** Standardmäßig gibt die Funktion **ClusterProbability** die Wahrscheinlichkeit des wahrscheinlichsten Clusters zurück. Mit der Syntax `ClusterProbability('cluster name')`können Sie jedoch einen anderen Cluster angeben. Beachten Sie in diesem Fall, dass die Ergebnisse der einzelnen Vorhersagefunktionen von den anderen Ergebnissen unabhängig sind. Das Wahrscheinlichkeitsergebnis in der zweiten Spalte könnte sich daher auf einen anderen Cluster beziehen als den in der ersten Spalte genannten Cluster.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query10"></a> Beispielabfrage 10: Zurückgeben aller möglichen Cluster mit Wahrscheinlichkeit und Entfernung  
 Im vorherigen Beispiel war das Wahrscheinlichkeitsergebnis nicht sehr hoch. Um zu bestimmen, ob es einen besseren Cluster gibt, verwenden Sie die Funktion [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md) zusammen mit der Funktion [Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md) , um eine geschachtelte Tabelle, die alle möglichen Cluster enthält, sowie die Wahrscheinlichkeit zurückzugeben, dass der neue Fall zu dem jeweiligen Cluster gehört. Das FLATTENED-Schlüsselwort wird verwendet, um das hierarchische Rowset zur besseren Anzeige in eine flache Tabelle zu ändern.  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|Cluster 2|0.602081403048383|0.397918596951617|  
|Cluster 10|0.719691686785675|0.280308313214325|  
|Cluster 4|0.867772590378791|0.132227409621209|  
|Cluster 5|0.931039872200985|0.0689601277990149|  
|Cluster 3|0.942359230072167|0.0576407699278328|  
|Cluster 6|0.958973668972756|0.0410263310272437|  
|Cluster 7|0.979081275926724|0.0209187240732763|  
|Cluster 1|0.999169044818624|0.000830955181376364|  
|Cluster 9|0.999831227795894|0.000168772204105754|  
|Cluster 8|1|0|  
  
 Standardmäßig werden die Ergebnisse nach Wahrscheinlichkeit geordnet. Die Ergebnisse bedeuten, dass trotz relativ niedriger Wahrscheinlichkeit für Cluster 2 dieser Cluster dennoch für den neuen Datenpunkt am besten geeignet ist.  
  
 **Hinweis:** Die zusätzliche Spalte `$DISTANCE`repräsentiert die Entfernung vom Datenpunkt zum Cluster. Standardmäßig verwendet der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Clustering-Algorithmus skalierbares EM-Clustering, bei dem jedem Datenpunkt mehrere Cluster zugewiesen werden und die Rangfolge der möglichen Cluster bestimmt wird.  Wenn Sie das Clustermodell allerdings mit dem K-Means-Algorithmus erstellen, kann jedem Datenpunkt nur ein Cluster zugewiesen werden, und diese Abfrage würde nur eine Zeile zurückgeben. Diese Unterschiede zu verstehen ist notwendig, um die Ergebnisse der Funktion [PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md) Spalten aus der zugrunde liegenden Struktur einbeziehen. Weitere Informationen zu den Unterschieden zwischen EM- und K-Means-Clustering finden Sie unter [Technische Referenz für den Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
## <a name="function-list"></a>Funktionsliste  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Modelle, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus erstellt werden, unterstützen jedoch die in der folgenden Tabelle aufgeführten, zusätzlichen Funktionen.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md)|Gibt den Cluster zurück, der mit der höchsten Wahrscheinlichkeit den Eingabefall enthält.|  
|[ClusterDistance &#40;DMX&#41;](../../dmx/clusterdistance-dmx.md)|Gibt den Abstand des Eingabefalls von dem angegebenen Cluster zurück, beziehungsweise, wenn kein Cluster angegeben wurde, den Abstand des Eingabefalls von dem wahrscheinlichsten Cluster.<br /><br /> Gibt die Wahrscheinlichkeit zurück, mit der der Eingabefall zum angegebenen Cluster gehört.|  
|[ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)|Gibt die Wahrscheinlichkeit zurück, mit der der Eingabefall zum angegebenen Cluster gehört.|  
|[IsDescendant &#40; DMX &#41;](../../dmx/isdescendant-dmx.md)|Bestimmt, ob ein Knoten ein untergeordnetes Element eines anderen Knotens im Modell ist.|  
|[IsInNode &#40; DMX &#41;](../../dmx/isinnode-dmx.md)|Zeigt an, ob der angegebene Knoten den aktuellen Fall enthält.|  
|[PredictAdjustedProbability &#40; DMX &#41;](../../dmx/predictadjustedprobability-dmx.md)|Gibt die gewichtete Wahrscheinlichkeit zurück.|  
|[PredictAssociation &#40; DMX &#41;](../../dmx/predictassociation-dmx.md)|Sagt eine Mitgliedschaft in einem assoziativen Dataset voraus.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md)|Gibt die Wahrscheinlichkeit zurück, mit der ein Eingabefall in ein vorhandenes Modell passt.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Gibt eine Tabelle mit Werten zurück, die sich auf den aktuellen vorhergesagten Wert beziehen.|  
|[PredictNodeId &#40; DMX &#41;](../../dmx/predictnodeid-dmx.md)|Gibt "Node_ID" für jeden Fall zurück.|  
|[PredictProbability &#40; DMX &#41;](../../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für den vorhergesagten Wert zurück.|  
|[PredictStdev &#40; DMX &#41;](../../dmx/predictstdev-dmx.md)|Gibt die vorhergesagte Standardabweichung für die angegebene Spalte zurück.|  
|[PredictSupport &#40; DMX &#41;](../../dmx/predictsupport-dmx.md)|Gibt den Unterstützungswert für einen bestimmten Status zurück.|  
|[PredictVariance &#40; DMX &#41;](../../dmx/predictvariance-dmx.md)|Gibt die Varianz einer angegebenen Spalte zurück.|  
  
 Die Syntax einzelner Funktionen finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Funktionsreferenz](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)   
 [Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
  
