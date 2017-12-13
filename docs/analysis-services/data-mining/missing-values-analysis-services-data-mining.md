---
title: "Fehlende Werte (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
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
- attributes [data mining]
- MISSING_VALUE_SUBSTITUTION
- MissingValueSubstitution property
- MISSING_VALUE_SUBSTITUTION parameter
- null values [Analysis Services]
- coding [Data Mining]
ms.assetid: 2b34abdc-7ed4-4ec1-8780-052a704d6dbe
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9fd36d5de83b72fcc62945de61aa5f7b2d0cb3e2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="missing-values-analysis-services---data-mining"></a>Fehlende Werte (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Behandlung von *fehlende Werte* ist ein wichtiger Teil der effektiven Modellierung. In diesem Abschnitt wird erläutert, was fehlende Werte sind, und es werden die Funktionen beschrieben, die in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für die Arbeit mit fehlenden Werten bereitgestellt werden, wenn Sie Data Mining-Strukturen und Miningmodelle erstellen.  
  
## <a name="definition-of-missing-values-in-data-mining"></a>Definition fehlender Werte in Data Mining  
 Ein fehlender Wert kann Verschiedenes bedeuten. Vielleicht war das Feld nicht zutreffend, oder das Ereignis trat nicht ein, oder die Daten waren nicht verfügbar. Möglicherweise kannte die Person, die die Daten eingegeben hat, den richtigen Wert nicht, oder sie hat nicht darauf geachtet, dass alle Felder ausgefüllt sind.  
  
 Es gibt jedoch viele Data Mining-Szenarien, in denen fehlende Werte wichtige Informationen liefern. Die Bedeutung der fehlenden Werte hängt zum größten Teil vom Kontext ab. Ein fehlender Datumswert in einer Liste von Rechnungen hat z. B. eine ganz andere Bedeutung als ein fehlendes Datum in einer Spalte, die Auskunft über das Einstellungsdatum eines Mitarbeiters gibt. Im Allgemeinen werden fehlende Werte in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] als informativ angesehen und die Wahrscheinlichkeiten so angepasst, dass fehlende Werte in den Berechnungen berücksichtigt werden. Hierdurch lässt sich sicherstellen, dass die Modelle ausgewogen sind und vorhandenen Fällen darin nicht zu viel Gewicht beigemessen wird.  
  
 Daher stellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zwei sehr unterschiedliche Mechanismen zur Verwaltung und Berechnung fehlender Werte bereit. Durch die erste Methode wird die Handhabung von NULL-Werten auf der Ebene der Miningstruktur gesteuert. Die zweite Methode wird je nach Algorithmus unterschiedlich implementiert, legt aber im Allgemeinen fest, wie fehlende Werte in Modellen, die NULL-Werte zulassen, verarbeitet und gezählt werden.  
  
## <a name="specifying-handling-of-nulls"></a>Festlegen der Behandlung von NULL-Werten  
 In der Datenquelle könnte fehlende Werte auf unterschiedliche Weise dargestellt werden: als NULL-Werte, als leere Zellen in einem Arbeitsblatt, als Wert "N/V" oder sonstiger Code oder als ein künstlicher Wert wie 9999. Für das Data Mining werden jedoch nur NULL-Werte als fehlende Werte betrachtet. Wenn die Daten Platzhalterwerte anstatt von NULL-Werten enthalten, können sich diese auf die Ergebnisse des Modells auswirken. Sie sollten sie daher durch NULL-Werte ersetzen oder die richtigen Werte nach Möglichkeit ableiten. Es sind verschiedene Tools verfügbar, mit denen Sie geeignete Werte ableiten und eintragen können, z. B. die Suchtransformation oder der Datenprofilerstellungs-Task in SQL Server Integration Services (SSIS) oder das in den Data Mining-Add-Ins für Excel verfügbare Tool Aus Beispiel füllen.  
  
 Wenn für die modellierte Aufgabe gilt, dass in einer Spalte keine Werte fehlen dürfen, sollten Sie das **NOT_NULL** -Modellierungsflag beim Definieren der Miningstruktur auf die Spalte anwenden. Dieses Flag gibt an, dass die Verarbeitung fehlschlagen soll, wenn ein Fall nicht über einen geeigneten Wert verfügt. Falls während der Verarbeitung eines Modells dieser Fehler auftritt, können Sie ihn protokollieren und Maßnahmen einleiten, um die Daten zu korrigieren, die für das Modell verwendet werden.  
  
