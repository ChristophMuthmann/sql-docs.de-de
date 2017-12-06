---
title: "Zeichnen von Daten auf einer sekundären Achse (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/30/2017
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
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 0a8ae605186909bf5f4423e3a707f3662f267cf1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>Zeichnen von Daten auf einer sekundären Achse (Berichts-Generator und SSRS)

Das Diagramm verfügt über zwei Achsentypen: primär und sekundär. Die sekundäre Achse ist nützlich beim Vergleichen von zwei Wertsätzen mit zwei unterschiedlichen Datenbereichen, die eine gemeinsame Kategorie verwenden.  
  
 Angenommen, Sie haben ein Diagramm, das Einnahmen und Steuern für das Jahr 2008 berechnet. In diesem Fall verwenden beide Wertsätze den Zeitraum 2008 gemeinsam. Wenn beide Reihen jedoch auf derselben Y-Achse gezeichnet werden, kann kein sinnvoller Vergleich durchgeführt werden, da die Skala der Y-Achse für die größten Werte im Dataset optimiert ist. Wenn die Einnahmen auf der primären Achse und die Steuern auf der sekundären Achse angezeigt werden, kann jede Reihe auf einer eigenen Y-Achse mit einer eigenen Werteskala dargestellt werden. Die Reihen verwenden nach wie vor eine gemeinsame X-Achse.  
  
 In Fällen, in denen mehr als zwei Reihen verglichen werden, sollten Sie einen anderen Ansatz für den Vergleich und die Anzeige mehrerer Reihen in einem Diagramm in Erwägung ziehen. Weitere Informationen hierzu finden Sie unter [Mehrere Reihen in einem Diagramm](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Ein Beispiel für dieses Diagramm ist als Beispielbericht verfügbar. Weitere Informationen zum Herunterladen des Beispielberichts und anderer Berichte finden Sie unter [Beispielberichte zu Berichts-Generator und Berichts-Designer](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>So zeichnen Sie eine Reihe auf der sekundären Achse  
  
1.  Klicken Sie mit der rechten Maustaste auf die Reihe im Diagramm oder auf ein Feld im Bereich **Werte** , das Sie auf der sekundären Achse anzeigen möchten. Klicken Sie anschließend auf **Reiheneigenschaften**. Das Dialogfeld **Reiheneigenschaften** wird angezeigt.  
  
2.  Klicken Sie auf **Achsen und Diagrammfläche**, und wählen Sie die sekundäre Achse aus, die Sie aktivieren möchten, d. h. die Wertachse oder die Kategorieachse.  

## <a name="next-steps"></a>Nächste Schritte

[Formatieren von Achsenbezeichnungen in einem Diagramm](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
[Angeben eines Achsenintervalls](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
