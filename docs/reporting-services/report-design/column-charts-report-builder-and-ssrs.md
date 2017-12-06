---
title: "Säulendiagramme (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7f962314d1c4b4c3c3c342c668979081d8c7305c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="column-charts-report-builder-and-ssrs"></a>Säulendiagramme (Berichts-Generator und SSRS)
  Ein Säulendiagramm zeigt eine Reihe als Satz vertikaler Balken an, die nach Kategorie gruppiert sind. Säulendiagramme sind nützlich, um Datenänderungen über einen bestimmten Zeitraum anzuzeigen oder Vergleiche zwischen Elementen zu veranschaulichen. Das einfache Säulendiagramm ist eng mit dem Balkendiagramm und dem Säulenbereichsdiagramm verbunden. Das Balkendiagramm zeigt Reihen als Sätze horizontaler Balken an, während das Bereichssäulendiagramm Reihen als Sätze vertikaler Balken mit verschiedenen Anfangs- und Endpunkten darstellt. Weitere Informationen finden Sie unter [Balkendiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md) und [Bereichsdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md).  
  
 Das Säulendiagramm ist für diese Daten ausgezeichnet geeignet, da alle drei Reihen einen gemeinsamen Zeitraum verwenden und so zuverlässige Vergleiche vorgenommen werden können.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>Variationen eines Säulendiagramms  
  
-   **Gestapelt**. Ein Säulendiagramm, in dem mehrere Reihen vertikal gestapelt werden. Wenn nur eine Reihe im Diagramm vorhanden ist, wird das gestapelte Säulendiagramm angezeigt wie ein Säulendiagramm.  
  
-   **Prozentual gestapelt**. Ein Säulendiagramm, in dem mehrere Reihen vertikal gestapelt sind, um auf 100 % der Diagrammfläche zu passen. Wenn nur eine Reihe im Diagramm vorhanden ist, werden alle Säulenbalken so angepasst, dass sie 100 % der Diagrammfläche ausfüllen.  
  
-   **3D gruppiert**. Ein Säulendiagramm, das in einem 3D-Diagramm einzelne Reihen in separaten Zeilen anzeigt.  
  
-   **3D-Zylinder**. Ein Säulendiagramm, dessen Balken wie Zylinder in einem 3D-Diagramm gestaltet sind.  
  
-   **Histogramm**. Ein Säulendiagramm, das das Diagramm berechnet, damit seine Balken in einer Normalverteilung angeordnet werden.  
  
-   **Pareto**. Ein Säulendiagramm, dessen Balken von der höchsten zur niedrigsten Instanz angeordnet werden.  
  
## <a name="data-considerations-for-a-column-chart"></a>Überlegungen zu Daten für ein Säulendiagramm  
  
-   Balken- und Säulendiagramme werden häufig verwendet, um Vergleiche zwischen Gruppen anzuzeigen. Wenn mehr als drei Reihen im Diagramm vorhanden sind, bietet sich eher ein gestapeltes Balken- oder Säulendiagramm an. Außerdem können Sie gestapelte Balken- oder Säulendiagramme in mehrere Gruppen zusammenfassen, wenn mehrere Reihen im Diagramm vorhanden sind. Weitere Informationen finden Sie unter [Balkendiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md).  
  
-   In einem Säulendiagramm haben Sie weniger Platz, um Kategorieachsenbezeichnungen horizontal anzuzeigen. Bei längeren Kategoriebezeichnungen sollten Sie erwägen, ein Balkendiagramm zu verwenden oder den Drehwinkel für die Bezeichnung zu ändern.  
  
-   Sie können den einzelnen Balken eines Säulendiagramms besondere Zeichnungsarten hinzufügen, um die visuelle Wirkung zu erhöhen. Zeichnungsarten schließen Keil, Prägen, Zylinder und Helligkeitsabstufungen ein. Diese Effekte sollen die Darstellung des 2D-Diagramms verbessern. Bei Verwendung eines 3D-Diagramms werden die Zeichnungsarten zwar ebenfalls übernommen, sie haben jedoch möglicherweise nicht den gleichen Effekt. Weitere Informationen zum Hinzufügen einer Zeichnungsart zu einem Diagramm finden Sie unter [Hinzufügen einer Abschrägung, Prägung und Struktur zu einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
-   Säulendiagramme besitzen die einzigartige Fähigkeit, ein Diagramm als Histogramm oder Paretodiagramm anzuzeigen. Legen Sie hierfür im Eigenschaftenfenster unter der ShowColumnAs-Eigenschaft für **Histogram** oder **Pareto** auf **TRUE**fest.  
  
## <a name="see-also"></a>Siehe auch  
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Diagrammtypen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Balkendiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Bereichsdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)   
 [Tutorial: Hinzufügen eines Balkendiagramms zu einem Bericht (Berichts-Generator)](../../reporting-services/tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [Leere und NULL-Datenpunkte in Diagrammen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
