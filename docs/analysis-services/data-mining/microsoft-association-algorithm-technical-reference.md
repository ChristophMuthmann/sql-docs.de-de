---
title: Microsoft Association Algorithm Technical Reference | Microsoft Docs
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
- MINIMUM_ITEMSET_SIZE parameter
- MAXIMUM_SUPPORT parameter
- association algorithms [Analysis Services]
- MINIMUM_SUPPORT parameter
- OPTIMIZED_PREDICTION_COUNT parameter
- associations [Analysis Services]
- MAXIMUM_ITEMSET_COUNT parameter
- MAXIMUM_ITEMSET_SIZE parameter
- MINIMUM_PROBABILITY parameter
ms.assetid: 50a22202-e936-4995-ae1d-4ff974002e88
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c1fcc5b1089397672226b526654f611147e81e99
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="microsoft-association-algorithm-technical-reference"></a>Technische Referenz für den Microsoft Association-Algorithmus
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus ist eine einfache Implementierung des bekannten Apriori-Algorithmus.  
  
 Sowohl der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus als auch der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus können zur Analyse von Zuordnungen dienen, die jeweils erfassten Regeln können jedoch abhängig vom Algorithmus differieren. In einem Entscheidungsstrukturmodell basieren die Aufteilungen, von denen bestimmte Regeln abgeleitet werden, auf Informationen, während die Regeln in einem Zuordnungsmodell vollständig auf Vertrauen beruhen. Daher ist in einem Zuordnungsmodell eine starke Regel bzw. eine Regel, deren Vertrauen hoch ist, nicht unbedingt interessant, da sie keine neuen Informationen bietet.  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Implementierung des Microsoft Association-Algorithmus  
 Der Apriori-Algorithmus analysiert keine Muster, sondern generiert und zählt *Kandidatenitemsets*. Ein Element (Item) kann ein Ereignis, ein Produkt oder der Wert eines Attributs sein. Dies hängt vom Typ der analysierten Daten ab.  
  
 Beim häufigsten Typ von Zuordnungsmodell werden den einzelnen Attributen, wie z. B. Produkt oder Ereignisname, boolesche Variablen zugeordnet, die die Werte "Ja/Nein" oder "Fehlend/Vorhanden" darstellen. Eine Warenkorbanalyse ist ein Beispiel für ein Zuordnungsregelnmodell, das mit booleschen Variablen das Vorhandensein oder Fehlen eines bestimmten Produkts im Warenkorb eines Kunden darstellt.  
  
 Für jedes Itemset erstellt der Algorithmus dann Ergebnisse, die Unterstützung und Vertrauen darstellen. Diese Ergebnisse können dazu verwendet werden, interessante Regeln zu ordnen und von den Itemsets abzuleiten.  
  
 Zuordnungsmodelle können auch für numerische Attribute verwendet werden. Wenn die Attribute fortlaufend sind, können die Zahlen *diskretisiert* oder in Buckets gruppiert werden. Die diskretisierten Werte können dann entweder als boolesche Werte oder Attribut/Wert-Paare behandelt werden.  
  
