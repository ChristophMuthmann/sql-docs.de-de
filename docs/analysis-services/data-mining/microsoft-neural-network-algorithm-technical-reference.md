---
title: "Technische Referenz f&#252;r den Microsoft Neural Network-Algorithmus | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "HIDDEN_NODE_RATIO-Parameter"
  - "MAXIMUM_INPUT_ATTRIBUTES-Parameter"
  - "HOLDOUT_PERCENTAGE-Parameter"
  - "Neural Network-Algorithmen [Analysis Services]"
  - "Ausgabeebene [Data Mining]"
  - "Neuronale Netzwerke"
  - "MAXIMUM_OUTPUT_ATTRIBUTES-Parameter"
  - "MAXIMUM_STATES-Parameter"
  - "SAMPLE_SIZE-Parameter"
  - "Verborgene Ebene"
  - "Verborgene Neuronen"
  - "Eingabeebene [Data Mining]"
  - "Aktivierungsfunktion [Data Mining]"
  - "Deltaregelnetzwerk mit Rückpropagierung"
  - "neural network model [Analysis Services]"
  - "Codierung [Data Mining]"
  - "HOLDOUT_SEED-Parameter"
ms.assetid: b8fac409-e3c0-4216-b032-364f8ea51095
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 26
---
# Technische Referenz f&#252;r den Microsoft Neural Network-Algorithmus
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus verwendet ein *mehrschichtiges Perzeptronnetzwerk*, das auch als *Netzwerk von Deltaregeln mit Rückpropagierung* bezeichnet wird. Es besteht aus bis zu drei Ebenen aus Neuronen oder *Perzeptronen*. Zu diesen Ebenen gehört eine Eingabeebene, eine optionale verborgene Ebene und eine Ausgabeebene.  
  
 Eine detaillierte Erläuterung von mehrschichtigen Perzeptronnetzwerken geht über den Rahmen dieser Dokumentation hinaus. In diesem Thema wird die grundlegende Implementierung des Algorithmus, einschließlich der Methode zum Normalisieren von Eingabe- und Ausgabewerten, erläutert sowie Funktionsauswahlverfahren zur Reduzierung der Attributkardinalität beschrieben. Das Thema enthält eine Beschreibung der Parameter und anderer Einstellungen, mit denen das Verhalten des Algorithmus angepasst wird. Ferner werden Links zu weiteren Informationen über das Abfragen von Modellen zur Verfügung gestellt.  
  
## Implementierung des Microsoft Neural Network-Algorithmus  
 In einem mehrschichtigen Perzeptronnetzwerk empfängt jedes Neuron mindestens eine Eingabe bzw. erstellt mindestens eine Ausgabe. Bei jeder Ausgabe handelt es sich um eine einfache nichtlineare Funktion der Summe der Eingaben im Neuron. Eingaben werden nur von Knoten der Eingabeebene an die Knoten der verborgenen Ebene und von der verborgenen Ebene an die Ausgabeebene weitergegeben; zwischen den Neuronen innerhalb einer Ebene sind keine Verbindungen vorhanden. Wenn keine verborgene Ebene eingeschlossen ist, wie in einem logistischen Regressionsmodell, werden Eingaben direkt von den Knoten der Eingabeebene an die der Ausgabeebene weitergegeben.  
  
 In einem Netzwerk, das mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus erstellt wurde, gibt es drei Neuronentypen:  
  
**Eingabeneuronen**  
  
 Eingabeneuronen stellen Eingabeattributwerte des Data Mining-Modells dar. Bei diskreten Eingabeattributen stellt ein Eingabeneuron in der Regel einen einzelnen Status des Eingabeattributs dar. Hierzu gehören auch fehlende Werte, wenn die Trainingsdaten NULL-Werte für dieses Attribut enthalten. Ein diskretes Eingabeattribut mit mehr als zwei Status generiert ein Eingabeneuron für jeden Status sowie ein Eingabeneuron für einen fehlenden Status, wenn NULL-Werte in den Trainingsdaten vorhanden sind. Ein kontinuierliches Eingabeattribut generiert zwei Eingabeneuronen: ein Neuron für einen fehlenden Status und ein Neuron für den Wert des kontinuierlichen Attributs selbst. Mit Eingabeneuronen werden einem oder mehreren verborgenen Neuronen Eingaben zur Verfügung gestellt.  
  
