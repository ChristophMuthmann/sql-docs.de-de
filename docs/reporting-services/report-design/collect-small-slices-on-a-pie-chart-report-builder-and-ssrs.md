---
title: Zusammenfassen von kleinen Slices in einem Kreisdiagramm (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9d9e756aff5d5363c934d7916c8cfad3e28691ce
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>Zusammenfassen von kleinen Slices in einem Kreisdiagramm (Berichts-Generator und SSRS)
Kreisdiagramme mit zu vielen Slices können unübersichtlich wirken. Erfahren Sie, wie Sie in einem paginierten Bericht von [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] viele kleine Slices zu einem einzigen Slice in einem Kreisdiagramm zusammenfassen.
 
 Wenn Sie kleinere Slices zu einem einzelnen Slice zusammenfassen möchten, müssen Sie zuerst entscheiden, ob der Schwellenwert für das Zusammenfassen kleiner Slices als Prozentanteil des Kreisdiagramms oder als fester Wert gemessen werden soll. 
 
 Im [Tutorial: Hinzufügen eines Kreisdiagramms zu einem Bericht (Berichts-Generator)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) wird das Zusammenfassen von kleinen Slices zu einem einzigen Slice ausführlich erläutert, falls Sie dies zunächst anhand von Beispieldaten ausprobieren möchten.
 
 ![report-builder-pie-chart-other-slice](../../reporting-services/report-design/media/report-builder-pie-chart-other-slice.png)
  
 Sie können kleinere Slices auch zu einem zweiten Kreisdiagramm zusammenfassen, das aus einem zusammengefassten Slice des ersten Kreisdiagramms gebildet wird. Das zweite Kreisdiagramm wird rechts vom ursprünglichen Kreisdiagramm dargestellt.  
  
 Slices von Trichter- oder Pyramidendiagrammen können nicht zu einem Slice zusammengefasst werden.  
  
 
## <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>So fassen Sie kleinere Slices zu einem einzelnen Slice in einem Kreisdiagramm zusammen  
  
1.  Öffnen Sie den Bereich Eigenschaften.  
  
2.  Klicken Sie auf der Entwurfsoberfläche auf ein Segment des Kreisdiagramms. Die Eigenschaften für die Reihe werden im Bereich "Eigenschaften" angezeigt.  
  
3.  Erweitern Sie im Abschnitt **Allgemein** den Knoten **CustomAttributes** .  
  
4.  Legen Sie die Eigenschaft CollectedStyle auf **SingleSlice**fest.  

    ![Berichts-Generator-Kreisdiagramm-einzelne-Slice-Eigenschaft](../../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
  
5.  Legen Sie den Schwellenwert für die Zusammenfassung und den Typ des Schwellenwerts fest. Die folgenden Beispiele zeigen häufig verwendete Methoden zum Festlegen der Schwellenwerte für die Zusammenfassung.  
  
    -   **Nach Prozentanteil.** So fassen Sie beispielsweise in einem Kreisdiagramm Slices zusammen, die weniger als 10 % darstellen:  
  
         Legen Sie die Eigenschaft CollectedThresholdUsePercent auf **True**fest.  
  
         Legen Sie die Eigenschaft CollectedThreshold auf **10**fest.  
  
        > [!NOTE]  
        >  Wenn Sie CollectedStyle auf **SingleSlice**, CollectedThreshold auf einen Wert größer als **100** und CollectedThresholdUsePercent auf **TRUE** festlegen, wird eine Ausnahme ausgelöst, weil das Diagramm keinen Prozentwert berechnen kann. Legen Sie CollectedThreshold zur Behebung dieses Problems auf einen Wert kleiner als **100** fest.  
  
    -   **Nach Datenwert.** So fassen Sie beispielsweise in einem Kreisdiagramm Slices zusammen, die weniger als 5000 darstellen:  
  
         Legen Sie die Eigenschaft CollectedThresholdUsePercent auf **False**fest.  
  
         Legen Sie die Eigenschaft CollectedThreshold auf **5000**fest.  
  
6.  Legen Sie die Eigenschaft CollectedLabel auf eine Zeichenfolge fest, die als Beschriftung für das zusammengefasste Segment angezeigt werden soll.  
  
7.  (Optional) Legen Sie die Eigenschaften CollectedSliceExploded, CollectedColor, CollectedLegendText und CollectedToolTip fest. Diese Eigenschaften ändern die Darstellung, die Farbe, den Bezeichnungstext, den Legendentext und die QuickInfo des zusammengefassten Slice.  
  
## <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>So fassen Sie kleinere Slices zu einem sekundären Legendenkreisdiagramm zusammen  
  
1.  Führen Sie die Schritte 1-3 von oben aus.  
  
2.  Legen Sie die Eigenschaft CollectedStyle auf **CollectedPie**fest.  
  
3.  Legen Sie die Eigenschaft CollectedThresholdproperty auf den Wert fest, der als Schwellenwert für die Zusammenfassung kleinerer Segmente zu einem einzelnen Segment verwendet werden soll. Wenn die Eigenschaft CollectedStyle auf **CollectedPie**festgelegt ist, wird die Eigenschaft CollectedThresholdUsePercentproperty immer auf **True**festgelegt, und der Schwellenwert für die Zusammenfassung wird stets in Prozent gemessen.  
  
4.  (Optional) Legen Sie die Eigenschaften CollectedColor, CollectedLabel, CollectedLegendText und CollectedToolTip fest. Alle anderen Eigenschaften mit der Bezeichnung "Collected" gelten nicht für den zusammengefassten Slice in einem Kreisdiagramm.  
  
> [!NOTE]  
>  Das sekundäre Kreisdiagramm wird auf der Grundlage der kleinen Slices in Ihren Daten berechnet, sodass es nur in der Vorschau angezeigt wird. Es wird nicht auf der Entwurfsoberfläche angezeigt.  
  
> [!NOTE]  
>  Sie können das sekundäre Kreisdiagramm nicht formatieren. Aus diesem Grund wird dringend empfohlen, beim Zusammenfassen von Slices in einem Kreisdiagramm die erste Methode zu verwenden.  
  
## <a name="see-also"></a>Siehe auch  
* [Tutorial: Add a Pie Chart to Your Report (Report Builder) (Tutorial: Hinzufügen eines Kreisdiagramms zu einem Bericht (Berichts-Generator))](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Kreisdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Formatieren von Datenpunkten in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
*  [Anzeigen von Datenpunktbezeichnungen außerhalb eines Kreisdiagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
*  [Anzeigen von Prozentwerten in einem Kreisdiagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)     
  
