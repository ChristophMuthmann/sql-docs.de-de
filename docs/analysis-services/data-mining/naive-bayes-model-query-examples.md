---
title: "Beispiele für Naive Bayes-Modell Abfragen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 622eaa381d4507cb75d66a93916743af40e73932
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="naive-bayes-model-query-examples"></a>Beispiele für Naive Bayes-Modellabfrage
  Beim Erstellen einer Abfrage für ein Data Mining-Modell können Sie entweder eine Inhaltsabfrage oder eine Vorhersageabfrage auswählen. Die Inhaltsabfrage liefert Details über die bei der Analyse ermittelten Muster. Die Vorhersageabfrage nimmt hingegen Vorhersagen für neue Daten anhand der im Modell befindlichen Muster vor. Sie können mit einer Abfrage des Data Mining-Schemarowsets auch Metadaten über das Modell abrufen. In diesem Abschnitt wird erklärt, wie diese Abfragen für Modelle erstellt werden, die auf dem Microsoft Naive Bayes-Algorithmus basieren.  
  
 **Inhaltsabfragen**  
  
 [Abrufen von Modellmetadaten mithilfe von DMX](#bkmk_Query1)  
  
 [Abrufen einer Zusammenfassung der Trainingsdaten](#bkmk_Query2)  
  
 [Suchen nach weiteren Informationen über Attribute](#bkmk_Query3)  
  
 [Verwenden von gespeicherten Systemprozeduren](#bkmk_Query4)  
  
 **Vorhersageabfragen**  
  
 [Vorhersagen von Ergebnissen mit einer SINGLETON-Abfrage](#bkmk_Query5)  
  
 [Abrufen von Vorhersagen mit Wahrscheinlichkeits- und Unterstützungswerten](#bkmk_Query6)  
  
 [Vorhersagen von Zuordnungen](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>Suchen nach Informationen über ein Naive Bayes-Modell  
 Der Inhalt eines Naive Bayes-Modells stellt aggregierte Informationen über die Verteilung der Werte in den Trainingsdaten zur Verfügung. Sie können auch Informationen über die Metadaten des Modells abrufen, indem Sie Abfragen für Data Mining-Schemarowsets erstellen.  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Abrufen von Modellmetadaten mit DMX  
 Metadaten für das Modell finden Sie, indem Sie das Data Mining-Schemarowset abfragen. Dazu gehören beispielsweise das Erstellungsdatum des Modells, das Datum der letzten Verarbeitung, der Name der Miningstruktur, auf der das Modell basiert, und der Name der als vorhersagbares Attribut verwendeten Spalten. Sie können auch die Parameter zurückgeben, die beim Erstellen des Modells verwendet wurden.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 Beispielergebnisse:  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 Das für dieses Beispiel verwendete Modell basiert auf dem Naive Bayes-Modell, das Sie im [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)erstellt haben und das durch Hinzufügen eines zweiten vorhersagbaren Attributs und durch Anwenden eines Filters auf die Trainingsdaten geändert wurde.  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Abrufen einer Zusammenfassung der Trainingsdaten  
 In einem Naive Bayes-Modell speichert der Knoten für Randstatistik aggregierte Informationen über die Verteilung der Werte in den Trainingsdaten. Diese Zusammenfassung ist sehr nützlich und erspart Ihnen das Erstellen von SQL-Abfragen für die Trainingsdaten, um die entsprechenden Informationen abzurufen.  
  
 Im folgenden Beispiel werden die Daten aus dem Knoten (NODE_TYPE = 24) mithilfe einer DMX-Inhaltsabfrage abgerufen. Da die statistischen Daten in einer geschachtelten Tabelle gespeichert sind, wird das FLATTENED-Schlüsselwort verwendet, um die Ergebnisse übersichtlicher anzuzeigen.  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  Setzen Sie den Namen der Spalten SUPPORT und PROBABILITY in Klammern, um ihn von den gleichnamigen reservierten Schlüsselwörtern für mehrdimensionale Ausdrücke (MDX) zu unterscheiden.  
  
 Teilergebnisse:  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Nicht vorhanden|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|8869|0.507263784|4|  
|TM_NaiveBayes|Bike Buyer|1|8615|0.492736216|4|  
|TM_NaiveBayes|Geschlecht|Nicht vorhanden|0|0|1|  
|TM_NaiveBayes|Geschlecht|V|8656|0.495081217|4|  
|TM_NaiveBayes|Geschlecht|M|8828|0.504918783|4|  
  
 Diese Ergebnisse geben beispielsweise Aufschluss über die Zahl der Trainingsfälle für jeden diskreten Wert (VALUETYPE = 4) in Verbindung mit der berechneten Wahrscheinlichkeit, die für fehlende Werte angepasst wurde (VALUETYPE = 1).  
  
 Eine Definition der Werte, die in der NODE_DISTRIBUTION-Tabelle in einem Naive Bayes-Modell bereitgestellt werden, finden Sie unter [Miningmodellinhalt von Naive Bayes-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md). Weitere Informationen zu den Auswirkungen von fehlenden Werten auf Unterstützungs- und Wahrscheinlichkeitsberechnungen finden Sie unter [Fehlende Werte &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Suchen von weiteren Informationen über Attribute  
 Da ein Naive Bayes-Modell häufig komplexe Informationen über die Beziehungen zwischen verschiedenen Attributen enthält, können diese Beziehungen am einfachsten im [Microsoft Naive Bayes-Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)angezeigt werden. Sie können jedoch DMX-Abfragen erstellen, um die Daten zurückzugeben.  
  
 Im folgenden Beispiel wird gezeigt, wie Informationen aus dem Modell über ein bestimmtes Attribut, `Region`, zurückgegeben werden.  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 Diese Abfrage gibt zwei Knotentypen zurück: den Knoten, der das Eingabeattribut (NODE_TYPE = 10) repräsentiert, und Knoten für jeden Wert des Attributs (NODE_TYPE = 11). Zur Identifizierung des Knotens wird die Knotenbeschriftung und nicht der Knotenname herangezogen, da die Beschriftung sowohl den Attributnamen als auch den Attributwert zeigt.  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 Einige der in den Knoten gespeicherten Spalten sind mit den Spalten aus den Knoten für Randstatistiken identisch. Dazu gehören das Knotenwahrscheinlichkeitsergebnis und die Knotenunterstützungswerte. Bei MSOLAP_NODE_SCORE handelt es sich jedoch um einen speziellen Wert, der nur für die Eingabeattributknoten bereitgestellt wird und der die relative Wichtigkeit dieses Attributs im Modell angibt. Im Bereich Abhängigkeitsnetzwerk des Viewers werden im Wesentlichen die gleichen Informationen angezeigt. Der Viewer bietet jedoch keine Bewertungen.  
  
 Die folgende Abfrage gibt die Wichtigkeitsbewertungen aller Attribute im Modell zurück:  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 Beispielergebnisse:  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 Durch Durchsuchen des Modellinhalts im [Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)erhalten Sie einen besseren Eindruck, welche statistischen Daten von Interesse sein können. Einige einfache Beispiele werden hier demonstriert. Häufig müssen Sie mehrere Abfragen ausführen oder die Ergebnisse speichern und auf dem Client verarbeiten.  
  
###  <a name="bkmk_Query4"></a> Beispielabfrage 4: Verwenden von gespeicherten Systemprozeduren  
 Zum Untersuchen von Ergebnissen können Sie neben eigenen Inhaltsabfragen auch einige Analysis Services-gespeicherte Systemprozeduren verwenden. Um eine gespeicherte Systemprozedur zu verwenden, verwenden Sie für den Namen der gespeicherten Prozedur das CALL-Schlüsselwort als Präfix:  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 Teilergebnisse:  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  Diese gespeicherten Systemprozeduren sind für die interne Kommunikation zwischen dem Analysis Services-Server und dem Client bestimmt und sollten nur der Einfachheit halber beim Entwickeln und Testen von Miningmodellen verwendet werden. Beim Erstellen von Abfragen für ein Produktionssystem sollten Sie immer eigene Abfragen mit DMX schreiben.  
  
 Weitere Informationen zu gespeicherten Analysis Services-Systemprozeduren finden Sie unter [Gespeicherte Data Mining-Prozeduren &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>Treffen von Vorhersagen mit einem Naive Bayes-Modell  
 Der Microsoft Naive Bayes-Algorithmus wird normalerweise weniger für die Vorhersage als vielmehr für die Untersuchung des Beziehungsgefüges von Eingabe- und vorhersagbaren Attributen verwendet. Das Modell unterstützt jedoch die Verwendung von Vorhersagefunktionen sowohl für die Vorhersage als auch für die Zuordnung.  
  
###  <a name="bkmk_Query5"></a> Beispielabfrage 5: Vorhersagen von Ergebnissen mit einer SINGLETON-Abfrage  
 In der folgenden Abfrage wird eine SINGLETON-Abfrage verwendet, um einen neuen Wert zur Verfügung zu stellen und basierend auf dem Modell vorherzusagen, ob ein Kunde mit diesen Merkmalen wahrscheinlich ein Fahrrad kaufen wird. Die einfachste Möglichkeit zum Erstellen einer SINGLETON-Abfrage für ein Regressionsmodell bietet das Dialogfeld **SINGLETON-Abfrageeingabe** . Sie können die folgende DMX-Abfrage erstellen, indem Sie das `TM_NaiveBayes` -Modell auswählen und anschließend **Singleton-Abfrage**und Werte aus der Dropdownliste für `[Commute Distance]` und `Gender`auswählen.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Beispielergebnisse:  
  
|expression|  
|----------------|  
|0|  
  
 Die Vorhersagefunktion gibt den wahrscheinlichsten Wert zurück, in diesem Fall 0. Dies bedeutet, dass dieser Kunde wahrscheinlich kein Fahrrad kaufen wird.  
  
###  <a name="bkmk_Query6"></a> Beispielabfrage 6: Abrufen von Vorhersagen mit Wahrscheinlichkeits- und Unterstützungswerten  
 Zusätzlich zum Vorhersagen eines Ergebnisses ist es häufig interessant zu wissen, wie stark die Vorhersage ist. In der folgenden Abfrage wird die gleiche Singleton-Abfrage verwendet wie im vorherigen Beispiel. Es wird jedoch die Vorhersagefunktion [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md) hinzugefügt, um eine geschachtelte Tabelle mit statistischen Daten zur Unterstützung der Vorhersage zurückzugeben.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Beispielergebnisse:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 Die letzte Zeile in der Tabelle zeigt die Anpassungen für Unterstützung und Wahrscheinlichkeit für den fehlenden Wert. Varianz- und Standardabweichungswerte sind immer 0, da Naive Bayes-Modelle keine kontinuierlichen Werte modellieren können.  
  
###  <a name="bkmk_Query7"></a> Beispielabfrage 7: Vorhersagen von Zuordnungen  
 Der Microsoft Naive Bayes-Algorithmus kann für die Zuordnungsanalyse verwendet werden, wenn die Miningstruktur eine geschachtelte Tabelle mit dem vorhersagbaren Attribut als Schlüssel verwendet. Sie könnten z.B. ein Naive Bayes-Modell mithilfe der Miningstruktur erstellen, die Sie im Data Mining-Tutorial in [Lektion 3: Erstellen eines Warenkorbszenarios &#40;Data Mining-Tutorial für Fortgeschrittene&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a) erstellt haben. Das in diesem Beispiel verwendete Modell wurde geändert, und der Falltabelle wurden Informationen zum Einkommen und zur Kundenregion hinzugefügt.  
  
 Das folgende Abfragebeispiel zeigt eine SINGLETON-Abfrage, die Produkte vorhersagt, die mit Käufen des Produkts `'Road Tire Tube'`verknüpft sind. Anhand dieser Informationen können Sie einem bestimmten Kundentyp Produkte empfehlen.  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Teilergebnisse:  
  
|Model|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>Funktionsliste  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes-Algorithmus unterstützt allerdings zusätzliche Funktionen, die in der folgenden Tabelle aufgelistet sind.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Bestimmt, ob ein Knoten ein untergeordnetes Element eines anderen Knotens im Modell ist.|  
|[Predict &#40;DMX&#41;](../../dmx/predict-dmx.md)|Gibt einen vorhergesagten Wert oder eine Gruppe von Werten für eine angegebene Spalte zurück.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Gibt die gewichtete Wahrscheinlichkeit zurück.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Sagt eine Mitgliedschaft in einem assoziativen Dataset voraus.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Gibt "Node_ID" für jeden Fall zurück.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für den vorhergesagten Wert zurück.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Gibt den Unterstützungswert für einen bestimmten Status zurück.|  
  
 Informationen zur Syntax einzelner Funktionen finden Sie unter [Data Mining-Erweiterungen – Funktionsreferenz &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Technische Referenz für den Microsoft Naive Bayes-Algorithmus](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Miningmodellinhalt von Naive Bayes-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