**Verborgene Neuronen**  
  
 Verborgene Neuronen empfangen die von Eingabeneuronen bereitgestellten Eingaben und stellen Ausgabeneuronen die empfangenen Ausgaben zur Verfügung.  
  
**Ausgabeneuronen**  
  
 Ausgabeneuronen stellen Ausgabeattributwerte des Data Mining-Modells dar. Bei diskreten Eingabeattributen stellt ein Ausgabeneuron in der Regel einen einzelnen Status eines vorhersagbaren Attributs dar. Hierzu gehören auch fehlende Werte. Ein binäres vorhersagbares Attribut erstellt z. B. einen Ausgabeknoten, der einen fehlenden oder vorhandenen Status beschreibt, und gibt somit an, ob für dieses Attribut ein Wert vorhanden ist. Eine boolesche Spalte, die als vorhersagbares Attribut verwendet wird, generiert drei Ausgabeneuronen: ein Neuron für einen TRUE-Wert, ein Neuron für einen FALSE-Wert und ein Neuron für einen fehlenden oder vorhandenen Status. Ein diskretes vorhersagbares Attribut, das über mehr als zwei Status verfügt, generiert ein Ausgabeneuron für jeden Status sowie ein Ausgabeneuron für einen fehlenden oder vorhandenen Status. Kontinuierliche vorhersagbare Spalten generieren zwei Ausgabeneuronen: ein Neuron für einen fehlenden oder vorhandenen Status und ein Neuron für den Wert der kontinuierlichen Spalte selbst. Wenn beim Überarbeiten des vorhersagbaren Spaltensatzes mehr als 500 Ausgabeneuronen generiert werden, generiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im Miningmodell ein Netzwerk zur Darstellung der zusätzlichen Ausgabeneuronen.  
  
 Ein Neuron empfängt Eingaben von anderen Neuronen oder von anderen Daten, je nachdem auf welcher Ebene des Netzwerks es sich befindet. Ein Eingabeneuron empfängt Eingaben von den ursprünglichen Daten. Verborgene Neuronen und Ausgabeneuronen empfangen Eingaben von den Ausgaben anderer Neuronen im neuronalen Netzwerk. Eingaben bilden die Beziehungen zwischen Neuronen, und die Beziehungen dienen als Analysepfad für einen bestimmten Satz von Fällen.  
  
 Jeder Eingabe ist der Wert *Gewichtung*zugeordnet. Dieser beschreibt die Relevanz oder Wichtigkeit einer bestimmten Eingabe an das verborgene oder Ausgabeneuron. Je größer die Gewichtung ist, die einer Eingabe zugewiesen wird, desto relevanter oder wichtiger ist der Wert dieser Eingabe. Gewichtungen können negativ sein, was bedeutet, dass ein bestimmtes Neuron durch die Eingabe eher deaktiviert als aktiviert werden kann. Der Wert jeder Eingabe wird durch die Gewichtung vervielfacht, um die Wichtigkeit einer Eingabe für ein bestimmtes Neuron zu betonen. Bei negativen Gewichtungen besteht der Effekt der Vervielfachung des Werts durch die Gewichtung in der Minderung der Wichtigkeit.  
  
 Dementsprechend ist jedem Neuron die einfache nichtlineare *Aktivierungsfunktion* zugeordnet. Diese beschreibt die Relevanz oder die Wichtigkeit eines bestimmten Neurons für die entsprechende Ebene eines neuronalen Netzwerks. Als Aktivierungsfunktion wird bei verborgenen Neuronen eine *hypertangentiale Funktion* (tanh) verwendet, bei Ausgabeneuronen dagegen eine *sigmoidale* Funktion. Bei beiden Funktionen handelt es sich um nicht nichtlineare, kontinuierliche Funktionen, die im neuronalen Netzwerk die Modellierung von nichtlinearen Beziehungen zwischen Eingabe- und Ausgabeneuronen ermöglichen.  
  