### <a name="support-probability-and-importance"></a>Unterstützung, Wahrscheinlichkeit und Wichtigkeit  
 *Unterstützung*, mitunter auch als *Häufigkeit*bezeichnet, steht für die Anzahl der Fälle, in denen das entsprechende Element oder die entsprechende Elementkombination enthalten ist. Nur Elemente, die mindestens die angegebene Menge an Unterstützung haben, können im Modell enthalten sein.  
  
 Ein *häufig enthaltenes Itemset* bezieht sich auf eine Sammlung von Elementen, bei denen die Elementkombination Unterstützung über dem durch den Parameter MINIMUM_SUPPORT definierten Schwellenwert erhält. Wenn das Itemset beispielsweise {A,B,C} lautet und der Wert MINIMUM_SUPPORT 10 beträgt, muss jedes einzelne Element A, B und C in mindestens 10 Fällen vorhanden sein, um in das Modell aufgenommen zu werden. Die Elementkombination {A,B,C} muss ebenfalls in mindestens 10 Fällen enthalten sein.  
  
 **Hinweis** : Sie können die Anzahl der Itemsets in einem Miningmodell auch steuern, indem Sie die maximale Länge eines Itemsets angeben, wobei Länge in diesem Fall für die Anzahl der Elemente steht.  
  
 Standardmäßig stellt die Unterstützung für ein bestimmtes Element oder Itemset die Anzahl der Fälle dar, die das Element bzw. die Elemente enthalten. Sie können den Wert MINIMUM_SUPPORT auch als prozentualen Anteil der Gesamtfälle im Dataset ausdrücken, indem Sie die Zahl als eine Dezimalzahl kleiner als 1 eingeben. Wenn Sie für MINIMUM_SUPPORT einen Wert von 0,03 angeben, bedeutet dies, dass mindestens 3 Prozent der Gesamtfälle im Dataset dieses Element oder Itemset enthalten müssen, damit es in das Modell aufgenommen wird. Experimentieren Sie mit dem Modell, um festzustellen, ob die Angabe der Anzahl oder des prozentualen Anteils sinnvoller ist.  
  
 Im Gegensatz dazu wird der Schwellenwert für Regeln nicht als Anzahl oder prozentualer Anteil ausgedrückt, sondern als Wahrscheinlichkeit, mitunter auch als *Vertrauen*bezeichnet. Wenn das Itemset {A,B,C} beispielsweise in 50 Fällen enthalten ist, das Itemset {A,B,D} ebenfalls in 50 Fällen und das Itemset {A,B} in weiteren 50 Fällen, ist offensichtlich, dass {A,B} kein starkes Vorhersagekriterium für {C} ist. Für die Gewichtung eines bestimmten Ergebnisses gegenüber allen bekannten Ergebnissen berechnet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] daher die Wahrscheinlichkeit der einzelnen Regel (z.B. „If {A,B} Then {C}“), indem die Unterstützung für das Itemset {A,B,C} durch die Unterstützung für alle verknüpften Itemsets dividiert wird.  
  
 Sie können die Anzahl von Regeln, die ein Modell erzeugt, einschränken, indem Sie einen Wert für MINIMUM_PROBABILITY festlegen.  
  
 Für jede erstellte Regel gibt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ein Ergebnis aus, das ihre *Wichtigkeit*angibt. Diese wird mitunter auch als *Lift*bezeichnet. Liftwichtigkeit wird für Itemsets und Regeln anders berechnet.  
  
 Die Wichtigkeit eines Itemsets wird als Wahrscheinlichkeit des Itemsets dividiert durch die zusammengesetzte Wahrscheinlichkeit der einzelnen Elemente im Itemset berechnet. Wenn ein Itemset beispielsweise {A,B} enthält, zählt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zunächst alle Fälle, die diese Kombination aus A und B enthalten, dividiert dann die Summe durch die Gesamtzahl der Fälle und normalisiert die Wahrscheinlichkeit.  
  
 Die Wichtigkeit einer Regel wird anhand des Wahrscheinlichkeitsprotokolls der rechten Seite der Regel in Bezug auf die linke Seite der Regel berechnet. In der Regel `If {A} Then {B}`berechnet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beispielsweise das Verhältnis der Fälle mit A und B gegenüber Fällen mit B, aber ohne A und normalisiert dieses Verhältnis anschließend anhand einer logarithmischen Skalierung.  
  
### <a name="feature-selection"></a>Funktionsauswahl  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus führt keine automatische Funktionsauswahl aus. Stattdessen stellt der Algorithmus Parameter bereit, die die Daten kontrollieren, die vom Algorithmus verwendet werden. Diese Parameter können Beschränkungen der Größe der einzelnen Itemsets oder die maximale und Mindestunterstützung umfassen, die erforderlich ist, um ein Itemset in das Modell aufzunehmen.  
  
-   Um Elemente und Ereignisse herauszufiltern, die zu allgemein und daher nicht interessant sind, senken Sie den Wert für MAXIMUM_SUPPORT, um sehr häufig auftretende Itemsets aus dem Modell zu entfernen.  
  
