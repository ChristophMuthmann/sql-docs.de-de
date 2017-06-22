---
title: "Hinzufügen einer Abschrägung, Prägung und Struktur zu einem Diagramm (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2081d22c9e0aefd82cda5dff97b8ece503fdd9b0
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="chart-effects---add-bevel-emboss-or-texture-report-builder"></a>Diagrammeffekte - Hinzufügen einer Abschrägung, Prägung, oder der Textur (Berichts-Generator)
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
  
 ![Kreisdiagramm mit konkaver Zeichnungsart](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "Kreisdiagramm mit konkaver Zeichnungsart")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>So fügen Sie einem Balken- oder Säulendiagramm Strukturarten hinzu  
  
1.  Wählen Sie das Balken- oder Säulendiagramm aus, das Sie optimieren möchten. Wählen Sie ein Datenfeld im Diagramm aus und nicht das gesamte Diagramm.  
  
2.  Öffnen Sie den Bereich Eigenschaften.  
  
3.  Erweitern Sie den Knoten **CustomAttributes** .  
  
4.  Wählen Sie für DrawingStyle eine Art aus der Dropdownliste aus.  
  
> [!NOTE]  
>  Sie können 3D nicht mit Abschrägungen oder Prägungen im selben Diagramm verwenden. Wenn Sie für das Diagramm 3D aktiviert haben, wird die PieDrawingStyle-Eigenschaft nicht angezeigt.  
  
 ![Balkendiagramm mit LightToDark-Zeichnungseffekt](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "Balkendiagramm mit LightToDark-Zeichnungseffekt")  
  
## <a name="see-also"></a>Siehe auch  
 [Balkendiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Säulendiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [Kreisdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
