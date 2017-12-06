---
title: Formatieren von Datenpunkten in einem Diagramm (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
f1_keywords:
- "10248"
- sql13.rtp.rptdesigner.serieslabelproperties.general.f1
ms.assetid: 08ec3818-f63a-4e89-b52c-750e47f48b85
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ef5d6f5c0abbe09505de7608ec18d309a112d0c9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="formatting-data-points-on-a-chart-report-builder-and-ssrs"></a>Formatieren von Datenpunkten in einem Diagramm (Berichts-Generator und SSRS)
In einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht stellt ein Datenpunkt die kleinste Entität im Diagramm dar. In Nicht-Formdiagrammen werden Datenpunkte entsprechend dem Diagrammtyp dargestellt. Eine Linienreihe besteht beispielsweise aus einem oder mehreren verbundenen Datenpunkten. In Formdiagrammen werden Datenpunkte durch einzelne Slices oder Segmente dargestellt, aus denen sich das gesamte Diagramm zusammensetzt. In einem Kreisdiagramm ist z. B. jedes Teil ein Datenpunkt. Weitere Informationen finden Sie unter [Diagrammtypen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md).  
  
 Ein oder mehrere Datenpunkte bilden eine Reihe. Standardmäßig werden alle Formatierungsoptionen für sämtliche Datenpunkte in der Reihe übernommen. Wenn Sie Eigenschaften für einzelne Datenpunkte angeben möchten, können Sie ein Feld oder einen Ausdruck in der Reihe angeben, mit dem zur Laufzeit einzelne Datenpunkte auf der Grundlage des Datasets formatiert werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-tooltips-and-drillthrough-actions-to-data-points"></a>Hinzufügen von QuickInfos und Drillthroughaktionen zu Datenpunkten  
 Sie können den einzelnen Datenpunkten QuickInfos hinzufügen, indem Sie den Wert der **ToolTip** -Eigenschaft für die Reihe festlegen. Wenn Sie QuickInfos anzeigen, ermöglichen Sie Benutzern das Anzeigen von Informationen zum Datenpunkt, beispielsweise des Gruppennamens, des Werts des Datenpunkts und des Prozentsatzes des Datenpunktes in Bezug auf die Gesamtreihe. Weitere Informationen finden Sie unter [Anzeigen von QuickInfos für eine Reihe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
 Sie können auch eine Drillthroughaktion für Datenpunkte in der Reihe angeben, um einen anderen Bericht oder eine URL anzuzeigen. Sie können Parameter übergeben, um Informationen zum Datenpunkt anzuzeigen, auf den geklickt wurde. Weitere Informationen finden Sie unter [Hinzufügen einer Drillthroughaktion für einen Bericht (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
## <a name="highlighting-individual-data-points-in-a-series"></a>Hervorheben von einzelnen Datenpunkten in einer Reihe  
 In einem Nicht-Formdiagramm können Sie einzelne Datenpunkte hervorheben, indem Sie einen Ausdruck für die Eigenschaft „Color“ angeben. Wenn Sie beispielsweise den höchsten Datenpunktwert in einer Reihe mit dem Namen `MyField` mit einer anderen Farbe hervorheben möchten, geben Sie einen Ausdruck wie den Folgenden an:  
  
 `=Iif(Fields!MyField.Value >= Max(Fields!MyField.Value, "MyDataSet"), "Red", "Green")`  
  
 In diesem Beispiel wird dem höchsten Wert für `MyField` die Farbe Rot zugewiesen, während alle anderen Datenpunkten in der Farbe Grün angezeigt werden. Wenn Sie mithilfe der **Fill** -Eigenschaft der Reihe eine Farbe für die Reihe angeben, werden im Diagramm die in der Palette angegebenen Farben überschrieben. Weitere Informationen finden Sie unter [Formatieren von Reihenfarben in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="positioning-data-point-labels-on-a-chart"></a>Positionieren von Datenpunktbezeichnungen in einem Diagramm  
 In allen Diagrammtypen können Sie Datenpunktbezeichnungen anzeigen, indem Sie mit der rechten Maustaste auf das Diagramm klicken und die Option **Datenbezeichnungen anzeigen**auswählen. Die Position der Datenpunktbezeichnungen wird entsprechend dem Diagrammtyp angegeben:  
  
-   In einem Balkendiagramm können Sie die Datenpunktbezeichnung mithilfe des benutzerdefinierten **BarLabelStyle** -Attributs neu positionieren. Es gibt vier mögliche Positionen: Außen, Links, Zentriert und Rechts. Wenn Sie die Balkenbezeichnungsart auf Außen festlegen, werden die Bezeichnungen außerhalb des Balkens platziert, sofern sie in den Diagrammbereich passen. Wenn die Bezeichnung nicht außerhalb des Balkens und im Diagrammbereich positioniert werden kann, wird sie im Balken positioniert.  
  
-   In einem Kreisdiagramm können Sie die Datenpunktbezeichnung mithilfe des benutzerdefinierten **PieLabelStyle** -Attributs neu positionieren. Beim Positionieren von Datenpunktbezeichnungen um ein Kreisdiagramm sind viele Aspekte zu berücksichtigen, u. a. die Größe des Kreisdiagramms, der verfügbare Platz zwischen dem Kreisdiagramm und der entsprechenden Legende sowie die Größe der Bezeichnungen. Weitere Informationen finden Sie unter [Anzeigen von Datenpunktbezeichnungen außerhalb eines Kreisdiagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md).  
  
-   In einem Pyramiden- oder Trichterdiagramm können Sie die Datenpunktbezeichnungen mithilfe des benutzerdefinierten **FunnelLabelStyle** -Attributs und des benutzerdefinierten **PyramidLabelStyle** -Attributs neu positionieren. Wenn Sie einen Pyramiden- oder Trichterdiagrammtyp ausgewählt haben, können Sie diese Attribute im Bereich **Eigenschaften** festlegen.  
  
-   In gestapelten Diagrammen werden Datenpunktbezeichnungen immer innerhalb der Reihe positioniert, und die **Position** -Eigenschaft für die Reihenbezeichnung wird ignoriert.  
  
-   In allen anderen Diagrammtypen können Sie die Datenpunktbezeichnung mithilfe der **Position** -Eigenschaft für die Reihenbezeichnung neu positionieren. Standardmäßig wird die Position von Datenpunktbezeichnungen automatisch vom Diagramm berechnet, um Bezeichnungskonflikte zu vermeiden. Wenn Sie einen Wert für **Position**festlegen, werden alle Datenpunktbezeichnungen auf dieselbe Weise positioniert, wodurch die Bezeichnungen einander überlappen können. Es empfiehlt sich, diesen Ansatz nur bei einer kleinen Anzahl von Datenpunkten zu verfolgen.  
  
 Weitere Informationen finden Sie unter [Positionieren von Bezeichnungen in einem Diagramm (Berichts-Generator und SSRS)](../../reporting-services/report-design/position-labels-in-a-chart-report-builder-and-ssrs.md).  
  
## <a name="adding-keywords-for-data-point-labels-tooltips-and-legend-text"></a>Hinzufügen von Schlüsselwörtern für Datenpunktbezeichnungen, QuickInfos und Legendentext  
 Sie können ein vorhandenes Element im Diagramm mithilfe von diagrammspezifischen Schlüsselwörtern darstellen, bei denen die Groß- und Kleinschreibung berücksichtigt wird. Diese Schlüsselwörter können nur auf Eigenschaften von QuickInfos, benutzerdefiniertem Legendentext und Datenpunktbezeichnungen angewendet werden. In vielen Fällen ist für ein Diagrammschlüsselwort ein entsprechender einfacher Ausdruck verfügbar, das Schlüsselwort kann jedoch schneller und einfacher eingegeben werden. Im Folgenden finden Sie eine Liste von Diagrammschlüsselwörtern.  
  
|Diagrammschlüsselwort|Description|Anwendbar auf Diagrammtyp|Beispiel für einen entsprechenden einfachen Ausdruck|  
|-------------------|-----------------|------------------------------|------------------------------------------------|  
|#VALY|Y-Wert des Datenpunkts|Alle|`=Fields!MyDataField.Value`|  
|#VALY2|Y-Wert Nr. 2 des Datenpunkts|Bereich, Blase|Keine|  
|#VALY3|Y-Wert Nr. 3 des Datenpunkts|Kurs, Kerze|Keine|  
|#VALY4|Y-Wert Nr. 4 des Datenpunkts|Kurs, Kerze|Keine|  
|#SERIESNAME|Reihenname|Alle|Keine|  
|#LABEL|Datenpunktbezeichnung|Alle|Keine|  
|#AXISLABEL|Achsenbezeichnung für Datenpunkt|Form|`=Fields!MyDataField.Value`|  
|#INDEX|Datenpunktindex|Alle|Keine|  
|#PERCENT|Prozentsatz für den Y-Wert des Datenpunkts|Alle|`=FormatPercent(Fields!MyDataField.Value/Sum(Fields!MyDataField.Value, "MyDataSet"),2)`|  
|#TOTAL|Summe aller Y-Werte in der Reihe|Alle|`=Sum(Fields!MyDataField.Value)`|  
|#LEGENDTEXT|Der Text, der dem Text des Legendenelements entspricht.|Alle|Keine|  
|#AVG|Durchschnitt aller Y-Werte in der Reihe|Alle|`=Avg(Fields!MyDataField.Value)`|  
|#MIN|Minimum aller Y-Werte in der Reihe|Alle|`=Min(Fields!MyDataField.Value)`|  
|#MAX|Maximum aller Y-Werte in der Reihe|Alle|`=Max(Fields!MyDataField.Value)`|  
|#FIRST|Der Erste aller Y-Werte in der Reihe|Alle|`=First(Fields!MyDataField.Value)`|  
  
 Schließen Sie zum Formatieren des Schlüsselworts eine [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Formatzeichenfolge in Klammern ein. Wenn Sie beispielsweise den Wert des Datenpunkts in einer QuickInfo als Zahl mit zwei Dezimalstellen anzeigen möchten, schließen Sie die Formatzeichenfolge „N2“ in geschweifte Klammern ein, z.B. „#VALY{N2}“ für die **ToolTip** -Eigenschaft der Reihe. Weitere Informationen zu [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Formatzeichenfolgen finden Sie auf MSDN unter [Formatierung von Typen](http://go.microsoft.com/fwlink/?LinkId=112024) . Weitere Informationen zum Formatieren von Zahlen in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [Formatieren von Zahlen und Datumsangaben (Berichts-Generator und SSRS)](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md).  
  
 Weitere Informationen zum Hinzufügen von Schlüsselwörtern zu einem Diagramm finden Sie unter [Anzeigen von QuickInfos für eine Reihe (Berichts-Generator und SSRS)](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md) und [Ändern des Texts eines Legendenelements (Berichts-Generator und SSRS)](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md).  
  
## <a name="increasing-readability-in-a-chart-with-multiple-data-points"></a>Verbessern der Lesbarkeit in einem Diagramm mit mehreren Datenpunkten  
 Wenn mehrere Reihen im Diagramm vorhanden sind, kann dieser Umstand die Lesbarkeit der Datenpunkte des Diagramms beeinträchtigen. Wenn Sie dem Diagramm mehrere Reihen hinzufügen, empfiehlt es sich, ein Verfahren anzuwenden, mit dem die einzelnen Reihen im Diagramm effektiv gelesen und erkannt werden. Weitere Informationen hierzu finden Sie unter [Mehrere Reihen in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md):  
  
 Zur Vereinfachung empfiehlt es sich, in Formdiagrammen nur ein Datenfeld und ein Kategoriefeld hinzuzufügen. Weitere Informationen finden Sie unter [Formdiagramme (Berichts-Generator und SSRS)](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md). Wenn für das Diagramm mehr als ein Datenfeld und Kategoriefeld erforderlich ist, sollten Sie den Diagrammtyp ändern. Sie können mit der rechten Maustaste auf die Reihe klicken und **Diagrammtyp ändern**auswählen.  
  
## <a name="inserting-data-point-markers"></a>Einfügen von Datenpunktmarkern  
 Ein Datenpunktmarker ist ein visueller Indikator, mit dem die einzelnen Datenpunkte in einer Reihe gekennzeichnet werden. In einem Punktdiagramm werden mit dem Marker Form und Größe der einzelnen Datenpunkte bestimmt. Die Größe des Markers wird durch den Diagrammtyp bestimmt. Sie können die Größe, die Farbe oder den Stil des Markers ändern. Marker sind für Bereichs- und Formdiagramme sowie für gestapelte Untertypen nicht verfügbar.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Anzeigen von QuickInfos für eine Reihe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [Anzeigen von Datenpunktbezeichnungen außerhalb eines Kreisdiagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)  
  
 [Anzeigen von Prozentwerten in einem Kreisdiagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatieren von Achsenbezeichnungen in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatieren von Achsenbezeichnungen als Datumsangabe oder Währung (Berichts-Generator und SSRS)](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Tutorial: Hinzufügen eines Kreisdiagramms zu einem Bericht (Berichts-Generator)](../../reporting-services/tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
