---
title: "Funktionsauswahl (Data Mining) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Miningmodelle [Analysis Services], Funktionsauswahl"
  - "Attribute [Data Mining]"
  - "Funktionsauswahlalgorithmen [Analysis Services]"
  - "Data Mining [Analysis Services], Funktionsauswahl"
  - "Neural Network-Algorithmen [Analysis Services]"
  - "Naive Bayes-Algorithmen [Analysis Services]"
  - "Entscheidungsstrukturalgorithmen [Analysis Services]"
  - "Datasets [Analysis Services]"
  - "Clustering-Algorithmen [Analysis Services]"
  - "Codierung [Data Mining]"
ms.assetid: b044e785-4875-45ab-8ae4-cd3b4e3033bb
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 37
---
# Funktionsauswahl (Data Mining)
  Die *Featureauswahl* ist ein wichtiger Teil für das Machine Learning. Die Featureauswahl bezieht sich auf das Reduzieren der Eingaben für die Verarbeitung und Analyse oder die Suche nach sinnvollen Eingaben. Ein verwandter Begriff ist die *Featureentwicklung* (oder *Featureextraktion*), der sich auf Verfahren zum Extrahieren nützlicher Informationen aus vorhandenen Daten bezieht.  
  
## Wofür dient die Featureauswahl?  
 Die Featureauswahl ist aus verschiedenen Gründen entscheidend für die Erstellung eines guten Modells. Einer ist, dass die Featureauswahl ein gewisses Maß an *Kardinalitätsreduzierung* impliziert, um die Anzahl der Attribute zu reduzieren, die beim Erstellen eines Modells berücksichtigt werden. Daten enthalten fast immer mehr Informationen als für das Erstellen des Modells erforderlich sind – oder die falsche Art von Informationen. Angenommen, Sie verfügen über ein Dataset mit 500 Spalten, die Merkmale von Kunden beschreiben. Wenn die Daten in einigen Spalten jedoch nur eine geringe Dichte aufweisen, bringt es nur sehr wenig, diese dem Modell hinzuzufügen, und wenn einige Spalten sich untereinander duplizieren, könnte die Verwendung beider Spalten Auswirkungen auf das Modell haben.  
  
 Dabei verbessert die Featureauswahl nicht nur die Qualität des Modells, sondern sie macht auch den Prozess der Modellierung effizienter. Wenn Sie nicht benötigte Spalten beim Erstellen des Modells verwenden, ist während des Trainingsprozesses mehr CPU und Arbeitsspeicher erforderlich, und das fertige Modell erfordert mehr Speicherplatz. Auch wenn die Ressourcen keine Rolle spielen, sollten Sie trotzdem mithilfe der Featureauswahl die besten Spalten identifizieren, da nicht benötigte Spalten die Qualität des Modells auf verschiedene Weise beeinträchtigen können:  
  
-   Abweichende oder redundante Daten erschweren die Erkennung sinnvolle Muster.  
  
-   Wenn das Dataset viele Dimensionen umfasst, erfordern die meisten Data Mining-Algorithmen ein viel größeres Trainingsdataset.  
  
 Bei der Featureauswahl wählt der Analyst oder das Modellierungstool oder ein Algorithmus aktiv Attribute basierend auf deren Eignung für die Analyse aus oder verwirft sie.  Der Analyst kann mithilfe der Featureentwicklung Features hinzufügen und vorhandene Daten entfernen oder ändern, während der Machine Learning-Algorithmus in der Regel Spalten bewertet und ihre Nützlichkeit im Modell überprüft.  
  
 ![Feature selection and engineering process](../../analysis-services/data-mining/media/ssdm-featureselectionprocess.png "Feature selection and engineering process")  
  
 Die Featureauswahl ist also hilfreich für die Lösung von zwei Problemen, nämlich dass zu viele Daten mit geringem Wert oder zu wenige hochwertige Daten vorhanden sind. Ziel der Featureauswahl sollte das Ermitteln der kleinstmöglichen Anzahl von Spalten aus der Datenquelle sein, die bei der Erstellung eines Modells von Bedeutung sind.  
  
