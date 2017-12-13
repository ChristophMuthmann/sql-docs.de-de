---
title: Zuordnungsmodellabfragen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b176b73816fb01ff7659e00f58dd4441bc689866
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="association-model-query-examples"></a>Beispiele für Zuordnungsmodellabfragen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn Sie eine Abfrage für ein Datamining-Modell erstellen, können Sie entweder eine Inhaltsabfrage Details über die Regeln und Itemsets, die während der Analyse ermittelten liefert erstellen oder Sie können eine Vorhersageabfrage, die in den Daten gefundenen Zuordnungen generiert erstellen Vorhersagen. Für ein Zuordnungsmodell basieren Vorhersagen üblicherweise auf Regeln und können für Empfehlungen verwendet werden. Bei Abfragen des Inhalts wird hingegen die Beziehung zwischen Itemsets analysiert. Sie können auch Metadaten über das Modell abrufen.  
  
 In diesem Abschnitt wird erklärt, wie diese Art von Abfragen für Modelle erstellt werden, die auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus basieren.  
  
 **Inhaltsabfragen**  
  
 [Abrufen von Modellmetadaten-Daten mithilfe von DMX](#bkmk_Query1)  
  
 [Abrufen von Metadaten aus dem Schemarowset](#bkmk_Query2)  
  
 [Abrufen der ursprünglichen Parameter für das Modell](#bkmk_Query3)  
  
 [Abrufen einer Liste von Itemsets und Produkten](#bkmk_Query4)  
  
 [Zurückgeben der obersten 10 Itemsets](#bkmk_Query5)  
  
 **Vorhersageabfragen**  
  
 [Vorhersagen von verknüpften Elementen](#bkmk_Query6)  
  
 [Bestimmen von Vertrauen für verwandte Itemsets](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> Suchen nach Informationen über das Modell  
 Alle Miningmodelle machen den vom Algorithmus erfassten Inhalt nach einem standardisierten Schema verfügbar. Dieses Schema wird als Miningmodell-Schemarowset bezeichnet. Abfragen für das Miningmodell-Schemarowset können Sie entweder mithilfe von DMX-Anweisungen oder mit gespeicherten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Prozeduren erstellen. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie die Schemarowsets mit einer SQL-ähnlichen Syntax auch direkt als Systemtabellen abfragen.  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Abrufen von Modellmetadaten mit DMX  
 Die folgende Abfrage gibt grundlegende Metadaten über das Zuordnungsmodell `Association`zurück, wie Name des Modells, die Datenbank, in der das Modell gespeichert ist, und die Anzahl der untergeordneten Knoten im Modell. Diese Abfrage ruft die Metadaten mithilfe einer DMX-Inhaltsabfrage vom übergeordneten Knoten des Modells ab:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  Setzen Sie den Namen der Spalte CHILDREN_CARDINALITY in Klammern, um ihn von dem gleichnamigen reservierten MDX-Schlüsselwort zu unterscheiden.  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|MODEL_CATALOG|Zuordnungstest|  
|MODEL_NAME|Zuordnung|  
|NODE_CAPTION|Modell für Zuordnungsregeln|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Modell für Zuordnungsregeln; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 Eine Definition der Bedeutung dieser Spalten in einem Zuordnungsmodell finden Sie unter [Miningmodellinhalt von Zuordnungsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Abrufen von weiteren Metadaten aus dem Schemarowset  
 Durch Abfragen des Data Mining-Schemarowsets erhalten Sie dieselben Informationen wie bei einer DMX-Inhaltsabfrage. Das Schemarowset bietet jedoch einige zusätzliche Spalten, wie das Datum der letzten Modellverarbeitung, die Miningstruktur und den Namen der als vorhersagbares Attribut verwendeten Spalte.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|Zuordnung|  
|SERVICE_NAME|Modell für Zuordnungsregeln|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|Zuordnung|  
|LAST_PROCESSED|9/29/2007 10:21:24 PM|  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Abrufen von ursprünglichen Parametern für das Modell  
 Die folgende Abfrage gibt eine einzelne Spalte mit Details über die Parametereinstellungen zurück, die beim Erstellen des Modells verwendet wurden.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Beispielergebnisse:  
  
 MAXIMUM_ITEMSET_COUNT=200000, MAXIMUM_ITEMSET_SIZE=3, MAXIMUM_SUPPORT=1, MINIMUM_SUPPORT=9.40923449156529E-04, MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0, MINIMUM_PROBABILITY=0.4  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>Suchen nach Informationen über Regeln und Itemsets  
 Ein Zuordnungsmodell dient im Wesentlichen zwei Zwecken: dem Finden von Informationen über häufig vorhandene Itemsets und dem Extrahieren von Details über bestimmte Regeln und Itemsets. Sie können beispielsweise eine Liste der Regeln extrahieren, die als besonders interessant eingestuft wurden, oder eine Liste mit den gängigsten Itemsets erstellen. Diese Informationen rufen Sie mit einer DMX-Inhaltsabfrage ab. Sie können auch mithilfe des **Microsoft Association Viewer**nach diesen Informationen suchen.  
  
###  <a name="bkmk_Query4"></a> Beispiel Abfrage 4: Abrufen der Liste von Itemsets und Produkten  
 Mit folgender Abfrage werden alle Itemsets sowie eine geschachtelte Tabelle abgerufen, in der die in den einzelnen Itemsets enthaltenen Produkte aufgeführt sind. Die Spalte NODE_NAME enthält die eindeutige ID des Itemsets innerhalb des Modells, während die Spalte NODE_CAPTION eine Textbeschreibung der Elemente zur Verfügung stellt. In diesem Beispiel wird die geschachtelte Tabelle vereinfacht, sodass ein Itemset, das zwei Produkte enthält, zwei Zeilen in den Ergebnissen generiert. Sie können das FLATTENED-Schlüsselwort auslassen, wenn der Client hierarchische Daten unterstützt.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> Beispielabfrage 5: Zurückgeben der obersten 10 Itemsets  
 Dieses Beispiel zeigt, wie einige der Gruppierungs- und Anordnungsfunktionen, die von DMX standardmäßig bereitgestellt werden, verwendet werden. Die Abfrage gibt die obersten 10 Itemsets zurück, wenn diese entsprechend der Unterstützung für jeden Knoten angeordnet sind. Die Ergebnisse müssen nicht explizit wie in Transact-SQL gruppiert werden. Sie können in jeder Abfrage nur eine Aggregatfunktion verwenden.  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Treffen von Vorhersagen mit dem Modell  
 Ein Zuordnungsregelnmodell wird häufig zum Generieren von Empfehlungen verwendet, die auf in den Itemsets gefundenen Korrelationen basieren. Wenn Sie eine Vorhersageabfrage auf Basis eines Modells für Zuordnungsregeln erstellen, werden die Regeln im Modell üblicherweise verwendet, um Vermutungen basierend auf neuen Daten zu erstellen.  [PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md) werden Empfehlungen zurückgegeben. Diese Funktion besitzt mehrere Argumente, mit denen Sie Abfrageergebnisse anpassen können.  
  
 Ein anderes Beispiel für den sinnvollen Einsatz von Abfragen bei einem Zuordnungsmodell ist die Rückgabe des Vertrauenswerts für verschiedene Regeln und Itemsets, sodass Sie die Effektivität verschiedener Cross-Selling-Strategien vergleichen können. In den folgenden Beispielen wird gezeigt, wie derartige Abfragen erstellt werden.  
  
###  <a name="bkmk_Query6"></a> Beispiel Abfrage 6: Vorhersagen von verknüpften Elementen  
 In diesem Beispiel wird das im [Data Mining-Tutorial für Fortgeschrittene &#40;Analysis Services – Data Mining&#41;](http://msdn.microsoft.com/library/404b31d5-27f4-4875-bd60-7b2b8613eb1b) erstellte Zuordnungsmodell verwendet. Es zeigt, wie Sie eine Vorhersageabfrage erstellen, die Aufschluss darüber gibt, welche Produkte Sie einem Kunden empfehlen sollten, der ein bestimmtes Produkt gekauft hat. Dieser Abfragetyp, bei dem Sie mithilfe einer **SELECT…UNION** -Anweisung Werte für das Modell bereitstellen, wird als SINGLETON-Abfrage bezeichnet. Da es sich bei der vorhersagbaren Modellspalte, die den neuen Werten entspricht, um eine geschachtelte Tabelle handelt, müssen Sie eine **SELECT** -Klausel verwenden, um den neuen Wert der geschachtelten Tabellenspalte zuzuordnen, sowie `[Model]`und eine weitere **SELECT** -Klausel, um die geschachtelte Tabellenspalte der Spalte auf Fallebene `[v Assoc Seq Line Items]`zuzuordnen. Durch Hinzufügen des Schlüsselworts INCLUDE-STATISTICS zur Abfrage können Sie die Wahrscheinlichkeit und die Unterstützung für die Empfehlungen sehen.  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 Beispielergebnisse:  
  
|Model|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patchkit|2113|0.142012|0.132389|  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> Beispielabfrage 7: Bestimmen von Vertrauen für verwandte Itemsets  
 Während Regeln nützlich sind, um Empfehlungen zu generieren, sind Itemsets eher für eine tiefer gehende Analyse der Muster im Dataset interessant. Wenn Sie beispielsweise mit den Empfehlungen, die von der vorherigen Beispielabfrage zurückgegeben wurden, nicht zufrieden sind, können Sie andere Itemsets, die das Produkt A enthalten, prüfen. So können Sie sich ein Bild machen, ob Produkt A ein Zubehör ist, das eher zusammen mit beliebigen anderen Produkten gekauft wird, oder ob Produkt A eng mit dem Kauf bestimmter Produkte verknüpft ist. Die einfachste Möglichkeit zur Prüfung dieser Beziehungen besteht darin, die Itemsets im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Viewer zu filtern. Sie können die gleichen Informationen jedoch auch mit einer Abfrage abrufen.  
  
 Mit der folgenden Beispielabfrage werden alle Itemsets zurückgegeben, die das Element "Water Bottle" enthalten, einschließlich des einzelnen Elements "Water bottle".  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 Beispielergebnisse:  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 Mit dieser Abfrage werden die Zeilen der geschachtelten Tabelle zurückgegeben, die den Kriterien entsprechen, sowie alle Zeilen der Außen- oder Falltabelle. Daher müssen Sie eine Bedingung hinzufügen, mit der die Falltabellenzeilen mit einem NULL-Wert für den Zielattributnamen entfernt werden.  
  
 [Zurück zum Anfang](#bkmk_top2)  
  
## <a name="function-list"></a>Funktionsliste  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association-Algorithmus unterstützt jedoch zusätzliche Funktionen, die in der folgenden Tabelle aufgeführt sind.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Bestimmt, ob ein Knoten ein untergeordnetes Element eines anderen Knotens im Diagramm für neuronale Netzwerke ist.|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|Zeigt an, ob der angegebene Knoten den aktuellen Fall enthält.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Gibt die gewichtete Wahrscheinlichkeit zurück.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Sagt eine Mitgliedschaft in einem assoziativen Dataset voraus.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Gibt eine Tabelle mit Werten zurück, die sich auf den aktuellen vorhergesagten Wert beziehen.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Gibt "Node_ID" für jeden Fall zurück.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für den vorhergesagten Wert zurück.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Gibt den Unterstützungswert für einen bestimmten Status zurück.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Gibt die Varianz für den vorhergesagten Wert zurück.|  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Association-Algorithmus](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Technische Referenz für die Microsoft Association-Algorithmus](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)   
 [Miningmodellinhalt von Zuordnungsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