### Trainieren von neuronalen Netzwerken  
 Das Trainieren eines Data Mining-Modells, das den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus verwendet, setzt sich aus mehreren Schritten zusammen: Diese Schritte hängen stark von den Werten ab, die Sie für die Algorithmusparameter festlegen.  
  
 Der Algorithmus führt zunächst eine Auswertung aus und extrahiert die Trainingsdaten aus der Datenquelle. Ein bestimmter Prozentsatz der Trainingsdaten, die als *zurückgehaltene Daten*bezeichnet werden, ist für die Messung der Genauigkeit des Netzwerks reserviert. Während des Trainingsprozesses wird das Netzwerk unmittelbar nach jeder Iteration der Trainingsdaten ausgewertet. Wenn die Genauigkeit des Modells nicht mehr zunimmt, wird der Trainingsprozess beendet.  
  
 Die Werte der Parameter *SAMPLE_SIZE* und *HOLDOUT_PERCENTAGE* werden zur Bestimmung der Anzahl von Fällen für die Stichprobe der Trainingsdaten verwendet. Des Weiteren werden sie zur Bestimmung der Anzahl von Fällen verwendet, die für die zurückgehaltenen Daten reserviert werden. Der Wert des Parameters *HOLDOUT_SEED* wird verwendet, um die einzelnen Fälle zufällig zu bestimmen, die für die auszunehmen Daten reserviert werden.  
  
> [!NOTE]  
>  Diese Algorithmusparameter unterscheiden sich von den Eigenschaften HOLDOUT_SIZE und HOLDOUT_SEED, die für eine Miningstruktur zum Definieren eines Testdatasets angewendet werden.  
  
 Der Algorithmus bestimmt als Nächstes die Anzahl und die Komplexität der Netzwerke, die das Miningmodell unterstützt. Wenn das Miningmodell mindestens ein Attribut enthält, das nur für die Vorhersage verwendet wird, erstellt der Algorithmus ein einzelnes Netzwerk, in dem jedes dieser Attribute dargestellt wird. Wenn das Miningmodell mindestens ein Attribut enthält, das sowohl für die Eingabe als auch für die Vorhersage verwendet wird, erstellt der Algorithmusanbieter ein Netzwerk für jedes dieser Attribute.  
  
 Bei Eingabe- und vorhersagbaren Attributen mit diskreten Werten stellt jedes Eingabe- oder Ausgabeneuron jeweils einen einzelnen Status dar. Bei Eingabe- und vorhersagbaren Attributen mit kontinuierlichen Werten stellt jedes Eingabe- oder Ausgabeneuron jeweils den Bereich und die Verteilung der Werte für das Attribut dar. Die maximale Anzahl der Status, die in beiden Fällen unterstützt wird, hängt vom Wert des Algorithmusparameters *MAXIMUM_STATES* ab. Wenn die Anzahl der Status eines bestimmten Attributs den Wert des Algorithmusparameters *MAXIMUM_STATES* übersteigt, werden die gebräuchlichsten und relevantesten Status bis zum Maximum der zulässigen Status für dieses Attribut ausgewählt. Die restlichen Status werden als fehlende Werte für die Analyse gruppiert.  
  
 Der Algorithmus verwendet dann beim Bestimmen der ersten Anzahl an Neuronen, die zum Erstellen der verborgenen Ebene verwendet werden, den Wert des Parameters *HIDDEN_NODE_RATIO*. Sie können den Parameter *HIDDEN_NODE_RATIO* auf 0 festlegen, um zu verhindern, dass in den Netzwerken eine verborgene Ebene erstellt wird, die der Algorithmus für das Miningmodell generiert. Somit wird sichergestellt, dass das neuronale Netzwerk als logistische Regression behandelt wird.  
  
 Der Algorithmusanbieter führt zum selben Zeitpunkt die iterative Auswertung der Gewichtung aller Eingaben im gesamten Netzwerk aus. Dabei vergleicht er den zuvor reservierten Trainingsdatensatz mit den tatsächlich bekannten Werten aller Fälle der zurückgehaltenen Daten mit der Vorhersage des Netzwerks in einem Prozess, der als *Batchlernvorgang*bezeichnet wird. Nach der Auswertung des gesamten Trainingsdatensatzes vergleicht der Algorithmus für jedes Neuron den vorhergesagten Wert mit dem Ist-Wert. Der Algorithmus berechnet bei Bedarf den Fehlergrad und passt die Gewichtungen an, die den Eingaben dieses Neurons zugeordnet sind. Dabei arbeitet der Algorithmus rückwärts von den Ausgabeneuronen ausgehend zu den Eingabeneuronen mithilfe eines Prozesses, der als *Rückpropagierung*bezeichnet wird. Der Algorithmus wiederholt dann diesen Prozess für den gesamten Trainingsdatensatz. Da der Algorithmus viele Gewichtungen und Ausgabeneuronen unterstützen kann, wird der Algorithmus der konjugierten Gradienten verwendet, um den Trainingsprozess beim Zuweisen und Auswerten der Eingabegewichtungen zu führen. Eine Erläuterung des Algorithmus der konjugierten Gradienten geht über den Rahmen dieser Dokumentation hinaus.  
  
