---
title: "Datamining-Algorithmen (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
caps.latest.revision: 74
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85f1333bc1f9674dcdb5274e0b2768c401fd2d7c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>Data Mining-Algorithmen (Analysis Services - Data Mining)
  Ein *Algorithmus* beim Data Mining (oder Machine Learning) besteht aus einer Reihe von Heuristiken und Berechnungen, durch die aus Daten ein Modell erstellt wird. Um ein Modell zu erstellen, werden vom Algorithmus zuerst die von Ihnen bereitgestellten Daten analysiert und bestimmte Muster oder Trends gesucht. Mithilfe der Ergebnisse dieser Analyse über zahlreiche Iterationen definiert der Algorithmus die optimalen Parameter zum Erstellen des Miningmodells. Diese Parameter werden dann für das gesamte Dataset übernommen, um aussagefähige Muster und ausführliche Statistiken zu extrahieren.  
  
 Das von einem Algorithmus aus Ihren Daten erstellte Miningmodell kann verschiedene Formen annehmen, einschließlich der folgenden:  
  
-   Eine Reihe von Clustern, die die Beziehungen der Fälle in einem Dataset beschreiben.  
  
-   Eine Entscheidungsstruktur, durch die ein Ergebnis vorhergesagt und beschrieben wird, wie sich unterschiedliche Kriterien auf dieses Ergebnis auswirken.  
  
-   Ein mathematisches Modell zum Vorhersagen von Umsätzen.  
  
-   Eine Gruppe von Regeln, die beschreiben, wie Produkte in einer Transaktion gruppiert werden, und die Wahrscheinlichkeiten, dass Produkte zusammen gekauft werden.  
  
 Die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining bereitgestellten Algorithmen sind die beliebtesten und am besten erforschten Methoden zum Ableiten von Mustern aus Daten. K-Means-Clustering ist z. B. einer der ältesten Clusteringalgorithmen, der in vielen verschiedenen Tools und mit vielen verschiedenen Implementierungen und Optionen zur Verfügung steht. Die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining verwendete spezifische Implementierung von K-Means-Clustering wurde allerdings von Microsoft Research entwickelt und anschließend für die Zusammenarbeit mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]optimiert. Alle Data Mining-Algorithmen von Microsoft können umfassend angepasst werden und sind mithilfe der bereitgestellten APIs vollständig programmierbar. Mithilfe der Data Mining-Komponenten in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]können Sie auch das Erstellen, Trainieren und erneute Trainieren von Modellen automatisieren.  
  
 Sie können auch Algorithmen von Drittanbietern verwenden, die der Spezifikation von OLE DB für Data Mining entsprechen, oder benutzerdefinierte Algorithmen entwickeln, die als Dienste registriert und dann innerhalb des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining-Frameworks verwendet werden können.  
  
## <a name="choosing-the-right-algorithm"></a>Auswählen des richtigen Algorithmus  
 Es kann schwierig sein, den besten Algorithmus für einen bestimmten analytischen Task auszuwählen. Während verschiedene Algorithmen zum Ausführen derselben Geschäftsaufgabe verwendet werden können, liefert jeder Algorithmus ein anderes Ergebnis, und einige Algorithmen können mehr als eine Ergebnisart ergeben. Sie können z. B. den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus nicht nur für Vorhersagen verwenden, sondern auch als Möglichkeit, die Anzahl der Spalten in einem Dataset zu reduzieren, weil die Entscheidungsstruktur Spalten identifizieren kann, die sich nicht auf das endgültige Miningmodell auswirken.  
  
### <a name="choosing-an-algorithm-by-type"></a>Auswählen eines Algorithmus nach Typ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining bietet die folgenden Algorithmentypen:  
  
-   **Klassifikationsalgorithmen** sagen basierend auf den anderen Attributen im Dataset mindestens eine diskrete Variable voraus.  
  
-   **Regressionsalgorithmen** sagen basierend auf anderen Attributen im Dataset mindestens eine kontinuierliche Variable voraus, z. B. den Gewinn oder Verlust.  
  
-   **Segmentierungsalgorithmen** teilen Daten in Gruppen oder Cluster aus Elementen auf, die ähnliche Eigenschaften haben.  
  
