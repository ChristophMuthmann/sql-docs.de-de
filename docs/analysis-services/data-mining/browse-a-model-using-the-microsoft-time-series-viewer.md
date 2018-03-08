---
title: Durchsuchen eines Modells mit dem Microsoft Time Series-Viewer | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- data mining [Analysis Services], continuous columns
- mining model content, viewing
- Microsoft Time Series Viewer
- charts [Analysis Services]
- Time Series Viewer [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6eaa320911fbba0f46472750bde9293b36430b46
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>Durchsuchen eines Modells mit Microsoft Time Series-Viewer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Viewer in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zeigt Miningmodelle an, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Algorithmus erstellt wurden. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Algorithmus ist ein Regressionsalgorithmus, der Data Mining-Modellen zur Vorhersage von kontinuierlichen Spalten, wie z. B. Umsatzzahlen, in Forecastingszenarien erstellt. Diese Zeitreihenmodelle können Informationen auf der Grundlage verschiedener Algorithmen enthalten:  
  
-   Dem ARTxp-Algorithmus, der für die kurzfristige Vorhersage optimiert ist  
  
-   Dem ARIMA-Algorithmus, der für die langfristige Vorhersage optimiert ist  
  
-   Einer Mischung aus ARTxp- und ARIMA-Algorithmus  
  
 Weitere Informationen zu diesen Algorithmen finden Sie unter [Microsoft Time Series Algorithm](../../analysis-services/data-mining/microsoft-time-series-algorithm.md) und [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
> [!NOTE]  
>  Wenn Sie detaillierte Informationen über die im Modell verwendeten Formeln und die entdeckten Muster sehen möchten, verwenden Sie den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree-Viewer. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) oder [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Viewer-Registerkarten  
 Wenn Sie ein Miningmodell in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]durchsuchen, wird das Modell im Data Mining-Designer auf der Registerkarte **Miningmodell-Viewer** mit dem jeweils geeigneten Viewer für das Modell angezeigt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series-Viewer enthält die folgenden Registerkarten:  
  
-   [Model](#BKMK_Tree)  
  
-   [Diagramme](#BKMK_Charts)  
  
 **Hinweis** Die für den Modellinhalt und in der Mininglegende angezeigten Informationen hängen von dem Algorithmus ab, den das Modell verwendet. Die Registerkarten **Modell** und **Diagramme** bleiben jedoch unabhängig von der Algorithmusmischung unverändert.  
  
###  <a name="BKMK_Tree"></a> Model  
 Wenn Sie ein Zeitreihenmodell erstellen, stellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das abgeschlossene Modell als Baumstruktur dar. Wenn die Daten mehrere Fallreihen enthalten, erstellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine separate Baumstruktur für jede Reihe. Beispiel: Sie erstellen Umsatzprognosen für die Regionen Pazifik, Nordamerika und Europa. Die Vorhersagen für jede dieser Regionen sind Fallreihen. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt eine separate Struktur für jede von dieser Reihe. Zum Anzeigen einer bestimmten Reihe wählen Sie die Reihe aus der Liste **Struktur** aus.  
  
 Das Zeitreihenmodell enthält für jede Struktur den Knoten **Alle** und wird dann in eine Reihe von Knoten unterteilt, die periodische Strukturen darstellen, die vom Algorithmus erkannt wurden. Sie können auf jeden Knoten klicken, um Statistiken anzuzeigen, z. B. die Anzahl der Fälle und die Gleichung.  
  
 Wenn Sie das Modell nur mit ARTxp erstellt haben, enthält die **Mininglegende** für den Stammknoten nur die Gesamtanzahl der Fälle. Für alle anderen Knoten enthält die **Mininglegende** ausführlichere Informationen über die Strukturaufteilung: Beispielsweise wird die Gleichung für den Knoten und die Anzahl von Fällen angezeigt. Die *Regel* in der Legende enthält Informationen, die die Reihe identifizieren, und die Zeitscheibe, für die die Regel gilt. Der Legendentext `M200 Europe Amount -2` gibt an, dass der Knoten das Modell für die Datenreihe M200 Europe zu einem Zeitpunkt zwei Zeitscheiben zuvor darstellt.  
  
 Wenn Sie das Modell nur mit ARIMA erstellt haben, enthält die Registerkarte **Modell** einen einzigen Knoten mit der Beschriftung **Alle**. Die **Mininglegende** für den Stammknoten enthält die ARIMA-Gleichung.  
  
 Wenn Sie ein gemischtes Modell erstellt haben, enthält der Stammknoten nur die Anzahl der Fälle und die ARIMA-Gleichung. Nach dem Stammknoten wird die Struktur in separate Knoten für jede periodische Struktur unterteilt. Für alle anderen Knoten enthält die Mininglegende für den Stammknoten den ARTxp- und den ARIMA-Algorithmus, die Gleichung für den Knoten und die Anzahl der Fälle im Knoten. Die ARTxp-Gleichung wird zuerst aufgelistet und wird als Strukturknotengleichung beschriftet. Darauf folgt die ARIMA-Gleichung. Weitere Informationen zum Interpretieren dieser Informationen finden Sie unter [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
 Im Allgemeinen zeigt das Entscheidungsstrukturdiagramm die wichtigste Teilung, den Knoten **Alle** , links vom Viewer an. In Entscheidungsstrukturen ist die Teilung nach dem Knoten **Alle** die wichtigste Teilung, da sie die Bedingung enthält, die die Fälle in den Trainingsdaten mit der stärksten Gewichtung teilt. In einem Zeitreihenmodell gibt die Hauptverzweigung den wahrscheinlichsten saisonbedingten Zyklus an. Teilungen nach dem Knoten **Alle** werden auf der rechten Seite der Verzweigung angezeigt.  
  
 Sie können einzelne Knoten in der Struktur erweitern oder reduzieren, um die nach jedem Knoten vorkommenden Teilungen anzuzeigen bzw. auszublenden. Sie können auch mithilfe der Optionen auf der Registerkarte **Entscheidungsstruktur** Einfluss darauf nehmen, wie die Struktur angezeigt wird. Mit dem Schieberegler **Ebene anzeigen** wird die Anzahl von in der Struktur gezeigten Ebenen angepasst. Verwenden Sie die Option **Standarderweiterung** , um die Standardzahl der für alle Strukturen im Modell angezeigten Ebenen festzulegen.  
  
 Die Schattierung der Hintergrundfarbe der einzelnen Knoten weist auf die Anzahl der Fälle hin, die im jeweiligen Knoten vorhanden sind. Die genaue Anzahl von Fällen in einem Knoten können Sie feststellen, indem Sie den Mauszeiger auf den Knoten richten, um einen InfoTipp zu dem Knoten anzuzeigen.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> Diagramme  
 Die Registerkarte **Diagramme** zeigt ein Diagramm an, in dem das Verhalten des vorhergesagten Attributs im Lauf der Zeit sowie fünf vorhergesagte zukünftige Werte dargestellt sind. Die vertikale Achse des Diagramms stellt die Werte der Zeitreihe dar, und die horizontale Achse stellt die Zeit dar.  
  
> [!NOTE]  
>  Die Zeitscheiben auf der Zeitachse richten sich nach den in den Daten verwendeten Einheiten: Sie können Tage, Monate oder auch Sekunden darstellen.  
  
 Mithilfe der Schaltfläche **ABS** können Sie zwischen absoluten und relativen Kurven hin- und herschalten. Falls Ihr Diagramm mehrere Modelle enthält, kann sich die Skalierung der Daten jedes einzelnen Modells erheblich unterscheiden. Wenn Sie eine absolute Kurve verwenden, kann ein Modell als flache Linie angezeigt werden, wohingegen ein anderes Modell erhebliche Änderungen aufweist. Dies ist der Fall, da die Skalierung eines Modells größer ist als die Skalierung des anderen Modells. Durch den Wechsel zu einer relativen Kurve ändern Sie den Maßstab so, dass der Änderungsprozentsatz anstelle absoluter Werte angezeigt wird. Dies vereinfacht den Vergleich von Modellen, die auf verschiedenen Maßstäben basieren.  
  
 Wenn das Miningmodell mehrere Zeitreihen enthält, können Sie eine oder mehrere Reihen für die Anzeige im Diagramm auswählen. Klicken Sie auf die Liste auf der rechten Seite des Viewers, und wählen Sie die gewünschte Reihe aus der Liste aus. Wenn das Diagramm zu komplex wird, können Sie die angezeigten Reihen filtern, indem Sie die Kontrollkästchen für die Reihen in der Legende aktivieren oder deaktivieren.  
  
 Im Diagramm werden Vergangenheits- und Zukunftsdaten angezeigt. Die Zukunftsdaten sind schattiert dargestellt, um sie von den Vergangenheitsdaten abzugrenzen. Die Datenwerte werden für Vergangenheitsdaten als durchgezogene Linien und für Vorhersagen als gepunktete Linien angezeigt. Sie können die Farbe der Linien ändern, die für die jeweiligen Serien verwendet werden, indem Sie die entsprechenden Eigenschaften in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]festlegen. Weitere Informationen finden Sie unter [Ändern der im Data Mining-Viewer verwendeten Farben](../../analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md).  
  
 Den anzuzeigenden Zeitbereich können Sie mithilfe der Zoomoptionen anpassen. Sie können auch einen bestimmten Zeitbereich anzeigen, indem Sie auf das Diagramm klicken, eine Zeitauswahl über das Diagramm ziehen und dann durch erneutes Klicken den ausgewählten Bereich vergrößern.  
  
 Mithilfe von **Vorhersageschritte** können Sie auswählen, wie viele zukünftige **Zeitschritte**Sie in dem Modell anzeigen möchten. Mit dem Kontrollkästchen **Abweichungen anzeigen** werden Fehlerbalken hinzugefügt, denen Sie entnehmen können, wie genau der vorhergesagte Wert ist.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodell-Viewer miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft Time Series-Algorithmus](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Datamining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