### Funktionsauswahl  
 Wenn die Anzahl der Eingabeattribute größer ist als der Wert des *MAXIMUM_INPUT_ATTRIBUTES*-Parameters oder die Anzahl der vorhersagbaren Attribute größer ist als der Wert des *MAXIMUM_OUTPUT_ATTRIBUTES*-Parameters, wird für die Funktionsauswahl ein entsprechender Algorithmus verwendet, um die Komplexität der im Miningmodell eingeschlossenen Netzwerke zu reduzieren. Mit der Funktionsauswahl wird die Anzahl der Eingabe- und vorhersagbaren Attribute reduziert. Dabei werden die Attribute beibehalten, die für das Modell statistisch am wichtigsten sind.  
  
 Die Funktionsauswahl wird automatisch von allen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining-Algorithmen zur Verbesserung der Analyse und zur Reduzierung der Verarbeitungslast verwendet. Die für die Funktionsauswahl in neuronalen Netzwerkmodellen verwendete Methode hängt vom Datentyp des Attributs ab. Zu Referenzzwecken zeigt die folgende Tabelle die für neuronale Netzwerkmodelle verwendeten Funktionsauswahlmethoden. Außerdem enthält die Tabelle die für den logistischen Regressionsalgorithmus verwendeten Funktionsauswahlmethoden, die auf dem neuronalen Netzwerkalgorithmus basieren.  
  
|Algorithmus|Analysemethode|Kommentare|  
|---------------|------------------------|--------------|  
|Neuronale Netzwerke|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Der Neural Networks-Algorithmus kann sowohl die Entropie- als auch die Bayes-basierte Bewertungsmethode verwenden, sofern die Daten kontinuierliche Spalten enthalten.<br /><br /> Standard.|  
|Logistische Regression|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Weil diesem Algorithmus kein Parameter zur Steuerung des Funktionsauswahlverhaltens übergeben werden kann, werden die Standardwerte verwendet. Wenn alle Attribute diskret oder diskretisiert sind, wird als Standardmethode Bayes-Dirichlet mit uniformer A-priori-Verteilung eingesetzt.|  
  
 Die Algorithmusparameter, die die Funktionsauswahl für ein neuronales Netzwerkmodell steuern, sind MAXIMUM_INPUT_ATTRIBUTES, MAXIMUM_OUTPUT_ATTRIBUTES und MAXIMUM_STATES. Sie können auch die Anzahl von verborgenen Ebenen kontrollieren, indem Sie den HIDDEN_NODE_RATIO-Parameter festlegen.  
  