-   **Zuordnungsalgorithmen** suchen nach Korrelationen zwischen verschiedenen Attributen in einem Dataset. Die häufigste Anwendung dieser Algorithmusart besteht im Erstellen von Zuordnungsregeln, die für eine Warenkorbanalyse verwendet werden können.  
  
-   **Sequenzanalysealgorithmen** fassen häufige Sequenzen oder Episoden in Daten zusammen, wie z. B. eine Reihe von Mausklicks auf einer Website oder eine Reihe von Protokollereignissen vor einer Computerwartung.  
  
 Es gibt jedoch keinen Grund, sich in Projektmappen auf einen Algorithmus zu beschränken. Erfahrene Analytiker verwenden manchmal einen Algorithmus, um die effizientesten Eingaben (d. h. Variablen) zu bestimmen, und wenden dann einen anderen Algorithmus an, um ein bestimmtes Ergebnis auf Grundlage dieser Daten vorherzusagen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Mithilfe von Data Mining können Sie mehrere Modelle für eine einzelne Miningstruktur erstellen. Daher können innerhalb einer einzelnen Data Mining-Projektmappe ein Clusteringalgorithmus, ein Entscheidungsstrukturmodell und ein Naïve Bayes-Modell verwendet werden, um unterschiedliche Sichten der Daten zu erhalten. Sie können mithilfe mehrerer Algorithmen in einer einzelnen Projektmappe auch separate Tasks ausführen: Beispielsweise können Sie mit dem Regressionsalgorithmus eine finanzielle Vorhersage generieren und mit dem Neural Network-Algorithmus die Faktoren analysieren, durch die Prognosen beeinflusst wird.  
  
### <a name="choosing-an-algorithm-by-task"></a>Auswählen eines Algorithmus nach Task  
 Um Ihnen die Auswahl eines Algorithmus für einen bestimmten Task zu erleichtern, ist in der folgende Tabelle angegeben, für welche Tasktypen die einzelnen Algorithmen üblicherweise verwendet werden.  
  