## Funktionsweise der Featureauswahl in SQL Server Data Mining  
 Die Featureauswahl wird immer ausgeführt, bevor das Modell trainiert wird. Bei manchen Algorithmen sind Methoden zur Featureauswahl „integriert“, sodass irrelevante Spalten ausgeschlossen und die besten Features automatisch erkannt werden. Jeder Algorithmus verfügt über einen eigenen Satz von Standardtechniken für die intelligente Anwendung der Featurereduzierung.  Sie können jedoch auch manuell Parameter festlegen, um das Verhalten der Funktionsauswahl zu beeinflussen.  
  
 Während der automatischen Featureauswahl wird für jedes Attribut ein Score berechnet, und nur die Attribute mit den besten Scores werden für das Modell ausgewählt. Sie können den Schwellenwert für die besten Ergebnisse auch anpassen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining bietet mehrere Methoden zum Berechnen dieser Scores. Welche spezifische Methode auf das jeweilige Modell angewendet wird, hängt von folgenden Faktoren ab:  
  
-   Im Modell verwendeter Algorithmus  
  
-   Datentyp des Attributs  
  
-   Für das Modell festgelegte Parameter  
  
 Die Funktionsauswahl wird auf Eingaben, vorhersagbare Attribute und Statuswerte in einer Spalte angewandt. Nachdem die Bewertung für die Funktionsauswahl abgeschlossen ist, werden nur die vom Algorithmus ausgewählten Attribute und Statusangaben bei der Modellerstellung berücksichtigt und für Vorhersagen zur Verfügung gestellt. Bei Auswahl eines vorhersagbaren Attributs, das den Schwellenwert für die Funktionsauswahl nicht erfüllt, kann das Attribut zwar trotzdem für die Vorhersage verwendet werden, in diesem Fall basieren die Vorhersagen jedoch ausschließlich auf den globalen, im Modell vorhandenen Statistiken.  
  
> [!NOTE]  
>  Die Funktionsauswahl betrifft nur die Spalten, die im Modell verwendet werden, und wirkt sich nicht auf die Speicherung der Miningstruktur aus. Die Spalten, die nicht in das Miningmodell aufgenommen werden, sind in der Struktur weiterhin verfügbar, und die Daten der Miningstrukturspalten werden zwischengespeichert.  
  
### Scores für die Featureauswahl  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining unterstützt diese gängigen und bewährten Methoden für das Bewerten von Attributen. Die bei bestimmten Algorithmen oder Datasets angewendete Methode hängt von den Datentypen und der Spaltenverwendung ab.  
  
-   Die Bewertung des *Interessantheitsgrads* wird zum Festlegen der Rangfolge und zum Sortieren von Attributen in Spalten verwendet, die nicht binäre, kontinuierliche, numerische Daten enthalten.  
  
-   Für Spalten, die diskrete und diskretisierte Daten enthalten, sind die*Shannon-Entropie* und zwei *Bayes* -Werte verfügbar. Wenn das Modell jedoch kontinuierliche Spalten enthält, wird der Interessantheitsgrad zur Bewertung aller Eingabespalten herangezogen, um die Konsistenz sicherzustellen.  
  
#### Interessantheitsgrad  
 Eine Funktion ist interessant, wenn sie eine nützliche Information offenbart. Allerdings kann die *Bedeutung* auf verschiedene Arten gemessen werden.  So kann *Neuheit* für die Ausreißererkennung bedeutsam sein, für die Klassifizierung können jedoch die Fähigkeit, eng verwandte Elemente unterscheiden zu können bzw. das *diskriminante Gewicht* interessanter sein.  
  
 Das in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining verwendete Maß der Bedeutung basiert auf der *Entropie*. Das bedeutet, dass Attribute mit einer zufälligen Verteilung eine höhere Entropie und einen geringeren Informationsgewinn haben und daher weniger interessant sind. Die Entropie eines bestimmten Attributs wird wie folgt mit der Entropie aller anderen Attribute verglichen:  
  
 Interessantheit(Attribut) = - (m - Entropie(Attribut)) * (m - Entropie(Attribut))  
  
 Die zentrale Entropie oder m steht für die Entropie des gesamten Featuresatzes. Durch Abziehen der Entropie des Zielattributs von der zentralen Entropie lässt sich einschätzen, wie viele Informationen das Attribut bereitstellt.  
  
 Dieses Ergebnis wird standardmäßig immer dann verwendet, wenn die Spalte nicht binäre, kontinuierliche, numerische Daten enthält.  
  
#### Shannon-Entropie  
 Die Shannon-Entropie stellt ein Maß für die Ungewissheit einer zufälligen Variable für ein bestimmtes Ergebnis dar. Beispielsweise kann die Entropie einen Münzwurfs als Funktion der Wahrscheinlichkeit des Ergebnisses "Kopf" dargestellt werden.  
  
 In Analysis Services wird die folgende Formel zur Berechnung der Shannon-Entropie verwendet:  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 Diese Bewertungsmethode ist für diskrete und diskretisierte Attribute verfügbar.  
  
