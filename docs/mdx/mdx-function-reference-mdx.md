---
title: MDX-Funktionsreferenz (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- member functions [MDX]
- level functions [MDX]
- MDX [Analysis Services], functions
- array functions
- string functions
- Multidimensional Expressions [Analysis Services], functions
- hierarchy functions [MDX]
- numeric functions [MDX]
- tuple functions
- subcube functions [MDX]
- functions [MDX]
- logical functions [MDX]
- set functions [MDX]
ms.assetid: e363722a-3e5b-40a9-a0b5-399dd2d93f6d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a6c3d086028a7906f540e716308fc9c15ee9287f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-function-reference-mdx"></a>MDX-Funktionsreferenz (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] bietet für die Verwendung von Funktionen in MDX (Multidimensional Expressions)-Syntax. Funktionen können in jeder gültigen MDX-Anweisung verwendet werden, z. B. in Abfragen, benutzerdefinierten Rollupdefinitionen und anderen Berechnungen. Dieser Abschnitt enthält Informationen zu den in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] enthaltenen MDX-Funktionen.  
  
 In den folgenden Tabellen können Sie Funktionen anhand der Kategorie ihres Rückgabewerts finden oder eine Funktion namentlich aus der alphabetischen Liste im Inhaltsverzeichnis auswählen.  
  
## <a name="array-functions"></a>Arrayfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[SetToArray &#40; MDX &#41;](../mdx/settoarray-mdx.md)|Konvertiert eine Menge oder mehrere Mengen in ein Array zum Verwenden in einer benutzerdefinierten Funktion.|  
  
## <a name="hierarchy-functions"></a>Hierarchiefunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Hierarchie &#40; MDX &#41;](../mdx/hierarchy-mdx.md)|Gibt die Hierarchie zurück, die ein angegebenes Element oder eine angegebene Ebene enthält.|  
|[Dimension &#40; MDX &#41;](../mdx/dimension-mdx.md)|Gibt die Dimension zurück, die ein angegebenes Element, eine angegebene Ebene oder eine angegebene Hierarchie enthält.|  
|[Dimensionen &#40; MDX &#41;](../mdx/dimensions-mdx.md)|Gibt eine Hierarchie zurück, die durch einen numerischen Ausdruck oder einen Zeichenfolgenausdruck angegeben ist.|  
  
## <a name="level-functions"></a>Ebenenfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Level &#40; MDX &#41;](../mdx/level-mdx.md)|Gibt die Ebene eines Elements zurück.|  
|[Ebenen &#40; MDX &#41;](../mdx/levels-mdx.md)|Gibt die Ebene zurück, deren Position in einer Dimension oder Hierarchie durch einen numerischen Ausdruck angegeben ist oder deren Name durch einen Zeichenfolgenausdruck angegeben ist.|  
  
## <a name="logical-functions"></a>Logische Funktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[IsAncestor &#40; MDX &#41;](../mdx/isancestor-mdx.md)|Gibt zurück, ob ein angegebenes Element ein Vorgänger eines anderen angegebenen Elements ist.|  
|[IsEmpty &#40; MDX &#41;](../mdx/isempty-mdx.md)|Gibt zurück, ob der ausgewertete Ausdruck dem leeren Zellenwert entspricht.|  
|[IsGeneration &#40; MDX &#41;](../mdx/isgeneration-mdx.md)|Gibt zurück, ob sich ein angegebenes Element in einer angegebenen Generation befindet.|  
|[IsLeaf &#40; MDX &#41;](../mdx/isleaf-mdx.md)|Gibt zurück, ob ein angegebenes Element ein Blattelement ist.|  
|[IsSibling &#40; MDX &#41;](../mdx/issibling-mdx.md)|Gibt zurück, ob ein angegebenes Element ein gleichgeordnetes Element eines anderen angegebenen Elements ist.|  
  
## <a name="member-functions"></a>Elementfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Vorgänger &#40; MDX &#41;](../mdx/ancestor-mdx.md)|Gibt den Vorgänger eines Elements in einer angegebenen Ebene oder in einem angegebenen Abstand zurück.|  
|[ClosingPeriod &#40; MDX &#41;](../mdx/closingperiod-mdx.md)|Gibt das letzte gleichgeordnete Element unter den nachfolgenden Werten eines Elements auf einer angegebenen Ebene zurück.|  
|[Cousin &#40; MDX &#41;](../mdx/cousin-mdx.md)|Gibt das untergeordnete Element mit derselben relativen Position unter einem übergeordneten Element wie das angegebene untergeordnete Element zurück.|  
|[CurrentMember &#40; MDX &#41;](../mdx/currentmember-mdx.md)|Gibt das aktuelle Element entlang einer angegebenen Dimension oder Hierarchie während einer Iteration zurück.|  
|[DataMember &#40; MDX &#41;](../mdx/datamember-mdx.md)|Gibt das systemgenerierte Datenelement zurück, das einem Nicht-Blattelement einer Dimension zugeordnet ist.|  
|[DefaultMember &#40; MDX &#41;](../mdx/defaultmember-mdx.md)|Gibt das Standardelement einer Dimension oder Hierarchie zurück.|  
|[FirstChild &#40; MDX &#41;](../mdx/firstchild-mdx.md)|Gibt das erste untergeordnete Element eines Elements zurück.|  
|[FirstSibling &#40; MDX &#41;](../mdx/firstsibling-mdx.md)|Gibt das erste untergeordnete Element für das übergeordnete Element eines Elements zurück.|  
|[Element &#40; Element &#41; &#40; MDX &#41;](../mdx/item-member-mdx.md)|Gibt ein Element aus einem angegebenen Tupel zurück.|  
|[Lag &#40; MDX &#41;](../mdx/lag-mdx.md)|Gibt das Element zurück, das eine angegebene Anzahl von Positionen vor einem angegebenen Element entlang der Dimension des Elements liegt.|  
|[LastChild &#40; MDX &#41;](../mdx/lastchild-mdx.md)|Gibt das letzte untergeordnete Element eines Elements zurück.|  
|[LastSibling &#40; MDX &#41;](../mdx/lastsibling-mdx.md)|Gibt das letzte untergeordnete Element des übergeordneten Elements eines angegebenen Elements zurück.|  
|[Lead &#40; MDX &#41;](../mdx/lead-mdx.md)|Gibt das Element zurück, das eine angegebene Anzahl von Positionen auf ein angegebenes Element entlang der Dimension des Elements folgt.|  
|[LinkMember &#40; MDX &#41;](../mdx/linkmember-mdx.md)|Gibt das Element zurück, das in einer angegebenen Hierarchie gleichbedeutend mit dem angegebenen Element ist.|  
|[Mitglieder &#40; Zeichenfolge &#41; &#40; MDX &#41;](../mdx/members-string-mdx.md)|Gibt ein durch einen Zeichenfolgenausdruck angegebenes Element zurück.|  
|[NextMember &#40; MDX &#41;](../mdx/nextmember-mdx.md)|Gibt das nächste Element in der Ebene zurück, die ein angegebenes Element enthält.|  
|[OpeningPeriod &#40; MDX &#41;](../mdx/openingperiod-mdx.md)|Gibt das erste gleichgeordnete Element unter den nachfolgenden Werten einer angegebenen Ebene optional bei einem angegebenen Element zurück.|  
|[ParallelPeriod &#40; MDX &#41;](../mdx/parallelperiod-mdx.md)|Gibt ein Element aus einer früheren Periode in derselben relativen Position wie ein angegebenes Element zurück.|  
|[Übergeordnete &#40; MDX &#41;](../mdx/parent-mdx.md)|Gibt das übergeordnete Element eines Elements zurück.|  
|[PrevMember &#40; MDX &#41;](../mdx/prevmember-mdx.md)|Gibt das vorherige Element in der Ebene zurück, die ein angegebenes Element enthält.|  
|[StrToMember &#40; MDX &#41;](../mdx/strtomember-mdx.md)|Gibt das durch eine Zeichenfolge im MDX-Format angegebene Element zurück.|  
|[UnknownMember &#40; MDX &#41;](../mdx/unknownmember-mdx.md)|Gibt das einer Ebene oder einem Element zugeordnete unbekannte Element zurück.|  
|[ValidMeasure &#40; MDX &#41;](../mdx/validmeasure-mdx.md)|Gibt ein gültiges Measure in einem virtuellen Cube zurück, indem für nicht passende Dimensionen ihre oberste Ebene erzwungen wird.|  
  
## <a name="numeric-functions"></a>Numerische Funktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Aggregat &#40; MDX &#41;](../mdx/aggregate-mdx.md)|Gibt einen Skalarwert zurück, der durch Aggregieren von Measures oder eines optional angegebenen numerischen Ausdrucks über den Tupeln einer angegebenen Menge berechnet wird.|  
|[AVG &#40; MDX &#41;](../mdx/avg-mdx.md)|Gibt den Mittelwert von Measures oder eines optionalen numerischen Ausdrucks, ausgewertet über einer angegebenen Menge, zurück.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|Gibt den aktuellen Berechnungsdurchlauf eines Cubes für den angegebenen Abfragekontext zurück.|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Gibt den Wert eines MDX-Ausdrucks zurück, der über dem angegebenen Berechnungsdurchlauf eines Cubes ausgewertet wird.|  
|[CoalesceEmpty &#40; MDX &#41;](../mdx/coalesceempty-mdx.md)|Koaliert einen leeren Zellwert mit einer Zahl oder einer Zeichenfolge und gibt den koalierten Wert zurück.|  
|[Korrelation &#40; MDX &#41;](../mdx/correlation-mdx.md)|Gibt den Korrelationskoeffizienten zweier Reihen zurück, die über einer Menge ausgewertet werden.|  
|[Anzahl &#40; Dimension &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)|Gibt die Anzahl der Dimensionen in einem Cube zurück.|  
|[Anzahl &#40; Hierarchieebenen &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)|Gibt die Anzahl der Ebenen in einer Dimension oder Hierarchie zurück.|  
|[Anzahl &#40; Set &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)|Gibt die Anzahl der Zellen in einer Menge zurück.|  
|[Anzahl &#40; Tupel &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)|Gibt die Anzahl der Dimensionen in einem Tupel zurück.|  
|[Kovarianz &#40; MDX &#41;](../mdx/covariance-mdx.md)|Gibt die Kovarianz der Gesamtheiten zweier Serien zurück, die über einer Menge mithilfe der Formel für die unausgewogene Auffüllung berechnet wurde.|  
|[CovarianceN &#40; MDX &#41;](../mdx/covariancen-mdx.md)|Gibt die Stichprobenkovarianz zweier Serien zurück, die über einer Menge mithilfe der Formel für die ausgewogene Auffüllung berechnet wurde.|  
|[DistinctCount &#40; MDX &#41;](../mdx/distinctcount-mdx.md)|Gibt die Anzahl der unterschiedlichen nicht leeren Tupel in einer Menge zurück.|  
|[IIf &#40; MDX &#41;](../mdx/iif-mdx.md)|Gibt in Abhängigkeit von einem logischen Test einen von zwei Werten zurück.|  
|[LinRegIntercept &#40; MDX &#41;](../mdx/linregintercept-mdx.md)|Berechnet die lineare Regression einer Menge und gibt den Wert des Konstanten Glieds in der regressionsgleichung y = Ax + b.|  
|[LinRegPoint &#40; MDX &#41;](../mdx/linregpoint-mdx.md)|Berechnet die lineare Regression einer Menge und gibt den Wert der *y* in der regressionsgleichung y = Ax + b.|  
|[LinRegR2 &#40; MDX &#41;](../mdx/linregr2-mdx.md)|Berechnet die lineare Regression einer Menge und gibt den Bestimmungskoeffizienten, R2, zurück.|  
|[LinRegSlope &#40; MDX &#41;](../mdx/linregslope-mdx.md)|Berechnet die lineare Regression einer Menge und gibt den Wert des Regressionskoeffizienten in der regressionsgleichung y = Ax + b.|  
|[LinRegVariance &#40; MDX &#41;](../mdx/linregvariance-mdx.md)|Berechnet die lineare Regression einer Menge und gibt die Varianz der regressionsgleichung zugeordnete y = Ax + b.|  
|[LookupCube &#40; MDX &#41;](../mdx/lookupcube-mdx.md)|Gibt den Wert eines MDX-Ausdrucks zurück, der über einem anderen angegebenen Cube in derselben Datenbank ausgewertet wird.|  
|[Maximale &#40; MDX &#41;](../mdx/max-mdx.md)|Gibt den Maximalwert eines numerischen Ausdrucks zurück, der über einer Menge ausgewertet wird.|  
|[Median &#40; MDX &#41;](../mdx/median-mdx.md)|Gibt den Median eines numerischen Ausdrucks zurück, der über einer Menge ausgewertet wird.|  
|[Min &#40; MDX &#41;](../mdx/min-mdx.md)|Gibt den Minimalwert eines numerischen Ausdrucks zurück, der über einer Menge ausgewertet wird.|  
|[Ordnungszahl &#40; MDX &#41;](../mdx/ordinal-mdx.md)|Gibt den nullbasierten Ordinalwert, der einer Ebene zugeordnet ist, zurück.|  
|[Vorhersagen &#40; MDX &#41;](../mdx/predict-mdx.md)|Gibt einen Wert eines numerischen Ausdrucks zurück, der über einem Data Mining-Modell ausgewertet wurde.|  
|[Rang &#40; MDX &#41;](../mdx/rank-mdx.md)|Gibt den einsbasierten Rang eines angegebenen Tupels in einer angegebenen Menge zurück.|  
|[RollupChildren &#40; MDX &#41;](../mdx/rollupchildren-mdx.md)|Gibt einen Wert zurück, der durch einen Rollup der Werte der untergeordneten Elemente eines angegebenen Elements mithilfe des angegebenen unären Operators generiert wird.|  
|[STDDEV &#40; MDX &#41;](../mdx/stddev-mdx.md)|Alias für [Stdev &#40; MDX &#41; ](../mdx/stdev-mdx.md).|  
|[StddevP &#40; MDX &#41;](../mdx/stddevp-mdx.md)|Alias für [StdevP &#40; MDX &#41; ](../mdx/stdevp-mdx.md).|  
|[StDev &#40; MDX &#41;](../mdx/stdev-mdx.md)|Gibt die Stichproben-Standardabweichung eines numerischen Ausdrucks zurück, die über einer Menge mithilfe der Formel für die ausgewogene Auffüllung berechnet wurde.|  
|[StdevP &#40; MDX &#41;](../mdx/stdevp-mdx.md)|Gibt die Standardabweichung eines numerischen Ausdrucks bezüglich der Gesamtheit zurück, die über einer Menge mithilfe der Formel für die unausgewogene Auffüllung berechnet wurde.|  
|[StrToValue &#40; MDX &#41;](../mdx/strtovalue-mdx.md)|Gibt den durch eine Zeichenfolge im MDX-Format angegebenen Wert zurück.|  
|[Summe &#40; MDX &#41;](../mdx/sum-mdx.md)|Gibt die Summe eines numerischen Ausdrucks zurück, der über einer Menge ausgewertet wird.|  
|[Wert &#40; MDX &#41;](../mdx/value-mdx.md)|Gibt den Wert eines Measures zurück.|  
|[Var &#40; MDX &#41;](../mdx/var-mdx.md)|Gibt die Stichprobenvarianz eines numerischen Ausdrucks zurück, der über einer Menge mithilfe der Formel für die ausgewogene Auffüllung berechnet wurde.|  
|[Varianz &#40; MDX &#41;](../mdx/variance-mdx.md)|Alias für [Var &#40; MDX &#41; ](../mdx/var-mdx.md).|  
|[VarianceP &#40; MDX &#41;](../mdx/variancep-mdx.md)|Alias für [VarP &#40; MDX &#41; ](../mdx/varp-mdx.md).|  
|[VarP &#40; MDX &#41;](../mdx/varp-mdx.md)|Gibt die Varianz eines numerischen Ausdrucks zurück, die über einer Menge mithilfe der Formel für die unausgewogene Auffüllung berechnet wurde.|  
  
## <a name="set-functions"></a>Mengenfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40; MDX &#41;](../mdx/addcalculatedmembers-mdx.md)|Gibt eine Menge zurück, die durch Hinzufügen berechneter Elemente zu einer angegebenen Menge erstellt wird.|  
|[AllMembers &#40; MDX &#41;](../mdx/allmembers-mdx.md)|Gibt eine Menge zurück, die alle Elemente der angegebenen Dimension, Hierarchie oder Ebene, einschließlich berechneter Elemente, enthält.|  
|[Vorgänger &#40; MDX &#41;](../mdx/ancestors-mdx.md)|Gibt die Menge aller Vorgänger eines Elements in einer angegebenen Ebene oder in einem angegebenen Abstand zurück.|  
|[ASCENDANTS &#40; MDX &#41;](../mdx/ascendants-mdx.md)|Gibt die Menge der vorausgehenden Elemente zu einem angegebenen Element zurück, einschließlich des Elements selbst.|  
|[Achse &#40; MDX &#41;](../mdx/axis-mdx.md)|Gibt eine in einer Achse definierte Menge zurück.|  
|[BottomCount &#40; MDX &#41;](../mdx/bottomcount-mdx.md)|Sortiert eine Menge in aufsteigender Reihenfolge und gibt die angegebene Anzahl von Tupeln mit den niedrigsten Werten zurück.|  
|[BottomPercent &#40; MDX &#41;](../mdx/bottompercent-mdx.md)|Sortiert eine Menge in aufsteigender Reihenfolge und gibt eine Menge von Tupeln mit den niedrigsten Werten zurück, deren kumulativer Gesamtwert kleiner oder gleich einem angegebenen Prozentsatz ist.|  
|[BottomSum &#40; MDX &#41;](../mdx/bottomsum-mdx.md)|Sortiert eine Menge in aufsteigender Reihenfolge und gibt eine Menge von Tupeln mit den niedrigsten Werten zurück, deren Gesamtwert kleiner oder gleich einem angegebenen Wert ist.|  
|[Untergeordnete Elemente &#40; MDX &#41;](../mdx/children-mdx.md)|Gibt die untergeordneten Elemente eines angegebenen Elements zurück.|  
|[Crossjoin &#40; MDX &#41;](../mdx/crossjoin-mdx.md)|Gibt das Kreuzprodukt mindestens einer Menge zurück.|  
|[CurrentOrdinal &#40; MDX &#41;](../mdx/currentordinal-mdx.md)|Gibt die aktuelle Iterationsnummer in einer Menge während einer Iteration zurück.|  
|[Nachfolger &#40; MDX &#41;](../mdx/descendants-mdx.md)|Gibt eine Menge von nachfolgenden Werten eines Elements auf einer angegebenen Ebene oder in einem angegebenen Abstand zurück. Optional können nachfolgende Werte anderer Ebenen ein- oder ausgeschlossen werden.|  
|[Unterschiedliche &#40; MDX &#41;](../mdx/distinct-mdx.md)|Gibt eine Menge zurück, wobei doppelte Tupel aus einer angegebenen Menge entfernt werden.|  
|[DrilldownLevel &#40; MDX &#41;](../mdx/drilldownlevel-mdx.md)|Führt einen Drilldown der Elemente einer Menge in eine Ebene unter der untersten Ebene aus, die in der Menge dargestellt ist, oder in eine Ebene unter einer optional angegebenen Ebene eines Elements, das in der Menge dargestellt wird.|  
|[DrilldownLevelBottom &#40; MDX &#41;](../mdx/drilldownlevelbottom-mdx.md)|Führt einen Drilldown der untersten Elemente einer Menge auf einer angegebenen Ebene in eine darunter liegende Ebene aus.|  
|[DrilldownLevelTop &#40; MDX &#41;](../mdx/drilldownleveltop-mdx.md)|Führt einen Drilldown der obersten Elemente einer Menge auf einer bestimmten Ebene in eine darunter liegende Ebene aus.|  
|[DrilldownMember &#40; MDX &#41;](../mdx/drilldownmember-mdx.md)|Führt einen Drilldown für Elemente in einer angegebenen Menge aus, die in einer angegebenen zweiten Menge vorhanden sind. Alternativ führt die Funktion einen Drilldown für eine Menge von Tupeln aus.|  
|[DrilldownMemberBottom &#40; MDX &#41;](../mdx/drilldownmemberbottom-mdx.md)|Führt einen Drilldown bei Elementen in einer angegebenen Menge aus, die in einer angegebenen zweiten Menge vorhanden sind, wobei das Resultset auf eine angegebene Anzahl von Elementen beschränkt wird. Alternativ führt die Funktion auch einen Drilldown für eine Menge von Tupeln aus.|  
|[DrilldownMemberTop &#40; MDX &#41;](../mdx/drilldownmembertop-mdx.md)|Führt einen Drilldown bei Elementen in einer angegebenen Menge aus, die in einer angegebenen zweiten Menge vorhanden sind, wobei das Resultset auf eine angegebene Anzahl von Elementen beschränkt wird. Alternativ können Sie diese Funktion einen Drilldown für eine Menge von Tupeln.|  
|[DrillupLevel &#40; MDX &#41;](../mdx/drilluplevel-mdx.md)|Führt einen Drillup bei Elementen einer Menge aus, die sich unterhalb einer angegebenen Ebene befinden.|  
|[DrillupMember &#40; MDX &#41;](../mdx/drillupmember-mdx.md)|Führt einen Drillup für die Elemente einer angegebenen Menge aus, die in einer zweiten angegebenen Menge vorhanden sind.|  
|[Außer &#40; MDX &#41;](../mdx/except-mdx-function.md)|Gibt die Differenzmenge zweier Mengen zurück. Optional werden doppelte Werte beibehalten.|  
|[Existiert &#40; MDX &#41;](../mdx/exists-mdx.md)|Gibt die Menge der Elemente einer Menge zurück, die mit mindestens einem Tupel mindestens einer anderen Menge vorhanden sind.|  
|[Extrahieren &#40; MDX &#41;](../mdx/extract-mdx.md)|Gibt eine Menge von Tupeln aus extrahierten Dimensionselementen zurück.|  
|[Filters &#40; MDX &#41;](../mdx/filter-mdx.md)|Filtert eine angegebene Menge basierend auf einer Suchbedingung und gibt dann das Resultset zurück.|  
|[Generieren von &#40; MDX &#41;](../mdx/generate-mdx.md)|Wendet eine Menge auf jedes Element einer anderen Menge an und verknüpft dann die entstehenden Mengen durch den Vereinigungsoperator. Alternativ gibt die Funktion eine verkettete Zeichenfolge zurück, die durch Auswerten eines Zeichenfolgenausdrucks über einer Menge erstellt wurde.|  
|[Head &#40; MDX &#41;](../mdx/head-mdx.md)|Gibt die erste angegebene Anzahl von Elementen aus einer Menge zurück, wobei doppelte Werte beibehalten werden.|  
|[HIERARCHIZE &#40; MDX &#41;](../mdx/hierarchize-mdx.md)|Ordnet die Elemente einer Menge hierarchisch an.|  
|[Intersect &#40; MDX &#41;](../mdx/intersect-mdx.md)|Gibt die Schnittmenge zweier Eingabesets zurück. Optional werden doppelte Werte beibehalten.|  
|[LastPeriods &#40; MDX &#41;](../mdx/lastperiods-mdx.md)|Gibt eine Menge von Elementen bis zu einem angegebenen Element, einschließlich des Elements, zurück.|  
|[Mitglieder &#40; Set &#41; &#40; MDX &#41;](../mdx/members-set-mdx.md)|Gibt die Menge der Elemente in einer Dimension, Ebene oder Hierarchie zurück.|  
|[MTd &#40; MDX &#41;](../mdx/mtd-mdx.md)|Gibt eine Menge von gleichgeordneten Elementen zurück, die derselben Ebene angehören wie ein angegebenes Element. Die Menge beginnt mit dem ersten gleichgeordneten Element und endet mit dem angegebenen Element, entsprechend der Einschränkung durch die Year-Ebene in der Time-Dimension.|  
|[NameToSet &#40; MDX &#41;](../mdx/nametoset-mdx.md)|Gibt eine Menge zurück, die das durch eine Zeichenfolge im MDX-Format angegebene Element enthält.|  
|[NonEmptyCrossjoin &#40; MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)|Gibt das Kreuzprodukt mindestens einer Menge als eine Menge zurück, wobei leere Tupel und Tupel ohne zugeordnete Daten einer Faktentabelle ausgeschlossen werden.|  
|[Reihenfolge &#40; MDX &#41;](../mdx/order-mdx.md)|Ordnet die Elemente einer angegebenen Menge an, wobei die Hierarchie optional beibehalten wird oder nicht.|  
|[PeriodsToDate &#40; MDX &#41;](../mdx/periodstodate-mdx.md)|Gibt eine Menge von gleichgeordneten Elementen zurück, die derselben Ebene angehören wie ein angegebenes Element. Die Menge beginnt mit dem ersten gleichgeordneten Element und endet mit dem angegebenen Element, entsprechend der Einschränkung durch die angegebene Ebene in der Time-Dimension.|  
|[QTD &#40; MDX &#41;](../mdx/qtd-mdx.md)|Gibt einen Satz von gleichgeordneten Elementen aus der gleichen Ebene wie ein angegebenes Element aus, beginnend mit dem ersten gleichgeordneten Element und endend mit dem angegebenen Element, entsprechend der Einschränkung durch die *Quartal* in der Zeitdimension.|  
|[Gleichgeordnete Elemente &#40; MDX &#41;](../mdx/siblings-mdx.md)|Gibt die gleichgeordneten Elemente eines angegebenen Elements zurück, einschließlich des Elements selbst.|  
|[StripCalculatedMembers &#40; MDX &#41;](../mdx/stripcalculatedmembers-mdx.md)|Gibt eine Menge zurück, die durch Entfernen berechneter Elemente aus einer angegebenen Menge entsteht.|  
|[StrToSet &#40; MDX &#41;](../mdx/strtoset-mdx.md)|Gibt die durch eine Zeichenfolge im MDX-Format angegebene Menge zurück.|  
|[Teilmenge &#40; MDX &#41;](../mdx/subset-mdx.md)|Gibt eine Teilmenge von Tupeln aus einer angegebenen Menge zurück.|  
|[Tail &#40; MDX &#41;](../mdx/tail-mdx.md)|Gibt eine Teilmenge vom Ende einer Menge zurück.|  
|[ToggleDrillState &#40; MDX &#41;](../mdx/toggledrillstate-mdx.md)|Schaltet den Drillstatus von Elementen um.|  
|[TopCount &#40; MDX &#41;](../mdx/topcount-mdx.md)|Sortiert eine Menge in absteigender Reihenfolge und gibt die angegebene Anzahl von Elementen mit den höchsten Werten zurück.|  
|[TopPercent &#40; MDX &#41;](../mdx/toppercent-mdx.md)|Sortiert eine Menge in absteigender Reihenfolge und gibt eine Menge von Tupeln mit den höchsten Werten zurück, deren kumulativer Gesamtwert kleiner oder gleich einem angegebenen Prozentsatz ist.|  
|[TopSum &#40; MDX &#41;](../mdx/topsum-mdx.md)|Sortiert eine Menge und gibt die obersten Elemente zurück, deren kumulative Summe mindestens einem angegebenen Wert entspricht.|  
|[Union &#40; MDX &#41;](../mdx/union-mdx.md)|Gibt die Vereinigungsmenge zweier Mengen zurück. Optional werden doppelte Werte beibehalten.|  
|[Unorder &#40; MDX &#41;](../mdx/unorder-mdx.md)|Entfernt eine erzwungene Reihenfolge von einer angegebenen Menge.|  
|[VisualTotals &#40; MDX &#41;](../mdx/visualtotals-mdx.md)|Gibt eine Menge zurück, die durch dynamische Gesamtwertbildung der untergeordneten Elemente in einer angegebenen Menge generiert wird. Optional wird im resultierenden Cellset ein Muster für den Namen des übergeordneten Elements verwendet.|  
|[WTD &#40; MDX &#41;](../mdx/wtd-mdx.md)|Gibt eine Menge von gleichgeordneten Elementen zurück, die derselben Ebene angehören wie ein angegebenes Element. Die Menge beginnt mit dem ersten gleichgeordneten Element und endet mit dem angegebenen Element, entsprechend der Einschränkung durch die Week-Ebene in der Time-Dimension.|  
|[YTD &#40; MDX &#41;](../mdx/ytd-mdx.md)|Gibt einen Satz von gleichgeordneten Elementen aus der gleichen Ebene wie ein angegebenes Element aus, beginnend mit dem ersten gleichgeordneten Element und endend mit dem angegebenen Element, entsprechend der Einschränkung durch die *Jahr* in der Zeitdimension.|  
  
## <a name="string-functions"></a>Zeichenfolgenfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Gibt den Wert eines MDX-Ausdrucks zurück, der über einem angegebenen Berechnungsdurchlauf eines Cubes ausgewertet wird.|  
|[CoalesceEmpty &#40; MDX &#41;](../mdx/coalesceempty-mdx.md)|Koaliert einen leeren Zellwert mit einer Zahl oder einer Zeichenfolge und gibt den koalierten Wert zurück.|  
|[Generieren von &#40; MDX &#41;](../mdx/generate-mdx.md)|Wendet eine Menge auf jedes Element einer anderen Menge an und verknüpft dann die entstehenden Mengen durch den Vereinigungsoperator. Alternativ gibt die Funktion eine verkettete Zeichenfolge zurück, die durch Auswerten eines Zeichenfolgenausdrucks über einer Menge erstellt wurde.|  
|[IIf &#40; MDX &#41;](../mdx/iif-mdx.md)|Gibt in Abhängigkeit von einem logischen Test einen von zwei Werten zurück.|  
|[LookupCube &#40; MDX &#41;](../mdx/lookupcube-mdx.md)|Gibt den Wert eines MDX-Ausdrucks zurück, der über einem anderen angegebenen Cube in derselben Datenbank ausgewertet wird.|  
|[MemberToStr &#40; MDX &#41;](../mdx/membertostr-mdx.md)|Gibt eine Zeichenfolge im MDX-Format zurück, die einem angegebenen Element entspricht.|  
|[Name der &#40; MDX &#41;](../mdx/name-mdx.md)|Gibt den Namen einer Dimension, einer Hierarchie, einer Ebene oder eines Elements zurück.|  
|[Datenbankeigenschaften &#40; MDX &#41;](../mdx/properties-mdx.md)|Gibt eine Zeichenfolge oder einen stark typisierten Wert zurück, der den Wert einer Elementeigenschaft enthält.|  
|[SetToStr &#40; MDX &#41;](../mdx/settostr-mdx.md)|Gibt eine Zeichenfolge im MDX-Format zurück, die einer angegebenen Menge entspricht.|  
|[TupleToStr &#40; MDX &#41;](../mdx/tupletostr-mdx.md)|Gibt eine Zeichenfolge im MDX-Format zurück, die einem angegebenen Tupel entspricht.|  
|[UniqueName &#40; MDX &#41;](../mdx/uniquename-mdx.md)|Gibt den eindeutigen Namen einer angegebenen Dimension, Hierarchie, Ebene oder eines angegebenen Elements zurück.|  
|[Benutzername &#40; MDX &#41;](../mdx/username-mdx.md)|Gibt den Domänennamen und den Benutzernamen der aktuellen Verbindung zurück.|  
  
## <a name="subcube-functions"></a>Teilcubefunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Diese &#40; MDX &#41;](../mdx/this-mdx.md)|Gibt den aktuellen Teilcube zurück.|  
|[Bewirkt, dass &#40; MDX &#41;](../mdx/leaves-mdx.md)|Gibt die Menge der Blattelemente in der angegebenen Dimension, im angegebenen Element oder Tupel zurück.|  
  
## <a name="tuple-functions"></a>Tupelfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Aktuelle &#40; MDX &#41;](../mdx/current-mdx.md)|Gibt das aktuelle Tupel in einer Menge während einer Iteration zurück.|  
|[Element &#40; Tupel &#41; &#40; MDX &#41;](../mdx/item-tuple-mdx.md)|Gibt ein Tupel aus einer Menge zurück.|  
|[Stamm &#40; MDX &#41;](../mdx/root-mdx.md)|Gibt ein Tupel, aus denen besteht die **alle** Elemente aus jeder Attributhierarchie in einem Cube, Dimension oder Tupel.|  
|[StrToTuple &#40; MDX &#41;](../mdx/strtotuple-mdx.md)|Gibt das durch eine Zeichenfolge im MDX-Format angegebene Tupel zurück.|  
  
## <a name="other-functions"></a>Weitere Funktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|[Fehler &#40; MDX &#41;](../mdx/error-mdx.md)|Löst einen Fehler aus. Optional wird eine angegebene Fehlermeldung ausgegeben.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Sprachreferenz &#40; MDX &#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
