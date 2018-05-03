---
title: Durchsuchen eines Modells mit dem Microsoft Naive Bayes-Viewer | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1e501269dfea1c72416236f750f451122b36dc40
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Durchsuchen eines Modells mit dem Microsoft Naive Bayes-Viewer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für naives Bayes-Verfahren in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zeigt Miningmodelle an, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes-Algorithmus erstellt wurden. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Algorithmus für das naive Bayes-Verfahren ist ein Klassifizierungsalgorithmus, der sehr gut an Modellierungsaufgaben für Vorhersagen angepasst werden kann. Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md).  
  
 Da der Hauptverwendungszweck eines naiven Bayes-Modells darin besteht, eine Möglichkeit zum schnellen Durchsuchen von Daten in einem Dataset bereitzustellen, verfügt der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für naives Bayes-Verfahren über verschiedene Methoden, die Interaktion zwischen vorhersagbaren Attributen und Eingabeattributen anzuzeigen.  
  
> [!NOTE]  
>  Wenn Sie detaillierte Informationen über die im Modell verwendeten Formeln und die entdeckten Muster anzeigen möchten, können Sie zum [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree-Viewer wechseln. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) oder [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Viewer-Registerkarten  
 Wenn Sie ein Miningmodell in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]durchsuchen, wird das Modell im Data Mining-Designer auf der Registerkarte **Miningmodell-Viewer** mit dem jeweils geeigneten Viewer für das Modell angezeigt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Viewer für naives Bayes-Verfahren stellt zum Durchsuchen der Daten folgende Registerkarten bereit:  
  
-   [Abhängigkeitsnetzwerk](#BKMK_Dependency)  
  
-   [Attributprofile](#BKMK_Profiles)  
  
-   [Attributmerkmale](#BKMK_Characteristics)  
  
-   [Attributunterscheidung](#BKMK_Discrimination)  
  
##  <a name="BKMK_Dependency"></a> Abhängigkeitsnetzwerk  
 Die Registerkarte **Abhängigkeitsnetzwerk** zeigt die Abhängigkeiten zwischen den Eingabeattributen und den vorhersagbaren Attributen in einem Modell an. Der Schieberegler auf der linken Seite des Viewers fungiert als Filter, der an die Stärken der Abhängigkeiten gebunden ist. Wenn Sie den Schieberegler nach unten ziehen, werden nur die stärksten Links angezeigt.  
  
 Wenn Sie einen Knoten auswählen, hebt der Viewer die Abhängigkeiten hervor, die knotenspezifisch sind. Wenn Sie beispielsweise einen vorhersagbaren Knoten auswählen, wird vom Viewer auch jeder Knoten hervorgehoben, der beim Vorhersagen des vorhersagbaren Knotens hilft.  
  
 Die Legende im unteren Bereich des Viewers verknüpft Farbcodes mit dem Abhängigkeitstyp im Diagramm. Wenn Sie einen vorhersagbaren Knoten auswählen, wird dieser z. B. türkis schattiert, und die Knoten, die den ausgewählten Knoten vorhersagen, orange.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Profiles"></a> Attributprofile  
 Die Registerkarte **Attributprofile** zeigt Histogramme in einem Raster an. Sie können dieses Raster verwenden, um die vorhersagbaren Attribute, die Sie im Feld **Vorhersagbar** auswählen, mit den anderen Attributen zu vergleichen, die im Modell enthalten sind. Jede Spalte in der Tabelle stellt einen Status des vorhersagbaren Attributs dar. Wenn das vorhersagbare Attribut viele Status hat, können Sie die Anzahl der Status verändern, die im Histogramm angezeigt werden, indem Sie die Option **Histogrammbalken**anpassen. Wenn die Anzahl, die Sie auswählen, kleiner ist als die Gesamtzahl von Status im Attribut, werden die Status nach Unterstützung sortiert, wobei die restlichen Status in einem einzigen grauen Bucket gesammelt werden.  
  
 Um eine Mininglegende anzuzeigen, die die Farben des Histogramms den Statuswerten eines Attributs zuordnet, aktivieren Sie das Kontrollkästchen **Legende anzeigen** . Die Mininglegende zeigt auch die Verteilung von Fällen für jedes Attribut/Wert-Paar an, das Sie auswählen.  
  
 Klicken Sie mit der rechten Maustaste auf die Registerkarte **Attributprofile** , und wählen Sie **Kopieren**aus, um die Inhalte des Rasters als HTML-Tabelle in die Zwischenablage zu kopieren.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Characteristics"></a> Attributmerkmale  
 Um die Registerkarte **Attributmerkmale** zu verwenden, wählen Sie aus der Liste **Attribut** ein vorhersagbares Attribut aus, und wählen Sie anschließend aus der Liste **Wert** einen Status des ausgewählten Attributs aus. Wenn Sie diese Variablen festlegen, zeigt die Registerkarte **Attributmerkmale** die Status der Attribute an, die mit dem ausgewählten Fall des ausgewählten Attributs verknüpft sind. Die Attribute sind nach ihrer Wichtigkeit sortiert.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Discrimination"></a> Attributunterscheidung  
 Wählen Sie zum Verwenden der Registerkarte **Attributunterscheidung** ein vorhersagbares Attribut und zwei ihrer Status aus den Listen **Attribut**, **Wert 1**und **Wert 2** aus. Das Raster auf der Registerkarte **Attributunterscheidung** zeigt daraufhin die folgenden Informationen in Spalten an:  
  
 **Attribut**  
 Listet weitere Attribute im Dataset auf, die einen Status enthalten, der den Status eines vorhersagbaren Attributs stark bevorzugt.  
  
 **Werte**  
 Zeigt den Wert des Attributs in der Spalte **Attribute** an.  
  
 **Begünstigt \<Wert 1 >**  
 Zeigt eine farbige Leiste an, die kennzeichnet, wie stark der Attributwert den in **Wert 1**dargestellten vorhersagbaren Attributwert bevorzugt.  
  
 **Begünstigt \<Wert 2 >**  
 Zeigt eine farbige Leiste an, die kennzeichnet, wie stark der Attributwert den in **Wert 2**dargestellten vorhersagbaren Attributwert bevorzugt.  
  
 [Zurück zum Anfang](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Naive Bayes-Algorithmus](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Miningmodell-Viewer miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Datamining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Datamining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