#### Bayes-Methode mit K2-A-priori-Verteilung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining stellt zwei Featureauswahlwerte bereit, die auf Bayes-Netzwerken basieren. Ein Bayes-Netzwerk ist ein *gerichteter* oder *azyklischer* Graph von Zuständen und Übergängen zwischen Zuständen. Das heißt, dass einige Zustände immer vor dem aktuellen Status liegen, andere Zustände sind nachgelagert, und der Graph stellt keine Wiederholungen oder Schleifen dar. Definitionsgemäß ermöglichen Bayes-Netzwerke die Verwendung vorherigen Wissens. Allerdings ist die Frage, welche der früheren Zustände zur Berechnung der Wahrscheinlichkeit nachfolgender Zustände verwendet werden sollen, für den Algorithmusentwurf, die Leistung und die Genauigkeit wichtig.  
  
 Der K2-Algorithmus zum Lernen von Bayes-Netzwerken wurde von Cooper und Herskovits entwickelt und wird häufig im Data Mining eingesetzt. Er ist skalierbar und kann mehrere Variablen analysieren, erfordert jedoch eine Sortierung der als Eingabe verwendeten Variablen. Weitere Informationen finden Sie in [Learning Bayesian Networks](http://go.microsoft.com/fwlink/?LinkId=105885) von Chickering, Geiger, und Heckerman.  
  
 Diese Bewertungsmethode ist für diskrete und diskretisierte Attribute verfügbar.  
  
#### Bayes-Dirichlet-Äquivalent mit uniformer A-priori-Verteilung  
 Bei der Bayes-Dirichlet-Äquivalent-Bewertung wird auch die Bayes-Analyse zur Bewertung eines Netzwerks anhand eines gegebenen Datasets verwendet. Diese Bewertungsmethode wurde von Heckerman entwickelt und basiert auf der von Cooper und Herskovits entwickelten BD-Metrik. Bei der Dirichlet-Verteilung handelt es sich um eine Multinominalverteilung, die die bedingte Wahrscheinlichkeit jeder Netzwerkvariablen beschreibt und über viele für das Lernen nützliche Eigenschaften verfügt.  
  
 Die Methode Bayes-Dirichlet-Äquivalent mit uniformer A-priori-Verteilung setzt einen Sonderfall der Dirichlet-Verteilung voraus, in dem eine mathematische Konstante zur Erstellung einer festen oder einheitlichen Verteilung von A-priori-Zuständen verwendet wird. Die Bayes-Dirichlet-Äquivalent-Bewertung unterstellt außerdem Likelihood-Äquivalenz, d. h. es wird nicht erwartet, dass die Daten äquivalente Strukturen unterscheiden können. Anders ausgedrückt bedeutet dies, wenn der Score von „Wenn A dann B“ dem Score von „Wenn B dann A“ entspricht, dann lassen sich die Strukturen nicht anhand der Daten unterscheiden, und die Kausalität kann nicht aus den Daten gefolgert werden.  
  
 Weitere Informationen zu Bayes-Netzwerken und der Implementierung dieser Bewertungsmethoden finden Sie in [Learning Bayesian Networks](http://go.microsoft.com/fwlink/?LinkId=105885).  
  
### Featureauswahlmethoden pro Algorithmus  
 Die folgende Tabelle enthält die Algorithmen, welche die Funktionsauswahl unterstützen, die von einem Algorithmus verwendeten Funktionsauswahlmethoden und die Parameter, mit denen sich das Funktionsauswahlverhalten steuern lässt:  
  
|Algorithmus|Analysemethode|Kommentare|  
|---------------|------------------------|--------------|  
|Naive Bayes|Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Der Microsoft Naive Bayes-Algorithmus akzeptiert nur diskrete oder diskretisierte Attribute, daher kann er den Interessantheitsgrad nicht verwenden.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Naive Bayes Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md).|  
|Entscheidungsstrukturen|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Wenn irgendeine Spalte nicht binäre kontinuierliche Werte enthält, wird der Interessantheitsgrad für alle Spalten verwendet, um die Konsistenz zu gewährleisten. Andernfalls wird die StandardFunktionsauswahlmethode oder die Methode angewendet, die Sie angegeben haben, als Sie das Modell erstellt haben.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Decision Trees Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md).|  
|Neuronales Netzwerk|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Der Microsoft Neural Networks-Algorithmus kann sowohl die Bayes- als auch die Entropie-basierte Methode verwenden, sofern die Daten kontinuierliche Spalten enthalten.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Neural Network Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).|  
|Logistische Regression|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Obwohl der Microsoft Logistic Regression-Algorithmus auf dem Microsoft Neural Network-Algorithmus basiert, können Sie keine logistischen Regressionsmodelle anpassen, um das Funktionsauswahlverhalten zu steuern. Deshalb wird die Funktionsauswahl immer standardmäßig nach der Methode ausgeführt, die für das Attribut am besten geeignet ist.<br /><br /> Wenn alle Attribute diskret oder diskretisiert sind, wird als Standardmethode Bayes-Dirichlet mit uniformer A-priori-Verteilung eingesetzt.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Logistic Regression Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).|  
|Clustering|Interessantheitsgrad|Der Microsoft Clustering-Algorithmus kann diskrete oder diskretisierte Daten verwenden. Da das Ergebnis jedes Attributs jedoch als Entfernung berechnet wird und als kontinuierliche Zahl dargestellt wird, muss der Interessantheitsgrad verwendet werden.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).|  
|Lineare Regression|Interessantheitsgrad|Der Microsoft Linear Regression-Algorithmus kann nur den Interessantheitsgrad verwenden, da dieser nur kontinuierliche Spalten unterstützt.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Linear Regression Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md).|  
|Zuordnungsregeln<br /><br /> Sequenzclustering|Wird nicht verwendet|Die Funktionsauswahl wird nicht mit diesen Algorithmen aufgerufen.<br /><br /> Durch Festlegen der Parameter MINIMUM_SUPPORT und MINIMUM_PROBABILIITY lässt sich jedoch das Verhalten des Algorithmus steuern und die Größe der Eingabedaten falls notwendig reduzieren.<br /><br /> Weitere Informationen finden Sie unter [Microsoft Association Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md) und [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).|  
|Zeitreihe|Wird nicht verwendet|Die Funktionsauswahl gilt nicht für Zeitreihenmodelle.<br /><br /> Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).|  
  
