---
title: Durchsuchen eines Modells mit dem Microsoft Struktur-Viewer | Microsoft Docs
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
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 61e3be434f2029216742813178b041b083174362
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>Durchsuchen eines Modells mit dem Microsoft Struktur-Viewer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Struktur-Viewer in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zeigt Entscheidungsbäume an, die mithilfe des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus erstellt werden. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus ist ein hybrider Entscheidungsstrukturalgorithmus, der sowohl Klassifizierung als auch Regression unterstützt. Deshalb können Sie auch diesen Viewer verwenden, um Modelle auf Grundlage des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression-Algorithmus anzuzeigen. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees-Algorithmus wird für vorhersagende Modellierung sowohl diskreter als auch fortlaufender Attribute verwendet. Weitere Informationen zu diesem Algorithmus finden Sie unter [Microsoft Decision Trees Algorithm](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md).  
  
> [!NOTE]  
>  Wenn Sie detaillierte Informationen über die im Modell verwendeten Formeln und die entdeckten Muster sehen möchten, verwenden Sie den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree-Viewer. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) oder [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_TabsPanes"></a> Viewer-Registerkarten  
 Wenn Sie ein Miningmodell in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]durchsuchen, wird das Modell im Data Mining-Designer auf der Registerkarte **Miningmodell-Viewer** mit dem jeweils geeigneten Viewer für das Modell angezeigt. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Struktur-Viewer umfasst die folgenden Registerkarten und Bereiche:  
  