-   Um Elemente und Itemsets herauszufiltern, die selten sind, erhöhen Sie den Wert für MINIMUM_SUPPORT.  
  
-   Um Regeln herauszufiltern, erhöhen Sie den Wert für MINIMUM_PROBABILITY.  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>Anpassen des Microsoft Association Rules-Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus unterstützt mehrere Parameter, die Auswirkungen auf das Verhalten, die Leistung und die Genauigkeit des resultierenden Miningmodells haben.  
  
### <a name="setting-algorithm-parameters"></a>Festlegen von Algorithmusparametern  
 Die Parameter für ein Miningmodell können Sie jederzeit mit dem Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ändern. Sie können Parameter auch programmgesteuert ändern, mit der <xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A> -Auflistung in AMO oder mit der [MiningModels-Element &#40; ASSL &#41; ](../../analysis-services/scripting/collections/miningmodels-element-assl.md) in XMLA. In der folgenden Tabelle wird jeder Parameter beschrieben.  
  
> [!NOTE]  
>  Sie können die Parameter in einem vorhandenen Modell nicht mit einer DMX-Anweisung ändern. Sie müssen die Parameter beim Erstellen des Modells in DMX CREATE MODEL oder ALTER STRUCTURE… ADD MODEL festlegen.  
  
 *MAXIMUM_ITEMSET_COUNT*  
 Gibt die maximal zu erzeugende Anzahl von Itemsets an. Wird keine Anzahl angegeben, wird der Standardwert verwendet.  
  
 Der Standardwert ist 200000.  
  
> [!NOTE]  
>  Itemsets werden nach Unterstützung geordnet. Bei Itemsets, die die gleiche Unterstützung haben, ist die Anordnung willkürlich.  
  
 *MAXIMUM_ITEMSET_SIZE*  
 Gibt die maximale Anzahl von Elementen an, die in einem Itemset zulässig sind. Wenn Sie diesen Wert auf 0 festlegen, geben Sie dadurch an, dass es für die Größe des Itemsets keine Begrenzung gibt.  
  
 Der Standardwert lautet 3.  
  
> [!NOTE]  
>  Durch Senken dieses Werts kann die zum Erstellen des Modells erforderliche Zeit möglicherweise reduziert werden, da die Verarbeitung des Modells angehalten wird, sobald die Begrenzung erreicht wird.  
  
 *MAXIMUM_SUPPORT*  
 Gibt die maximale Anzahl von Fällen an, in denen ein Itemset unterstützt werden kann. Dieser Parameter kann verwendet werden, um Elemente auszuschließen, die häufig auftreten und daher potenziell wenig Bedeutung haben.  
  
 Wenn dieser Wert kleiner als 1 ist, entspricht er einem prozentualen Anteil an der Gesamtzahl von Fällen. Werte, die größer als 1 sind, entsprechen der absoluten Anzahl von Fällen, die das Itemset enthalten können.  
  
 Der Standardwert lautet 1.  
  
 *MINIMUM_ITEMSET_SIZE*  
 Gibt die Mindestanzahl von Elementen an, die in einem Itemset zulässig sind. Wenn Sie diese Zahl erhöhen, enthält das Modell möglicherweise weniger Itemsets. Dies kann nützlich sein, wenn Sie beispielsweise aus einem einzelnen Element bestehende Itemsets ignorieren möchten.  
  
 Der Standardwert lautet 1.  
  
> [!NOTE]  
>  Die Modellverarbeitungszeit kann nicht durch Erhöhen des Mindestwerts reduziert werden, da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im Rahmen der Verarbeitung ohnehin Wahrscheinlichkeiten für einzelne Elemente berechnen muss. Durch Erhöhen des Werts können Sie jedoch kleinere Itemsets herausfiltern.  
  
 *MINIMUM_PROBABILITY*  
 Gibt die Mindestwahrscheinlichkeit an, dass eine Regel wahr ist.  
  
 Wenn Sie diesen Wert beispielsweise auf 0,5 festlegen, kann keine Regel mit einer Wahrscheinlichkeit von weniger als 50 Prozent generiert werden.  
  
 Der Standardwert ist 0,4.  
  
 *MINIMUM_SUPPORT*  
 Gibt an, in wie vielen Fällen das Itemset mindestens enthalten sein muss, damit der Algorithmus eine Regel generiert.  
  
 Wenn dieser Wert auf unter 1 festgelegt wird, wird die Mindestanzahl von Fällen als prozentualer Anteil an der Gesamtzahl von Fällen berechnet.  
  
 Wird dieser Wert auf eine Ganzzahl über 1 festgelegt, so wird die Mindestanzahl von Fällen als Anzahl von Fällen, die das Itemset enthalten müssen, berechnet. Der Algorithmus setzt den Wert dieses Parameters möglicherweise automatisch herauf, wenn der Speicherplatz knapp ist.  
  
 Der Standardwert ist 0,03. Dies bedeutet, dass ein Itemset in mindestens 3 Prozent der Fälle enthalten sein muss, um in das Modell aufgenommen zu werden.  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 Definiert die Anzahl von Elementen, die zum Optimieren einer Vorhersage zwischengespeichert werden.  
  
 Der Standardwert ist 0. Wenn der Standard verwendet wird, werden so viele Vorhersagen vom Algorithmus erzeugt, wie in der Abfrage angefordert werden.  
  
 Wenn Sie für *OPTIMIZED_PREDICTION_COUNT,* einen Wert ungleich null angeben, können Vorhersageabfragen höchstens die angegebene Anzahl von Elementen zurückgeben, selbst wenn Sie weitere Vorhersagen anfordern. Durch Festlegen eines Werts kann jedoch die Vorhersageleistung gesteigert werden.  
  
 Wenn der Wert beispielsweise auf 3 festgelegt wird, werden vom Algorithmus nur drei Elemente für die Vorhersage zwischengespeichert. Es werden keine zusätzlichen Vorhersagen angezeigt, die möglicherweise gleich wahrscheinlich zu den drei zurückgegebenen Elementen sind.  
  
### <a name="modeling-flags"></a>Modellierungsflags  
 Die folgenden Modellierungsflags werden zur Verwendung mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus unterstützt.  
  
 NOT NULL  
 Gibt an, dass die Spalte keinen NULL-Wert enthalten kann. Ein Fehler tritt auf, wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] während des Modelltrainings einen NULL-Wert erkennt.  
  
 Gilt für die Miningstrukturspalte.  
  
 MODEL_EXISTENCE_ONLY  
 Dies bedeutet, dass die Spalte zwei mögliche Statuswerte haben kann: **Missing** und **Existing**. Ein NULL-Wert ist ein fehlender Wert.  
  
 Gilt für die Miningmodellspalte.  
  
## <a name="requirements"></a>Anforderungen  
 Ein Associationmodell muss eine Schlüsselspalte, Eingabespalten und eine einzelne vorhersagbare Spalte enthalten.  
  
### <a name="input-and-predictable-columns"></a>Eingabespalten und vorhersagbare Spalten  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Association Rules-Algorithmus unterstützt bestimmte Eingabespalten und vorhersagbare Spalten. Diese sind in der nachstehenden Tabelle aufgelistet. Weitere Informationen zur Bedeutung der Inhaltstypen in einem Miningmodell finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Column|Inhaltstypen|  
|------------|-------------------|  
|Eingabeattribut|Cyclical, Discrete, Discretized, Key, Table, Ordered|  
|Vorhersagbares Attribut|Zyklisch, Diskret, Diskretisiert, Tabelle und Sortiert|  
  
> [!NOTE]  
>  Zyklische und sortierte Inhaltstypen werden unterstützt, der Algorithmus behandelt sie jedoch als diskrete Werte und führt keine spezielle Verarbeitung durch.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Association-Algorithmus](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Zuordnungsmodellabfragen](../../analysis-services/data-mining/association-model-query-examples.md)   
 [Miningmodellinhalt von Zuordnungsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
