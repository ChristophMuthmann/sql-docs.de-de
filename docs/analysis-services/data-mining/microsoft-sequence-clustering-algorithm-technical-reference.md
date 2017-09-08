---
title: Microsoft Sequence Clustering Algorithm Technical Reference | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MAXIMUM_SEQUENCE_STATES parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_STATES parameter
- sequence clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: 251c369d-6b02-4687-964e-39bf55c9b009
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7e26ac40b7cb47370107f348548cf2cc7489efa1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Technische Referenz für den Microsoft Sequence Clustering-Algorithmus
  Der Microsoft Sequence Clustering-Algorithmus ist ein hybrider Algorithmus, der Markov-Kettenanalysen verbindet, um sortierte Sequenzen zu identifizieren, und die Ergebnisse dieser Analyse mit Clustering-Techniken verbindet, um Cluster basierend auf den Sequenzen und anderen Attributen im Modell zu erstellen. In diesem Thema werden die Implementierung des Algorithmus, die Anpassung des Algorithmus und die speziellen Anforderungen für Sequenzclustermodelle beschrieben.  
  
 Weitere allgemeine Informationen über den Algorithmus, einschließlich Durchsuchen und Abfragen von Sequenzclustermodellen, finden Sie unter [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md).  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Implementierung des Microsoft Sequence Clustering-Algorithmus  
 Das Microsoft Sequence Clustering-Modell verwendet Markov-Modelle, um Sequenzen zu identifizieren und die Wahrscheinlichkeit von Sequenzen zu bestimmen. Ein Markov-Modell ist ein gerichteter Graf, der die Übergänge zwischen unterschiedlichen Status speichert. Der Microsoft Sequence Clustering-Algorithmus verwendet n-Ordnung-Markov-Ketten, kein Hidden Markov-Modell.  
  
 Die Anzahl der Ordnungen in einer Markov-Kette gibt Aufschluss darüber, wie viele Status zur Bestimmung der Wahrscheinlichkeit der aktuellen Status verwendet werden. In einem Markov-Modell der 1. Ordnung hängt die Wahrscheinlichkeit des aktuellen Status nur vom vorherigen Status ab. In einer Markov-Kette der 2. Ordnung hängt die Wahrscheinlichkeit eines Status von den beiden vorherigen Status ab usw. Für jede Markov-Kette speichert eine Übergangsmatrix die Übergänge für jede Kombination von Status. Mit zunehmender Länge der Markov-Kette nimmt auch die Größe der Matrix exponentiell zu, und die Matrix weist eine äußerst geringe Dichte auf. Die Verarbeitungszeit nimmt dabei proportional zu.  
  
 Es kann hilfreich sein, die Kette anhand des Beispiels der Clickstreamanalyse visuell darzustellen. Diese Analyse untersucht die Besuche auf den Seiten einer Website. Jeder Benutzer erstellt eine lange Sequenz von Klicks für jede Sitzung. Beim Erstellen eines Modells zur Analyse von Benutzerverhalten auf einer Website besteht das für das Trainieren verwendete Dataset aus einer Sequenz von URLs, die in einen Graf konvertiert werden, der die Anzahl aller Instanzen des gleichen Klickpfads enthält. Der Graf enthält beispielsweise die Wahrscheinlichkeit, dass der Benutzer von Seite 1 auf Seite 2 wechselt (10 %), die Wahrscheinlichkeit, dass der Benutzer von Seite 1 auf Seite 3 wechselt (20 %) usw. Wenn Sie alle möglichen Pfade und Pfadteile zusammennehmen, erhalten Sie einen Grafen, der möglicherweise wesentlich länger und komplexer ist als ein einzelner beobachteter Pfad.  
  
 Standardmäßig verwendet der Microsoft Sequence Clustering-Algorithmus die EM-Clusteringmethode (Expectation Maximization). Weitere Informationen finden Sie unter [Technische Referenz für den Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
 Die Ziele des Clusterings sind sowohl die sequenziellen als auch die nicht sequenziellen Attribute. Jeder Cluster wird zufällig mit einer Wahrscheinlichkeitsverteilung ausgewählt. Darüber hinaus verfügt jeder Cluster über eine Markov-Kette, die die Gesamtmenge der Pfade darstellt, sowie über eine Matrix, die die Sequenzstatusübergänge und Wahrscheinlichkeiten enthält. Basierend auf der ursprünglichen Verteilung wird anhand der Bayes-Regel die Wahrscheinlichkeit eines Attributs, einschließlich einer Sequenz, in einem bestimmten Cluster berechnet.  
  
 Der Microsoft Sequence Clustering-Algorithmus unterstützt zusätzliche nicht sequenzielle Attribute für das Modell. Das bedeutet, dass diese zusätzlichen Attribute mit den Sequenzattributen kombiniert werden, um Cluster von Fällen mit ähnlichen Attributen wie in einem typischen Clustermodell zu erstellen.  
  
 Ein Sequenzclustermodell erstellt tendenziell weitaus mehr Cluster als ein typisches Clustermodell. Daher führt der Microsoft Sequence Clustering-Algorithmus eine *Clusterzerlegung*durch, um Cluster basierend auf Sequenzen und anderen Attributen zu trennen.  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>Funktionsauswahl in einem Sequenzclustermodell  
 Die Funktionsauswahl wird beim Erstellen von Sequenzen nicht aufgerufen. In der Clusteringphase ist sie jedoch gültig.  
  
|Modelltyp|Funktionseauswahlmethode|Kommentare|  
|----------------|------------------------------|--------------|  
|Sequenzclustering|Wird nicht verwendet|Die Funktionsauswahl wird nicht aufgerufen, allerdings lässt sich das Verhalten des Algorithmus durch Festlegen der Parameter MINIMUM_SUPPORT und MINIMUM_PROBABILIITY steuern.|  
|Clustering|Interessantheitsgrad|Obwohl der Clusteringalgorithmus diskrete oder diskretisierte Attribute verwenden kann, wird die Bewertung jedes Attributs als Distanz berechnet und ist daher kontinuierlich. Daher wird der Interessantheitsgrad verwendet.|  
  
 Weitere Informationen finden Sie unter [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
### <a name="optimizing-performance"></a>Optimieren der Leistung  
 Der Microsoft Sequence Clustering-Algorithmus unterstützt verschiedene Möglichkeiten zur Optimierung der Verarbeitung:  
  
-   Kontrollieren der Anzahl generierter Cluster durch Festlegen eines Werts für den CLUSTER_COUNT-Parameter.  
  
-   Reduzieren der Anzahl der als Attribute eingeschlossenen Sequenzen durch Erhöhen des Werts des MINIMUM_SUPPORT-Parameters. Als Folge werden seltene Sequenzen ausgeschlossen.  
  
-   Reduzieren der Komplexität vor dem Verarbeiten des Modells durch Gruppieren von verknüpften Attributen.  
  
 Im Allgemeinen haben Sie mehrere Möglichkeiten, die Leistung einer Markow-Kette n-ter Ordnung zu verbessern:  
  
-   Kontrollieren der Länge der möglichen Sequenzen.  
  
-   Programmgesteuertes Reduzieren des Werts von „n“.  
  
-   Speichern ausschließlich von Wahrscheinlichkeiten, die einen angegebenen Schwellenwert überschreiten.  
  
 Eine umfassende Erläuterung dieser Methoden würde den Rahmen dieses Themas sprengen.  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>Anpassen des Sequence Clustering-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus unterstützt mehrere Parameter, die sich auf das Verhalten, die Leistung und die Genauigkeit des resultierenden Miningmodells auswirken. Sie können auch das Verhalten des fertigen Modells ändern, indem Sie die Modellierungsflags setzen, die die Verarbeitungsweise der Trainingsdaten steuern.  
  
### <a name="setting-algorithm-parameters"></a>Festlegen von Algorithmusparametern  
 In der folgenden Tabelle werden die Parameter beschrieben, die mit dem Microsoft Sequence Clustering-Algorithmus verwendet werden können.  
  
 CLUSTER_COUNT  
 Gibt die ungefähre Anzahl der vom Algorithmus zu erstellenden Cluster an. Falls die ungefähre Anzahl von Clustern nicht aus den Daten erstellt werden kann, erstellt der Algorithmus so viele Cluster wie möglich. Durch Festlegen des CLUSTER_COUNT-Parameters auf 0 wird der Algorithmus zum Verwenden heuristischer Methoden veranlasst, um die Anzahl von zu erstellenden Clustern so gut wie möglich zu bestimmen.  
  
 Der Standardwert lautet 10.  
  
> [!NOTE]  
>  Eine festgelegte Zahl ungleich null dient als Hinweis für den Algorithmus, der daraufhin mit dem Ziel fortfährt, die angegebene Zahl zu finden, am Ende jedoch eine höhere oder niedrigere Zahl finden kann.  
  
 MINIMUM_SUPPORT  
 Gibt die Mindestzahl an Fällen an, die als Unterstützung eines Attributs zum Erstellen eines Clusters erforderlich ist.  
  
 Der Standardwert lautet 10.  
  
 MAXIMUM_SEQUENCE_STATES  
 Gibt die maximale Anzahl von Status an, die eine Sequenz annehmen kann.  
  
 Das Festlegen dieses Werts auf eine Zahl größer 100 kann dazu führen, dass das vom Algorithmus erstellte Modell keine aussagekräftigen Informationen enthält.  
  
 Der Standardwert ist 64.  
  
 MAXIMUM_STATES  
 Gibt die maximale Anzahl vom Algorithmus unterstützter Status für ein nicht sequenzielles Attribut an. Falls die Anzahl der Status für ein nicht sequenzielles Attribut größer als die maximale Anzahl von Status ist, verwendet der Algorithmus die gebräuchlichsten Status und behandelt die restlichen Status als **Missing**.  
  
 Der Standardwert ist 100.  
  
### <a name="modeling-flags"></a>Modellierungsflags  
 Die folgenden Modellierungsflags werden zur Verwendung mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus unterstützt.  
  
 NOT NULL  
 Gibt an, dass die Spalte keinen NULL-Wert enthalten kann. Ein Fehler tritt auf, wenn Analysis Services während des Modelltrainings einen NULL-Wert erkennt.  
  
 Gilt für die Miningstrukturspalte.  
  
 MODEL_EXISTENCE_ONLY  
 Dies bedeutet, dass die Spalte zwei mögliche Statuswerte haben kann: **Missing** und **Existing**. Der Wert 0 wird als **Missing** behandelt.  
  
 Gilt für die Miningmodellspalte.  
  
 Weitere Informationen zur Verwendung fehlender Werte in Miningmodellen und zu den Auswirkungen fehlender Werte auf die Wahrscheinlichkeitsergebnisse finden Sie unter [ Fehlende Werte &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
## <a name="requirements"></a>Anforderungen  
 Die Falltabelle muss eine case ID-Spalte aufweisen. Optional kann die Falltabelle andere Spalten enthalten, die Attribute über den Fall speichern.  
  
 Der Microsoft Sequence Clustering-Algorithmus erfordert als geschachtelte Tabelle gespeicherte Sequenzinformationen. Die geschachtelte Tabelle muss eine einzelne Key Sequence-Spalte enthalten. Eine **Key Sequence** -Spalte kann jeden Datentyp enthalten, der sortiert werden kann, einschließlich Zeichenfolgen-Datentypen. Die Spalte muss jedoch eindeutige Werte für jeden Fall enthalten. Darüber hinaus müssen Sie vor dem Verarbeiten des Modells sicherstellen, dass sowohl die Falltabelle als auch die geschachtelte Tabelle in aufsteigender Reihenfolge nach dem Schlüssel, der die Tabellen verknüpft, sortiert wird.  
  
> [!NOTE]  
>  Wenn Sie ein Modell erstellen, das zwar den Microsoft Sequence-Algorithmus, jedoch keine Sequenzspalte verwendet, enthält das resultierende Modell keine Sequenzen, sondern gruppiert einfach Fälle basierend auf anderen Attributen, die im Modell enthalten sind.  
  
### <a name="input-and-predictable-columns"></a>Eingabespalten und vorhersagbare Spalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus unterstützt bestimmte Eingabespalten und vorhersagbare Spalten. Diese sind in der nachstehenden Tabelle aufgelistet. Weitere Informationen zur Bedeutung der Inhaltstypen in einem Miningmodell finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Column|Inhaltstypen|  
|------------|-------------------|  
|Eingabeattribut|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Table und Ordered|  
|Vorhersagbares Attribut|Continuous, Cyclical, Discrete, Discretized, Table und Ordered|  
  
## <a name="remarks"></a>Hinweise  
  
-   Verwenden Sie die [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md)-Funktion, um Voraussagen über Sequenzen zu treffen. Weitere Informationen zu den Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die die Sequenzvorhersage unterstützen, finden Sie unter [Von den SQL Server 2012-Editionen unterstützte Funktionen](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
-   Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus unterstützt nicht die Verwendung von PMML (Predictive Model Markup Language) zum Erstellen von Miningmodellen.  
  
-   Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus unterstützt Drillthrough, die Verwendung von OLAP-Miningmodellen und die Verwendung von Data Mining-Dimensionen.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Sequence Clustering-Abfragebeispiele](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Miningmodellinhalt von Sequence Clustering-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
