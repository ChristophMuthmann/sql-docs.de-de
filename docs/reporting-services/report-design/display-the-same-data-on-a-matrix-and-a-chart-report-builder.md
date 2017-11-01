---
title: Anzeigen derselben Daten in einer Matrix und einem Diagramm (Berichts-Generator) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bf125e2438d3d79662920c8fbc93faab8e8024d4
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>Anzeigen derselben Daten in einer Matrix und einem Diagramm (Berichts-Generator)
  Wenn sie dieselben Daten in einer Matrix und einem Diagramm anzeigen möchten, müssen Sie für beide Datenbereiche Eigenschaften festlegen, um dasselbe Dataset anzugeben, und außerdem identische Ausdrücke für Filter, Gruppen, Sortierungen und Daten.  
  
 Da beide Datenbereiche denselben Vorgänger für die Daten aufweisen (das Berichtsdataset), können Sie der Matrix eine interaktive Sortierschaltfläche hinzufügen, auf die Benutzer klicken können, um die Sortierreihenfolge in der Matrix und im Diagramm zu ändern. Weitere Informationen finden Sie unter [Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Wenn die Spaltengruppenwerte der Matrix als Legende für das Diagramm verwendet werden sollen, müssen Sie die Farben für die Reihendaten im Diagramm angeben und anschließend dieselben Farben als Füllfarben für den Hintergrund der Textfelder in der Matrixzelle verwenden, in der die Gruppenwerte angezeigt werden. Weitere Informationen finden Sie unter [Angeben von Farben, die für mehrere Formdiagramme konsistent sind &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md).  
  
 Wenn zu viele Gruppenwerte für die Gruppendefinitionen vorhanden sind, wird der Bericht zur Laufzeit möglicherweise überladen angezeigt. Möglicherweise müssen Sie Werte filtern, Gruppen kombinieren oder den Schwellenwert für das Diagramm anpassen, sodass die Gruppen automatisch kombiniert werden. Weitere Informationen finden Sie unter [Linking Multiple Data Regions to the Same Dataset &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>So fügen Sie eine Matrix und ein Diagramm zum Anzeigen derselben Daten hinzu  
  
1.  Öffnen Sie einen Bericht in der Entwurfsansicht.  
  
2.  Klicken Sie auf der Registerkarte **Einfügen** in der Gruppe **Datenbereiche** auf **Matrix**, und klicken Sie dann in den Bericht oder in ein Rechteck im Bericht. Dem Bericht wird eine neue Matrix hinzugefügt.  
  
3.  Klicken Sie auf der Registerkarte **Einfügen** in der Gruppe **Datenbereiche** auf **Diagramm**, und wählen Sie dann den Diagrammtyp aus. Dem Bericht wird ein Diagramm hinzugefügt.  
  
4.  (Optional) Klicken Sie auf der Registerkarte **Einfügen** in der Gruppe **Berichtselemente** auf **Rechteck**und anschließend auf den Bericht. Dem Bericht wird ein Rechteck hinzugefügt. Ziehen Sie die Matrix und das Diagramm aus Schritt 2 und 3 in das Rechteck.  
  
     Wenn Sie mehrere Datenbereiche in den Rechteckcontainer platzieren, können Sie steuern, wie die Matrix und das Diagramm beim Anzeigen des Berichts gerendert werden.  
  
     In den nächsten Schritten wählen Sie dasselbe Datasetfeld für die Anzeige in der Matrix und für die Anzeige im Diagramm aus.  
  
5.  Ziehen Sie ein numerisches Datasetfeld aus dem Berichtsdatenbereich in die Datenzelle in der Matrix.  
  
     Standardmäßig wird die Aggregatfunktion „Sum“ zum Berechnen des Gruppenwerts verwendet. Wenn Sie die Aggregatfunktion in der Matrix ändern, müssen Sie diese auch im Diagramm ändern.  
  
6.  Klicken Sie in der Matrix mit der rechten Maustaste auf die Zelle mit den Daten, klicken Sie auf **Textfeldeigenschaften**, und klicken Sie anschließend auf **Zahl**. Wählen Sie ein für den Datasetfeldwert geeignetes Format aus.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Ziehen Sie das in Schritt 3 ausgewählte Datasetfeld in den Bereich **Werte** des Diagramms.  
  
9. Klicken Sie im Diagramm mit der rechten Maustaste auf die Y-Achse, klicken Sie auf **Achseneigenschaften**, und klicken Sie anschließend auf **Zahl**. Wählen Sie dasselbe Format für die Daten aus, die Sie in Schritt 4 ausgewählt haben.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     In den nächsten Schritten legen Sie die Zeilengruppe der Matrix und die Reihengruppe des Diagramms auf denselben Ausdruck fest. Außerdem legen Sie die Sortierreihenfolge für die Reihengruppe des Diagramms fest.  
  
11. Ziehen Sie das Datasetfeld, nach dem die Sortierung für Matrixzeilen erfolgen soll, aus dem Berichtsdatenbereich in den Bereich Zeilengruppen.  
  
     Die Matrixzeilengruppe fügt standardmäßig einen Sortierungsausdruck hinzu, der mit dem Gruppierungsausdruck identisch ist.  
  
12. Ziehen Sie das in Schritt 9 verwendete Datasetfeld in den Bereich **Reihengruppen** des Diagramms.  
  
13. Klicken Sie mit der rechten Maustaste auf die Gruppe im Bereich **Reihengruppen** , und klicken Sie anschließend auf **Reihengruppeneigenschaften**.  
  
14. Klicken Sie auf **Sortierung**.  
  
15. Klicken Sie auf **Hinzufügen**. Im Sortierungsausdrucksraster wird eine neue Zeile angezeigt.  
  
16. Wählen Sie unter **Sortieren nach**in der Dropdownliste das Datasetfeld aus, das Sie in Schritt 9 als Sortierkriterium ausgewählt haben.  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     In den nächsten Schritten legen Sie die Spaltengruppe der Matrix und die Kategoriegruppe des Diagramms auf denselben Ausdruck fest. Außerdem legen Sie die Sortierreihenfolge für die Kategoriegruppe des Diagramms fest.  
  
18. Ziehen Sie das Datasetfeld, nach dem die Sortierung für Matrixspalten erfolgen soll, aus dem Berichtsdatenbereich in den Bereich Spaltengruppen.  
  
     Die Matrixspaltengruppe fügt standardmäßig einen Sortierungsausdruck hinzu, der mit dem Gruppierungsausdruck identisch ist.  
  
19. Ziehen Sie das in Schritt 16 verwendete Datasetfeld in den Bereich **Kategoriegruppen** des Diagramms.  
  
20. Klicken Sie mit der rechten Maustaste auf die Gruppe im Bereich **Kategoriegruppen** , und klicken Sie anschließend auf **Kategoriegruppeneigenschaften**.  
  
21. Klicken Sie auf **Sortierung**.  
  
22. Klicken Sie auf **Hinzufügen**. Im Sortierungsausdrucksraster wird eine neue Zeile angezeigt.  
  
23. Wählen Sie unter **Sortieren nach**in der Dropdownliste das Datasetfeld aus, das Sie in Schritt 16 als Sortierkriterium ausgewählt haben.  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. Zeigen Sie das Ergebnis als Vorschau an. In den Zeilen- und Spaltengruppen der Matrix werden dieselben Daten wie in den Reihen- und Kategoriegruppen des Diagramms angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Verknüpfen mehrerer Datenbereiche das gleiche Dataset &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Hinzufügen von Datasetfiltern, Datenbereichsfiltern, und Gruppenfilter &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tabellen, Matrizen und Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Diagramme &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  

