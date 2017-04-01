---
title: "Hinzuf&#252;gen oder Entfernen von R&#228;ndern aus einem Diagramm (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Hinzuf&#252;gen oder Entfernen von R&#228;ndern aus einem Diagramm (Berichts-Generator und SSRS)
Bei Säulen- und Punktdiagrammen in paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichten fügt das Diagramm an den Enden der X-Achse automatisch Seitenränder hinzu. Bei Balkendiagrammen werden an den Enden der x-Achse automatisch Seitenränder hinzugefügt. Bei allen anderen Diagrammtypen fügt das Diagramm keine Seitenränder hinzu. Die Größe der Seitenränder kann nicht geändert werden.  
  
 Dieses Thema gilt nicht für Kreis-, Ring-, Trichter- oder Pyramidendiagramme.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## So aktivieren oder deaktivieren Sie Seitenränder  
  
1.  Klicken Sie mit der rechten Maustaste auf die Achse, und wählen Sie **Achseneigenschaften** aus. Das Dialogfeld **Eigenschaften für vertikale Achsen** oder **Eigenschaften für horizontale Achsen** wird angezeigt.  
  
2.  Legen Sie auf der Seite **Achsenoptionen** die Eigenschaft **Seitenränder** fest:  
  
    -   **Automatisch:** Das Diagramm bestimmt basierend auf dem Diagrammtyp, ob ein Seitenrand hinzugefügt wird.  
  
    -   **Deaktiviert:** Balken-, Säulen- und Punktdiagramme haben keine Seitenränder.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Formatieren von Achsenbezeichnungen in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Achseneigenschaften (Dialogfeld), Achsenoptionen &#40;Berichts-Generator und SSRS&#41;](../Topic/Axis%20Properties%20Dialog%20Box,%20Axis%20Options%20\(Report%20Builder%20and%20SSRS\).md)   
 [Angeben eines Achsenintervalls &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Formatieren von Achsenbezeichnungen als Datumsangabe oder Währung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  