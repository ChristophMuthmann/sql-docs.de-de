---
title: Microsoft Clustering Algorithm Technical Reference | Microsoft Docs
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
- clustering [Data Mining]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- CLUSTER_SEED parameter
- MODELLING_CARDINALITY parameter
- MINIMUM_SUPPORT parameter
- STOPPING_TOLERANCE parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- CLUSTERING_METHOD parameter
- soft clustering [Data Mining]
- clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 16d3dae2010f43a15cf11d83891bdf30b5b5b518
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-clustering-algorithm-technical-reference"></a>Technische Referenz für den Microsoft Clustering-Algorithmus
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In diesem Abschnitt wird die Implementierung des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus einschließlich der Parameter erklärt, mit denen Sie das Verhalten von Clustermodellen steuern können. Außerdem bietet der Abschnitt Anleitungen zur Verbesserung der Leistung beim Erstellen und Verarbeiten von Clustermodellen.  
  
 Weitere Informationen zum Verwenden von Clustermodellen finden Sie in folgenden Themen:  
  
-   [Miningmodellinhalt, für das Clustering-Modelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [Clusteringmodellabfragen](../../analysis-services/data-mining/clustering-model-query-examples.md)  
  
## <a name="implementation-of-the-microsoft-clustering-algorithm"></a>Implementierung des Microsoft Clustering-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus stellt zwei Methoden zum Erstellen von Clustern und zum Zuweisen von Datenpunkten zu den Clustern zur Verfügung. Die erste Methode, der *K-Means-Algorithmus* , ist eine harte Clustermethode. Dies bedeutet, dass ein Datenpunkt nur zu einem Cluster gehören kann und dass für die Mitgliedschaft der einzelnen Datenpunkte in diesem Cluster nur eine einzige Wahrscheinlichkeit berechnet wird. Die zweite Methode, die *Expectation Maximization (EM)* -Methode, ist eine *weiche Clustermethode* . Dies bedeutet, dass ein Datenpunkt stets zu mehreren Clustern gehört und dass für jede Kombination aus Datenpunkt und Cluster eine Wahrscheinlichkeit berechnet wird.  
  
 Den zu verwendenden Algorithmus können Sie durch Festlegen des *CLUSTERING_METHOD* -Parameters auswählen. Die Standardmethode für das Clustering ist die skalierbare EM-Methode.  
  
### <a name="em-clustering"></a>EM-Clustering  
 Beim EM-Clustering optimiert der Algorithmus iterativ ein Clusteranfangsmodell, um die Daten anzupassen, und bestimmt die Wahrscheinlichkeit, mit der ein Datenpunkt in einem Cluster vorhanden ist. Der Algorithmus beendet den Prozess, wenn das probabilistische Modell den Daten entspricht. Die Funktion, mit der bestimmt wird, ob die Daten übereinstimmen, ist der Log-Likelihood für die Daten unter Vorgabe des Modells.  
  
 Wenn während des Prozesses leere Cluster generiert werden oder die Mitgliedschaft eines oder mehrerer Cluster unter einen vorgegebenen Schwellenwert fällt, werden den Clustern mit niedrigen Auffüllungen bei neuen Punkten neue Ausgangswerte zugewiesen und der EM-Algorithmus wird erneut ausgeführt.  
  
 Die Ergebnisse der EM-Clustermethode sind probabilistisch. Dies bedeutet, dass jeder Datenpunkt zu allen Clustern gehört, jede Zuweisung eines Datenpunkts zu einem Cluster jedoch eine andere Wahrscheinlichkeit hat. Da die Methode ein Überlappen der Cluster zulässt, überschreitet die Summe der Elemente aller Cluster möglicherweise die Gesamtelemente im Trainingssatz. In den Miningmodellergebnissen werden Ergebnisse, die Unterstützung angeben, angepasst, um dies zu berücksichtigen.  
  
 Der EM-Algorithmus ist der in Microsoft Clustering-Modellen verwendete Standardalgorithmus. Dieser Algorithmus wird als Standard verwendet, da er mehrere Vorteile gegenüber dem K-Means-Clustering bietet:  
  
-   Erfordert höchstens einen Datenbankscan.  
  
-   Funktioniert trotz des beschränkten Arbeitsspeichers (RAM).  
  
-   Verfügt über die Fähigkeit, einen Vorwärtscursor zu verwenden.  
  
-   Übertrifft Samplingansätze.  
  
 Die Microsoft-Implementierung stellt zwei Optionen bereit: skalierbares und nicht skalierbares EM. Standardmäßig werden beim skalierbaren EM die ersten 50.000 Datensätze verwendet, um dem Anfangsscan Werte zuzuweisen. Ist dieser Vorgang erfolgreich, verwendet das Modell nur diese Daten. Wenn das Modell mit 50.000 Datensätzen nicht geeignet ist, werden weitere 50.000 Datensätze gelesen. In nicht skalierbarem EM wird das ganze Dataset unabhängig von seiner Größe gelesen. Mit dieser Methode werden unter Umständen zwar genauere Cluster erstellt, die Arbeitsspeicheranforderungen können jedoch erheblich sein. Da skalierbares EM-Clustering mit einem lokalen Puffer arbeitet, erfolgt die Iteration durch die Daten deutlich schneller und der Algorithmus nutzt den CPU-Arbeitsspeichercache besser aus als das nicht skalierbare EM-Clustering. Darüber hinaus ist das skalierbare EM dreimal so schnell wie das nicht skalierbare EM, auch wenn alle Daten in den Hauptspeicher passen. In den meisten Fällen führt die Verbesserung der Leistung nicht zu einer geringeren Qualität des Gesamtmodells.  
  
 Einen technischen Bericht mit einer Beschreibung der EM-Implementierung im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus finden Sie unter [Scaling EM (Expectation Maximization) Clustering to Large Databases](http://go.microsoft.com/fwlink/?LinkId=45964)(Skalieren des EM-Clusterings in großen Datenbanken).  
  
### <a name="k-means-clustering"></a>K-Means-Clustering  
 K-Means-Clustering ist eine gängige Methode zum Zuweisen der Clustermitgliedschaft, indem Unterschiede zwischen Elementen eines Clusters minimiert und die Entfernung zwischen den Clustern gleichzeitig maximiert werden. Das Wort „Means“ im Begriff K-Means bezieht sich auf den *Schwerpunkt* des Clusters. Hierbei handelt es sich um einen willkürlich ausgewählten Datenpunkt, der so lange iterativ optimiert wird, bis er das genaue arithmetische Mittel aller Datenpunkte des Clusters repräsentiert. Das "K" verweist auf eine beliebige Anzahl von Punkten, mit denen dem Clusterprozess Anfangswerte zugewiesen werden. Der K-Means-Algorithmus berechnet das Quadrat der euklidischen Entfernungen zwischen Datensätzen in einem Cluster und dem Vektor, der das arithmetische Clustermittel darstellt, und konvergiert zu einer endgültigen Menge von K-Clustern, wenn diese Summe den Mindestwert erreicht.  
  
 Der K-Means-Algorithmus weist jeden Datenpunkt genau einem Cluster zu und lässt keine Unsicherheit in Bezug auf die Mitgliedschaft zu. Die Mitgliedschaft in einem Cluster wird als Entfernung vom Schwerpunkt ausgedrückt.  
  
 In der Regel wird der K-Means-Algorithmus zum Erstellen von Clustern kontinuierlicher Attribute verwendet, wobei die Berechnung der Entfernung zu einem arithmetischen Mittel unkompliziert ist. Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Implementierung passt die K-Means-Methode jedoch mithilfe von Wahrscheinlichkeiten an, um diskrete Attribute zu gruppieren.  Für diskrete Attribute wird die Entfernung eines Datenpunkts von einem bestimmten Cluster wie folgt berechnet:  
  
 1 - P (Datenpunkt, Cluster)  
  
> [!NOTE]  
>  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus macht die zur Berechnung von K-Means verwendete Abstandsfunktion nicht verfügbar. Abstandsmaße stehen im abgeschlossenen Modell nicht zur Verfügung. Sie können jedoch mithilfe einer Vorhersagefunktion einen Wert zurückgeben, der dem Abstand entspricht, wobei der Abstand als Wahrscheinlichkeit eines Datenpunkts, der zum Cluster gehört, berechnet wird. Weitere Informationen finden Sie unter [ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md).  
  
 Der K-Means-Algorithmus bietet zwei Methoden zum Abfragen des Datasets: die nicht skalierbare K-Means-Methode oder die skalierbare K-Means-Methode. Bei der nicht skalierbaren K-Means-Methode wird das gesamte Dataset geladen und ein Clustering durchlaufen. Dahingegen verwendet der Algorithmus bei der skalierbaren K-Means-Methode die ersten 50.000 Fälle und liest zusätzliche Fälle nur dann, wenn weitere Daten erforderlich sind, um eine passende Übereinstimmung zwischen Modell und Daten zu erzielen.  
  
### <a name="updates-to-the-microsoft-clustering-algorithm-in-sql-server-2008"></a>Updates des Microsoft Clustering-Algorithmus in SQL Server 2008  
 In SQL Server 2008 wurde die Standardkonfiguration des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Clusteringalgorithmus so geändert, dass der interne Parameter NORMALIZATION = 1 verwendet wird. Normalisierung erfolgt unter Verwendung der Z-Ergebnisstatistiken, und es wird eine Normalverteilung angenommen. Ziel dieses geänderten Standardverhaltens ist, die Auswirkung von Attributen mit großen Magnituden und vielen Ausreißern zu minimieren. Die z-Ergebnis-Normalisierung kann jedoch zu einer Änderung der Clusteringergebnisse in anormalen (z. B. gleichmäßigen) Verteilungen führen. Um eine Normalisierung zu vermeiden, jedoch das gleiche Verhalten wie mit dem K-Means-Clustering-Algorithmus in SQL Server 2005 zu erzielen, können Sie im Dialogfeld **Parametereinstellungen** den benutzerdefinierten Parameter NORMALIZATION hinzuzufügen und dessen Wert auf 0 festlegen.  
  
> [!NOTE]  
>  Der NORMALIZATION-Parameter ist eine interne Eigenschaft des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus und wird nicht unterstützt. Im Allgemeinen wird die Verwendung von Normalisierung in Clusteringmodellen empfohlen, da sie die Modellergebnisse verbessert.  
  
## <a name="customizing-the-microsoft-clustering-algorithm"></a>Anpassen des Microsoft Clustering-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus unterstützt mehrere Parameter, die sich auf das Verhalten, die Leistung und die Genauigkeit des resultierenden Miningmodells auswirken.  
  
### <a name="setting-algorithm-parameters"></a>Festlegen von Algorithmusparametern  
 In der folgenden Tabelle werden die Parameter beschrieben, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus verwendet werden können. Diese Parameter wirken sich sowohl auf die Leistung als auch auf die Genauigkeit des resultierenden Miningmodells aus.  
  
 CLUSTERING_METHOD  
 Gibt an, welche Clustermethode vom Algorithmus verwendet wird. Die folgenden Clustermethoden stehen zur Verfügung:  
  
|ID|Methode|  
|--------|------------|  
|1|EM skalierbar|  
|2|EM nicht skalierbar|  
|3|K-Means skalierbar|  
|4|K-Means nicht skalierbar|  
  
 Die Standardeinstellung ist 1 (EM skalierbar).  
  
 CLUSTER_COUNT  
 Gibt die ungefähre Anzahl der vom Algorithmus zu erstellenden Cluster an. Falls die ungefähre Anzahl von Clustern nicht aus den Daten erstellt werden kann, erstellt der Algorithmus so viele Cluster wie möglich. Durch Festlegen des CLUSTER_COUNT-Parameters auf 0 wird der Algorithmus zur Verwendung heuristischer Methoden veranlasst, um die Anzahl von zu erstellenden Clustern so gut wie möglich zu bestimmen.  
  
 Der Standardwert lautet 10.  
  
 CLUSTER_SEED  
 Gibt den numerischen Ausgangswert für die zufällige Clustergenerierung in der Anfangsphase der Modellerstellung an.  
  
 Durch Ändern dieses Werts können Sie die Art und Weise ändern, wie Anfangscluster erstellt werden, und anschließend Modelle vergleichen, die mit unterschiedlichen Anfangswerten erstellt wurden. Wenn der Anfangswert geändert wird, die gefundenen Cluster sich jedoch nicht erheblich ändern, kann das Modell als relativ stabil betrachtet werden.  
  
 Die Standardeinstellung ist 0.  
  
 MINIMUM_SUPPORT  
 Gibt die Mindestanzahl von Fällen an, die erforderlich sind, um einen Cluster zu erstellen. Wenn die Zahl der Fälle im Cluster kleiner als dieser Wert ist, gilt der Cluster als leer und wird verworfen.  
  
 Wenn Sie diese Zahl zu hoch festgelegt haben, entgehen Ihnen möglicherweise gültige Cluster.  
  
> [!NOTE]  
>  Wenn Sie die Standardclustermethode EM verwenden, haben einige Cluster möglicherweise einen niedrigeren Unterstützungswert als der angegebene Wert. Dies liegt daran, dass jeder Fall im Hinblick auf seine Mitgliedschaft in allen möglichen Clustern ausgewertet wird und für einige Cluster möglicherweise nur minimale Unterstützung besteht.  
  
 Der Standardwert lautet 1.  
  
 MODELLING_CARDINALITY  
 Gibt die Anzahl von Stichprobenmodellen an, die während des Clusterprozesses erstellt werden.  
  
 Eine Reduzierung der Anzahl von Kandidatenmodellen kann zwar zur Verbesserung der Leistung führen, beinhaltet jedoch das Risiko, einige gute Kandidatenmodelle zu verpassen.  
  
 Der Standardwert lautet 10.  
  
 STOPPING_TOLERANCE  
 Gibt den Wert an, mit dem bestimmt wird, wann Konvergenz erreicht ist und die Modellerstellung mit dem Algorithmus abgeschlossen ist. Konvergenz ist erreicht, wenn die Gesamtänderung der Clusterwahrscheinlichkeiten kleiner als das Verhältnis des STOPPING_TOLERANCE-Parameters geteilt durch die Modellgröße ist.  
  
 Der Standardwert lautet 10.  
  
 SAMPLE_SIZE  
 Gibt die Anzahl von Fällen an, die bei jedem Durchlauf des Algorithmus verwendet werden, wenn der CLUSTERING_METHOD-Parameter auf eine der skalierbaren Clustermethoden festgelegt ist. Das Festlegen des SAMPLE_SIZE-Parameters auf 0 bewirkt eine Clustererstellung für das gesamte Dataset in einem einzelnen Durchlauf. Das gesamte Dataset in einem einzelnen Durchlauf zu laden, kann zu Problemen mit dem Arbeitsspeicher und der Leistung führen.  
  
 Der Standardwert ist 50.000.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Gibt die maximale Anzahl von Eingabeattributen an, die der Algorithmus verarbeiten kann, bevor die Funktionsauswahl aufgerufen wird. Wenn dieser Wert auf 0 festgelegt wird, ist keine maximale Anzahl von Attributen angegeben.  
  
 Durch Erhöhen der Attributanzahl kann die Leistung erheblich beeinträchtigt werden.  
  
 Der Standardwert lautet 255.  
  
 MAXIMUM_STATES  
 Gibt die maximale Anzahl der vom Algorithmus unterstützten Attributstatus an. Wenn ein Attribut mehr Status als die maximale Anzahl hat, verwendet der Algorithmus die gebräuchlichsten Status und ignoriert die restlichen Status.  
  
 Durch Erhöhen der Statusanzahl kann die Leistung erheblich beeinträchtigt werden.  
  
 Der Standardwert ist 100.  
  
### <a name="modeling-flags"></a>Modellierungsflags  
 Der Algorithmus unterstützt die folgenden Modellierungsflags. Modellierungsflags werden beim Erstellen der Miningstruktur oder des Miningmodells definiert. Die Modellierungsflags geben an, wie die Werte in den einzelnen Spalten während der Analyse behandelt werden.  
  
|Modellierungsflag|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Die Spalte kann zwei mögliche Statuswerte haben: Missing und Existing. Ein NULL-Wert ist ein fehlender Wert.<br /><br /> Gilt für die Miningmodellspalte.|  
|NOT NULL|Die Spalte darf keinen NULL-Wert enthalten. Ein Fehler tritt auf, wenn Analysis Services während des Modelltrainings einen NULL-Wert erkennt.<br /><br /> Gilt für die Miningstrukturspalte.|  
  
## <a name="requirements"></a>Anforderungen  
 Ein Clustermodell muss eine Schlüsselspalte und Eingabespalten enthalten. Sie können Eingabespalten auch als vorhersagbar definieren. Auf **Predict Only** festgelegte Spalten werden nicht verwendet, um Cluster zu erstellen. Die Verteilung dieser Werte in den Clustern wird berechnet, nachdem die Cluster erstellt sind.  
  
### <a name="input-and-predictable-columns"></a>Eingabespalten und vorhersagbare Spalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering-Algorithmus unterstützt bestimmte Eingabespalten und vorhersagbare Spalten. Diese sind in der nachstehenden Tabelle aufgelistet. Weitere Informationen zur Bedeutung der Inhaltstypen in einem Miningmodell finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Column|Inhaltstypen|  
|------------|-------------------|  
|Eingabeattribut|Continuous, Cyclical, Discrete, Discretized, Key, Table, Ordered|  
|Vorhersagbares Attribut|Continuous, Cyclical, Discrete, Discretized, Table, Ordered|  
  
> [!NOTE]  
>  Zyklische und sortierte Inhaltstypen werden unterstützt, der Algorithmus behandelt sie jedoch als diskrete Werte und führt keine spezielle Verarbeitung durch.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)   
 [Clusteringmodellabfragen](../../analysis-services/data-mining/clustering-model-query-examples.md)   
 [Miningmodellinhalt, für das Clustering-Modelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
