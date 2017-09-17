---
title: Microsoft Decision Trees Algorithm Technical Reference | Microsoft Docs
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
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c098b5144a06cae6afb5b79ca4bf395a68768bd3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Technische Referenz für den Microsoft Decision Trees-Algorithmus
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus ist ein hybrider Algorithmus, der verschiedene Methoden zum Erstellen einer Struktur integriert und mehrere analytische Tasks, wie Regression, Klassifikation und Zuordnung, unterstützt. Der Microsoft Decision Trees-Algorithmus unterstützt die Modellierung sowohl diskreter als auch fortlaufender Attribute.  
  
 In diesem Thema wird die Implementierung des Algorithmus erläutert und beschrieben, wie das Verhalten des Algorithmus für verschiedene Aufgaben angepasst wird. Ferner werden Links zu weiteren Informationen über das Abfragen von Entscheidungsstrukturmodellen zur Verfügung gestellt.  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>Implementierung des Decision Trees-Algorithmus  
 Der Microsoft Decision Trees-Algorithmus wendet den Bayes-Ansatz zum Erlernen kausaler Interaktionsmodelle durch die Ermittlung ungefährer posteriorer Verteilungen für die Modelle an. Eine ausführliche Erläuterung dieses Ansatzes finden Sie im Dokument auf der Website Microsoft Research durch [Speichern der Struktur und Parameter](http://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409).  
  
 Die Methodologie zur Bewertung des Informationswerts der für das Lernen erforderlichen *vorherigen Informationen* basiert auf der Annahme der *Likelihood-Äquivalenz*. Diese besagt, dass keine Daten bei der Unterscheidung von Netzwerkstrukturen helfen sollen, die andernfalls die gleichen Assertionen der bedingten Unabhängigkeit darstellen. Für jeden Fall wird ein einzelnes vorheriges Bayes-Netzwerk und ein einziges Vertrauensmaß für dieses Netzwerk angenommen.  
  
 Mithilfe dieser vorherigen Netzwerke berechnet der Algorithmus die relativen *Posterior-Wahrscheinlichkeiten* der Netzwerkstrukturen anhand der aktuellen Trainingsdaten und identifiziert die Netzwerkstrukturen, die die höchsten Posterior-Wahrscheinlichkeiten besitzen.  
  
 Der Microsoft Decision Trees-Algorithmus verwendet andere Methoden, um die beste Struktur zu berechnen. Die verwendete Methode hängt vom Task ab, der entweder die lineare Regressions-, die Klassifizierungs- oder die Zuordnungsanalyse sein kann. Ein einzelnes Modell kann mehrere Strukturen für andere vorhersagbare Attribute enthalten. Darüber hinaus kann jede Struktur mehrere Verzweigungen enthalten. Dies hängt davon ab, wie viele Attribute und Werte in den Daten vorhanden sind. Die Form und Tiefe der Struktur eines bestimmten Modells hängt von der Bewertungsmethode und anderen verwendeten Parametern ab. Änderungen in den Parametern können auch beeinflussen, wo die Knoten sich teilen.  
  
### <a name="building-the-tree"></a>Erstellen der Struktur  
 Wenn der Microsoft Decision Trees-Algorithmus die Menge möglicher Eingabewerte erstellt, führt er *feature selection* aus, um die Attribute zu identifizieren, die die meisten Informationen liefern, und berücksichtigt die Werte nicht mehr, die äußerst selten sind. Der Algorithmus gruppiert außerdem Werte in *Container*, um Gruppen von Werten zu erstellen, die zur Optimierung der Leistung als eine Einheit verarbeitet werden können.  
  
 Eine Struktur wird erstellt, indem die Korrelationen zwischen einer Eingabe und dem gewünschten Ergebnis bestimmt werden. Nachdem alle Attribute mit Korrelationen versehen wurden, identifiziert der Algorithmus das einzige Attribut, das die Ergebnisse am saubersten trennt. Dieser Punkt der besten Trennung wird mit einer Gleichung gemessen, die den Informationsgewinn berechnet. Das Attribut, das das beste Ergebnis für den Informationsgewinn aufweist, wird zum Teilen der Fälle in Teilmengen verwendet. Diese Teilmengen werden anschließend vom gleichen Prozess rekursiv analysiert, bis die Struktur nicht weiter aufgeteilt werden kann.  
  
 Die präzise Gleichung zur Bewertung des Informationsgewinns hängt von den beim Erstellen des Algorithmus festgelegten Parametern, vom Datentyp der vorhersagbaren Spalte und vom Datentyp der Eingabe ab.  
  
### <a name="discrete-and-continuous-inputs"></a>Diskrete und kontinuierliche Eingaben  
 Wenn das vorhersagbare Attribut diskret ist und die Eingaben diskret sind, wird die Zählung der Ausgaben je Eingabe durch Erstellen einer Matrix und Generieren von Bewertungen für jede Zelle in der Matrix vorgenommen.  
  
 Wenn hingegen das vorhersagbare Attribut diskret ist und die Eingaben kontinuierlich sind, wird die Eingabe der kontinuierlichen Spalten automatisch diskretisiert. Sie können die Standardeinstellung übernehmen und die optimale Anzahl von Containern durch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ermitteln lassen, oder Sie können die Art und Weise steuern, wie kontinuierliche Eingaben diskretisiert werden, indem Sie die <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> - und die <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> -Eigenschaft festlegen. Weitere Informationen finden Sie unter [Ändern der Diskretisierung von Spalten in Miningmodellen](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 Bei kontinuierlichen Attributen bestimmt der Algorithmus anhand einer linearen Regression, wo sich die Entscheidungsstruktur teilt.  
  
 Wenn es sich bei dem vorhersagbaren Attribut um einen kontinuierlichen numerischen Datentyp handelt, wird die Funktionsauswahl auch auf die Ausgaben angewendet, um die mögliche Zahl von Ausgaben zu reduzieren und das Modell schneller zu erstellen. Sie können den Schwellenwert für die Funktionsauswahl ändern und so die Zahl der möglichen Werte erhöhen oder reduzieren, indem Sie den MAXIMUM_OUTPUT_ATTRIBUTES-Parameter festlegen.  
  
 Eine ausführlichere Erläuterung zur Funktionsweise des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus im Zusammenhang mit diskreten vorhersagbaren Spalten finden Sie unter [Learning Bayesian Networks: The Combination of Knowledge and Statistical Data](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf). Weitere Informationen zur Funktionsweise des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus im Zusammenhang mit kontinuierlichen vorhersagbaren Spalten finden Sie im Anhang des Dokuments [Autoregressive Tree Models for Time-Series Analysis](http://go.microsoft.com/fwlink/?LinkId=45966)(Autoregressive Strukturmodelle zur Zeitreihenanalyse).  
  
### <a name="scoring-methods-and-feature-selection"></a>Bewertungsmethoden und Funktionsauswahl  
 Der Microsoft Decision Trees-Algorithmus bietet drei Formeln zur Bewertung des Informationsgewinns: Shannon-Entropie, Bayes-Methode mit K2-A-priori-Verteilung und Bayes-Netzwerk mit einheitlicher Dirichlet-Verteilung von A-priori-Zuständen. Alle drei Methoden sind im Data Mining-Bereich etabliert. Es wird empfohlen, mit verschiedenen Parametern und Bewertungsmethoden zu experimentieren, um festzustellen, welche die besten Ergebnisse erzielen. Weitere Informationen zu diesen Bewertungsmethoden finden Sie unter [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
 Die Funktionsauswahl wird automatisch von allen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining-Algorithmen zur Verbesserung der Analyse und zur Reduzierung der Verarbeitungslast verwendet. Die für die Funktionsauswahl verwendete Methode hängt vom Algorithmus ab, mit dem das Modell erstellt wird. Die Algorithmusparameter, die die Funktionsauswahl für ein Entscheidungsstrukturmodell steuern, sind MAXIMUM_INPUT_ATTRIBUTES und MAXIMUM_OUTPUT.  
  
|Algorithmus|Analysemethode|Kommentare|  
|---------------|------------------------|--------------|  
|Entscheidungsstrukturen|Interessantheitsgrad<br /><br /> Shannon-Entropie<br /><br /> Bayes-Methode mit K2-A-priori-Verteilung<br /><br /> Bayes-Dirichlet mit uniformer A-priori-Verteilung (Standard)|Wenn irgendeine Spalte nicht binäre kontinuierliche Werte enthält, wird der Interessantheitsgrad für alle Spalten verwendet, um die Konsistenz zu gewährleisten. Andernfalls wird die Standardmethode oder die angegebene Methode verwendet.|  
|Lineare Regression|Interessantheitsgrad|Der Linear Regression-Algorithmus verwendet nur den Interessantheitsgrad, da er nur kontinuierliche Spalten unterstützt.|  
  
### <a name="scalability-and-performance"></a>Skalierbarkeit und Leistung  
 Die Klassifizierung ist eine wichtige Data Mining-Strategie. Im Allgemeinen steigt die Menge an Informationen, die zur Klassifizierung der Fälle erforderlich ist, direkt proportional zur Anzahl der Eingabedatensätze. Dies schränkt den Umfang der Daten ein, die klassifiziert werden können. Der Microsoft Decision Trees-Algorithmus verwendet die folgenden Methoden, um diese Probleme zu lösen, die Leistung zu verbessern und Speicherbeschränkungen aufzuheben:  
  
-   Funktionsauswahl zur Optimierung der Auswahl von Attributen.  
  
-   Bayes-Bewertung zur Kontrolle der Strukturzunahme.  
  
-   Optimierung der Klasseneinteilung für kontinuierliche Attribute.  
  
-   Dynamische Gruppierung von Eingabewerten zur Bestimmung der wichtigsten Werte.  
  
 Der Microsoft Decision Trees-Algorithmus ist schnell und skalierbar und ist auf eine einfache Parallelisierung ausgelegt. Dies bedeutet, dass alle Prozessoren zusammenarbeiten, um ein einzelnes, konsistentes Modell zu erstellen. Die Kombination dieser Eigenschaften macht die Entscheidungsstrukturklassifizierung zu einem idealen Tool für Data Mining.  
  
 Wenn schwerwiegende Leistungseinschränkungen vorliegen, können Sie die Verarbeitungszeit während des Trainings eines Entscheidungsstrukturmodells mit den folgenden Methoden verbessern. Beachten Sie in diesem Fall jedoch, dass durch Entfernen von Attributen zur Verbesserung der Verarbeitungsleistung die Ergebnisse des Modells verändert werden und möglicherweise für die Gesamtpopulation weniger repräsentativ sind.  
  
-   Erhöhen Sie den Wert des COMPLEXITY_PENALTY-Parameters, um die Strukturzunahme einzuschränken.  
  
-   Schränken Sie die Anzahl von Elementen in Zuordnungsmodellen ein, um die Anzahl von Strukturen zu begrenzen, die erstellt werden.  
  
-   Erhöhen Sie den Wert des MINIMUM_SUPPORT-Parameters, um Überanpassung zu vermeiden.  
  
-   Beschränken Sie die Anzahl von diskreten Werten für ein Attribut auf 10 oder weniger. Sie könnten versuchen, Werte auf andere Weisen in anderen Modellen zu gruppieren.  
  
    > [!NOTE]  
    >  Mit den in  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] verfügbaren Tools zum Durchsuchen von Daten können Sie die Verteilung der Werte in Ihren Daten visuell darstellen und die Daten vor Beginn des Data Mining-Vorgangs entsprechend gruppieren. Weitere Informationen finden Sie unter [Datenprofilerstellungs-Task und -Viewer](../../integration-services/control-flow/data-profiling-task-and-viewer.md). Sie können auch die [Data Mining-Add-Ins für Excel 2007](http://www.microsoft.com/downloads/details.aspx?FamilyID=7C76E8DF-8674-4C3B-A99B-55B17F3C4C51)verwenden, um Daten in Microsoft Excel zu durchsuchen, zu gruppieren und mit neuen Bezeichnungen versehen.  
  
## <a name="customizing-the-decision-trees-algorithm"></a>Anpassen des Decision Trees-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus unterstützt Parameter, die sich auf die Leistung und Genauigkeit des resultierenden Miningmodells auswirken. Sie können außerdem Modellierungsflags für die Miningmodellspalten oder Miningstrukturspalten festlegen, um die Verarbeitung der Daten zu steuern.  
  
> [!NOTE]  
>  Der Microsoft Decision Trees-Algorithmus ist in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar, einige erweiterte Parameter, mit denen das Verhalten des Microsoft Decision Trees-Algorithmus angepasst werden kann, stehen jedoch nur in bestimmten Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zur Verfügung. Eine Liste der Funktionen, die von den Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt werden, finden Sie unter [Von den SQL Server 2012-Editionen unterstützte Funktionen](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="setting-algorithm-parameters"></a>Festlegen von Algorithmusparametern  
 In der folgenden Tabelle sind die Parameter beschrieben, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus verwendet werden können.  
  
 *COMPLEXITY_PENALTY*  
 Steuert das Anwachsen der Entscheidungsstruktur. Ein niedriger Wert führt zu einer größeren Anzahl von Teilungen, und ein hoher Wert führt zu einer niedrigeren Anzahl von Teilungen. Der Standardwert richtet sich nach der Anzahl von Attributen in einem bestimmten Modell und ist der nachstehenden Liste zu entnehmen:  
  
-   Für die Attribute 1-9 lautet der Wert 0,5.  
  
-   Für 10 bis 99 Attribute lautet der Wert 0,9.  
  
-   Für 100 oder mehr Attribute lautet der Wert 0,99.  
  
 *FORCE_REGRESSOR*  
 Zwingt den Algorithmus, die angegebenen Spalten als Regressoren zu verwenden, unabhängig von ihrer durch den Algorithmus berechneten Wichtigkeit der Spalten. Dieser Parameter wird nur für Entscheidungsstrukturen verwendet, die ein kontinuierliches Attribut vorhersagen.  
  
> [!NOTE]  
>  Durch Festlegen dieses Parameters wird der Algorithmus gezwungen, zu versuchen, das Attribut als Regressor zu verwenden. Ob das Attribut im endgültigen Modell tatsächlich als Regressor verwendet wird, hängt von den Analyseergebnissen ab. Sie können feststellen, welche Spalten als Regressoren verwendet wurden, indem Sie den Modellinhalt abfragen.  
  
 [Nur in einigen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Definiert die Anzahl von Eingabeattributen, die der Algorithmus verarbeiten kann, bevor die Funktionsauswahl aufgerufen wird.  
  
 Der Standardwert lautet 255.  
  
 Legen Sie diesen Wert auf 0 fest, um die Funktionsauswahl zu deaktivieren.  
  
 [Nur in einigen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Definiert die Anzahl von Ausgabeattributen, die der Algorithmus verarbeiten kann, bevor die Funktionsauswahl aufgerufen wird.  
  
 Der Standardwert lautet 255.  
  
 Legen Sie diesen Wert auf 0 fest, um die Funktionsauswahl zu deaktivieren.  
  
 [Nur in einigen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar]  
  
 *MINIMUM_SUPPORT*  
 Bestimmt die Mindestanzahl von Blattfällen, die zum Generieren einer Teilung in der Entscheidungsstruktur erforderlich sind.  
  
 Der Standardwert lautet 10.  
  
 Sie müssen möglicherweise diesen Wert erhöhen, wenn das Dataset sehr groß ist, um übermäßiges Trainieren zu vermeiden.  
  
 *SCORE_METHOD*  
 Bestimmt die zum Berechnen des Teilungsergebnisses zu verwendende Methode. Die folgenden Optionen stehen zur Verfügung:  
  
|ID|Name|  
|--------|----------|  
|1|Entropie|  
|3|Bayes-Methode mit K2-A-priori-Verteilung|  
|4|Bayes-Dirichlet-Äquivalent (BDE) mit uniformer A-priori-Verteilung<br /><br /> (Standard)|  
  
 Der Standardwert ist 4 oder BDE.  
  
 Eine Erläuterung dieser Bewertungsmethoden finden Sie unter [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
 *SPLIT_METHOD*  
 Bestimmt die zum Teilen des Knotens zu verwendende Methode. Die folgenden Optionen stehen zur Verfügung:  
  
|ID|Name|  
|--------|----------|  
|1|**Binary:** Gibt an, dass die Struktur unabhängig von der tatsächlichen Anzahl der Werte für das Attribut in zwei Verzweigungen aufgeteilt werden soll.|  
|2|**Complete:** Gibt an, dass die Struktur so viele Teilungen erstellen kann, wie Attributwerte vorhanden sind.|  
|3|**Both:** Gibt an, dass Analysis Services bestimmen kann, ob eine binäre oder vollständige Teilung verwendet werden soll, um die besten Ergebnisse zu erzielen.|  
  
 Der Standardwert lautet 3.  
  
### <a name="modeling-flags"></a>Modellierungsflags  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Tree-Algorithmus unterstützt die folgenden Modellierungsflags. Wenn Sie die Miningstruktur oder das Miningmodell erstellen, definieren Sie Modellierungsflags, die angeben, wie die Werte in den einzelnen Spalten während der Analyse behandelt werden. Weitere Informationen finden Sie unter [Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Modellierungsflag|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Dies bedeutet, dass die Spalte zwei mögliche Statuswerte haben kann: **Missing** und **Existing**. Ein NULL-Wert ist ein fehlender Wert.<br /><br /> Gilt für die Miningmodellspalten.|  
|NOT NULL|Gibt an, dass die Spalte keinen NULL-Wert enthalten kann. Ein Fehler tritt auf, wenn Analysis Services während des Modelltrainings einen NULL-Wert erkennt.<br /><br /> Gilt für die Miningstrukturspalten.|  
  
### <a name="regressors-in-decision-tree-models"></a>Regressoren in Entscheidungsstrukturmodellen  
 Auch wenn Sie den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus nicht verwenden, kann jedes Entscheidungsstrukturmodell, das über kontinuierliche numerische Eingaben und Ausgaben verfügt, potenziell Knoten enthalten, die eine Regression für ein kontinuierliches Attribut darstellen.  
  
 Sie müssen nicht angeben, dass eine Spalte mit kontinuierlichen numerischen Daten einen Regressor darstellt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus verwendet die Spalte automatisch als potenziellen Regressor und unterteilt das Dataset selbst dann in Bereiche mit sinnvollen Mustern, wenn Sie das REGRESSOR-Flag nicht für die Spalte festlegen.  
  
 Sie können durch Einsatz des FORCE_REGRESSOR-Parameters jedoch gewährleisten, dass der Algorithmus einen bestimmten Regressor verwendet. Dieser Parameter kann nur mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus und dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus verwendet werden. Wenn das Modellierungsflag festgelegt wurde, versucht der Algorithmus Regressionsgleichungen der Form `a*C1 + b*C2 + ...` zu finden, um die Muster den Knoten der Struktur zuzuordnen. Dann wird die Summe der Restwerte berechnet, und wenn die Abweichung zu groß ist, wird die Struktur unterteilt.  
  
 Wenn Sie beispielsweise das Kaufverhalten von Kunden mithilfe des Attributs **Einkommen** vorhersagen und das Modellierungsflag REGRESSOR für die Spalte festlegen, versucht der Algorithmus zuerst, die Werte der Spalte **Einkommen** mithilfe einer Standardregressionsformel zuzuordnen. Ist die Abweichung zu groß, dann wird die Regressionsformel ignoriert und die Struktur nach einem anderen Attribut unterteilt. Der Decision Tree-Algorithmus versucht nach der Unterteilung, jedem der Zweige einen Regressor für Einkommen zuzuordnen.  
  
## <a name="requirements"></a>Anforderungen  
 Ein Entscheidungsstrukturmodell muss eine Schlüsselspalte, Eingabespalten und mindestens eine vorhersagbare Spalte enthalten.  
  
### <a name="input-and-predictable-columns"></a>Eingabespalten und vorhersagbare Spalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus unterstützt bestimmte Eingabespalten und vorhersagbare Spalten. Diese sind in der nachstehenden Tabelle aufgelistet. Weitere Informationen zur Bedeutung der Inhaltstypen in einem Miningmodell finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Column|Inhaltstypen|  
|------------|-------------------|  
|Eingabeattribut|Continuous, Cyclical, Discrete, Discretized, Key, Ordered, Table|  
|Vorhersagbares Attribut|Continuous, Cyclical, Discrete, Discretized, Ordered, Table|  
  
> [!NOTE]  
>  Zyklische und sortierte Inhaltstypen werden unterstützt, der Algorithmus behandelt sie jedoch als diskrete Werte und führt keine spezielle Verarbeitung durch.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Decision Trees-Abfragebeispiele](../../analysis-services/data-mining/decision-trees-model-query-examples.md)   
 [Miningmodellinhalt von Entscheidungsstrukturmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
