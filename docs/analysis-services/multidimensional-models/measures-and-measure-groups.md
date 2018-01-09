---
title: Measures und Measuregruppen | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- measure groups [Analysis Services]
- measures [Analysis Services], about measures
- OLAP objects [Analysis Services], measures
- aggregate functions [Analysis Services]
- granularity
- measure groups [Analysis Services], about measure groups
- measures [Analysis Services]
- aggregations [Analysis Services], measures
- fact tables [Analysis Services]
ms.assetid: 4f0122f9-c3a5-4172-ada3-5bc5f7b1cc9a
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c8775c33a50d25379f1de53f00b7e66830cbf971
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="measures-and-measure-groups"></a>Measures und Measuregruppen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Ein Cube enthält *Measures* in *Measuregruppen*, Geschäftslogik sowie eine Auflistung von Dimensionen, die Kontext für die Auswertung der numerischen Daten, die ein Measure enthält. Measures und Measuregruppen sind wesentliche Bestandteile eines Cubes. Ein Cube kann ohne mindestens eines dieser Elemente nicht bestehen.  
  
 In diesem Thema werden [Measures](#bkmk_measure) und [Measure Groups](#bkmk_mg)beschrieben. Außerdem enthält es die folgende Tabelle mit Links zu Schritten zum Erstellen und Konfigurieren von Measures und Measuregruppen.  
  
|**Link**|**Beschreibung**|  
|--------------|---------------------|  
|[Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Wählen Sie einen von mehreren Ansätzen zum Erstellen von Measures und Measuregruppen aus.|  
|[Konfigurieren von Measureeigenschaften](../../analysis-services/multidimensional-models/configure-measure-properties.md)|Wenn Sie den Cube-Assistenten zum Starten des Cubes verwendet haben, müssen Sie möglicherweise die Aggregationsmethode ändern, ein Datenformat anwenden, die Sichtbarkeit des Measures in Clientanwendungen festlegen oder einen Measureausdruck hinzufügen, um die Daten vor dem Aggregieren von Werten zu bearbeiten.|  
|[Konfigurieren von Measuregruppeneigenschaften](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|In einem mehrdimensionalen Modell entspricht eine Measuregruppe einer Faktentabelle im als Quelle verwendeten Data Warehouse. Anhand von Eigenschaften für eine Measuregruppe können Sie Cacheverhalten, Speicher und Verarbeitungsrichtlinien festlegen, die kollektiv auf Ebene der Measuregruppe gelten. Die Partitionskonfiguration richtet sich teilweise nach den Eigenschaften, die Sie für Measuregruppenobjekte festgelegten.|  
|[Verwenden von Aggregatfunktionen](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|Machen Sie sich mit den Aggregationsmethoden vertraut, die einem Measure zugewiesen werden können.|  
|[Erweiterung auswählen](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|Semiadditives Verhalten bezieht sich auf Aggregationen, die nur für einige Dimensionen gültig sind. Ein typisches Beispiel ist der Saldo eines Bankkontos. Möglicherweise möchten Sie Saldi nach Kunde und Region hinzufügen, aber nicht nach Zeit. Beispielsweise würden Sie keine Saldi vom gleichen Konto über mehrere aufeinanderfolgende Tage hinzufügen wollen. Zum Definieren von semiadditivem Verhalten verwenden Sie den Assistenten zum Hinzufügen von Business Intelligence.|  
|[Verknüpfte Measuregruppen](../../analysis-services/multidimensional-models/linked-measure-groups.md)|Führen Sie eine vorhandene Measuregruppe in anderen Cubes in derselben Datenbank oder in anderen Analysis Services-Datenbanken einem anderen Zweck zu.|  
  
##  <a name="bkmk_measure"></a> Measures  
 Ein Measure stellt eine Spalte mit quantifizierbaren (und gewöhnlich numerischen) Daten dar, die aggregiert werden können. Measures stellen einen bestimmen Aspekt der Organisationstätigkeit dar, ausgedrückt in finanzieller Hinsicht (z. B. Umsatz, Margen oder Kosten), als Anzahlen (Menge des Bestands, Anzahl der Mitarbeiter, Kunden und Bestellungen) oder als eine komplexere Berechnung, die die Geschäftslogik umfasst.  
  
 Jeder Cube muss über mindestens ein Measure verfügen, die meisten besitzen jedoch mehrere, einige sogar Hunderte. Strukturell gesehen ist ein Measure häufig einer Quellspalte in einer Faktentabelle zugeordnet, wobei die Spalte die Werte enthält, die zum Laden des Measures verwendet werden. Alternativ können Sie ein Measure auch mithilfe von MDX definieren.  
  
 Measures sind kontextbezogen und gelten für numerische Daten in einem Kontext, der durch die Dimensionselemente bestimmt wird, die in der Abfrage enthalten sind. Beispielsweise wird ein Measure, durch das **Verkäufe des Wiederverkäufers** berechnet werden, durch einen **Sum** -Operator gesichert und fügt die Beträge der Verkäufe für jedes in der Abfrage enthaltene Dimensionselement hinzu. Unabhängig davon, ob die Abfrage einzelne Produkte angibt, sich auf eine Kategorie bezieht oder nach Zeit oder Geografie segmentiert ist, sollte das Measure einen Vorgang erzeugen, der für die in der Abfrage enthaltenen Dimensionen gültig ist.  
  
 In diesem Beispiel werden die **Verkäufe des Wiederverkäufers** zu verschiedenen Ebenen der **Vertriebsgebietshierarchie** aggregiert.  
  
 ![PivotTable mit Measures und Dimensionen als Legende](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "PivotTable mit Measures und Dimensionen als Legende")  
  
 Measures erzeugen gültige Ergebnisse, wenn die Faktentabelle, die die numerischen Quelldaten enthält, auch Zeiger auf in der Abfrage verwendete Dimensionstabellen enthält. Wenn in dem Beispiel mit Verkäufen des Wiederverkäufers in jeder Zeile, in der ein Betrag der Verkäufe gespeichert wird, auch ein Zeiger auf eine Produkttabelle, eine Datentabelle oder eine Vertriebsgebietstabelle gespeichert wird, werden Abfragen, die Elemente aus solchen Dimensionen enthalten, korrekt aufgelöst.  
  
 Was geschieht, wenn das Measure keinen Bezug zu den in der Abfrage verwendeten Dimensionen aufweist? In der Regel werden Analysis Services das Standardmeasure anzeigen, und der Wert wird für alle Elemente gleich sein. In diesem Beispiel weisen **Internetverkäufe**, durch die Direktverkäufe von Kunden über den Onlinekatalog gemessen werden, keine Beziehung zur Vertriebsorganisation auf.  
  
 ![PivotTable mit wiederholten Measurewerten](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "Pivottable mit wiederholten Measurewerten")  
  
 Um die Wahrscheinlichkeit zu senken, solche Verhaltensweisen in einer Clientanwendung zu finden, könnten Sie mehrere Cubes oder Perspektiven innerhalb derselben Datenbank erstellen und sicherstellen, dass jeder Cube oder jede Perspektive nur verknüpfte Objekte enthält. Sie müssen die Beziehungen zwischen der Measuregruppe (mit der Faktentabelle verknüpft) und den Dimensionen überprüfen.  
  
##  <a name="bkmk_mg"></a> Measure Groups  
 In einem Cube werden Measures nach den ihnen zugrunde liegenden Faktentabellen in Measuregruppen gruppiert. Measuregruppen werden verwendet, um Dimensionen Measures zuzuordnen. Measuregruppen werden auch für Measures verwendet, die Distinct Count als Aggregationsverhalten haben. Durch das Platzieren der Distinct Count Measures in der jeweils zugehörigen Measuregruppe wird die Aggregationsverarbeitung optimiert.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.MeasureGroup> -Objekt besteht aus grundlegenden Informationen wie dem Gruppennamen, dem Speichermodus und dem Verarbeitungsmodus. Es enthält auch seine Bestandteile, die Measures, Dimensionen und Partitionen, die die Measuregruppe bilden.  
  
## <a name="see-also"></a>Siehe auch  
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