-   [Entscheidungsstruktur](#BKMK_DecisionTree)  
  
-   [Abhängigkeitsnetzwerk](#BKMK_DependencyNetwork)  
  
-   [Mininglegende](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a> Entscheidungsstruktur  
 Wenn Sie ein Entscheidungsbaummodell erstellen, erstellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine separate Struktur für jedes vorhersagbare Attribut. Sie können eine individuelle Struktur anzeigen, indem Sie sie im Viewer auf der Registerkarte **Entscheidungsstruktur** in der Liste **Struktur** auswählen.  
  
 Eine Entscheidungsstruktur setzt sich aus einer Reihe von Teilungen zusammen, wobei sich die vom Algorithmus als am wichtigsten bestimmte Teilung links vom Viewer im Knoten **Alle** befindet. Weitere Unterteilungen befinden sich rechts davon. Die Aufteilung im Knoten **Alle** ist außerordentlich wichtig, da sie die stärkste Bedingung für die Teilungsursache im Datensatz darstellt und daher die erste Teilung verursacht hat.  
  
 Sie können einzelne Knoten in der Struktur erweitern oder reduzieren, um die nach jedem Knoten vorkommenden Teilungen anzuzeigen bzw. auszublenden. Sie können auch mithilfe der Optionen auf der Registerkarte **Entscheidungsstruktur** Einfluss darauf nehmen, wie die Struktur angezeigt wird. Mit dem Schieberegler **Ebene anzeigen** wird die Anzahl von in der Struktur gezeigten Ebenen angepasst. Verwenden Sie die Option **Standarderweiterung** , um die Standardzahl der für alle Strukturen im Modell angezeigten Ebenen festzulegen.  
  
#### <a name="predicting-discrete-attributes"></a>Vorhersagen von diskreten Attributen  
 Wenn eine Struktur mit einem diskreten vorhersagbaren Attribut erstellt wird, zeigt der Viewer auf jedem Knoten in der Struktur Folgendes an:  
  
-   Die Bedingung, die die Teilung verursacht hat.  
  
-   Ein Histogramm, das die Verteilung der Zustände der vorhersagbaren Attribute nach Verwendungshäufigkeit sortiert darstellt.  
  
 Sie können die Option **Histogramm** verwenden, um die Zahl der Status zu ändern, die im Histogramm der Struktur angezeigt werden. Dies ist sinnvoll, wenn die vorhersagbaren Attribute viele Status haben. Die Status werden in einem Histogramm in der Reihenfolge Ihrer Verwendungshäufigkeit von links nach rechts angezeigt. Wenn die Zahl der Status, die Sie auswählen, niedriger ist als die Gesamtzahl der Status im Attribut, werden die Status, die am seltensten verwendet werden, kollektiv in Grau anzeigt. Halten Sie zur Anzeige der genauen Zahl jedes Status eines Knoten den Zeiger über den Knoten, um einen InfoTipp anzuzeigen, oder wählen Sie den Knoten aus, um in der **Mininglegende**seine Details anzuzeigen.  
  
 Die Hintergrundfarbe jedes Knotens stellt die Konzentration von Fällen des speziellen Attributstatus dar, den Sie über die Option **Hintergrund** auswählen. Sie können diese Option verwenden, um Knoten zu markieren, die ein spezielles Ziel enthalten, das Sie interessiert.  
  
#### <a name="predicting-continuous-attributes"></a>Vorhersagen von kontinuierlichen Attributen  
 Wenn eine Struktur mithilfe eines kontinuierlichen Attributs erstellt ist, zeigt der Viewer für jeden Knoten in der Struktur ein Rautendiagramm statt eines Histogramms an. Das Rautendiagramm verfügt über eine Zeile, die den Bereich des Attributs darstellt. Die Raute befindet sich in der Mitte des Knotens. Die Breite der Raute gibt die Varianz des Attributs an diesem Knoten an. Eine schlankere Raute gibt an, dass der Knoten eine genauere Vorhersage erstellen kann. Der Viewer zeigt auch die Regressionsgleichung an, mit der die Teilung im Knoten festgelegt wird.  
  
#### <a name="additional-decision-tree-display-options"></a>Weitere Anzeigeoptionen der Entscheidungsstruktur  
 Wenn Drillthrough für das Entscheidungsstrukturmodell aktiviert ist, können Sie auf die Trainingsfälle zugreifen, die einen Knoten unterstützen, indem Sie mit der rechten Maustaste auf den Knoten in der Struktur klicken und **Drillthrough**auswählen. Sie können Drillthrough im Data Mining-Assistenten aktivieren, oder indem Sie auf dem Miningmodell auf der Registerkarte **Miningmodelle** die Drillthrough-Eigenschaft anpassen.  
  
 Sie können die Zoomoptionen verwenden, die sich auf der Registerkarte **Entscheidungsstruktur** befinden, um eine Struktur zu vergrößern oder zu verkleinern, oder **An Bildschirmgröße anpassen** verwenden, um das Modell dem Viewer-Bildschirm anzupassen. Wenn eine Struktur zu groß ist, um auf den Bildschirm zu passen, können Sie die Option **Navigation**verwenden, um durch die Struktur zu navigieren. Wenn Sie auf **Navigation** klicken, wird ein separates Navigationsfenster geöffnet, mit dem Sie Abschnitte des Modells auswählen und anzeigen können.  
  
 Sie können auch das Bild der Strukturansicht in die Zwischenablage kopieren, sodass sie es in Dokumente oder Bildbearbeitungsprogramme einfügen können. Verwenden Sie **Diagrammsicht kopieren** , um nur den Abschnitt der Struktur zu kopieren, die im Viewer angezeigt wird, oder verwenden Sie **Gesamtes Diagramm kopieren** , um alle erweiterten Knoten in der Struktur zu kopieren.  
  
 [Zurück zum Anfang](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a> Abhängigkeitsnetzwerk  
 Das **Abhängigkeitsnetzwerk** zeigt die Abhängigkeiten zwischen den Eingabeattributen und den vorhersagbaren Attributen im Modell an. Der Schieberegler auf der linken Seite des Viewers fungiert als Filter, der an die Stärken der Abhängigkeiten gebunden ist. Wenn Sie den Schieberegler nach unten verschieben, werden nur die stärksten Links im Viewer angezeigt.  
  
 Wenn Sie einen Knoten auswählen, hebt der Viewer die Abhängigkeiten hervor, die knotenspezifisch sind. Wenn Sie beispielsweise einen vorhersagbaren Knoten auswählen, wird vom Viewer auch jeder Knoten hervorgehoben, der beim Vorhersagen des vorhersagbaren Knotens hilft.  
  
 Wenn der Viewer zahlreiche Knoten enthält, können Sie mithilfe der Schaltfläche **Knoten finden** nach bestimmten Knoten suchen. Durch Klicken auf **Knoten finden** wird das Dialogfeld **Knoten finden** geöffnet, in dem Sie mit einem Filter nach bestimmten Knoten suchen und diese auswählen können.  
  
 Die Legende im unteren Bereich des Viewers verknüpft Farbcodes mit dem Abhängigkeitstyp im Diagramm. Wenn Sie einen vorhersagbaren Knoten auswählen, wird dieser z. B. türkis schattiert, und die Knoten, die den ausgewählten Knoten vorhersagen, orange.  
  
 [Zurück zum Anfang](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a> Mininglegende  
 In der **Mininglegende** werden folgende Informationen angezeigt, wenn Sie einen Knoten im Entscheidungsstrukturmodell auswählen:  
  
-   Die Zahl der Fälle im Knoten, unterteilt nach den Status der vorhersagbaren Attribute.  
  
-   Die Wahrscheinlichkeit jedes Falls des vorhersagbaren Attributs für den Knoten.  
  
-   Ein Histogramm, das die Zahl jedes Status für das vorhersagbare Attribut enthält.  
  
-   Die Bedingungen, die erforderlich sind, um einen speziellen Knoten zu erreichen, auch als *Knotenpfad*bezeichnet.  
  
-   Das lineare Regressionsmodell für die Regressionsformel.  
  
 Sie können mit der **Mininglegende** wie im Projektmappen-Explorer andocken und arbeiten.  
  
 [Zurück zum Anfang](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Decision Trees-Algorithmus](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Miningmodell-Viewern &#40; Datamining-Modell-Designer &#41;](http://msdn.microsoft.com/library/4ba391d5-c97b-4848-ba7c-7d096fa4b7dd)   
 [Miningmodell-Viewer miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Datamining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Datamining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