### Bewertungsmethoden  
 Bei der*Bewertung* handelt es sich um eine Form der Normalisierung, was im Trainingskontext eines neuronalen Netzwerks den Prozess bezeichnet, mit dem ein Wert, z. B. eine diskrete Textbeschriftung, in einen Wert konvertiert wird, der mit anderen Eingaben verglichen und im Netzwerk gewichtet werden kann. Wenn ein Eingabeattribut beispielsweise Gender ist und die möglichen Werte Male und Female sind, während ein anderes Eingabeattribut Income lautet mit einem variablen Wertebereich, sind die Werte für jedes Attribut nicht direkt vergleichbar und müssen auf eine gemeinsame Skalierung codiert werden, sodass die Gewichtungen berechnet werden können. Bei der Bewertung werden diese Eingaben zu numerischen Werten normalisiert, insbesondere zu einem Wahrscheinlichkeitsbereich. Die für die Normalisierung verwendeten Funktionen tragen auch zu einer gleichmäßigeren Verteilung des Eingabewerts auf einer einheitlichen Skala bei, sodass Extremwerte die Analyseergebnisse nicht beeinträchtigen.  
  
 Ausgaben des neuronalen Netzwerks werden ebenfalls codiert. Wenn es ein einzelnes Ziel für die Ausgabe (d. h. Vorhersage) gibt oder mehrere Ziele vorhanden sind, die nur für die Vorhersage und nicht für die Eingabe verwendet werden, erstellt das Modell ein einzelnes Netzwerk, und eine Normalisierung der Werte erscheint nicht erforderlich. Wenn mehrere Attribute für die Eingabe und die Vorhersage verwendet werden, muss das Modell mehrere Netzwerke erstellen. Daher müssen alle Werte normalisiert sein, und die Ausgaben müssen beim Verlassen des Netzwerks codiert werden.  
  
 Die Codierung der Eingaben basiert auf der Summierung jedes einzelnen diskreten Werts im Trainingsfall und Multiplizierung dieses Werts mit der Gewichtung. Dies wird als *gewichtete Summe*bezeichnet, die an die Aktivierungsfunktion in der verborgenen Ebene übergeben wird. Ein z-Ergebnis wird wie folgt zur Codierung verwendet:  
  
 **Diskrete Werte**  
  
 `μ = p` (die vorherige Wahrscheinlichkeit eines Status)  
  
 `StdDev  = sqrt(p(1-p))`  
  
 **Kontinuierliche Werte**  
  
 Derzeitiger Wert = `1 - μ/σ`  
  
 Kein vorhandener Wert = `-μ/σ`  
  
 Nachdem die Werte codiert wurden, durchlaufen die Eingaben die gewichtete Summierung, wobei die Netzwerkränder als Gewichtungen fungieren.  
  
 Bei der Codierung für Ausgaben wird die sigmoidale Funktion verwendet, die über für Vorhersagen nützliche Eigenschaften verfügt. Eine dieser Eigenschaften besteht darin, dass die Ausgabe dieser Funktion unabhängig davon, wie die ursprünglichen Werte skaliert sind und ob die Werte negativ oder positiv sind, stets einen Wert zwischen 0 und 1 aufweist. Dies eignet sich für die Schätzung von Wahrscheinlichkeiten. Eine andere nützliche Eigenschaft besteht darin, dass die sigmoidale Funktion einen glättenden Effekt hat, sodass die Wahrscheinlichkeit mit zunehmender Entfernung der Werte vom Wendepunkt langsam gegen 0 oder 1 gehen.  
  
## Anpassen des Neural Network-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus unterstützt mehrere Parameter, die Auswirkungen auf das Verhalten, die Leistung und die Genauigkeit des resultierenden Miningmodells haben. Sie können die Verarbeitungsweise der Daten auch durch Festlegen der Modellierungsflags für die Spalten oder durch Festlegen von Verteilungsflags ändern, um anzugeben, wie die Werte innerhalb der Spalten behandelt werden sollen.  
  
### Festlegen von Algorithmusparametern  
 In der folgenden Tabelle werden die Parameter beschrieben, die mit dem Microsoft Neural Network-Algorithmus verwendet werden können.  
  
 HIDDEN_NODE_RATIO  
 Legt das Verhältnis von verborgenen Neuronen zu Eingabe- und Ausgabeneuronen fest. Die folgende Formel bestimmt die erste Anzahl von Neuronen in der verborgenen Ebene:  
  
 HIDDEN_NODE_RATIO * SQRT(Gesamtzahl der Eingabeneuronen \* Gesamtzahl der Ausgabeneuronen)  
  
 Der Standardwert ist 4.0.  
  
 HOLDOUT_PERCENTAGE  
 Gibt den Prozentsatz von Fällen in den Trainingsdaten an, die zum Berechnen des Fehlers für zurückgehaltene Daten verwendet werden. Dieser dient als Teil des Beendigungskriteriums beim Trainieren des Miningmodells.  
  
 Der Standardwert ist 30.  
  
 HOLDOUT_SEED  
 Gibt eine Zahl an, die als Ausgangswert für den Pseudozufallszahlen-Generator zum zufälligen Generieren von zurückgehaltenen Daten verwendet wird. Wenn dieser Parameter auf 0 festgelegt ist, wird der Ausgangswert vom Algorithmus basierend auf dem Namen des Miningmodells generiert. So wird sichergestellt, dass der Inhalt bei erneuter Verarbeitung des Modells gleich bleibt.  
  
 Der Standardwert ist 0.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Gibt die maximale Anzahl von Eingabeattributen an, die an den Algorithmus übergeben werden kann, bevor die Funktionsauswahl verwendet wird. Wenn dieser Wert auf 0 festgelegt wird, ist die Funktionsauswahl für Eingabeattribute deaktiviert.  
  
 Der Standardwert ist 255.  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 Gibt die maximale Anzahl von Ausgabeattributen an, die an den Algorithmus übergeben werden kann, bevor die Funktionsauswahl verwendet wird. Wenn dieser Wert auf 0 festgelegt wird, ist die Funktionsauswahl für Ausgabeattribute deaktiviert.  
  
 Der Standardwert ist 255.  
  
 MAXIMUM_STATES  
 Gibt die maximale Anzahl an diskreten Status pro Attribut an, die vom Algorithmus unterstützt wird. Wenn die Anzahl der Status eines bestimmten Attributs größer ist als die für den Parameter festgelegte Statusanzahl, verwendet der Algorithmus für dieses Attribut die gebräuchlichsten Status und behandelt die restlichen Status als fehlend.  
  
 Der Standardwert ist 100.  
  
 SAMPLE_SIZE  
 Gibt die Anzahl von Fällen an, die zum Trainieren des Modells verwendet werden. Der Algorithmus verwendet entweder diese Anzahl oder den Prozentsatz aller Fälle, die – wie im HOLDOUT_PERCENTAGE-Parameter angegeben – nicht in den zurückgehaltenen Daten eingeschlossen sind, je nachdem, welcher Wert kleiner ist.  
  
 Mit anderen Worten, wenn der HOLDOUT_PERCENTAGE-Parameter auf 30 festgelegt ist, verwendet der Algorithmus entweder den Wert dieses Parameters oder einen Wert, der bis zu 70 % gleich der Gesamtzahl der Fälle ist, je nachdem, welcher Wert kleiner ist.  
  
 Der Standardwert ist 10.000.  
  
