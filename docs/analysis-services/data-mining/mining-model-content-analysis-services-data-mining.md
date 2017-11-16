---
title: "Miningmodellinhalt (Analysis Services – Datamining) | Microsoft Docs"
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
- algorithms [data mining]
- standard deviation
- confidence scores [data mining]
- mining models [Analysis Services]
- variance
- machine learning algorithms [Analysis Services]
- model content
- support [data mining]
- node distribution
ms.assetid: e7c039f6-3266-4d84-bfbd-f99b6858acf4
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4097a5ab62a6e30f2056216ec83eb0c568547479
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mining-model-content-analysis-services---data-mining"></a>Miningmodellinhalt (Analysis Services &ndash;</ph> Data Mining)
  Nachdem Sie ein Miningmodell, das Daten aus der zugrunde liegenden Miningstruktur enthält, entworfen und verarbeitet haben, ist das Miningmodell vollständig und enthält *Miningmodellinhalt*. Sie können diesen Inhalt verwenden, um Vorhersagen zu treffen oder die Daten zu analysieren.  
  
 Der Miningmodellinhalt umfasst Metadaten zum Modell, Datenstatistiken sowie vom Miningalgorithmus erkannte Muster. Je nach verwendetem Algorithmus kann der Modellinhalt Regressionsformeln, Regel- und Itemset-Definitionen sowie Gewichtungen und andere Statistiken enthalten.  
  
 Der Miningmodellinhalt wird in einer Standardstruktur präsentiert, unabhängig davon, welcher Algorithmus verwendet wurde. Sie können die Struktur im Microsoft Generic Content Tree Viewer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]durchsuchen und anschließend zu einem der benutzerdefinierten Viewer wechseln, um sich die Interpretation und die grafische Darstellung für jeden Modelltyp anzeigen zu lassen. Sie können auch Abfragen für den Miningmodellinhalt erstellen, indem Sie einen beliebigen Client verwenden, der das MINING_MODEL_CONTENT-Schemarowset unterstützt. Weitere Informationen finden Sie unter [Data Mining-Abfragetasks und Anweisungen](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
 In diesem Abschnitt wird die grundlegende Inhaltsstruktur, die für alle Miningmodelltypen bereitgestellt wird, beschrieben. Es werden die Knotentypen beschrieben, die allen Miningmodellinhalten gemeinsam sind, und Richtlinien zur Interpretation der Daten vorgestellt.  
  
 [Struktur des Miningmodellinhalts](#bkmk_Structure)  
  
 [Knoten im Modellinhalt](#bkmk_Nodes)  
  
 [Miningmodellinhalt nach Algorithmustyp](#bkmk_AlgoType)  
  
 [Miningmodellinhalt-Anzeigetools](#bkmk_Viewing)  
  
 [Miningmodellinhalt-Abfragetools](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> Struktur des Miningmodellinhalts  
 Der Inhalt jedes Modells wird als Reihe von *Knoten*dargestellt. Ein Knoten ist ein Objekt innerhalb eines Miningmodells, das Metadaten und Informationen über einen Teil des Modells enthält. Knoten werden in einer Hierarchie angeordnet. Die genaue Anordnung der Knoten in der Hierarchie und die Bedeutung der Hierarchie ist vom verwendeten Algorithmus abhängig. Wenn Sie z. B. ein Entscheidungsstrukturmodell verwenden, kann das Modell mehrere Strukturen enthalten, die alle mit dem Modellstamm verbunden sind. Wenn Sie ein neuronales Netzwerkmodell erstellen, kann das Modell ein oder mehrere Netzwerke enthalten sowie einen Statistikknoten.  
  
 Der erste Knoten in jedem Modell wird *Stammknoten*oder *übergeordneter* Modellknoten genannt. Jedes Modell hat einen Stammknoten (NODE_TYPE = 1). Der Stammknoten enthält in der Regel einige Metadaten über das Modell sowie die Anzahl der untergeordneten Knoten, jedoch wenige Informationen über die Muster, die vom Modell erkannt wurden.  
  
 Je nachdem mit welchem Algorithmus Sie das Modell erstellt haben, verfügt der Stammknoten über eine unterschiedliche Anzahl von untergeordneten Knoten. Untergeordnete Knoten haben eine andere Bedeutung und unterscheiden sich im Inhalt, je nach Algorithmus und Datentiefe bzw. Datenkomplexität.  
  
##  <a name="bkmk_Nodes"></a> Knoten im Miningmodellinhalt  
 In einem Miningmodell ist ein Knoten ein universell einsetzbarer Container, in dem Informationen zum gesamten Modell oder zu einem Teil des Modells gespeichert werden. Die Struktur der Knoten ist immer dieselbe und enthält die Spalten, die im Data Mining-Schemarowset definiert sind. Weitere Informationen finden Sie unter [DMSCHEMA_MINING_MODEL_CONTENT-Rowset](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md).  
  
 Jeder Knoten enthält Metadaten über den Knoten. Dazu gehört eine ID, die für jedes Modell einzigartig ist, die ID des übergeordneten Knotens und die Anzahl der untergeordneten Knoten, über die ein Knoten verfügt. Aus den Metadaten geht das Modell hervor, zu dem der Knoten gehört, sowie der Datenbankkatalog, in dem dieses spezielle Modell gespeichert ist. Welche weiteren Informationen im Knoten angegeben sind, hängt vom Algorithmus ab, den Sie zur Erstellung des Modells verwendet haben. Dazu gehören:  
  
-   Anzahl aller Fälle in den Trainingsdaten, die einen bestimmten vorhergesagten Wert unterstützen  
  
-   Statistische Angaben wie Mittelwert, Standardabweichung und Varianz  
  
-   Koeffizienten und Formeln  
  
-   Definition von Regeln und Querzeigern  
  
-   XML-Fragmente, die einen Teil des Modells beschreiben  
  
### <a name="list-of-mining-content-node-types"></a>Liste von Mininginhalts-Knotentypen  
 In der folgenden Tabelle werden die verschiedenen Knotentypen aufgeführt, die in Data Mining-Modellen ausgegeben werden. Da jeder Algorithmus Informationen anders verarbeitet, generiert jedes Modell nur ganz bestimmte Knotentypen. Wenn Sie den Algorithmus ändern, ändern sich möglicherweise auch die Knotentypen. Auch der Inhalt der Knoten kann sich ändern, wenn Sie das Modell erneut verarbeiten.  
  
> [!NOTE]  
>  Wenn Sie einen anderen Datamining-Dienst verwenden, oder wenn Sie Ihre eigenen Algorithmus-Plug-in erstellen, möglicherweise weitere benutzerdefinierte Knotentypen zur Verfügung.  
  
|NODE_TYPE-ID|Knotenbezeichnung|Knoteninhalt|  
|-------------------|----------------|-------------------|  
|1|Model|Metadaten- und Stamminhaltsknoten. Gilt für alle Modelltypen.|  
|2|Struktur|Stammknoten einer Klassifizierungsstruktur. Gilt für Entscheidungsstrukturmodelle.|  
|3|Interior|Innerer geteilter Knoten einer Struktur. Gilt für Entscheidungsstrukturmodelle.|  
|4|Distribution|Endknoten einer Struktur. Gilt für Entscheidungsstrukturmodelle.|  
|5|Cluster|Vom Algorithmus erkanntes Cluster. Gilt für Clusteringmodelle und Sequenzclustermodelle.|  
|6|Unknown|Unbekannter Knotentyp.|  
|7|ItemSet|Vom Algorithmus erkanntes Itemset. Gilt für Zuordnungsmodelle und Sequenzclustermodelle.|  
|8|AssociationRule|Vom Algorithmus erkannte Zuordnungsregel. Gilt für Zuordnungsmodelle und Sequenzclustermodelle.|  
|9|PredictableAttribute|Vorhersagbares Attribut. Gilt für alle Modelltypen.|  
|10|InputAttribute|Eingabeattribut. Gilt für Entscheidungsstrukturen und Naïve Bayes-Modelle.|  
|11|InputAttributeState|Statistik über die Status eines Eingabeattributs. Gilt für Entscheidungsstrukturen und Naïve Bayes-Modelle.|  
|13|Sequenz|Oberster Knoten für die Markov-Modell-Komponente eines Sequenzclusters. Gilt für alle Sequenzclustermodelle.|  
|14|Transition|Markov-Übergangsmatrix. Gilt für alle Sequenzclustermodelle.|  
|15|TimeSeries|Nicht-Stammknoten einer Zeitreihenstruktur. Gilt nur für Zeitreihenmodelle.|  
|16|TsTree|Stammknoten einer Zeitreihenstruktur, die sich auf eine vorhersagbare Zeitreihe bezieht. Gilt für Zeitreihenmodelle, aber nur, wenn das Modell mit dem MIXED-Parameter erstellt wurde.|  
|17|NNetSubnetwork|Ein Subnetzwerk. Gilt für neuronale Netzwerkmodelle.|  
|18|NNetInputLayer|Gruppe, die die Knoten der Eingabeebene enthält. Gilt für neuronale Netzwerkmodelle.|  
|19|NNetHiddenLayer|Gruppe, die die Knoten zur Beschreibung der verborgenen Ebene enthält. Gilt für neuronale Netzwerkmodelle.|  
|21|NNetOutputLayer|Gruppe, die die Knoten der Ausgabeebene enthält. Gilt für neuronale Netzwerkmodelle.|  
|21|NNetInputNode|Knoten in der Eingabeebene, der einem Eingabeattribut mit den entsprechenden Status entspricht. Gilt für neuronale Netzwerkmodelle.|  
|22|NNetHiddenNode|Knoten in der verborgenen Ebene. Gilt für neuronale Netzwerkmodelle.|  
|23|NNetOutputNode|Knoten in der Ausgabeebene. Dieser Knoten entspricht normalerweise einem Ausgabeattribut und den entsprechenden Status. Gilt für neuronale Netzwerkmodelle.|  
|24|NNetMarginalNode|Randstatistik über den Trainingssatz. Gilt für neuronale Netzwerkmodelle.|  
|25|RegressionTreeRoot|Stamm einer Regressionsstruktur. Gilt für lineare Regressionsmodelle und Entscheidungsstrukturmodelle, die kontinuierliche Eingabeattribute enthalten.|  
|26|NaiveBayesMarginalStatNode|Randstatistik über den Trainingssatz. Gilt für Naïve Bayes-Modelle.|  
|27|ArimaRoot|Stammknoten eines ARIMA-Modells. Gilt nur für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|28|ArimaPeriodicStructure|Eine periodische Struktur in einem ARIMA-Modell. Gilt nur für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|29|ArimaAutoRegressive|Autoregressiver Koeffizient für einen einzelnen Ausdruck in einem ARIMA-Modell.<br /><br /> Gilt nur für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|30|ArimaMovingAverage|Koeffizient für den gleitenden Durchschnitt für einen einzelnen Ausdruck in einem ARIMA-Modell. Gilt nur für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|1000|CustomBase|Ausgangspunkt für benutzerdefinierte Knotentypen. Benutzerdefinierte Knotentypen müssen ganze Zahlen sein, deren Wert größer ist als diese Konstante. Gilt für Modelle, die mit benutzerdefinierten Plug-In-Algorithmen erstellt wurden.|  
  
### <a name="node-id-name-caption-and-description"></a>Knoten-ID, Name, Beschriftung und Beschreibung  
 Der Stammknoten jedes Modells hat immer 0 als eindeutige ID (**NODE_UNIQUE_NAME**). Alle Knoten-IDs werden automatisch von Analysis Services zugewiesen und können nicht geändert werden.  
  
 Der Stammknoten für jedes Modell enthält auch einige grundlegende Metadaten über das Modell. Diese Metadaten umfassen die Analysis Services-Datenbank, in der das Modell gespeichert ist (**MODEL_CATALOG**), das Schema (**MODEL_SCHEMA**) und der Name des Modells (**MODEL_NAME**). Diese Informationen werden in jedem Knoten des Modells angezeigt, d. h. Sie müssen nicht den Stammknoten abfragen, um diese Metadaten abzurufen.  
  
 Zusätzlich zum Namen, der als eindeutige ID dient, verfügt jeder Knoten über einen *Namen* (**NODE_NAME**). Dieser Name wird automatisch vom Algorithmus für Anzeigezwecke erstellt und kann nicht bearbeitet werden.  
  
> [!NOTE]  
>  Mit dem Microsoft Clustering-Algorithmus können Benutzer jedem Cluster einen Anzeigenamen zuweisen. Diese Anzeigenamen werden jedoch nicht auf dem Server persistent gespeichert, und wenn Sie das Modell erneut verarbeiten, werden vom Algorithmus neue Clusternamen erstellt.  
  
 *Beschriftung* und *Beschreibung* für jeden Knoten werden automatisch vom Algorithmus erstellt und dienen als Beschreibungshilfe, um den Inhalt eines Knotens besser verstehen zu können. Der für jedes Feld generierte Text hängt vom Modelltyp ab. In einigen Fällen können der Name, die Beschriftung und die Beschreibung genau dieselbe Zeichenfolge enthalten. In anderen Modellen wiederum kann die Beschreibung jedoch zusätzliche Informationen enthalten. Details zur Implementierung finden Sie im Abschnitt zu den einzelnen Modelltypen.  
  
> [!NOTE]  
>  Der Analysis Services-Server unterstützt die Umbenennung von Knoten nur dann, wenn Sie die Knoten mit einem benutzerdefinierten Plug-In-Algorithmus erstellen, der die Möglichkeit zur Umbenennung implementiert. Um das Umbenennung zu aktivieren, müssen Sie die Methoden überschreiben, wenn Sie den Plug-In-Algorithmus erstellen.  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>Übergeordnete Knoten, untergeordnete Knoten und Knotenkardinalität  
 Die Beziehung zwischen über- und untergeordneten Knoten in einer Baumstruktur wird durch den Wert in der PARENT_UNIQUE_NAME-Spalte festgelegt. Dieser Wert wird im untergeordneten Knoten gespeichert und informiert Sie über die ID des übergeordneten Knotens. Es folgen nun einige Beispiele dafür, wie diese Informationen verwendet werden können:  
  
-   Ein PARENT_UNIQUE_NAME, der NULL ist, bedeutet, dass der Knoten der oberste Knoten des Modells ist.  
  
-   Wenn der Wert von PARENT_UNIQUE_NAME 0 ist, bedeutet dies, dass der Knoten dem obersten Knoten des Modells direkt untergeordnet sein muss. Das liegt daran, dass die ID des Stammknotens immer 0 ist.  
  
-   Sie können Funktionen innerhalb einer Data Mining-Erweiterung (DMX)-Abfrage verwenden, um unter- oder übergeordnete Knoten eines bestimmten Knotens zu finden. Weitere Informationen zur Verwendung von Funktionen in Abfragen finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md).  
  
 *Kardinalität* verweist auf die Anzahl der Elemente in einem Satz. Im Kontext eines verarbeiteten Miningmodells sagt die Kardinalität aus, wie viele direkt untergeordnete Elemente ein bestimmter Knoten hat. Wenn z. B. ein Entscheidungsstrukturmodell über einen Knoten für [Jahreseinkommen] und dieser Knoten wiederum über zwei untergeordnete Knoten verfügt, einen für die Bedingung [Jahreseinkommen] = Hoch und einen für die Bedingung [Jahreseinkommen] = Niedrig, dann wäre der Wert von CHILDREN_CARDINALITY für den Knoten [Jahreseinkommen] 2.  
  
> [!NOTE]  
>  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]werden nur die unmittelbar untergeordneten Knoten beim Berechnen der Kardinalität eines Knoten gezählt. Wenn Sie jedoch einen benutzerdefinierten Plug-In-Algorithmus erstellen, können Sie CHILDREN_CARDINALITY überladen, um die Kardinalität anders zu zählen. Die ist beispielsweise dann sinnvoll, wenn Sie die Gesamtzahl der untergeordneten Knoten bestimmten möchten und nicht nur die direkt untergeordneten Knoten.  
  
 Auch wenn die Kardinalität für alle Modelle auf dieselbe Weise gezählt wird, hängt die Interpretation oder die Verwendung des Kardinalitätswerts davon ab, welchen Modelltyp Sie verwenden. Beispielsweise gibt die Kardinalität des obersten Knotens in einem Clusteringmodell Aufschluss darüber, wie viele Muster insgesamt gefunden wurden. In anderen Modelltypen hat die Kardinalität möglicherweise immer einen festgelegten Wert, der vom Knotentyp abhängig ist. Weitere Informationen zum Interpretieren von Kardinalitätswerten finden Sie in den Abschnitten zu den einzelnen Modelltypen.  
  
> [!NOTE]  
>  Einige Modelle, z. B. solche, die mithilfe des Microsoft Neural Network-Algorithmus erstellt wurden, enthalten zusätzlich einen besonderen Knotentyp mit beschreibenden Statistiken über die Trainingsdaten für das gesamte Modell. Definitionsgemäß verfügen diese Knoten nie über untergeordnete Knoten.  
  
### <a name="node-distribution"></a>Knotenverteilung  
 Die NODE_DISTRIBUTION-Spalte enthält eine geschachtelte Tabelle, die in vielen Knoten wichtige und detaillierte Informationen zu den vom Algorithmus entdeckten Mustern bereitstellt. Die genauen Statistiken in dieser Tabelle hängen ab vom Modelltyp, der Position des Knotens in der Struktur, und davon, ob es sich bei dem vorhersagbaren Attribut um einen fortlaufenden numerischen Wert oder um einen diskreten Wert handelt. Die Statistiken geben Auskunft zu den Mindest- und Höchst-Werten eines Attributs, zu Werte-Gewichtungen, zur Anzahl der Fälle in einem Knoten, zu den in einer Regressionsformel verwendeten Koeffizienten sowie zu statistischen Maßen wie Standardabweichung und Varianz. Weitere Informationen zur Interpretation der Knotenverteilung finden Sie im Abschnitt zum jeweiligen Modelltyp.  
  
> [!NOTE]  
>  Die Tabelle NODE_DISTRIBUTION ist möglicherweise leer. Dies ist abhängig vom Knotentyp. So dienen bestimmte Knoten nur zur Organisation einer Sammlung untergeordneter Knoten. Diese untergeordneten Knoten enthalten dann die ausführlichen Statistiken.  
  
 Die geschachtelte Tabelle NODE_DISTRIBUTION enthält immer die folgenden Spalten. Der Inhalt jeder Spalte hängt vom Modelltyp ab. Weitere Informationen über bestimmte Modelltypen finden Sie unter [Miningmodellinhalt nach Algorithmustyp](#bkmk_AlgoType).  
  
 ATTRIBUTE_NAME  
 Der Inhalt ist vom Algorithmus abhängig. Dabei kann es sich um den Namen einer Spalte, z. B. ein vorhersagbares Attribut, eine Regel, ein Itemset oder eine Algorithmus-interne Information handeln, z. B. einen Teil einer Formel.  
  
 Diese Spalte kann auch ein Attribut-Wert-Paar enthalten.  
  
 ATTRIBUTE_VALUE  
 Wert des Attributs, das mit ATTRIBUTE_NAME benannt ist.  
  
 Wenn mit dem Attributnamen eine Spalte bezeichnet wird, dann enthält ATTRIBUTE_VALUE im einfachsten Fall einen der diskreten Werte für diese Spalte.  
  
 Je nachdem wie der Algorithmus Werte verarbeitet, kann ATTRIBUTE_VALUE auch ein Flag enthalten, aus dem hervorgeht, ob für das Attribut ein Wert vorhanden ist (**Vorhanden**) oder ob der Wert NULL lautet (**Fehlt**).  
  
 In einem Modell, das z. B. dazu dient, Kunden ausfindig zu machen, die ein bestimmtes Produkt mindestens einmal gekauft haben, kann die ATTRIBUTE_NAME-Spalte das Attribut-Wert-Paar enthalten, das das gewünschte Element definiert, z. B. `Model = 'Water bottle'`. Die ATTRIBUTE_VALUE-Spalte würde nur das Schlüsselwort **Vorhanden** oder **Fehlt**enthalten.  
  
 Alias  
 Anzahl der Fälle, die über dieses Attribut-Wert-Paar verfügen oder dieses Itemset bzw. diese Regel enthalten.  
  
 In der Regel gibt der Unterstützungswert eines Knotens Aufschluss darüber, wie viele Fälle aus dem Trainingssatz im aktuellen Knoten enthalten sind. In den meisten Modelltypen gibt der Unterstützungswert eine genaue Anzahl von Fällen an. Unterstützungswerte sind insofern nützlich, als dass sie Einsicht in die Verteilung der Daten innerhalb Ihrer Trainingsfälle erlauben, ohne dass dazu die Trainingsdaten abgefragt werden müssen. Der Analysis Services-Server verwendet diese gespeicherten Daten außerdem für einen Vergleich der gespeicherten Wahrscheinlichkeit mit der vorherigen Wahrscheinlichkeit, um so festzustellen, ob die Inferenz stark oder schwach ist.  
  
 So zeigt z. B. in einer Klassifizierungsstruktur der Unterstützungswert die Anzahl der Fälle an, die über die beschriebene Kombination von Attributen verfügen.  
  
 In einer Entscheidungsstruktur wird die Summe der Unterstützungswerte auf jeder Ebene einer Struktur zu den Unterstützungswerten des übergeordneten Knotens hinzuaddiert. Wenn z. B. ein Modell 1200 Fälle enthält und erst nach Geschlecht und dann wiederum nach Einkommen (Werte: Niedrig, Mittel, Hoch) gleichmäßig unterteilt ist, dann beläuft sich die Summe der untergeordneten Knoten von Knoten (2) – also der Knoten (4), (5) und (6) – immer auf die Anzahl der Fälle von Knoten (2).  
  
|Knoten-ID und Knotenattribute|Unterstützte Anzahl|  
|---------------------------------|-------------------|  
|(1) Modellstamm|1200|  
|(2) Geschlecht = Männlich<br /><br /> (3) Geschlecht = Weiblich|600<br /><br /> 600|  
|(4) Geschlecht = Männlich und Einkommen = Hoch<br /><br /> (5) Geschlecht = Männlich und Einkommen = Mittel<br /><br /> (6) Geschlecht = Männlich und Einkommen = Niedrig|200<br /><br /> 200<br /><br /> 200|  
|(7) Geschlecht = Weiblich und Einkommen = Hoch<br /><br /> (8) Geschlecht = Weiblich und Einkommen = Mittel<br /><br /> (9) Geschlecht = Weiblich und Einkommen = Niedrig|200<br /><br /> 200<br /><br /> 200|  
  
 Bei einem Clusteringmodell kann die Anzahl für die Unterstützung gewichtet werden, um die Wahrscheinlichkeit der Zugehörigkeit zu mehreren Clustern zu berücksichtigen. Die Mitgliedschaft zu mehreren Clustern ist die Standardclustermethode. In diesem Szenario, in dem nicht jeder Fall notwendigerweise nur zu einem Cluster gehört, und in einem solchen Modell entspricht die Summe der Unterstützungswerte für alle Cluster möglichweise nicht 100 %.  
  
 PROBABILITY  
 Gibt die Wahrscheinlichkeit für diesen bestimmten Knoten innerhalb des gesamten Modells an.  
  
 Allgemein steht die Wahrscheinlichkeit für die Unterstützung dieses bestimmten Werts, geteilt durch die Gesamtzahl der Fälle innerhalb des Knotens (NODE_SUPPORT).  
  
 Jedoch wird die Wahrscheinlichkeit leicht angepasst, um eine Verschiebung durch fehlende Werte in den Daten auszuschließen.  
  
 Wenn z. B. die aktuellen Werte für [Anzahl Kinder] 'Eins' und 'Zwei' sind, möchten Sie die Erstellung eines Modells vermeiden, das die Vorhersage trifft, dass es nicht möglich sei, keine Kinder oder auch drei Kinder zu haben. Um sicherzustellen, dass fehlende Werte zwar unwahrscheinlich aber nicht unmöglich sind, addiert der Algorithmus den Ergebnissen der Zählung der aktuellen Werte eines jeden Attributs den Wert 1 hinzu.  
  
 Beispiel:  
  
 Wahrscheinlichkeit von [Anzahl Kinder  = Eins] = [Anzahl der Fälle, in denen Anzahl Kinder = Eins] + 1/[Anzahl aller Fälle] + 3  
  
 Wahrscheinlichkeit von [Anzahl Kinder  = Zwei] = [Anzahl der Fälle, in denen Anzahl Kinder  = Zwei] + 1/[Anzahl aller Fälle] + 3  
  
> [!NOTE]  
>  Die Anpassung von 3 wird berechnet, indem der Gesamtzahl der vorhandenen Werte (n) der Wert 1 hinzugefügt wird.  
  
 Nach der Anpassung ist die Summe der Wahrscheinlichkeiten aller Werte immer noch 1. Die Wahrscheinlichkeit für den Wert ohne Daten (in diesem Beispiel [Anzahl Kinder = 'Null', 'Drei' oder ein beliebiger anderer Wert]) beginnt bei einem Wert sehr nahe bei NULL und steigt mit zunehmender Anzahl von Fällen langsam an.  
  
 Varianz  
 Gibt die Varianz der Werte innerhalb des Knotens an. Für diskrete Werte ist die Varianz definitionsgemäß 0. Wenn das Modell fortlaufende Werte unterstützt, wird die Varianz als σ (sigma) berechnet. Dazu wird der Nenner n oder die Anzahl der Fälle im Knoten verwendet.  
  
 Für die Darstellung der Standardabweichung (**StDev**) werden allgemein zwei Definitionen herangezogen. Eine dieser Methoden zur Berechnung der Standardabweichung berücksichtigt die Verschiebung, die andere nicht. Im Allgemeinen wird bei der Berechnung der Standardabweichung durch Microsoft-Data Mining-Algorithmen die Verschiebung nicht berücksichtigt.  
  
 Bei dem Wert, der in der NODE_DISTRIBUTION-Tabelle aufgeführt wird, handelt es sich um den Ist-Wert für alle diskreten und diskretisierten Attribute bzw. den Mittelwert für fortlaufende Werte.  
  
 VALUE_TYPE  
 Gibt den Datentyp des Werts oder eines Attributs und die Verwendung des Werts an. Bestimmte Werttypen gelten nur für bestimmte Modelltypen:  
  
|VALUE_TYPE-ID|Wertebezeichnung|Wertetypname|  
|--------------------|-----------------|---------------------|  
|1|Fehlt|Gibt an, dass die Falldaten keinen Wert für dieses Attribut enthalten haben. Der **Missing** -Zustand wird getrennt von Attributen berechnet, die über Werte verfügen.|  
|2|Vorhanden|Gibt an, dass die Falldaten einen Wert für dieses Attribut enthalten.|  
|3|Continuous|Gibt an, dass es sich bei dem Wert des Attributs um einen fortlaufenden numerischen Wert handelt, der deshalb als Mittelwert dargestellt werden kann (gemeinsam mit der Varianz und der Standardabweichung).|  
|4|Discrete|Gibt einen Wert an, entweder numerisch oder Text, der als diskret behandelt wird.<br /><br /> **Hinweis** Diskrete Werte können auch fehlen; bei Berechnungen wird jedoch anders mit ihnen umgegangen. Informationen finden Sie unter [Fehlende Werte &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).|  
|5|Discretized|Gibt an, dass das Attribut numerische Werte enthält, die diskretisiert wurden. Der Wert ist eine formatierte Zeichenfolge, die die Diskretisierungsbuckets beschreibt.|  
|6|Vorhanden|Gibt an, dass das Attribut über fortlaufende numerische Werte verfügt und dass Werte in den Daten vorliegen, im Gegensatz zu Werten, die fehlen oder abgeleitet sind.|  
|7|Koeffizient|Gibt einen numerischen Wert an, der einen Koeffizienten darstellt.<br /><br /> Ein Koeffizient ist ein Wert, der beim Berechnen des Werts der abhängigen Variable verwendet wird. Beispielsweise wird in einem Modell, das Regressionsformeln erstellt, um das Einkommen auf der Grundlage des Alters vorauszuberechnen, der Koeffizient in der Formel verwendet, die Alter und Einkommen miteinander in Beziehung setzt.|  
|8|Ergebnisgewinn|Gibt einen numerischen Wert an, der den Ergebnisgewinn eines Attributs darstellt.|  
|9|Statistik|Gibt einen numerischen Wert an, der eine Statistik für einen Regressor darstellt.|  
|10|Eindeutiger Knotenname|Gibt an, dass der Wert weder als numerischer Wert noch als Zeichenfolge behandelt werden soll, sondern als der eindeutige Bezeichner eines anderen Inhaltsknotens in einem Model.<br /><br /> In einem neuronalen Netzwerkmodell beispielsweise verweisen IDs von Knoten in der Ausgabeebene auf Knoten in der verborgenen Ebene bzw. von Knoten in der verborgenen Ebene auf Knoten in der Eingabeebene.|  
|11|Konstantes Glied|Gibt einen numerischen Wert an, der das konstante Glied in einer Regressionsformel darstellt.|  
|12|Periodizität|Gibt an, dass der Wert eine periodische Struktur in einem Modell kennzeichnet.<br /><br /> Gilt für nur Zeitreihenmodelle, die ein ARIMA-Modell enthalten.<br /><br /> Hinweis: Der Microsoft Time Series-Algorithmus erkennt automatisch periodische Strukturen auf Grundlage der Trainingsdaten. Dies hat zum Ergebnis, dass die Periodizitäten im endgültigen Modell möglicherweise Periodizitätswerte enthalten, die Sie beim Erstellen des Modells nicht in Form von Parametern angegeben haben.|  
|13|Autoregressive Reihenfolge|Gibt an, dass der Wert die Anzahl der autoregressiven Reihen darstellt.<br /><br /> Gilt für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|14|Reihenfolge für gleitenden Durchschnitt|Wert, der die Anzahl der gleitenden Durchschnitte in einer Reihe angibt.<br /><br /> Gilt für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|15|Differenzreihenfolge|Gibt an, dass der Wert einen Wert darstellt, aus dem hervorgeht, wie oft für die Reihe eine Unterscheidung getroffen wurde.<br /><br /> Gilt für Zeitreihenmodelle, die den ARIMA-Algorithmus verwenden.|  
|16|Boolean|Stellt einen booleschen Typ dar.|  
|17|Andere|Stellt einen benutzerdefinierten Wert dar, der vom Algorithmus definiert wird.|  
|18|Zuvor gerenderte Zeichenfolge|Stellt einen benutzerdefinierten Wert dar, den der Algorithmus als Zeichenfolge rendert. Es wurde keine Formatierung vom Objektmodell angewendet.|  
  
 Die Werttypen werden von der ADMOMD.NET-Enumeration abgeleitet. Weitere Informationen finden Sie unter <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>.  
  
### <a name="node-score"></a>Knotenergebnis  
 Die Bedeutung des Knotenergebnisses hängt vom verwendeten Modelltyp ab und kann außerdem je nach Knotentyp unterschiedlich ausfallen. Weitere Informationen über die jeweilige Berechnung von NODE_SCORE für die verschiedenen Modelle und Knotentypen finden Sie unter [Miningmodellinhalt nach Algorithmustyp](#bkmk_AlgoType).  
  
### <a name="node-probability-and-marginal-probability"></a>Knotenwahrscheinlichkeit und marginale Wahrscheinlichkeit  
 Das Miningmodell-Schemarowset umfasst die Spalten NODE_PROBABILITY und MARGINAL_PROBABILITY für alle Modelltypen. Diese Spalten enthalten nur in jenen Knoten Werte, in denen ein Wahrscheinlichkeitswert auch Sinn macht. Zum Beispiel enthält der Stammknoten eines Modells nie ein Wahrscheinlichkeitsergebnis.  
  
 In den Knoten, die Wahrscheinlichkeitsergebnisse bereitstellen, wird zwischen Knotenwahrscheinlichkeit und marginaler Wahrscheinlichkeit unterschieden.  
  
-   **Marginale Wahrscheinlichkeit** ist die Wahrscheinlichkeit für das Erreichen des Knotens vom übergeordneten Knoten aus.  
  
-   **Knotenwahrscheinlichkeit** ist die Wahrscheinlichkeit für das Erreichen des Knotens vom Stamm aus.  
  
-   Die**Knotenwahrscheinlichkeit** ist immer kleiner oder gleich der **marginalen Wahrscheinlichkeit**.  
  
 Wenn z. B. die Gesamtheit aller Kunden in einer Entscheidungsstruktur gleichmäßig nach Geschlecht unterteilt ist (ohne dass irgendwelche Werte fehlen), sollte die Wahrscheinlichkeit der untergeordneten Knoten .5 betragen. Für den Fall aber, dass jeder Knoten für das Geschlecht gleichmäßig nach Einkommensverhältnissen unterteilt ist (hoch, mittel und niedrig), sollte in diesem Fall das MARGINAL_PROBABILITY-Ergebnis für jeden untergeordneten Knoten immer .33 betragen. Der NODE_PROBABILTY-Wert hingegen ist das Produkt aller Wahrscheinlichkeiten, die zu diesem Knoten führen, und ist deswegen immer kleiner als der MARGINAL_PROBABILITY-Wert.  
  
|Ebene von Knoten/Attribut und Wert|Marginale Wahrscheinlichkeit|Knotenwahrscheinlichkeit|  
|----------------------------------------|--------------------------|----------------------|  
|Modellstamm<br /><br /> Alle Zielkunden|1|1|  
|Zielkunden unterteilt nach Geschlecht|.5|.5|  
|Zielkunden unterteilt nach Geschlecht und in der Folge wiederum dreifach unterteilt nach Einkommen|.33|0,5 x 0,33 = 0,165|  
  
### <a name="node-rule-and-marginal-rule"></a>Knotenregel und marginale Regel  
 Das Miningmodell-Schemarowset umfasst auch die Spalten NODE_RULE und MARGINAL_RULE für alle Modelltypen. Diese Spalten enthalten XML-Fragmente, die zur Serialisierung eines Modells oder zur Darstellung eines Teils der Modellstruktur verwendet werden können. Diese Spalten sind möglicherweise für einige Knoten leer, wenn ein Wert an dieser Stelle keinen Sinn machen würde.  
  
 Zwei Arten von XML-Regeln werden bereitgestellt, die den zwei Arten von Wahrscheinlichkeitswerten sehr ähnlich sind. Das XML-Fragment in MARGINAL_RULE definiert das Attribut und den Wert für den aktuellen Knoten, das XML-Fragment in NODE_RULE beschreibt den Pfad vom Modellstamm zum aktuellen Knoten.  
  
##  <a name="bkmk_AlgoType"></a> Miningmodellinhalt nach Algorithmustyp  
 Jeder Algorithmus speichert andere Arten von Informationen als Teil des Inhaltsschemas. Zum Beispiel generiert der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Clustering-Algorithmus viele untergeordnete Knoten, von denen jeder ein mögliches Cluster darstellt. Jeder Clusterknoten enthält Regeln, die Eigenschaften beschreiben, die den Elementen im Cluster gemeinsam sind. Im Gegensatz dazu enthält der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Linear Regression-Algorithmus überhaupt keine untergeordneten Knoten, sondern der übergeordnete Knoten des Modells enthält die Gleichung, die die lineare Beziehung beschreibt, die von der Analyse aufgedeckt wurde.  
  
 In der folgenden Tabelle finden Sie Links zu weiterführenden Informationen zum jeweiligen Algorithmustyp.  
  
-   **Themen zu Modellinhalten:** Hier wird die Bedeutung der verschiedenen Knotentypen für die verschiedenen Algorithmen erklärt, und Sie erhalten Hilfestellung bei der Frage, welche Knoten für einen bestimmten Modelltyp am besten geeignet sind.  
  
-   **Themen zu Abfragen:** Enthalten Beispiele von Abfragen an einen bestimmten Modelltyp und Hilfestellungen zur Auswertung der Ergebnisse.  
  
|Algorithmus oder Modelltyp|Modellinhalt|Abfragen von Mining-Modellen|  
|-----------------------------|-------------------|----------------------------|  
|Modelle für Zuordnungsregeln|[Miningmodellinhalt von Zuordnungsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)|[Beispiele für Zuordnungsmodellabfragen](../../analysis-services/data-mining/association-model-query-examples.md)|  
|Clustermodelle|[Miningmodellinhalt von Entscheidungsstrukturmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Beispiele für Clusteringmodellabfragen](../../analysis-services/data-mining/clustering-model-query-examples.md)|  
|Entscheidungsstrukturmodell|[Miningmodellinhalt von Entscheidungsstrukturmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Beispiele für Entscheidungsstruktur-Modellabfragen](../../analysis-services/data-mining/decision-trees-model-query-examples.md)|  
|Lineare Regressionsmodelle|[Miningmodellinhalt von linearen Regressionsmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[Beispiele für lineare Regressionsmodellabfrage](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Logistische Regressionsmodelle|[Miningmodellinhalt von logistischen Regressionsmodellen &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)|[Beispiele für lineare Regressionsmodellabfrage](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Naïve Bayes-Modelle|[Miningmodellinhalt von Naive Bayes-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Beispiele für Naive Bayes-Modellabfrage](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)|  
|Neuronale Netzwerkmodelle|[Miningmodellinhalt von neuronalen Netzwerkmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[Neuronale Beispiele für Netzwerkmodellabfragen](../../analysis-services/data-mining/neural-network-model-query-examples.md)|  
|Sequenzclustering|[Miningmodellinhalt von Sequence Clustering-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)|[Sequenzclusteringmodellabfragebeispiele](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)|  
|Zeitreihenmodelle|[Miningmodellinhalt von Zeitreihenmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[Abfragebeispiel Zeitreihenmodell](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> Miningmodellinhalt-Anzeigetools  
 Wenn Sie ein Modell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]durchsuchen möchten, können Sie die Informationen im **Microsoft Generic Content Tree Viewer**anzeigen. Dieser ist sowohl in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] als auch in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verfügbar.  
  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Viewer zeigt die Spalten, Regeln, Eigenschaften, Attribute, Knoten sowie andere Inhalte des Modells an, indem er auf die Informationen im Inhalts-Schemarowset des Miningmodells zurückgreift. Das Schemarowset für den Inhalt ist ein allgemeines Framework zum Darstellen detaillierter Informationen über den Inhalt eines Data Mining-Modells. Sie können Modellinhalt in jedem Client anzeigen, der hierarchische Rowsets unterstützt. Der Viewer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] stellt diese Informationen in einem HTML-Tabellen-Viewer dar, der alle Modelle in einem einheitlichen Format anzeigt, sodass Sie die Struktur der Modelle, die Sie erstellen, leichter nachvollziehen können. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
##  <a name="bkmk_Querying"></a> Miningmodellinhalt-Abfragetools  
 Um Mining-Modellinhalt abzurufen, müssen Sie eine Abfrage für das Data Mining-Modell erstellen.  
  
 Die einfachste Möglichkeit, eine Inhaltsabfrage zu erstellen, ist, die folgende DMX-Anweisung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auszuführen:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Weitere Informationen finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md).  
  
 Sie können auch mithilfe der Data Mining-Schemarowsets Data Mining-Modellinhalte abfragen. Ein Schemarowset ist eine Standardstruktur, mit deren Hilfe Clients Informationen über Mining-Strukturen und Modelle ermitteln, durchsuchen und abfragen können. Sie können die Schemarowsets mit XMLA-, Transact-SQL- oder DMX-Anweisungen abfragen.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie außerdem auf die Informationen in den Data Mining-Schemarowsets zugreifen, indem Sie eine Verbindung zur [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz herstellen und die Systemtabellen abfragen. Weitere Informationen finden Sie unter [Data Mining Schema Rowsets &#40;SSAS&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  

