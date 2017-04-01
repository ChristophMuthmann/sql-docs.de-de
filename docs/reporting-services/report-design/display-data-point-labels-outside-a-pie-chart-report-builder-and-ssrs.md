---
title: "Anzeigen von Datenpunktbezeichnungen au&#223;erhalb eines Kreisdiagramms (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
caps.latest.revision: 6
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# Anzeigen von Datenpunktbezeichnungen au&#223;erhalb eines Kreisdiagramms (Berichts-Generator und SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]wird die Kreisdiagrammkennzeichnung optimiert, um Bezeichnungen auf nur einigen Segmenten der Daten anzuzeigen. Die Bezeichnungen überschneiden sich möglicherweise, wenn das Kreisdiagramm zu viele Slices enthält. Eine Lösung besteht darin, die Bezeichnungen außerhalb des Kreisdiagramms anzuzeigen, wodurch möglicherweise mehr Platz für längere Datenbezeichnungen vorhanden ist. Wenn Sie feststellen, dass sich die Bezeichnungen immer noch überschneiden, können Sie mehr Platz schaffen, indem Sie 3D aktivieren. Dadurch wird der Durchmesser des Kreisdiagramms reduziert und mehr Platz um das Diagramm herum verfügbar.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### So zeigen Sie Datenpunktbezeichnungen innerhalb eines Kreisdiagramms an  
  
1.  Fügen Sie dem Bericht ein Kreisdiagramm hinzu. Weitere Informationen finden Sie unter [Hinzufügen eines Diagramms zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Diagramm, und wählen Sie **Datenbezeichnungen anzeigen** aus.  
  
### So zeigen Sie Datenpunktbezeichnungen außerhalb eines Kreisdiagramms an  
  
1.  Erstellen Sie ein Kreisdiagramm, und zeigen Sie die Datenbezeichnungen an.  
  
2.  Öffnen Sie den Bereich Eigenschaften.  
  
3.  Klicken Sie auf der Entwurfsoberfläche auf das Kreisdiagramm, um die **Category** -Eigenschaften im Eigenschaftenbereich anzuzeigen.  
  
4.  Erweitern Sie den Knoten **CustomAttributes** . Eine Liste der Attribute für das Kreisdiagramm wird angezeigt.  
  
5.  Legen Sie die **PieLabelStyle** -Eigenschaft auf **Außen**fest.  
  
6.  Legen Sie die **PieLineColor** -Eigenschaft auf **Schwarz**fest. Die PieLineColor-Eigenschaft definiert Legendenzeilen für jede Datenpunktbezeichnung.  
  
### So verhindern Sie überlappende Bezeichnungen außerhalb eines Kreisdiagramms  
  
1.  Erstellen Sie ein Kreisdiagramm mit externen Bezeichnungen.  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste außerhalb des Kreisdiagramms, aber in den Diagrammrahmen, und wählen Sie **Diagrammflächeneigenschaften** aus. Das Dialogfeld **Diagrammflächeneigenschaften** erscheint daraufhin.  
  
3.  Wählen Sie auf der Registerkarte **3D-Optionen** die Option **3D aktivieren**aus.  
  
4.  Wenn das Diagramm mehr Platz für Bezeichnungen bieten, aber dennoch zweidimensional bleiben soll, legen Sie die Eigenschaften **Drehung** und **Neigung** auf **0** fest.  
  
## Siehe auch  
 [Kreisdiagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Zusammenfassen von kleinen Slices in einem Kreisdiagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Anzeigen von Prozentwerten in einem Kreisdiagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  