|Beispiele für Tasks|Microsoft-Algorithmen|  
|-----------------------|---------------------------------|  
|**Vorhersagen eines diskreten Attributs:**<br /><br /> Kennzeichnen von Kunden in einer Liste potenzieller Käufer als Kunden mit wahrscheinlicher oder unwahrscheinlicher Kaufabsicht.<br /><br /> Berechnen der Wahrscheinlichkeit, dass ein Server innerhalb der nächsten sechs Monate ausfällt.<br /><br /> Kategorisieren von Therapieergebnissen und Untersuchen verwandter Faktoren.|[Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft Naive Bayes-Algorithmus](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)|  
|**Vorhersagen eines kontinuierlichen Attributs:**<br /><br /> Vorhersagen des Verkaufstrends für das nächste Jahr.<br /><br /> Vorhersagen von Websitebesuchern anhand historischer und saisonaler Trends.<br /><br /> Generieren einer Risikobewertung anhand demografischer Daten.|[Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft Time Series-Algorithmus](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)<br /><br /> [Microsoft Linear Regression-Algorithmus](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)|  
|**Vorhersagen einer Sequenz:**<br /><br /> Ausführen einer Clickstreamanalyse für eine Unternehmenswebsite.<br /><br /> Analysieren der Faktoren, die zu einem Serverausfall führen.<br /><br /> Aufzeichnen und Analysieren von Arbeitsabläufen während ambulanter Arztbesuche, um Best Practices für allgemeine Abläufe aufzustellen.|[Microsoft Sequence Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
|**Suchen von Gruppen aus allgemeinen Elementen in Transaktionen:**<br /><br /> Bestimmen der Produktplatzierung mithilfe der Warenkorbanalyse.<br /><br /> Vorschlagen zusätzlicher Produktkäufe für einen Kunden.<br /><br /> Analysieren einer Besucherumfrage zu einer Veranstaltung, um festzustellen, welche Aktivitäten oder Stände eine Korrelation aufweisen, und zukünftige Aktivitäten zu planen.|[Microsoft Association-Algorithmus](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)|  
|**Suchen von Gruppen mit ähnlichen Elementen:**<br /><br /> Gruppieren von Patientenrisikoprofilen auf der Grundlage von Attributen wie demografischen oder Verhaltensdaten.<br /><br /> Analysieren von Benutzern anhand von Browsing- und Kaufmustern.<br /><br /> Identifizieren von Servern mit ähnlichen Verwendungsmerkmalen.|[Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft Sequence Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Die folgende Tabelle enthält Links zu Schulungsressourcen für die einzelnen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining bereitgestellten Data Mining-Algorithmen:  
  
|||  
|-|-|  
|**Grundlegende Algorithmusbeschreibung**|Erläutert die Bedeutung und Funktionsweise des Algorithmus und zeigt mögliche Geschäftsszenarien auf, in denen der Algorithmus hilfreich sein könnte.|  
||[Microsoft Association-Algorithmus](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft Linear Regression-Algorithmus](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)<br /><br /> [Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)<br /><br /> [Microsoft Naive Bayes-Algorithmus](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft Sequence Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)<br /><br /> [Microsoft Time Series-Algorithmus](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)|  
|**Technische Referenz**|Stellt technische Details zur Implementierung des Algorithmus ggf. mit Verweisen auf wissenschaftliche Artikel bereit. Listet die Parameter auf, die Sie festlegen können, um das Verhalten des Algorithmus zu steuern und die Ergebnisse im Modell anzupassen. Beschreibt Datenanforderungen sowie Leistungstipps, falls möglich.|  
||[Technische Referenz für den Microsoft Association-Algorithmus](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Linear Regression-Algorithmus](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Naive Bayes-Algorithmus](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Sequence Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Technische Referenz für den Microsoft Time Series-Algorithmus](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)|  
|**Modellinhalt**|Beschreibt die Strukturierung der Informationen innerhalb der einzelnen Data Mining-Modelltypen und erläutert, wie die in den einzelnen Knoten gespeicherten Informationen interpretiert werden.|  
||[Miningmodellinhalt von Zuordnungsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [Miningmodellinhalt von Clustermodellen &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [Miningmodellinhalt von Entscheidungsstrukturmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [Miningmodellinhalt von linearen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)<br /><br /> [Miningmodellinhalt von Naive Bayes-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [Miningmodellinhalt von neuronalen Netzwerkmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [Miningmodellinhalt von Sequence Clustering-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)<br /><br /> [Miningmodellinhalt von Zeitreihenmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**Data Mining-Abfragen**|Stellt mehrere Abfragen bereit, die mit jedem Modelltyp verwendet werden können. Zu den Beispielen gehören Inhaltsabfragen, die Aufschluss über die im Modell enthaltenen Muster geben, und Vorhersageabfragen, die Sie beim Generieren von Vorhersagen auf Grundlage dieser Muster unterstützen.|  
||[Beispiele für Zuordnungsmodellabfragen](../../analysis-services/data-mining/association-model-query-examples.md)<br /><br /> [Beispiele für Clusteringmodellabfragen](../../analysis-services/data-mining/clustering-model-query-examples.md)<br /><br /> [Beispiele für Entscheidungsstruktur-Modellabfragen](../../analysis-services/data-mining/decision-trees-model-query-examples.md)<br /><br /> [Beispiele für lineare Regressionsmodellabfrage](../../analysis-services/data-mining/linear-regression-model-query-examples.md)<br /><br /> [Logistische Regressionsmodell-Abfragebeispiele](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)<br /><br /> [Beispiele für Naive Bayes-Modellabfrage](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)<br /><br /> [Neuronale Beispiele für Netzwerkmodellabfragen](../../analysis-services/data-mining/neural-network-model-query-examples.md)<br /><br /> [Sequenzclusteringmodellabfragebeispiele](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)<br /><br /> [Abfragebeispiel Zeitreihenmodell](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|**Thema**|**Description**|  
|---------------|---------------------|  
|Bestimmen des von einem Data Mining-Modell verwendeten Algorithmus|[Abfragen der Parameter, mit denen ein Miningmodell erstellt wird](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)|  
|Erstellen eines benutzerdefinierten Plug-In-Algorithmus|[Plug-In-Algorithmen](../../analysis-services/data-mining/plugin-algorithms.md)|  
|Durchsuchen eines Modells mit einem algorithmusspezifischen Viewer|[Data Mining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Anzeigen des Inhalts eines Modells unter Verwendung eines generischen Tabellenformats|[Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|Hier erfahren Sie, wie die Daten eingerichtet und Algorithmen zum Erstellen von Modellen verwendet werden|[Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)<br /><br /> [Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Tools](../../analysis-services/data-mining/data-mining-tools.md)  
  
  

