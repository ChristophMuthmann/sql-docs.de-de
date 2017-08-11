---
title: Formdiagramme (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b8404c1-aa89-4350-8bd6-203bc0446ee4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84ee7a9030bb27725994a33860b26b8754034cd9
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="shape-charts-report-builder-and-ssrs"></a>Formdiagramme (Berichts-Generator und SSRS)
  Ein Formdiagramm zeigt Wertdaten als Prozentsatz des Ganzen an. Formdiagramme werden üblicherweise zum Anzeigen proportionaler Vergleiche zwischen verschiedenen Werten in einem Satz verwendet. Kategorien werden durch einzelne Segmente der Form dargestellt. Die Größe des Segments wird durch den Wert bestimmt. Formdiagramme werden ähnlich verwendet wie Kreisdiagramme, außer dass die Kategorien von der größten zur kleinsten angeordnet werden.  
  
 Ein Trichterdiagramm zeigt Werte als progressiv abnehmende Verhältnisse an. Die Größe eines Bereichs wird durch den Reihenwert als Prozentsatz der Summe aller Werte bestimmt. Beispielsweise lassen sich in einem Trichterdiagramm Websitebesuchertrends darstellen. Das Trichterdiagramm zeigt meist einen großen Bereich ganz oben an, der die Besuche der Startseite angibt. Die anderen Bereiche werden proportional kleiner. Weitere Informationen zu Hinzufügen von Daten zu einem Trichterdiagramm finden Sie unter [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 Die folgende Abbildung zeigt ein Beispiel für ein Trichterdiagramm.  
  
 ![Trichterdiagramm](../../reporting-services/report-design/media/rs-funnelchart.gif "Trichterdiagramm")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variationen  
  
-   **Pyramide**. Ein Pyramidendiagramm zeigt proportionale Daten in Form einer Pyramide an.  
  
## <a name="data-considerations-for-shape-charts"></a>Überlegungen zu Daten für ein Formdiagramm  
  
-   Formdiagramme sind wegen ihrer visuellen Wirkung in Berichten beliebt. Bei Formdiagrammen handelt es sich jedoch um einen sehr vereinfachten Diagrammtyp, der Ihre Daten möglicherweise nicht optimal darstellt. Verwenden Sie ein Formdiagramm ggf. erst, nachdem die Daten zu sieben Datenpunkten oder weniger aggregiert wurden. Mit dem Formdiagramm sollte im Allgemeinen nur eine Kategorie pro Datenbereich angezeigt werden.  
  
-   Formdiagramme zeigen jede Datengruppe als separates Segment im Diagramm an. Sie müssen mindestens ein Datenfeld und ein Kategoriefeld hinzufügen. Wenn dem Formdiagramm mehr als ein Datenfeld hinzugefügt wird, werden beide Datenfelder im selben Diagramm angezeigt.  
  
-   Formdiagramme eignen sich sehr gut, um proportionale Prozentwerte in sortierter Reihenfolge anzuzeigen. Um die Konsistenz zu wahren, werden die Werte im Dataset jedoch standardmäßig nicht sortiert. Es bietet sich an, die Werte vom höchsten zum niedrigsten Wert zu sortieren, um die Daten möglichst exakt als Trichter oder Pyramide darzustellen. Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
-   NULL-, leere und negative Werte haben keine Auswirkungen auf die Berechnung von Verhältnissen. Aus diesem Grund werden diese Werte nicht in einem Formdiagramm angezeigt. Wenn Sie diese Werte in Ihrem Diagramm visuell darstellen möchten, ändern Sie den Diagrammtyp. Weitere Informationen zum Hinzufügen von leeren Punkte zu einem nicht-Formdiagramm finden Sie unter [Hinzufügen von leeren Punkten zum Diagramm &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md).  
  
-   Wenn Sie mithilfe einer benutzerdefinierten Palette eigene Farben in einem Formdiagramm definieren, müssen in der Palette genügend Farben vorhanden sein, damit jeder Datenpunkt mit einer eigenen Farbe hervorgehoben werden kann. Weitere Informationen finden Sie unter [Formatieren von Reihenfarben in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   Im Gegensatz zu allen anderen Diagrammtypen zeigt ein Formdiagramm einzelne Datenpunkte und keine einzelnen Reihen in der Legende an.  
  
-   Einstellungen für die Wert- und Kategorieachse werden bei Trichterdiagrammen ignoriert. Wenn mehrere Kategorien- oder Reihengruppen vorhanden sind, werden die Gruppenbezeichnungen in der Diagrammlegende angezeigt.  
  
-   Formdiagrammtypen können nicht mit anderen Diagrammtypen im gleichen Diagrammbereich kombiniert werden. Wenn Sie Vergleiche zwischen Daten in einem Formdiagramm und Daten in einem anderen Diagrammtyp anzeigen möchten, müssen Sie einen zweiten Diagrammbereich hinzufügen.  
  
-   Sie können zusätzliche Zeichnungsarten für Kreis- und Ringdiagramme verwenden, um die visuelle Wirkung zu erhöhen. Finden Sie unter [Formatieren von Reihenfarben in einem Diagramm &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md) für Weitere Informationen.  
  
## <a name="see-also"></a>Siehe auch  
 [Diagramme &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatieren eines Diagramms &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Leere und Null-Datenpunkte in Diagrammen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Kreisdiagramme &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
