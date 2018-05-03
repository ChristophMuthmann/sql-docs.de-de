---
title: Sequence Clustering-Modell Abfragebeispiele | Microsoft Docs
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
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ba0770f707dbd27b4efafcc648040da8dbbed4db
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sequence-clustering-model-query-examples"></a>Sequenzclusteringmodellabfragebeispiele
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Beim Schreiben einer Abfrage für ein Data Mining-Modell können Sie entweder eine Inhaltsabfrage oder eine Vorhersageabfrage erstellen. Die Inhaltsabfrage liefert Details über die im Modell gespeicherten Informationen. Die Vorhersageabfrage nimmt hingegen Vorhersagen basierend auf von Ihnen angegebenen neuen Daten anhand der im Modell befindlichen Muster vor. Für ein Sequenzclustermodell bieten Inhaltsabfragen in der Regel weitere Details über die gefundenen Cluster oder über die Übergänge innerhalb dieser Cluster. Mit einer Abfrage können Sie auch Metadaten zum Modell abrufen.  
  
 Vorhersageabfragen für ein Sequenzclustermodell erstellen in der Regel Empfehlungen basierend auf den Sequenzen und Übergängen, auf nicht sequenziellen Attributen, die in das Modell einbezogen wurden, oder auf einer Kombination aus sequenziellen und nicht sequenziellen Attributen.  
  
 In diesem Abschnitt wird erklärt, wie die Abfragen für Modelle erstellt werden, die auf dem Microsoft Sequence Clustering-Algorithmus basieren. Allgemeine Informationen über das Erstellen von Abfragen finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md).  
  
 **Inhaltsabfragen**  
  
 [Verwenden des Data Mining-Schemarowsets zur Rückgabe von Modellparametern](#bkmk_Query1)  
  
 [Abrufen einer Liste von Sequenzen für einen Status](#bkmk_Query2)  
  
 [Verwenden von gespeicherten Systemprozeduren](#bkmk_Query3)  
  
 **Vorhersageabfragen**  
  
 [Vorhersagen des bzw. der nächsten Statuswerte](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> Suchen nach Informationen über das Sequenzclustermodell  
 Um aussagekräftige Abfragen für den Inhalt eines Miningmodells zu erstellen, müssen Sie die Struktur des Inhaltsmodells kennen und wissen, in welchen Knotentypen welche Arten von Informationen gespeichert sind. Weitere Informationen finden Sie unter [Miningmodellinhalt von Sequence Clustering-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
###  <a name="bkmk_Query1"></a> Beispielabfrage 1: Verwenden des Data Mining-Schemarowsets zur Rückgabe von Modellparametern  
 Durch Abfrage des Data Mining-Schemarowsets können Sie verschiedene Arten von Informationen über das Modell ermitteln, wie grundlegende Metadaten, Datum und Uhrzeit der Modellerstellung und der letzten Modellverarbeitung, den Namen der Miningstruktur, auf der das Modell basiert, und die als vorhersagbares Attribut verwendete Spalte.  
  
 Die folgende Abfrage gibt die Parameter zurück, die verwendet wurden, um das Modell `[Sequence Clustering]`zu erstellen und zu trainieren. Sie können dieses Modell in Lektion 5 vom [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)erstellen.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 Beispielergebnisse:  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 Beachten Sie, dass dieses Modell mit dem Standardwert 10 für CLUSTER_COUNT erstellt wurde. Wenn Sie eine Anzahl von Clustern ungleich null für CLUSTER_COUNT angeben, behandelt der Algorithmus diese Zahl als Hinweis für die ungefähre Anzahl der zu suchenden Cluster. Im Zuge der Analyse kann der Algorithmus jedoch mehr oder weniger Cluster ermitteln. In diesem Fall hat der Algorithmus festgestellt, dass 15 Cluster am besten zu den Trainingsdaten passen. Daher enthält die Liste der Parameterwerte für die abgeschlossenen Modellberichte die Anzahl der Cluster wie vom Algorithmus bestimmt und nicht in Form des Werts, der beim Erstellen des Modells übergeben wurde.  
  
 Wie unterscheidet sich dieses Verhalten von der Bestimmung der besten Anzahl von Clustern durch den Algorithmus? Erstellen Sie zum Experimentieren ein anderes Clustermodell, das die gleichen Daten verwendet. Setzen Sie jedoch CLUSTER_COUNT auf 0. In diesem Fall erkennt der Algorithmus 32 Cluster. Durch Verwenden des Standardwerts 10 für CLUSTER_COUNT beschränken Sie daher die Zahl der Ergebnisse.  
  
 Standardmäßig wird der Wert 10 verwendet, da eine geringere Anzahl an Clustern den Benutzern erleichtert, die Daten zu durchsuchen und Gruppierungen der Daten zu verstehen. Jedes Modell und jeder Datensatz ist jedoch anders. Sie können mit verschiedenen Anzahlen von Clustern experimentieren, um zu sehen, welcher Parameterwert das präziseste Modell liefert.  
  
###  <a name="bkmk_Query2"></a> Beispielabfrage 2: Abrufen einer Liste von Sequenzen für einen Status  
 Der Miningmodellinhalt speichert die in den Trainingsdaten gefundenen Sequenzen als ersten Status verbunden mit einer Liste aller zugehörigen zweiten Status. Der erste Status wird als Bezeichnung für die Sequenz verwendet. Die zugehörigen zweiten Status werden als Übergänge bezeichnet.  
  
 Die folgende Abfrage gibt beispielsweise die vollständige Liste der ersten Status im Modell zurück, bevor die Sequenzen in Cluster gruppiert werden.  Zum Abrufen dieser Liste geben Sie die Liste der Sequenzen (NODE_TYPE = 13) zurück, deren übergeordneter Knoten der Modellstammknoten ist (PARENT_UNIQUE_NAME = 0). Das FLATTENED-Schlüsselwort erleichtert die Lesbarkeit der Ergebnisse.  
  
> [!NOTE]  
>  Der Name der Spalten PARENT_UNIQUE_NAME, Support und Probability muss in Klammern eingeschlossen werden, um ihn von dem reservierten Schlüsselwort mit demselben Namen zu unterscheiden.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 Teilergebnisse:  
  
|NODE_UNIQUE_NAME|Product 1|Sequence Support|Sequence Probability|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Nicht vorhanden|0|#######|  
|1081327|All-Purpose Bike Stand|17|0.00111|  
|1081327|Bike Wash|64|0.00418|  
|1081327|(Zeilen 4 bis 36 wurden weggelassen)|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 Die Liste der Sequenzen im Modell wird immer in aufsteigender Reihenfolge alphabetisch sortiert. Die Sortierung der Sequenzen ist wichtig, da Sie die zugehörigen Übergänge anhand der fortlaufenden Nummer der Sequenz ermitteln können. Der Wert **Missing** hat stets den Übergang 0.  
  
 In den vorherigen Ergebnissen hat das Produkt "Women's Mountain Shorts" die Sequenznummer 37 im Modell. Anhand der Informationen können Sie alle Produkte anzeigen, die nach "Women's Mountain Shorts" gekauft wurden.  
  
 Dazu verweisen Sie auf den für NODE_UNIQUE_NAME in der vorherigen Abfrage zurückgegebenen Wert, um die ID des Knotens abzurufen, der alle Sequenzen für das Modell enthält. Diesen Wert übergeben Sie an die Abfrage als ID des übergeordneten Knotens, um nur die in diesen Knoten eingeschlossenen Übergänge abzurufen. Dieser Knoten enthält eine Liste aller Sequenzen für das Modell. Wenn Sie jedoch die Liste der Übergänge für einen bestimmten Cluster sehen möchten, könnten Sie die ID des Clusterknotens übergeben und nur die diesem Cluster zugeordneten Sequenzen anzeigen.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 Beispielergebnisse:  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 Der durch diese ID repräsentierte Knoten enthält eine Liste der Sequenzen, die auf das Produkt "Women's Mountain Shorts" folgen, sowie die Unterstützungs- und Wahrscheinlichkeitswerte.  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 Beispielergebnisse:  
  
|t.Product2|t.P2 Support|t.P2 Probability|  
|----------------|------------------|----------------------|  
|Nicht vorhanden|230.7419|0.456012|  
|Classic Vest|8.16129|0.016129|  
|Cycling Cap|60.83871|0.120235|  
|Half-Finger Gloves|30.41935|0.060117|  
|Long-Sleeve Logo Jersey|86.80645|0.171554|  
|Racing Socks|28.93548|0.057185|  
|Short-Sleeve Classic Jersey|60.09677|0.118768|  
  
 Beachten Sie, dass die Unterstützung der verschiedenen auf "Women's Mountain Shorts" bezogenen Sequenzen 506 im Modell entspricht. Die Unterstützungswerte für die Übergänge belaufen sich auch auf 506. Bei den Zahlen handelt es sich jedoch nicht um ganze Zahlen, was etwas befremdlich erscheint, wenn Sie davon ausgehen, dass die Unterstützung nur eine Anzahl von Fällen darstellt, die jeden Übergang enthalten. Da die Methode zum Erstellen von Clustern jedoch Teilmitgliedschaften berechnet, muss die Wahrscheinlichkeit eines Übergangs innerhalb eines Clusters anhand der Wahrscheinlichkeit, das er zu diesem bestimmten Cluster gehört, gewichtet werden.  
  
 Wenn beispielsweise vier Cluster vorliegen, beträgt die Chance, dass eine bestimmte Sequenz zu Cluster 1 gehört, 40 Prozent, dass sie zu Cluster 2 gehört, 30 Prozent, zu Cluster 3 20 Prozent und zu Cluster 4 10 Prozent. Nachdem der Algorithmus den Cluster ermittelt hat, zu dem der Übergang am wahrscheinlichsten gehört, gewichtet er die Wahrscheinlichkeiten innerhalb des Clusters anhand der Cluster-A-priori-Wahrscheinlichkeiten.  
  
###  <a name="bkmk_Query3"></a> Beispielabfrage 3: Verwenden von gespeicherten Systemprozeduren  
 Sie können aus diesen Abfragebeispielen ersehen, dass die im Modell gespeicherten Informationen komplex sind und Sie gegebenenfalls mehrere Abfragen erstellen müssen, um die gewünschten Informationen abzurufen. Der Microsoft Sequence Clustering-Viewer bietet jedoch einen Satz leistungsstarker Tools, mit denen die in einem Sequenzclustermodell enthaltenen Informationen grafisch durchsucht werden können. Mit dem Viewer können Sie außerdem eine Abfrage und einen Drilldown für das Modell durchführen.  
  
 In den meisten Fällen werden die im Microsoft Sequence Clustering-Viewer dargestellten Informationen erstellt, indem das Modell anhand der Analysis Services-gespeicherten Systemprozeduren abgefragt wird. Die gleichen Informationen können Sie auch abrufen, indem Sie DMX (Data Mining-Erweiterungen)-Abfragen für den Modellinhalt schreiben. Die Analysis Services-gespeicherten Systemprozeduren bieten eine schnelle und einfache Möglichkeiten, Modelle zu erforschen und zu testen.  
  
> [!NOTE]  
>  Gespeicherte Systemprozeduren dienen zur internen Verarbeitung durch Server und Clients, die Microsoft zur Interaktion mit dem Analysis Services-Server zur Verfügung stellt. Daher behält sich Microsoft das Recht vor, sie jederzeit zu ändern. Obwohl die Prozeduren hier der Übersichtlichkeit halber beschrieben sind, unterstützen wir ihre Verwendung in einer Produktionsumgebung nicht. Um die Stabilität und Kompatibilität in einer Produktionsumgebung zu gewährleisten, sollten Sie eigene Abfragen immer mit DMX schreiben.  
  
 Dieser Abschnitt enthält Beispiele, wie mit gespeicherten Systemprozeduren Abfragen für ein Sequenzclustermodell erstellt werden können:  
  
#### <a name="cluster-profiles-and-sample-cases"></a>Clusterprofile und Beispielfälle  
 Die Registerkarte Clusterprofile enthält eine Liste der Cluster im Modell, die Größe der einzelnen Cluster und ein Histogramm, das die im Cluster enthaltenen Statuswerte angibt. Es gibt zwei gespeicherte Systemprozeduren, die Sie in Abfragen verwenden können, um ähnliche Informationen abzurufen:  
  
-   `GetClusterProfile` gibt die Merkmale des Clusters mit allen Informationen zurück, die in der Tabelle NODE_DISTRIBUTION für den Cluster gefunden werden.  
  
-   `GetNodeGraph` gibt Knoten und Kanten zurück, mit denen eine mathematische Grafikdarstellung der Cluster erstellt werden kann. Diese hängen von der ersten Registerkarte der Sequenzclustersicht ab. Die Knoten entsprechen Clustern, und die Kanten stellen die Gewichtung oder Stärke dar.  
  
 Im folgenden Beispiel wird veranschaulicht, wie anhand der gespeicherten Systemprozedur `GetClusterProfiles`alle Cluster im Modell mit den entsprechenden Profilen zurückgegeben werden. Diese gespeicherte Prozedur führt eine Reihe von DMX-Anweisungen aus, die die Gesamtmenge der Profile im Modell zurückgeben. Um diese gespeicherte Prozedur zu verwenden, müssen Sie jedoch die Adresse des Modells kennen.  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 Das folgende Beispiel veranschaulicht, wie das Profil für einen bestimmten Cluster, Cluster 12, mit der gespeicherten Systemprozedur `GetNodeGraph`abgerufen wird und die Cluster-ID, die in der Regel der Nummer im Clusternamen entspricht, angegeben wird.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 Bei Weglassen der Cluster-ID, wie in der folgenden Abfrage gezeigt, gibt `GetNodeGraph` eine sortierte, vereinfachte Liste aller Clusterprofile zurück:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 Die Registerkarte **Clusterprofil** enthält außerdem ein Histogramm von Modellbeispielfällen. Diese Beispielfälle stellen die idealisierten Fälle für das Modell dar. Sie sind nicht auf gleiche Weise im Modell gespeichert wie die Trainingsdaten. Zum Abrufen der Beispielfälle für das Modell müssen Sie eine spezielle Syntax verwenden.  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 Weitere Informationen finden Sie unter [SELECT FROM &#60;Modell&#62;.SAMPLE_CASES &#40;DMX&#41;](../../dmx/select-from-model-sample-cases-dmx.md).  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>Clustermerkmale und Clusterunterscheidung  
 Auf der Registerkarte **Clustermerkmale** werden die Hauptattribute jedes Clusters nach Wahrscheinlichkeit geordnet zusammengefasst. Sie können feststellen, wie viele Fälle zu einem Cluster gehören und wie sich die Fälle im Cluster verteilen: Jedes Merkmal hat eine bestimmte Unterstützung. Um die Merkmale eines bestimmten Clusters anzuzeigen, muss Ihnen die ID des Clusters bekannt sein.  
  
 In den folgenden Beispielen werden anhand der gespeicherten Systemprozedur `GetClusterCharacteristics`alle Merkmale von Cluster 12 zurückgegeben, deren Wahrscheinlichkeitsergebnis über dem angegebenen Schwellenwert von 0,0005 liegt.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 Um die Merkmale aller Cluster zurückzugeben, lassen Sie die Cluster-ID leer.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 Mit dem folgenden Beispiel wird die gespeicherte Systemprozedur `GetClusterDiscrimination` aufgerufen, um die Merkmale von Cluster 1 und Cluster 12 zu vergleichen.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 Wenn Sie eine eigene Abfrage in DMX schreiben möchten, um zwei Cluster zu vergleichen oder einen Cluster mit dem entsprechenden Komplement zu vergleichen, müssen Sie zunächst einen Satz Merkmale abrufen und anschließend die Merkmale für den gewünschten Cluster abrufen und beide Sätze vergleichen. Dieses Szenario ist komplizierter und erfordert normalerweise Clientverarbeitungsleistung.  
  
#### <a name="states-and-transitions"></a>Status und Übergänge  
 Auf der Registerkarte **Statusübergänge** des Microsoft Sequence Clustering-Viewers werden komplizierte Abfragen am Back-End ausgeführt, um die statistischen Daten für verschiedene Cluster abzurufen und zu vergleichen. Zur Reproduktion dieser Ergebnisse ist eine komplexere Abfrage und Clientverarbeitungsleistung erforderlich.  
  
 Sie können jedoch mit den in Beispiel 2 dieses Abschnitts beschriebenen DMX-Abfragen, [Inhaltsabfragen](#bkmk_ContentQueries), Wahrscheinlichkeiten und Statuswerte für Sequenzen oder für einzelne Übergänge abrufen.  
  
## <a name="using-the-model-to-make-predictions"></a>Treffen von Vorhersagen mit dem Modell  
 Vorhersageabfragen für ein Sequenzclustermodell können viele der Vorhersagefunktionen integrieren, die von anderen Clustermodellen verwendet werden. Darüber hinaus können Sie die spezielle Vorhersagefunktion [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md)verwenden, um Empfehlungen oder Vorhersagen zu den nächsten Statuswerten vorzunehmen.  
  
###  <a name="bkmk_Query4"></a> Beispielabfrage 4: Vorhersagen des bzw. der nächsten Statuswerte  
 Mit der [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md) -Funktion können Sie anhand eines Werts den wahrscheinlich nächsten Status vorhersagen. Außerdem können Sie mehrere nächste Statuswerte vorhersagen: Sie können beispielsweise eine Liste mit den drei wahrscheinlichsten Produkten zurückgeben, die der Kunde kaufen wird, um ihm eine Liste mit Empfehlungen zu präsentieren.  
  
 Bei der folgenden Beispielabfrage handelt es sich um eine SINGLETON-Abfrage, die die fünf besten Vorhersagen mit den entsprechenden Wahrscheinlichkeiten zurückgibt. Da das Modell eine geschachtelte Tabelle enthält, müssen Sie bei der Erstellung von Vorhersagen die geschachtelte Tabelle `[v Assoc Seq Line Items]`als Spaltenverweis verwenden. Wenn Sie außerdem Werte als Eingaben bereitstellen, müssen Sie die Spalten sowohl der Falltabelle als auch der geschachtelten Tabelle verknüpfen, wie in den geschachtelten SELECT-Anweisungen gezeigt.  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Beispielergebnisse:  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 Obwohl möglicherweise nur eine Spalte zu erwarten wäre, sind in den Ergebnissen drei Spalten vorhanden, da die Abfrage stets eine Spalte für die Falltabelle zurückgibt. In diesem Fall sind die Ergebnisse vereinfacht. Die Abfrage gibt eine einzelne Spalte zurück, die zwei geschachtelte Tabellenspalten enthält.  
  
 Die Spalte $sequence wird standardmäßig von der `PredictSequence` -Funktion zurückgegeben, um die Vorhersageergebnisse zu sortieren. Die Spalte `[Line Number]`ist für die Zuordnung der Sequenzschlüssel im Modell erforderlich. Die Schlüssel werden jedoch nicht ausgegeben.  
  
 Interessanterweise sind die besten vorhergesagten Sequenzen nach "All-Purpose Bike Stand" "Cycling Cap" und "Cycling Cap". Dies ist kein Fehler. Je nachdem, wie die Daten dem Kunden präsentiert werden und wie sie beim Trainieren des Modells gruppiert werden, sind Sequenzen dieser Art möglich. Ein Kunde kauft beispielsweise eine Fahrradkappe (rot) und anschließend eine weitere Fahrradkappe (blau), oder er kauft zwei Kappen nacheinander, wenn keine Möglichkeit bestand, die Menge anzugeben.  
  
 Die Werte in den Zeilen 6 und 7 sind Platzhalter. Wenn Sie das Ende der Kette möglicher Übergänge erreicht haben, statt die Vorhersageergebnisse zu beenden, wird der als Eingabe übergebene Wert den Ergebnissen hinzugefügt. Wenn Sie die Zahl der Vorhersagen auf 20 erhöhen, wären die Werte für die Zeilen 6 bis 20 alle gleich: "All-Purpose Bike Stand".  
  
## <a name="function-list"></a>Funktionsliste  
 Alle Algorithmen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] unterstützen einen gemeinsamen Funktionssatz. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus unterstützt die zusätzlichen Funktionen, die in der folgenden Tabelle aufgeführt werden.  
  
|||  
|-|-|  
|Vorhersagefunktion|Verwendung|  
|[Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md)|Gibt den Cluster zurück, der mit der höchsten Wahrscheinlichkeit den Eingabefall enthält.|  
|[ClusterDistance &#40;DMX&#41;](../../dmx/clusterdistance-dmx.md)|Gibt den Abstand des Eingabefalls von dem angegebenen Cluster zurück, beziehungsweise, wenn kein Cluster angegeben wurde, den Abstand des Eingabefalls von dem wahrscheinlichsten Cluster.<br /><br /> Diese Funktion kann mit jedem Clusteringmodell verwendet werden (EM, K-Means usw.), die Ergebnisse unterscheiden sich jedoch in Abhängigkeit von dem Algorithmus.|  
|[ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)|Gibt die Wahrscheinlichkeit zurück, mit der der Eingabefall zum angegebenen Cluster gehört.|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|Zeigt an, ob der angegebene Knoten den aktuellen Fall enthält.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|Gibt die angepasste Wahrscheinlichkeit für einen bestimmten Status zurück.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Sagt eine assoziative Mitgliedschaft voraus.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md)|Gibt die Wahrscheinlichkeit zurück, mit der ein Eingabefall in ein vorhandenes Modell passt.|  
|["PredictHistogram" & #40; DMX & #41;](../../dmx/predicthistogram-dmx.md)|Gibt eine Tabelle zurück, die einem Histogramm für die Vorhersage einer bestimmten Spalte entspricht.|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|Gibt die Knoten-ID des Knotens zurück, für den der Fall klassifiziert ist.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für einen bestimmten Status zurück.|  
|[PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md)|Sagt zukünftige Sequenzwerte für eine angegebene Gruppe von Sequenzdaten voraus.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Gibt die vorhergesagte Standardabweichung für die angegebene Spalte zurück.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|Gibt den Unterstützungswert für einen bestimmten Status zurück.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|Gibt die Varianz einer angegebenen Spalte zurück.|  
  
 Eine Liste der Funktionen, die von allen [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Algorithmen verwendet werden, finden Sie unter [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Die Syntax einzelner Funktionen finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Funktionsreferenz](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft Sequence Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Miningmodellinhalt von Sequence Clustering-Modelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
