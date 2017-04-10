---
title: "Anzeigen von Prozentwerten in einem Kreisdiagramm (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# Anzeigen von Prozentwerten in einem Kreisdiagramm (Berichts-Generator und SSRS)
  Standardmäßig werden Kategorien in der Legende angezeigt, um jeden Wert zu identifizieren. Wenn Sie das Kreisdiagramm mit Kategoriebezeichnungen versehen haben, möchten Sie möglicherweise Prozentsätze in der Legende anzeigen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### So zeigen Sie Prozentwerte als Bezeichnungen in einem Kreisdiagramm an  
  
1.  Fügen Sie dem Bericht ein Kreisdiagramm hinzu. Weitere Informationen finden Sie unter [Hinzufügen eines Diagramms zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Kreisdiagramm, und wählen Sie **Datenbezeichnungen anzeigen** aus. Die Datenbezeichnungen sollten innerhalb jedes Segments des Kreisdiagramms angezeigt werden.  
  
3.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf die Bezeichnungen, und wählen Sie **Reihenbezeichnungseigenschaften** aus. Das Dialogfeld **Reihenbezeichnungseigenschaften** wird angezeigt.  
  
4.  Geben Sie für die Option **Bezeichnungsdaten** den Wert **#PERCENT** ein.  
  
5.  (Optional) Wenn Sie die Anzahl von Dezimalstellen in der Bezeichnung angeben möchten, geben Sie „#PERECENT{P*n*}“ an, wobei *n* die Anzahl der anzuzeigenden Dezimalstellen darstellt. Geben Sie z. B. "#PERCENT{P0}" ein, um keine Dezimalstellen anzuzeigen.  
  
### So zeigen Sie Prozentwerte in der Legende eines Kreisdiagramms an  
  
1.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Kreisdiagramm, und wählen Sie **Reiheneigenschaften** aus. Das Dialogfeld **Reiheneigenschaften** wird angezeigt.  
  
2.  Geben Sie unter **Legende** den Wert **#PERCENT** für die Eigenschaft **Benutzerdefinierter Legendentext** ein.  
  
## Siehe auch  
 [Kreisdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatieren der Legende in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)   
 [Anzeigen von Datenpunktbezeichnungen außerhalb eines Kreisdiagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Zusammenfassen von kleinen Segmenten in einem Kreisdiagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  