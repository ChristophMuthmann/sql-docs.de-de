---
title: "Tests und Überprüfung (Datamining) | Microsoft Docs"
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
- testing data mining models
- comparing mining models
- continuous attribute charts
- data mining [Analysis Services], models
- charts [Analysis Services]
- predictive modeling [Analysis Services]
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- confidence scores [data mining]
- displaying mining accuracy
- predictions [Analysis Services], comparing mining models
- scoring [data mining]
- lift charts [Analysis Services]
- classification matrix [Analysis Services]
- CRISP-DM
- accuracy testing [data mining]
ms.assetid: 197144f5-21ed-4009-b448-fe412fb3916c
caps.latest.revision: "61"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 38ef15322528bfae0dbd1b134d80fb7d1a56a734
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="testing-and-validation-data-mining"></a>Tests und Überprüfung (Data Mining)
  Die Überprüfung ist der Prozess des Bewertens, welche Leistung die Miningmodelle mit echten Daten erzielen. Es ist wichtig, dass Sie Ihre Miningmodelle überprüfen, indem Sie ihre Qualität und Merkmale studieren, bevor Sie sie in einer Produktionsumgebung bereitstellen.  
  
 In diesem Abschnitt werden einige grundlegende Konzepte im Zusammenhang mit der Modellqualität und die Strategien zur Modellvalidierung vorgestellt, die in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zur Verfügung stehen. Eine Übersicht dazu, wie Modellüberprüfungen in den größeren Data Mining-Prozess eingebunden werden können, finden Sie unter [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>Methoden zum Testen und Überprüfen von Data Mining-Modellen  
 Es gibt viele Ansätze zum Bewerten der Qualität und der Eigenschaften eines Data Mining-Modells.  
  
-   Verwenden Sie verschiedene Measures für die statistische Gültigkeit, um zu bestimmen, ob Probleme mit den Daten oder dem Modell vorliegen.  
  
-   Teilen Sie die Daten in Trainings- und Testsätze auf, um die Genauigkeit von Vorhersagen zu testen.  
  
-   Bitten Sie betriebswirtschaftliche Experten, die Ergebnisse des Data Mining-Modells zu überprüfen und zu bestimmen, ob die erkannten Muster für das gewollte Geschäftsszenario bedeutungsvoll sind.  
  
 Alle diese Methoden sind in der Data Mining-Methodologie nützlich und werden beim Erstellen, Testen und Optimieren von Modellen zur Lösung eines bestimmten Problems iterativ eingesetzt. Es gibt keine einzelne umfassende Regel, aus der Sie ableiten können, wann ein Modell ausreichend ist bzw. wann ausreichend Daten vorliegen.  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>Definition von Kriterien zum Überprüfen von Data Mining-Modellen  
 Data Mining-Measures lassen sich im Allgemeinen den Kategorien Genauigkeit, Zuverlässigkeit und Nützlichkeit zuteilen.  
  
 Die*Genauigkeit* ist ein Maß, das besagt, wie gut ein Ergebnis vom Modell mit den Attributen der bereitgestellten Daten korreliert wird. Es gibt verschiedenen Measures für die Genauigkeit, die jedoch alle von den verwendeten Daten abhängig sind. In der Praxis können Werte fehlen oder ungenau sein, oder die Daten können durch mehrere Prozesse verändert worden sein. Insbesondere in der Untersuchungs- und Entwicklungsphase kann es sein, dass eine bestimmte Menge an Fehlern in den Daten akzeptiert wird, insbesondere wenn Daten mit relativ einheitlichen Merkmalen vorliegen. Beispielsweise kann ein Modell, mit dem der Umsatz einer bestimmten Niederlassung anhand der vergangenen Umsätze vorhergesagt wird, auch dann stark korreliert und sehr genau sein, wenn die betreffende Niederlassung durchgängig eine falsche Buchhaltungsmethode verwendet hat. Deshalb müssen Genauigkeitsmaße durch Bewertungen der Zuverlässigkeit ausgeglichen werden.  
  
 Durch die*Zuverlässigkeit* wird bewertet, wie sich ein Data Mining-Modell bei Anwendung auf unterschiedliche Datasets verhält. Ein Data Mining-Modell ist zuverlässig, wenn es unabhängig von den bereitgestellten Testdaten die gleichen Typen von Vorhersagen erzeugt oder die gleichen Arten von Mustern sucht. Beispielsweise würde sich das Modell, das für die Niederlassung erzeugt wurde, in der die falsche Buchhaltungsmethode verwendet wurde, nicht gut auf andere Niederlassungen verallgemeinern lassen, und daher wäre es nicht zuverlässig.  
  
 Die*Nützlichkeit* schließt verschiedene Metriken ein, aus denen hervorgeht, ob das Modell nützliche Informationen liefert. Beispielsweise kann ein Data Mining-Modell, das den Standort einer Niederlassung mit dem Umsatz korreliert, sowohl genau als auch zuverlässig, aber nicht nützlich sein, weil sich dieses Ergebnis nicht dadurch verallgemeinern lässt, dass dem gleichen Standort weitere Niederlassungen hinzugefügt werden. Darüber hinaus beantwortet es die grundlegende Geschäftsfrage nicht, warum an bestimmten Standorten höhere Umsätze erzielt werden. Es kann sich auch herausstellen, dass ein anscheinend erfolgreiches Modell in Wirklichkeit bedeutungslos ist, weil es auf Kreuzkorrelationen der Daten basiert.  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>Tools zum Testen und Überprüfen von Miningmodellen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt mehrere Ansätze zur Überprüfung von Data Mining-Lösungen, die alle Phasen der Data Mining-Testmethoden unterstützen.  
  
-   Partitionieren der Daten in Test- und Trainingssätze  
  
-   Filtern von Modellen, um verschiedene Kombinationen der gleichen Quelldaten zu schulen und zu testen.  
  
-   Das Messen von *Prognosegüte* und *Gewinn*. Ein *Prognosegütediagramm* ist eine Methode zur visuellen Darstellung der Verbesserung, die verglichen mit dem Anstellen Zufallsvorhersage aus dem Einsatz eines Data Mining-Modells resultiert.  
  
-   Ausführen der *Kreuzvalidierung* für Datasets  
  
-   Generieren von *Klassifikationsmatrizen*. Diese Diagramme tragen dazu bei, zutreffende und falsche Vermutungen in eine Tabelle einzufügen und zu sortieren, sodass Sie mühelos messen können, wie genau das Modell den Zielwert vorhersagt.  
  
-   Erstellen von *Punktdiagrammen* , um die Eignung einer Regressionsformel zu beurteilen.  
  
-   Erstellen von *Gewinndiagrammen* , in denen finanzielle Gewinne oder Kosten mit dem Miningmodell verknüpft werden, damit Sie den Wert der Empfehlungen beurteilen können.  
  
 Der Sinn dieser Metrik liegt nicht darin herauszufinden, ob das Data Mining-Modell die Antwort auf Ihre Geschäftsfrage liefert; vielmehr stellt diese Metrik objektive Messwerte bereit, mit denen Sie die Zuverlässigkeit Ihrer Daten für Vorhersageanalysen beurteilen und entscheiden können, ob bei der Entwicklung eine bestimmte Iteration implementiert werden soll.  
  
 Dieser Abschnitt enthält eine Übersicht der einzelnen Methoden und führt Sie durch die Schritte zur Messung der Genauigkeit von Modellen, die Sie mithilfe von SQL Server Data Mining erstellen.  
  
### <a name="related-topics"></a>Verwandte Themen  
  
|Thema|Links|  
|------------|-----------|  
|Erfahren Sie mehr darüber, wie Sie ein Testdataset mithilfe eines Assistenten oder mit DMX-Befehlen einrichten können.|[Trainings- und Testdatasets](../../analysis-services/data-mining/training-and-testing-data-sets.md)|  
|Erfahren Sie mehr darüber, wie Sie die Verteilung und die Repräsentativität der Daten in einer Miningstruktur testen können.|[Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Informationen Sie zu den Typen von Genauigkeitsdiagrammen.|[Prognosegütediagramm &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gewinndiagramm &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Punktdiagramm &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Erfahren Sie mehr darüber, wie Sie eine Klassifikationsmatrix, auch bekannt unter dem Namen Verwirrungsmatrix, erstellen, um die Anzahl von als wahr positiv, falsch positiv, wahr negativ und falsch negativ klassifizierten Ergebnissen zu ermitteln.|[Klassifikationsmatrix &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Tasks und Anweisungen für Test und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
