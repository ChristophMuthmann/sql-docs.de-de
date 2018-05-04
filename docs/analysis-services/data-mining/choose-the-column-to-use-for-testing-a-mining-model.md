---
title: Wählen Sie die Spalte zum Testen eines Miningmodells zu verwendenden | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 30896ea2f3dd1ec8fbb7f07087552e17612ed3ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>Auswählen der zum Testen eines Miningmodells zu verwendenden Spalte
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Bevor Sie die Genauigkeit eines Miningmodells messen können, müssen Sie sich entscheiden, welches Ergebnis Sie bewerten möchten. Bei den meisten Data Mining-Modellen müssen Sie mindestens eine Spalte auswählen, die als vorhersagbares Attribut verwendet werden soll, wenn Sie das Modell erstellen. Wenn Sie die Genauigkeit des Modells testen, müssen Sie daher im Allgemeinen dieses Attribut zum Testen auswählen.  
  
 In der folgenden Liste werden einige weitere Überlegungen zum Auswählen des vorhersagbaren Attributs, das in Tests verwendet werden soll, beschrieben:  
  
-   Einige Data Mining-Modelle können mehrere Attribute vorhersagen – beispielsweise neuronale Netzwerke, die die Beziehungen zwischen vielen Attributen untersuchen können.  
  
-   Andere Typen von Miningmodellen – beispielsweise Clustermodelle – verfügen nicht immer über ein vorhersagbares Attribut. Clustermodelle können nicht getestet werden, außer wenn sie über ein vorhersagbares Attribut verfügen.  
  
-   Sie müssen als Ergebnis ein kontinuierliches vorhersagbares Attribut auswählen, um ein Punktdiagramm zu erstellen oder die Genauigkeit eines Regressionsmodells zu messen. In diesem Fall können Sie keinen Zielwert angeben. Wenn Sie etwas anderes als ein Punktdiagramm erstellen, muss die zugrunde liegende Miningstrukturspalte auch einen Inhaltstyp von **Diskret** oder **Diskretisiert**haben.  
  
-   Wenn Sie ein diskretes Attribut als vorhersagbares Ergebnis auswählen, können Sie auch einen Zielwert angeben, oder Sie können das Feld **Wert vorhersagen** leer lassen. Wenn Sie **Wert vorhersagen**einschließen, wird vom Diagramm nur die Effektivität des Modells bei der Vorhersage des Zielwerts gemessen. Wenn Sie kein Zielergebnis angeben, wird das Modell in Bezug auf seine Genauigkeit gemessen, alle Ergebnisse vorherzusagen.  
  
-   Wenn Sie mehrere Modelle einschließen und sie in einem einzelnen Genauigkeitsdiagramm vergleichen möchten, müssen alle Modelle die gleiche vorhersagbare Spalte verwenden.  
  
-   Beim Erstellen eines Kreuzvalidierungsberichts werden alle Modelle von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] automatisch analysiert, die dasselbe vorhersagbare Attribut haben.  
  
-   Wenn die Option **Vorhersagespalten und -werte synchronisieren**ausgewählt wird, werden von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] automatisch vorhersagbare Spalten ausgewählt, die über die gleichen Namen und übereinstimmenden Datentypen verfügen. Wenn die Spalten diese Kriterien nicht erfüllen, können Sie diese Option deaktivieren und manuell eine vorhersagbare Spalte auswählen. Dies ist möglicherweise erforderlich, wenn Sie das Modell mit einem externen Dataset testen, das andere Spalten enthält als das Modell. Wenn Sie jedoch eine Spalte mit dem falschen Datentyp auswählen, werden entweder ein Fehler bzw. falsche Ergebnisse angezeigt.  
  
### <a name="specify-the-outcome-to-predict"></a>Bestimmen des vorhersagbaren Ergebnisses  
  
1.  Doppelklicken Sie auf die Miningstruktur, um sie in Data Mining-Designer zu öffnen.  
  
2.  Klicken Sie auf die Registerkarte **Mininggenauigkeitsdiagramm** .  
  
3.  Klicken Sie auf die Registerkarte **Eingabeauswahl** .  
  
4.  Klicken Sie auf der Registerkarte **Eingabeauswahl** unter **Name der vorhersagbaren Spalte**auf eine vorhersagbare Spalte für jedes Modell, das Sie im Diagramm einbeziehen.  
  
     Im Feld **Name der vorhersagbaren Spalte** werden nur die Miningmodellspalten aufgelistet, für die als Verwendungstyp **Vorhersagen** oder **Nur vorhersagen**festgelegt wurde.  
  
5.  Wenn Sie den Liftwert für ein Modell bestimmen möchten, müssen Sie einen bestimmten zu messenden Ergebniswert auswählen, indem Sie ihn aus der Liste **Wert vorhersagen** auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen und Zuordnen von Modelltestdaten](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Wählen Sie eine Genauigkeit Diagrammtyp und einen Satz Diagrammoptionen](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