## <a name="calculation-of-the-missing-state"></a>Berechnen des Status "Missing"  
 Für den Data Mining-Algorithmus sind fehlende Werte informativ. In Falltabellen ist der Status **Missing** ebenso wie jeder andere Status zulässig. Darüber hinaus kann ein Data Mining-Modell mithilfe anderer Werte vorhersagen, ob ein Wert fehlt. Anders ausgedrückt: Die Tatsache, dass ein Wert fehlt, wird nicht als Fehler angesehen.  
  
 Während der Erstellung eines Miningmodells wird der Status **Missing** dem Modell automatisch für alle diskreten Spalten hinzugefügt. Wenn beispielsweise die Eingabespalte für [Geschlecht] die beiden möglichen Werte „Männlich“ und „Weiblich“ enthält, wird automatisch ein dritter Wert hinzugefügt, der den Wert **Nicht vorhanden** darstellt, und das Histogramm, das die Verteilung aller Werte der Spalte zeigt, beinhaltet stets die Anzahl der Fälle mit **Nicht vorhanden** -Werten. Wenn in der Spalte Geschlecht keine Werte fehlen, zeigt das Histogramm, dass der -Status in 0 Fällen vorkommt.  
  
 Das automatische Einfügen des Status **Missing** hat folgenden Sinn: Sie halten es für möglich, dass sich in den Daten nicht für alle möglichen Werte Beispiele finden und möchten nicht, dass das Modell die Möglichkeit ausschließt, nur weil die Daten kein Beispiel enthalten. Wenn die Umsatzdaten eines Ladens beispielsweise zeigen, dass alle Kunden, die ein bestimmtes Produkt kauften, zufällig Frauen waren, ist es nicht wünschenswert, ein Modell zu erstellen, das vorhersagt, dass nur Frauen das Produkt kaufen können. Stattdessen fügt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] einen Platzhalter namens **Nicht vorhanden**für den zusätzlichen unbekannten Wert hinzu, sodass andere mögliche Statuswerte berücksichtigt werden können.  
  
 Beispielsweise enthält die folgende Tabelle die Verteilung der Werte für den Knoten (Alle) des Entscheidungsstrukturmodells, das für das Bike Buyer-Lernprogramms erstellt wurde. In diesem Beispielszenario enthält die Spalte [Bike Buyer] das vorhersagbare Attribut, wobei 1 für "Ja" und 0 für "Nein" steht.  
  