## Parameter für die Funktionsauswahl  
 In Algorithmen, die die Funktionsauswahl unterstützen, können Sie mithilfe der folgenden Parameter steuern, wann die Funktionsauswahl aktiviert wird. Jeder Algorithmus verfügt über einen Standardwert für die Anzahl zulässiger Eingaben, Sie können diesen Standardwert jedoch überschreiben und die Anzahl der Attribute angeben. In diesem Abschnitt sind die Parameter zur Verwaltung der Funktionsauswahl aufgeführt.  
  
#### MAXIMUM_INPUT_ATTRIBUTES  
 Falls ein Modell mehr Spalten enthält als durch die im *MAXIMUM_INPUT_ATTRIBUTES*-Parameter angegebene Zahl, ignoriert der Algorithmus alle Spalten, die er als irrelevant errechnet.  
  
#### MAXIMUM_OUTPUT_ATTRIBUTES  
 Entsprechend gilt: Falls ein Modell mehr vorhersagbare Spalten enthält als durch die im *MAXIMUM_OUTPUT_ATTRIBUTES*-Parameter angegebene Zahl, ignoriert der Algorithmus gleichermaßen alle Spalten, die er als irrelevant errechnet.  
  
#### MAXIMUM_STATES  
 Wenn ein Modell mehr Fälle enthält, als im *MAXIMUM_STATES*-Parameter angegeben sind, werden die am wenigsten verbreiteten Status in einer Gruppe zusammengefasst und als fehlend behandelt. Wird einer dieser Parameter auf 0 festgelegt, ist die Funktionsauswahl ausgeschaltet. Dies wirkt sich auf die Verarbeitungszeit und die Leistung aus.  
  
 Neben diesen Methoden für die Funktionsauswahl können Sie den Algorithmus bei der Identifizierung oder Heraufstufung aussagekräftiger Attribute unterstützen, indem Sie *Modellierungsflags* für das Modell oder *Verteilungsflags* für die Struktur festlegen. Weitere Informationen zu diesen Konzepten finden Sie unter [Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md) und [Spaltenverteilungen &#40;Data Mining&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
## Siehe auch  
 [Anpassen von Miningmodellen und -strukturen](../../analysis-services/data-mining/customize-mining-models-and-structure.md)  
  
  