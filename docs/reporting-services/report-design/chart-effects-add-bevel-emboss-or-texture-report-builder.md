---
title: "Hinzufügen einer Abschrägung, eines Reliefs und von Texturstilen zu einem Diagramm (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
caps.latest.revision: "6"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e476980a27d2eeb6502836067726ffadc551587c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="chart-effects---add-bevel-emboss-or-texture-report-builder"></a>Diagrammeffekte: Hinzufügen einer Abschrägung, eines Relief oder von Texturstilen (Berichts-Generator)
  Bei bestimmten Diagrammtypen können Sie einen Zeichnungseffekt angeben, um die visuelle Wirkung des Diagramms zu erhöhen. Diese Zeichnungseffekte werden nur für die Reihen des Diagramms übernommen. Sie haben keine Auswirkungen auf andere Diagrammelemente.  
  
 Wenn Sie eine Variante eines Kreis- oder Ringdiagramms verwenden, können Sie einen weichen Rand oder eine konkave Zeichnungsart angeben ähnlich wie Abschrägungs- oder Prägungseffekte für ein Bild.  
  
 Bei Verwendung einer Variante eines Balken- oder Säulendiagramms können Sie Strukturarten wie Zylinder, Keil und Helligkeitsabstufungen auf einzelne Balken oder Säulen anwenden.  
  
 Zusätzlich zu diesen Zeichnungsarten können vielen Diagrammelementen Rahmen und Schatten hinzugefügt werden, um eine Illusion von Tiefe zu vermitteln. Weitere Informationen zu anderen Möglichkeiten, das Diagramm zu formatieren, finden Sie unter [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>So fügen Sie Abschrägungs- und Prägungseffekte zu einem Kreis- oder Ringdiagramm hinzu  
  
1.  Wählen Sie auf der Registerkarte **Ansicht** die Option **Eigenschaften** aus, um den Eigenschaftenbereich zu öffnen.  
  
2.  Wählen Sie das Kreis- oder Ringdiagramm aus, das Sie optimieren möchten. Wählen Sie ein Datenfeld im Diagramm aus und nicht das gesamte Diagramm.  
  
3.  Erweitern Sie im Bereich Eigenschaften den Knoten **CustomAttributes** .  
  
4.  Wählen Sie für PieDrawingStyle eine Art aus der Dropdownliste aus.  
  
> [!NOTE]  
>  Sie können 3D nicht mit Abschrägungen oder Prägungen im selben Diagramm verwenden. Wenn Sie für das Diagramm 3D aktiviert haben, wird die PieDrawingStyle-Eigenschaft nicht angezeigt.  
  
 ![Kreisdiagramm mit konkaver Zeichnungsart](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "Pie chart with concave drawing style")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>So fügen Sie einem Balken- oder Säulendiagramm Strukturarten hinzu  
  
1.  Wählen Sie das Balken- oder Säulendiagramm aus, das Sie optimieren möchten. Wählen Sie ein Datenfeld im Diagramm aus und nicht das gesamte Diagramm.  
  
2.  Öffnen Sie den Bereich Eigenschaften.  
  
3.  Erweitern Sie den Knoten **CustomAttributes** .  
  
4.  Wählen Sie für DrawingStyle eine Art aus der Dropdownliste aus.  
  
> [!NOTE]  
>  Sie können 3D nicht mit Abschrägungen oder Prägungen im selben Diagramm verwenden. Wenn Sie für das Diagramm 3D aktiviert haben, wird die PieDrawingStyle-Eigenschaft nicht angezeigt.  
  
 ![Balkendiagramm mit LightToDark-Zeichnungseffekt](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "Bar chart with LightToDark drawing effect")  
  
## <a name="see-also"></a>Siehe auch  
 [Balkendiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Säulendiagramme (Berichts-Generator und SSRS)](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [Kreisdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