|Wert|Fälle|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Missing|0|  
  
 Diese Verteilung zeigt, dass etwa eine Hälfte der Kunden ein Fahrrad gekauft hat und die andere Hälfte nicht. Dieses Dataset ist sehr sauber; daher ist für jeden Fall ein Wert in der Spalte [Bike Buyer] vorhanden, und die Anzahl der **Nicht vorhanden** -Werte ist 0. Wäre jedoch in einem Fall kein Wert im Feld [Bike Buyer] vorhanden, dann würde [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die betreffende Zeile als Fall mit einem **Nicht vorhanden** -Wert zählen.  
  
 Ist die Eingabe eine kontinuierliche Spalte, dann tabellarisiert das Modell zwei mögliche Zustände für das Attribut: **Existing** und **Missing**. Anders ausgedrückt: Entweder enthält die Spalte einen Wert eines numerischen Datentyps, oder sie enthält keinen Wert. Für die Fälle, in denen ein Wert gegeben ist, berechnet das Modell den Mittelwert, die Standardabweichung und andere aussagekräftige Statistiken. Für die Fälle, in denen kein Wert vorhanden ist, liefert das Modell die Anzahl der **Missing** -Werte und passt die Vorhersagen entsprechend an. Welche Methode zum Anpassen der Vorhersage eingesetzt wird, hängt vom Algorithmus ab und wird im folgenden Abschnitt beschrieben.  
  
> [!NOTE]  
>  Für Attribute in einer geschachtelten Tabelle sind fehlende Werte nicht informativ. Wenn ein Kunde beispielsweise kein Produkt gekauft hat, dann enthält die geschachtelte **Products** -Tabelle keine Zeile für das Produkt, und im Mining-Modell würde kein Attribut für das fehlende Produkt erstellt. Wenn Sie jedoch an den Kunden interessiert sind, die bestimmte Produkte nicht gekauft haben, können Sie ein Modell erstellen, das durch Verwendung einer NOT EXISTS-Anweisung im Modellfilter nach dem Nichtvorhandensein der Produkte in der geschachtelten Tabelle gefiltert wird. Weitere Informationen finden Sie unter [Anwenden eines Filters auf ein Miningmodell](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
## <a name="adjusting-probability-for-missing-states"></a>Anpassen der Wahrscheinlichkeit für den Status "Missing"  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zählt nicht nur die Werte, sondern berechnet auch die Wahrscheinlichkeit der einzelnen Werte im Dataset. Das gilt auch für den **Missing** -Wert. In der nachfolgenden Tabelle werden beispielsweise die Wahrscheinlichkeiten der Fälle aus dem vorigen Beispiel dargestellt:  
  
|Wert|Fälle|Probability|  
|-----------|-----------|-----------------|  
|0|9296|50.55%|  
|1|9098|49.42%|  
|Missing|0|0.03%|  
  
 Es mag seltsam erscheinen, dass für den **Missing** -Wert eine Wahrscheinlichkeit von 0,03 % berechnet wird, obwohl die Anzahl der Fälle gleich 0 ist. Dieses Verhalten ist jedoch beabsichtigt und stellt eine Anpassung dar, mit deren Hilfe das Modell unbekannte Werte handhaben kann.  
  
 Im Allgemeinen wird die Wahrscheinlichkeit berechnet, indem die Anzahl der positiven Fälle durch die Anzahl aller möglichen Fälle geteilt wird. In diesem Beispiel berechnet der Algorithmus die Summe der Fälle, die eine bestimmte Bedingung ([Bike Buyer] = 1 oder [Bike Buyer] = 0) erfüllen, und dividiert diese Zahl durch die Gesamtzahl der Zeilen. Damit den **Missing** -Fällen Rechnung getragen wird, wird der Anzahl aller möglichen Fälle 1 hinzugefügt. Infolgedessen ist die Wahrscheinlichkeit für unbekannte Fälle nicht mehr Null, sondern eine sehr kleine Zahl, die angibt, dass der Status nur unwahrscheinlich, aber nicht unmöglich ist.  
  
 Durch die Addition des kleinen **Missing** -Werts wird das Vorhersageergebnis nicht geändert. Es ermöglicht jedoch eine bessere Modellierung bei Szenarien, bei denen die Verlaufsdaten nicht alle möglichen Ergebnisse enthalten.  
  
> [!NOTE]  
>  Verschiedene Data Mining-Anbieter behandeln fehlende Werte unterschiedlich. Beispielsweise nehmen manche Anbieter an, dass es sich um eine effiziente Darstellung handelt, wenn in einer geschachtelten Spalte Werte fehlen. Fehlende Werte in einer nicht geschachtelten Spalte werden jedoch als Zufallsprodukt betrachtet.  
  
 Wenn Sie sicher sind, dass die Daten alle möglichen Ergebnisse darstellen, und eine Anpassung der Wahrscheinlichkeiten verhindern möchten, sollten Sie in der Miningstruktur für die Spalte das NOT_NULL-Modellierungsflag festlegen.  
  
> [!NOTE]  
>  Jeder Algorithmus, einschließlich benutzerdefinierter Algorithmen, die Sie möglicherweise von einem Drittanbieter-Plug-In erhalten, kann fehlende Werte unterschiedlich behandeln.  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>Besondere Behandlung von fehlenden Werten in Entscheidungsstrukturmodellen  
 Der Microsoft Decision Trees-Algorithmus berechnet die Wahrscheinlichkeiten für fehlende Werte anders als andere Algorithmen. Statt einfach 1 zur Gesamtzahl der Fälle zu addieren, passt der Decision Trees-Algorithmus mithilfe einer etwas anderen Formel die Wahrscheinlichkeit für den Status **Missing** an.  
  
 In einem Entscheidungsstrukturmodell wird die Wahrscheinlichkeit des Status **Missing** wie folgt berechnet:  
  
 StatusWahrscheinlichkeit = (KnotenVorherWahrscheinlichkeit) * (StatusUnterstützungswerte + 1)/(KnotenUnterstützungswerte + GesamtzahlStatuswerte)  
  
Der Decision Trees-Algorithmus bietet eine zusätzliche Anpassung des Algorithmus, der die Anwendung von Filtern für das Modell zu kompensieren durch die viele Statuswerte während des Trainings ausgeschlossen werden kann.  
  
 Wenn ein Statuswert während des Trainings vorhanden ist, aber an einem bestimmten Knoten über null (0) Unterstützungswerte verfügt, wird in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]die Standardanpassung vorgenommen. Wenn ein Statuswert während des Trainings jedoch nie auftritt, legt der Algorithmus die Wahrscheinlichkeit auf genau null (0) fest. Diese Anpassung gilt nicht nur für den Status **Missing** , sondern auch für andere Statuswerte, die in den Trainingsdaten vorhanden sind, infolge der Modellfilterung aber keine (0) Unterstützungswerte besitzen.  
  
 Aus dieser zusätzlichen Anpassung ergibt sich folgende Formel:  
  
 StateProbability = 0.0 wenn dieser Status über 0 Unterstützungswerte im Trainingssatz verfügt  
  
 ELSE StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStatesWithNonZeroSupport)  
  
 Im Endeffekt soll durch diese Anpassung die Stabilität der Struktur aufrechterhalten werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Die folgenden Themen stellen weitere Informationen zur Behandlung fehlender Werte bereit.  
  
|Aufgaben|Links|  
|-----------|-----------|  
|Hinzufügen von Flags zu einzelnen Modellspalten, um die Behandlung fehlender Werte zu steuern|[Anzeigen oder Ändern von Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Festlegen von Eigenschaften für ein Miningmodell, um die Behandlung fehlender Werte zu steuern|[Ändern der Eigenschaften eines Miningmodells](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)|  
|Informationen zum Angeben der Modellierungsflags in DMX|[Modellierungsflags &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|Ändern der Methode, die von der Miningstruktur zur Behandlung fehlender Werte verwendet wird|[Ändern der Eigenschaften einer Miningstruktur](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodellinhalt &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Modellierungsflags &#40;Data Mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
