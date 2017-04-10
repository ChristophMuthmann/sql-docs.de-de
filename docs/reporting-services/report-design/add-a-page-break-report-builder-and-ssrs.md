---
title: "Hinzuf&#252;gen eines Seitenumbruchs (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 3846cd48-2787-47e9-b13b-7fc45a205f68
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Hinzuf&#252;gen eines Seitenumbruchs (Berichts-Generator und SSRS)
  Sie können Rechtecken, Datenbereichen oder Gruppen innerhalb von Datenbereichen einen Seitenumbruch hinzufügen, um die Datenmenge auf jeder Seite zu steuern. Durch Hinzufügen von Seitenumbrüchen kann die Leistung von veröffentlichten Berichten verbessert werden, da beim Anzeigen des Berichts nur die Elemente auf jeder Seite verarbeitet werden müssen. Wenn der ganze Bericht aus einer einzelnen Seite besteht, müssen alle Elemente verarbeitet werden, bevor Sie den Bericht anzeigen können.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### So fügen Sie einen Seitenumbruch zu einem Datenbereich hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Handle in der Ecke des Datenbereichs, und klicken Sie anschließend auf **Tablix-Eigenschaften**.  
  
2.  Wählen Sie auf der Registerkarte **Allgemein** unter **Seitenumbruchoptionen**eine der folgenden Optionen aus:  
  
    -   **Seitenumbruch hinzufügen vor**. Aktivieren Sie diese Option, wenn Sie vor der Tabelle einen Seitenumbruch hinzufügen möchten.  
  
    -   **Seitenumbruch hinzufügen nach**. Aktivieren Sie diese Option, wenn Sie nach der Tabelle einen Seitenumbruch hinzufügen möchten.  
  
    -   **Tabelle möglichst für eine einzelne Seite anpassen**. Aktivieren Sie diese Option, wenn die Daten auf einer Seite bleiben sollen.  
  
### So fügen Sie einen Seitenumbruch zu einem Rechteck hinzu  
  
1.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Rechteck, dem Sie einen Seitenumbruch hinzufügen möchten, und klicken Sie anschließend auf **Rechteckeigenschaften**.  
  
2.  Wählen Sie auf der Registerkarte **Allgemein** unter **Seitenumbruchoptionen**eine der folgenden Optionen aus:  
  
    -   **Seitenumbruch hinzufügen vor**. Aktivieren Sie diese Option, wenn Sie vor dem Rechteck einen Seitenumbruch hinzufügen möchten.  
  
    -   **Seitenumbruch hinzufügen nach**. Aktivieren Sie diese Option, wenn Sie nach dem Rechteck einen Seitenumbruch hinzufügen möchten.  
  
    -   **Rahmen an Seitenumbruch auslassen**. Aktivieren Sie diese Option, wenn für den Seitenumbruch kein Rahmen hinzugefügt werden soll.  
  
    -   **Inhalte nach Möglichkeit auf einer Seite zusammenhalten**. Aktivieren Sie diese Option, wenn der Inhalt innerhalb des Rechtecks auf einer Seite bleiben soll.  
  
### So fügen Sie einer Gruppe in einer Tabelle, Matrix oder Liste einen Seitenumbruch hinzu  
  
1.  Klicken Sie im Bereich „Gruppierung“ mit der rechten Maustaste auf eine Zeilengruppe, und klicken Sie anschließend auf **Gruppeneigenschaften**.  
  
    > [!NOTE]  
    >  Seitenumbrüche werden für Spaltengruppen ignoriert.  
  
2.  Wählen Sie auf der Registerkarte **Seitenumbrüche** die Option **Zwischen den einzelnen Instanzen einer Gruppe** aus, um einen Seitenumbruch zwischen den einzelnen Instanzen einer Gruppe in der Tabelle hinzuzufügen.  
  
3.  Klicken Sie wahlweise auf **Auch am Anfang einer Gruppe** oder **Auch am Ende einer Gruppe** , um festzulegen, dass ein Seitenumbruch hinzugefügt wird, wenn eine Gruppe in der Tabelle beginnt bzw. endet.  
  
## Siehe auch  
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Seitenkopf- und Seitenfußzeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
  
  