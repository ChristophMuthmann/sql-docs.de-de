---
title: "3D, Abschrägungen und andere Effekte in einem Diagramm (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f6d149a116c243fba0587afe1dcf969f9356c57f
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="chart-effects---3d-bevel-and-other-report-builder"></a>Diagrammeffekte - 3D, Abschrägungen und andere (Berichts-Generator)
  Dreidimensionale (3D-)Effekte können verwendet werden, um Tiefe zu vermitteln und dem Diagramm in Ihren paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichten eine optische Wirkung zu verleihen. Wenn Sie beispielsweise in einem explodierten Kreisdiagramm ein bestimmtes Segment des Kreises hervorheben möchten, können Sie die Perspektive des Diagramms so drehen und ändern, dass den Benutzern dieses Segment zuerst ins Auge fällt. Wenn 3D-Effekte auf das Diagramm angewendet werden, werden der Farbverlauf und alle Schraffurstile deaktiviert.  
  
 Dreidimensionale Effekte können auf einzelne Diagramme angewendet werden. In einem Bericht können sowohl zwei- als auch dreidimensionale Diagramme angezeigt werden.  
  
 Für alle Diagrammtypen können Sie in einer Diagrammfläche des Dialogfelds **Diagrammflächeneigenschaften** dreidimensionale Effekte hinzufügen, indem Sie die Option **3D aktivieren**auswählen. Weitere Informationen finden Sie unter [Hinzufügen von 3D-Effekten zu einem Diagramm &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md).  
  
 Eine andere Möglichkeit, Diagrammen visuelle Effekte hinzuzufügen, ist das Hinzufügen von Balken-, Säulen-, Ring- und Kreisdiagrammen Abschrägungen, Prägungen und Strukturarten. Weitere Informationen finden Sie unter [Hinzufügen einer Abschrägung, Prägung und Struktur zu einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>Koordinatenbasierte dreidimensionale Diagramme  
 Bei koordinatenbasierten Diagrammtypen (Säulen-, Balken-, Flächen-, Punkt-, Linien- und Bereichsdiagramme) wird das Diagramm durch dreidimensionale Effekte mit einer dritten Achse, der so genannten "Z-Achse", angezeigt. Die Einführung dieser dritten Achse ermöglicht es Ihnen, eine Vielzahl visueller Verbesserungen auf das Diagramm anzuwenden.  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>Ändern der Leerstellen in einem 3D-Diagramm  
 Beim Darstellen einer Diagrammfläche im dreidimensionalen Modus wird jede Reihe in einer separaten Zeile entlang der Z-Achse des Diagramms angezeigt. Um den Abstand zwischen den einzelnen Reihen zu ändern, ändern Sie den Punktzwischenraum im Diagramm. Geben Sie dazu einen anderen Wert für die Eigenschaft **Punktzwischenraum** im Dialogfeld 3D-Effekte ein.  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>Ändern der Projektion eines 3D-Diagramms  
 Es gibt zwei Arten von 3D-Projektionen: "Schräg" und "Perspektive". Mit einer schrägen Projektion wird einem zweidimensionalen Diagramm eine Tiefendimension hinzugefügt. Die Z-Achse wird gleichwinklig zu den horizontalen und vertikalen Achsen gezeichnet, die wie in einem zweidimensionalen Diagramm senkrecht zueinander stehen.  
  
 Bei der perspektivischen Projektion wird das Diagramm durch Schätzen einer Sichtebene transformiert, indem das Diagramm neu gezeichnet wird, als würde es von diesem Punkt aus betrachtet. Der Wert **Drehung** verlagert die Sicht vertikal von der "Bodenebene" bei 0 auf eine höhere Ebene bei 90. Der Wert **Neigung** verlagert den Betrachtungswinkel nach links oder rechts. Der Wert 0 entspricht einer zweidimensionalen Sicht des Diagramms. Der Wert **Perspektive** definiert den Prozentsatz der Verzerrung, der beim Anzeigen der Projektion verwendet wird. Bei dieser Projektion werden die Proportionen des Diagramms beibehalten, die Darstellung des Diagramms wird jedoch verzerrt. Daher ist es äußerst effizient, einen niedrigen Wert für die Perspektive zu verwenden.  
  
> [!NOTE]  
>  Die schrägen und perspektivischen Projektionen sind separate Projektionstypen und können daher nicht zusammen im gleichen Diagramm verwendet werden.  
  
### <a name="clustering-data"></a>Clustering-Daten  
 In 2D-Diagrammen werden mehrere Datenreihen nebeneinander angezeigt. Beim Clustering werden einzelne Reihen in separaten Zeilen eines 3D-Diagramms dargestellt. Bei einem Diagramm, das beispielsweise drei Reihen Datenpunkte enthält, wird durch Clustering jede der drei Reihen in einer separaten Zeile entlang der Z-Achse angezeigt. Standardmäßig werden alle in 3D angezeigten Diagrammtypen durch Clustering gruppiert.  
  
 Clustering kann für Balken- und Säulendiagramme deaktiviert werden. Wenn Clustering deaktiviert ist, werden mehrere Balken- und Säulenreihen nebeneinander in einer Zeile angezeigt.  
  
## <a name="shape-based-three-dimensional-charts"></a>Formbasierte dreidimensionale Diagramme  
 Für formbasierte Diagrammtypen (Kreis-, Ring-, Trichter-, Pyramidendiagramme) stehen weniger dreidimensionale Effekte zur Verfügung. Wenn Sie mit formbasierten Diagrammtypen arbeiten, können Sie nur die Drehungs- und Neigungswerte ändern.  
  
## <a name="rotations"></a>Drehungen  
 Diagramme können horizontal und vertikal von -90 bis +90 Grad gedreht werden. Mit einem positiven horizontalen Winkel wird das Diagramm gegen den Uhrzeigersinn um die X-Achse gedreht, während ein positiver vertikaler Winkel das Diagramm im Uhrzeigersinn um die Y-Achse dreht.  
  
## <a name="highlighting-3d-effects"></a>Hervorheben von 3D-Effekten  
 Sie können einem dreidimensionalen Diagramm über die **Schattierung** -Eigenschaft Hervorhebungen hinzufügen. Die Eigenschaft wird bei Auswahl einer Diagrammfläche im Fenster Eigenschaften unter Area3DStyle angezeigt. Mit einer einfachen Hervorhebung wird der gleiche Farbton für die Diagrammflächenelemente übernommen. Mit einer realistischen Hervorhebung werden die Farbtöne der Diagrammflächenelemente abhängig von einem angegebenen Beleuchtungswinkel geändert.  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Achsenbezeichnungen in einem Diagramm &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatieren eines Diagramms &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Hinzufügen von 3D-Effekten zu einem Diagramm &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/chart-effects-add-3d-effects-report-builder.md)  
  
  
