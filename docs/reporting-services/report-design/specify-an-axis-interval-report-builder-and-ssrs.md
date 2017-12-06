---
title: Angeben eines Achsenintervalls (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/02/2016
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
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
caps.latest.revision: "14"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7cb249020f268163a449435c196bd3279d207b24
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>Angeben eines Achsenintervalls (Berichts-Generator und SSRS)
Erfahren Sie, wie Sie die Anzahl der Bezeichnungen und Teilstriche auf der Kategorieachse (X) in einem Diagramm ändern, indem Sie das Achsenintervalls in einem [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -paginierten Bericht festlegen.
 
Auf der Wertachse (in der Regel die Y-Achse) stellen die Achsenintervalle ein konsistentes Maß für die Datenpunkte im Diagramm bereit. 

Ein automatisches Achsenintervall führt auf der Kategorieachse (in der Regel die X-Achse) manchmal zu Kategorien ohne Achsenbezeichnungen. Sie können die Anzahl der Intervalle in der Interval-Eigenschaft der Achse festlegen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] berechnet die Anzahl der Intervalle zur Laufzeit basierend auf den Daten im Resultset. Weitere Informationen zum Berechnen von Achsenintervallen finden Sie unter [Formatieren von Achsenbezeichnungen in einem Diagramm](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  

Informationen zum Festlegen des Achsenintervalls mit Beispieldaten finden Sie unter [Tutorial: Hinzufügen eines Säulendiagramms zu einem Bericht](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md).
  
> [!NOTE]  
>  Die Kategorieachse ist normalerweise die horizontale Achse oder x-Achse. Bei Balkendiagrammen ist die Kategorieachse jedoch die vertikale Achse oder y-Achse.  
>
> Dieses Thema gilt nicht für:
>-   Datums- oder Zeitwerte auf der Kategorieachse. Standardmäßig werden **DateTime** -Werte als Tage angezeigt. Sie können ein anderes Datums- oder Zeitintervall angeben, z. B. ein Monats- oder Zeitintervall. Weitere Informationen finden Sie unter [Formatieren von Achsenbezeichnungen als Datumsangaben oder Währung](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md).  
>-  Kreis-, Ring-, Trichter- oder Pyramidendiagramme, die keine Achsen haben. 
  
## <a name="to-show-all-the-category-labels-on-the-x-axis"></a>So zeigen Sie alle Kategoriebezeichnungen auf der X-Achse an  

In diesem Säulendiagramm ist das horizontale Bezeichnungsintervall auf „Auto“ festgelegt.

![report-builder-column-chart-preview-x-axis-interval-auto](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-auto.png)
  
1.  Klicken Sie mit der rechten Maustaste auf die Kategorieachse, und klicken Sie anschließend auf **Eigenschaften für horizontale Achsen**.   

    ![report-builder-column-chart-x-axis-labels](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-labels.png)
  
2.  Legen Sie auf der Registerkarte **Achsenoptionen** im Dialogfeld **Eigenschaften für horizontale Achsen** den Wert **1** für die Option **Intervall** fest, um jede Kategoriegruppenbezeichnung anzuzeigen. Geben Sie **2**ein, um jede zweite Kategoriegruppenbezeichnung auf der X-Achse anzuzeigen. 

     ![report-builder-column-chart-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-x-axis-interval-one.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    Das Säulendiagramm zeigt jetzt alle Bezeichnungen für die horizontale Achse an.

    ![report-builder-column-chart-preview-x-axis-interval-one](../../reporting-services/report-design/media/report-builder-column-chart-preview-x-axis-interval-one.png)
  
    > [!NOTE]  
    >  Wenn Sie ein Achsenintervall festlegen, wird die automatische Kennzeichnung deaktiviert. Wenn Sie einen Wert für das Achsenintervall angeben, kann es je nach Anzahl der Kategorien auf der Kategorieachse zu unerwartetem Kennzeichnungsverhalten kommen.  

## <a name="change-the-label-interval-in-properties-pane"></a>Ändern des Bezeichnungsintervalls im Eigenschaftenbereich

Sie können das Bezeichnungsintervall auch im Eigenschaftenbereich festlegen.

1.  Klicken Sie in der Berichtsentwurfsansicht auf das Diagramm, und wählen Sie dann die horizontalen Achsenbezeichnungen aus.

3. Legen Sie im Eigenschaftenbereich „LabelInterval“ auf **1**fest.

    ![report-builder-column-chart-set-label-interval](../../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    Das Diagramm sieht genauso aus wie in der Entwurfsansicht. 
    
5.  Klicken Sie auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen.

    ![report-builder-column-chart-label-interval-one-preview](../../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    Jetzt zeigt das Diagramm alle seine Bezeichnungen an.
  
## <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>So aktivieren Sie eine variable Intervallberechnung auf einer Achse  

Standardmäßig wird das Achsenintervall von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf „Auto“ festgelegt. In diesem Verfahren wird erläutert, wie es wieder auf den Standardwert gesetzt wird. 
  
1.  Klicken Sie mit der rechten Maustaste auf die Diagrammachse, die Sie ändern möchten, und klicken Sie dann auf **Achseneigenschaften**. 
  
2.  Legen Sie auf der Registerkarte **Achsenoptionen** im Dialogfeld **Eigenschaften für horizontale Achsen** den Wert **Auto** für die Option **Intervall** fest. Im Diagramm wird die optimale Anzahl von Kategoriebezeichnungen, die auf die Achse passen, im Berichts-Generator angezeigt.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatieren von Datenpunkten in einem Diagramm (Berichts-Generator und SSRS)](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Sortieren von Daten in einem Datenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Achseneigenschaften (Dialogfeld), Achsenoptionen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
 [Angeben einer logarithmischen Skalierung (Berichts-Generator und SSRS)](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Zeichnen von Daten auf einer sekundären Achse (Berichts-Generator und SSRS)](../../reporting-services/report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