### Modellierungsflags  
 Die folgenden Modellierungsflags werden zur Verwendung mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus unterstützt.  
  
 NOT NULL  
 Gibt an, dass die Spalte keinen NULL-Wert enthalten kann. Ein Fehler tritt auf, wenn Analysis Services während des Modelltrainings einen NULL-Wert erkennt.  
  
 Gilt für die Miningstrukturspalten.  
  
 MODEL_EXISTENCE_ONLY  
 Gibt an, dass das Modell nur berücksichtigen soll, ob ein Wert für das Attribut vorhanden ist oder ob ein Wert fehlt. Der genaue Wert spielt keine Rolle.  
  
 Gilt für die Miningmodellspalten.  
  
### Verteilungsflags  
 Die folgenden Verteilungsflags werden zur Verwendung mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus unterstützt. Die Flags dienen nur als Hinweise für das Modell. Wenn der Algorithmus eine andere Verteilung erkennt, wird die gefundene Verteilung und nicht die von dem Hinweis zur Verfügung gestellte Verteilung verwendet.  
  
 Normal  
 Gibt an, dass die Werte innerhalb der Spalte so behandelt werden sollen, als würden sie die normale oder Gauß'sche Verteilung darstellen.  
  
 Uniform  
 Gibt an, dass die Werte innerhalb der Spalte so behandelt werden sollen, als wären sie gleichmäßig verteilt. Das heißt, die Wahrscheinlichkeit der einzelnen Werte ist ungefähr gleich und ist eine Funktion der Gesamtzahl der Werte.  
  
 Log Normal  
 Gibt an, dass die Werte innerhalb der Spalte so behandelt werden sollen, als wären sie entlang der *Protokollnormalkurve* verteilt. Dies bedeutet, dass der Logarithmus der Werte normal verteilt ist.  
  
## Anforderungen  
 Ein neuronales Netzwerkmodell muss mindestens eine Eingabespalte und eine Ausgabespalte enthalten.  
  
### Eingabespalten und vorhersagbare Spalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus unterstützt bestimmte Eingabespalten und vorhersagbare Spalten. Diese sind in der nachstehenden Tabelle aufgelistet.  
  
|Column|Inhaltstypen|  
|------------|-------------------|  
|Eingabeattribut|Continuous, Cyclical, Discrete, Discretized, Key, Table und Ordered|  
|Vorhersagbares Attribut|Continuous, Cyclical, Discrete, Discretized und Ordered|  
  
> [!NOTE]  
>  Zyklische und sortierte Inhaltstypen werden unterstützt, der Algorithmus behandelt sie jedoch als diskrete Werte und führt keine spezielle Verarbeitung durch.  
  
## Siehe auch  
 [Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Miningmodellinhalt von neuronalen Netzwerkmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Neuronale Beispiele für Netzwerkmodellabfragen](../../analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  